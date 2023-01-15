[tarql](https://tarql.github.io/)
=================================

The basic idea behind `tarql` is to develop a `CONSTRUCT` SPARQL query that
instead of executing agains a triple store is executed against a CSV file.

Install
-------

Start by accessing the [releases page](https://github.com/tarql/tarql/releases)
and download a compressed file with the latest version. Then uncompress the
file, it will create a new folder in your system with the release number
appended, for instace `tarql-1.2`.

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

The file [SoilData.csv](data/SoilData.csv) contains a simple set of
hypothetical measurements referring to three soil profiles collected in two
different sites. The goal is to transform this dataset into [GloSIS](https://github.com/rapw3k/glosis) compliant
RDF.

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

#### Remove duplicates

By default tarql generates a triple for each line in CSV file. Most likely the
data in the CSV is not normalised, and thus many duplicate results. You can
observe this with the example for the Profile class above. 

The tool provides a specific argument to deal with duplicates: `--dedup`. It
supresses all duplicate triples up to a given line in the output. In general you
will want to use this argument with a large enough number to cover all the
triples produced.

```
$ tarql --dedup 1000 tarql/profile.sparql data/SoilData.csv
```  

If your only intention is to load tarql's output to a triple store, you might not need to
worry about duplicate triples. Most likely the software automatically discards
the duplicates on load.

### Site

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

### Layer

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
FROM <file:data.csv>
WHERE {
    BIND (URI(CONCAT('https://example.org/layer#', ?Layer)) AS ?uri_layer)
    BIND (URI(CONCAT('https://example.org/profile#', ?Profile)) AS ?uri_profile)
}
```
