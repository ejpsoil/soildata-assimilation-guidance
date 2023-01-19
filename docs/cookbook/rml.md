[RML.io](https://rml.io/)
=========================

RML.io is a toolset for the generation of knowledge graphs. They automate
the creation of RDF from diverse data sources, primarily unstructured tabular
data. 

RML.io has programmes to be used on-line and to be installed on computer systems
(Linux, MacIntosh and Windows platforms are supported). The former are useful
for prototyping, whereas the latter are meant for actual transformations of
large datasets.

The YARRRML syntax
------------------

The RML tools apply data transformations according to a set of rules recorded in
a YAML file. This file must respect a specific syntax, named
[YARRRML](https://rml.io/yarrrml/spec/). This specification defines a number of
sections (or environments) in the YAML file that lay out the structure of the
resulting triples.

The first of these sections is named `prefixes` and provides the space for the
definition of URI abbreviations, in all similar to the Turtle syntax. Each
abbreviation is encoded as a list item and can be used in the reminder of the
YARRRML as it would be in a Turtle knowledge graph.

```yml
prefixes:
 rdf: http://www.w3.org/1999/02/22-rdf-syntax-ns#
 xsd: http://www.w3.org/2001/XMLSchema#
 geo: http://www.opengis.net/ont/geosparql#
```

Next comes the `mappings` section, where the actual transformations are encoded. This
section is to be populated with sub-sections, one for each individual subject
class (or type) necessary in the output RDF. For instance, if the transformation must produce
triples for profiles and layers, then a sub-suction for each is necessary. The
name of these subject sub-sections is arbitrarily chosen by the user.

```yml
mappings:
  profile:

  layer:
```

For each subject class sub-section at least one data source needs to be specified in
the `sources` section. The source can be declared within square brackets (i.e. a YAML
collection), providing a path to a file followed by a tilde and then a type.
The sources section can be more intricate, as YARRRML supports [a wide range of different data sources](https://rml.io/yarrrml/spec/#data-sources), including flat tables, databases and Web APIs. 

```yml
mappings:
  profile:
    sources:
      - ['SoilData.csv~csv']
```

The following sub-section of the class declares the subject and has the simple
name of `s`. Its purpose is to define the URI structure for the instances of the
class. In principle this is also the first element that makes reference to the
contents of the source file. In the case of CSV, as in this example, the column
names are used. They are invoked using the dollar character (`$`), with the
column name within parenthesis. The practical result is the generation of an
individual element (subject in this case) for each distinct value found in the
source column. 

```yml
  profile:
    sources:
      - ['SoilData.csv~csv']
    s: http://my.soil.org#$(profile_id)
```

With the subject defined, triples can be completed with predicates and objects
in sub-section `po`. This section is itself composed by a list, whose items
comprise a pair: predicate (item `p`) and object (item `o`). The predicate is
encoded as a URI in a similar way to the subject, using abbreviations if
necessary. As for the object it can be decomposed further into a `value` and a
`datatype` to accommodate literals.   

The example below creates triples for the layer class subject, using the
`layer_id` column in the source to generate subject URIs. The source column
`layer_order` is used to complete triples declaring the order of a layer within
a profile.

```yml
prefixes:
 xsd: http://www.w3.org/2001/XMLSchema#
 iso28258: http://w3id.org/glosis/model/iso28258/2013#

mappings:
  layer:
    sources:
      - ['SoilData.csv~csv']
    s: http://my.soil.org#$(layer_id)
    po:
      - p: iso28258:ProfileElement.order
        o:
           value: "$(layer_order)"
           datatype: xsd:integer
```

The encoding of the predicates and objects list can be shortened with
collections. Instead of discriminating value and datatype, they can be expressed
as elements of a collection. This formulation is useful when the object is
itself a URI. Note how in the example below (for the layer class) the tilde is
used again, to indicate the object type. 

```yml
    po:
      - [iso28258:Profile.elementOfProfile, http://my.soil.org#$(layer_id)~iri]
```

This was just a brief introduction to the YARRRML syntax. It goes far deeper,
even allowing for some functional programming. While the guidelines in this
document make enough of a start to automated RDF generation, the
[documentation](https://w3id.org/yarrrml) is indispensable to take full
advantage of the RML tool set.

Matey
-----

The simplest way to start using RML.io is through the
[Matey](https://rml.io/yarrrml/matey/) online user interface. It is an
excellent prototyping tool and will help you getting acquainted with the
YARRRML syntax.

The standard view of Matey has 4 sections:
- a section for input data;
- a section to define YARRRML rules;
- a section to display RDF output;
- a section to visualise exported RML.io rules from YARRRML.

There are various examples available to guide you through the basics of YARRRML and
RML. Take some time to experiment with these examples, try modifying the
output, or even to create further transformation rules.  

Eventually you will find the limitatios of Matey, while convinient for
prototyping, it does not scale for large datasets or to process a large number
of source files. For that you need to use the command line interface.

Install
-------

Using RML.io in your system requires two programmes, a parser for the YARRRML syntax
(`yarrrml-parser`) and a
transformer that converts tabular data to RDF (`rmlmapper`).

The first of these programmes is installed with `npm`:

````
npm i -g @rmlio/yarrrml-parser
````

`rmlmapper` is a Java programme, that can be downloaded directly from the
project [GitHub page](https://github.com/RMLio/rmlmapper-java/releases). For
instance:

```
wget https://github.com/RMLio/rmlmapper-java/releases/download/v6.1.3/rmlmapper-6.1.3-r367-all.jar
```

It can then be run with the Java Runtime Environment:

```
java -jar rmlmapper-6.1.3-r367-all.jar
```

At this stage it might be useful to create a shortcut to call the programme with
a simple command like `rmlmapper`.
How to do this depends on your system and is beyond the scope of this document.

How to use
----------

**Note**: before starting a data transformation into RDF you must devise a URI policy for your data. Please refer to the [URI Policy](./uri.md) document for details.

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

### Profiles

The simplest place to start is with the profiles. There are three essential elements
to generate for each profile:
  - A new URI for the profile;
  - The declaration of the new profile as an instance of the class `GL_Profile`;
  - The association with the respective site. 

Below are the contents of the file [profile.yarrrml](rml/profile.yarrrml) that
encodes this transformation. Note how the URIs of both the profile and the site
are created using the prefixes.

```yml
prefixes:
 wosis_prf: http://wosis.isric.org/profile#  
 wosis_sit: http://wosis.isric.org/site#
 glosis_pr: http://w3id.org/glosis/model/profile# 
 iso28258: http://w3id.org/glosis/model/iso28258/2013#

mappings:
  profile:
    sources:
      - ['SoilData.csv~csv']
    s: wosis_prf:$(profile_id)
    po:
      - [a, glosis_pr:GL_Profile]
      - [iso28258:Profile.profileSite, wosis_sit:$(site_id)~iri]
```

To perform the actual transformation you must first apply `yarrrml-parser` to create
the RML transformation file and then use `rmlmapper` to obtain the actual
knowledge graph. By default `rmlmapper` creates a Turtle file that is printed to
the standard output (STDOUT). You can use the parameters `-o` to redirect output
to a text file and `-s` to select an alternative serialisation syntax.

```
yarrrml-parser -i profile.yarrrml -o profile.rml.ttl
rmlmapper -s turtle -m profile.rml.ttl
``` 

### Sites

Sites are the spatial features in the knowledge graph,
therefore they require the creation of appropriate GeoSPARQL instances. Three
new elements must be addressed in this transformation:
  - Declaration of the site as an instance of the class `geo:Feature`;
  - Creation of a `geo:Geometry` instance to host the actual geo-spatial
    information;
  - A literal of the type `geo:wktLiteral` or `geo:gmlLiteral` to encode the geometry.

The file [site.yarrrml](rml/site.yarrrml) achieves this transformation. Its
contents are reproduced below:

```yml
prefixes:
 geo: http://www.opengis.net/ont/geosparql#
 glosis_sp: http://w3id.org/glosis/model/siteplot# 
 wosis_sit: http://wosis.isric.org/site#
 wosis_geo: http://wosis.isric.org/geometry#

mappings:
  site:
    sources:
      - ['SoilData.csv~csv']
    s: wosis_sit:$(site_id)
    po:
      - [a, glosis_sp:GL_Site]
      - [a, geo:Feature]
      - [geo:hasGeometry, wosis_geo:$(site_id)~iri]

  geometry:
    sources:
      - ['SoilData.csv~csv']
    s: wosis_geo:$(site_id)
    po:
      - [a, geo:Point]
      - p: geo:asWKT
        o:
           value: "POINT($(lon) $(lat))"
           datatype: geo:wktLiteral
```

This example also shows the inclusion of two different classes in the same
transformation. Note how the Feature is associated with the geometry using the
`geo:hasGeometry` object property. Also important is the creation of the WKT
literal, as it requires a verbose declaration of the object to make the
type explicit.

### Layers

Having created a transformation for the sites, one for the layers is not much of
a challenge. Download the file [layer.yarrrml](rml/layer.yarrrml) and try it
yourself. 

Look carefully at the transformation file, note how the object properties from
the [ISO28258 module](https://rapw3k.github.io/glosis/docs/iso-28258-doc/index-en.html) are used to declare the layers depths.

**Question**: what would be different if in the source dataset horizons were
identified instead of layers? 

### Measurements

An example transformation for the measurements in the original dataset is
available in the file [measurements.yarrrml](rml/measurements.yarrrml). The extra
elements to address in this transformation are:
  - Instance of the respective Observation class;
  - Instance of the respective Result class;
  - Relation between Observation and Result;
  - Numerical literal with the measurement result.

**Question**: Identify in the [Layer Horizon module](https://rapw3k.github.io/glosis/docs/glosis-lh-doc/index-en.html) of GloSIS which are the units of measurement
associated with the Result instances used in this example. 

**Exercise I**: Create a new `yarrrml` file including all the transformations given
above, creating all necessary triples for sites, profiles, layers and
measurements. Make sure it is correctly parsed by `yarrrml-parser` and generate
a new, complete, knowledge graph.

**Exercise II**: Modify the transformation you obtained in the previous exercise
so that it declares all pH measurements as resulting from a H2O procedure
(water solution).

More
----

Now that you obtained a RDF knowledge graph you can publish it to the internet.
Follow the guide on [Virtuoso](virtuoso.md) to learn how.

In alternative to RML, you may transform tabular data into RDF with SPARQL
queries using [tarql](tarql.md). Follow that guide for the details.
