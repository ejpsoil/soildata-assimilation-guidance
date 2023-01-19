[tarql](https://tarql.github.io/)
=================================

The basic idea behind `tarql` is to develop a `CONSTRUCT` SPARQL query that
instead of executing against a triple store is executed against a CSV file. The
result is a knowledge graph that may itself be deployed to a triple store or
outright published on the web.

Install
-------

Start by accessing the [releases page](https://github.com/tarql/tarql/releases)
and download a compressed file with the latest version. Then uncompress the
file, it will create a new folder in your system with the release number
appended, for instance `tarql-1.2`.

The sub-folder `bin` contains executables for both Linux and Windows. You may
run the executable directly or install it for wider system use. On Linux it is
common practice to copy the programme folder to `/opt` and then create a
symbolic link in `/usr/local/bin`.

```bash
$ unzip tarql-1.2.zip
$ sudo mv tarql-1.2 /opt
$ sudo ln -s /opt/tarql-1.2/bin/tarql /usr/local/bin/tarql
```

Finally try invoking the executable to make sure it is functioning.

```bash
$ tarql --help
```

Use
---

**Note**: before starting a data transformation into RDF you must devise a URI
policy for your data. Please refer to the [URI Policy](uri.md) document for
details.

The file [SoilData.csv](data/SoilData.csv) contains a simple set of hypothetical
measurements referring to three soil profiles collected in two different sites.
The goal is to transform this dataset into
[GloSIS](https://github.com/rapw3k/glosis) compliant RDF.

```csv
site_id,lat,lon,profile_id,layer_id,upper_depth,lower_depth,pH,SOC,
1,49.43,8.31,1,11,0,15,7.4,6,
1,49.43,8.31,1,12,15,40,7.2,4,
1,49.43,8.31,2,21,0,10,8,3,
1,49.43,8.31,2,22,10,30,8.1,2,
2,46.82,11.45,3,31,0,15,6.8,1,
2,46.82,11.45,3,32,15,30,6.7,1,
2,46.82,11.45,3,33,30,60,6.7,0,
```

### Profile

The Profile class is the most simple in GloSIS, making it a good place to
start. It only requires the declaration of a new instance and its association
with the respective site, in essence just two triples. To do so two URIs must be
created, one for the profile and another for the site. 

The Listing below shows a complete example creating URIs according to the policy
used for the [World Soil Information
Service](https://www.isric.org/explore/wosis) (WoSIS). The `CONSTRUCT` clause in
the query is pretty vanilla, whereas in the `WHERE` clause the URIs are created
with the `BIND` and `URI` functions. The important thing to note in this query
is the use of column names in the CSV file as variables, `?site_id` and
`?profile_id`. `tarql` matches every variable with the CSV columns, replacing
them with the corresponding values. 

```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX glosis_pr: <http://w3id.org/glosis/model/profile#>
PREFIX iso28258: <http://w3id.org/glosis/model/iso28258/2013#>

CONSTRUCT { 
    ?uri_profile rdf:type glosis_pr:GL_Profile ; 
               iso28258:Profile.profileSite ?uri_site .
}
WHERE {
    BIND (URI(CONCAT('http://wosis.isric.org/site#', ?site_id)) AS ?uri_site)
    BIND (URI(CONCAT('http://wosis.isric.org/profile#', ?profile_id)) AS ?uri_profile)
}
```

**Exercise**: try running this example using the [`profile.sparql`](tarql/profile.sparql) file in the
`tarql` folder against the [`SoilData.csv`](data/SoilData.csv) file. You should
issue a command like:

```bash
$ tarql tarql/profile.sparql data/SoilData.csv
```

### Remove duplicates

By default `tarql` generates a triple for each line in the CSV file. Most likely the
data in the CSV is not normalised, and thus many duplicates result. You can
observe this with the example for the Profile class above. 

The tool provides a specific argument to deal with duplicates: `--dedup`. It
suppresses all duplicate triples up to a given line in the output. In general you
will want to use this argument with a large enough number to cover all the
triples produced.

```bash
$ tarql --dedup 1000 tarql/profile.sparql data/SoilData.csv
```  

If your only intention is to load `tarql`'s output to a triple store, you might not need to
worry about duplicate triples. Most likely the software automatically discards
the duplicates on load.

### Site

The next example deals with the Site class, whose instances are spatial
features. Therefore an additional instance of the GeoSPARQL Point class must be
created, with the associated geometry literal. The `BIND` and `URI` are again at
your service to create the URIs. The `STRDT` function is used to create the
geometry instance with the appropriate type. The listing below is available in
the file [`site.sparql`](tarql/site.sparql).

```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX geo: <http://www.opengis.net/ont/geosparql#>
PREFIX glosis_sp: <http://w3id.org/glosis/model/siteplot#>

CONSTRUCT { 
    ?uri_site rdf:type glosis_sp:GL_Site ;
              rdf:type geo:Feature ;
              geo:hasGeometry ?uri_geo .

    ?uri_geo rdf:type geo:Point ; 
             geo:asWKT ?geom .
}
WHERE {
    BIND (URI(CONCAT("http://wosis.isric.org/site#", ?site_id)) AS ?uri_site)
    BIND (URI(CONCAT("http://wosis.isric.org/geometry#", ?site_id)) AS ?uri_geo)
    BIND (STRDT(CONCAT("POINT(", $lon, ", ", $lat, ")"), geo:wktLiteral) AS ?geom)
}
```

**Exercise**: try modifying the query above so that it produces a GML literal
instead of WKT. Which of the literals do you prefer?

### Layer

Instances for the layer should not be a challenge, after succeeding with sites and
profiles. The list below provides and example, creating triples relating the
layer to the respective profile and declaring its extent with ISO-28258
predicates. 

```sparql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX glosis_lh: <http://w3id.org/glosis/model/layerhorizon#>
PREFIX iso28258: <http://w3id.org/glosis/model/iso28258/2013#>

CONSTRUCT { 
    ?uri_layer rdf:type glosis_lh:GL_Layer ; 
        iso28258:ProfileElement.elementOfProfile ?uri_profile ;
        iso28258:ProfileElement.upperDepth ?Top ;
        iso28258:ProfileElement.lowerDepth ?Bottom .
}
WHERE {
    BIND (URI(CONCAT('https://example.org/layer#', ?Layer)) AS ?uri_layer)
    BIND (URI(CONCAT('https://example.org/profile#', ?Profile)) AS ?uri_profile)
}
```

**Exercise**: save the query below in a file and use `tarql` to run it against
the [SoilData.csv](data/SoilData.csv) file. 


**Advanced exercise**: hop on to the WoSIS RDF pilot and verify how a [GloSIS
Observation
instance](https://virtuoso.isric.org/describe/?url=http%3A%2F%2Fwosis.isric.org%2Fobservation%234180696&sid=11)
is formed. Create a new query to generate the approapriate instances for the pH
measurements in the [SoilData.csv](data/SoilData.csv) file. Don't forget to
create the associated [GloSIS
Result](https://virtuoso.isric.org/describe/?url=http%3A%2F%2Fwosis.isric.org%2Fresult%234180696&sas=SAME_AS_OFF&sid=11)
instance(s).

More
----

Now that you obtained a RDF knowledge graph you can publish it to the internet.
Follow the guide on [Virtuoso](virtuoso.md) to learn how.

In alternative to `tarql`, you may instead transform tabular data into RDF with
[RML.io](rml.md), a transformation tool-set based on YAML configuration files.
