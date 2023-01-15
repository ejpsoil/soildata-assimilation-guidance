# Publish a codelist as a file in a web accessible folder

*status: draft*

This recipe presents a minimal approach for publishing a (extended) code list. 

The most rich and common format for code list storage is RDF (turtle, json-ld, or rdf/xml) using the SKOS ontology. It is the format used by for example Glosis to [publish its codelists](https://github.com/rapw3k/glosis/blob/master/glosis_cl.ttl). Tools like GeoNetwork are able to ingest codelists based on the SKOS ontology.

An alternative format is based on the [iso19135:2005](https://www.iso.org/standard/32553.html) standard. TC 211 develops the iso19135 standard to offer a format for code lists in the spatial data community. The standard is for example used in the [gmx-codelists](https://standards.iso.org/iso/19139/resources/gmxCodelists.xml) as used in iso19139:2007.

The minimal approach described here is for example used in Lituania. From the [SoilBody GML](https://www.inspire-geoportal.lt/geonetwork/srv/metadata/d07c5dce-4a6e-4042-ac48-8b589c57d6d1) the dataset links to locally extended codelists published in an XML format inspired by the INSPIRE registry. See https://inspire-geoportal.lt/resources/codelist/SO/OtherHorizonNotationTypeValue.xml. This format is probably selected because it is supported by Hale Studio.

The location of the codelist can be a webserver folder, a git repository, even a shared sharepoint folder. But it is important that the url of the file is persistent for at least 10+ years. Because the datasets which link to codelist items depend on its availability. A single file typically lists a number of concepts, or even concept schemes. You can reference a concept within the file by concatenating the concept identifier to the url with "#", e.g. https://inspire-geoportal.lt/resources/codelist/SO/OtherHorizonNotationTypeValue.xml#Ap). 

Persistency can be improved by adding an intermediary layer between the storage of the file and the url on which it is made available, mechanisms such as provided by DOI and W3ID.Glosis codelists are for example stored at https://github.com/rapw3k/glosis but are referenced as http://w3id.org/glosis/model/codelists and then forwarded.

## Extending INSPIRE codelists

In [this article](https://wetransform.to/news-and-events/inspire-codelists/) Wetransform explains how and which INSPIRE codelists can be extended.
Either the UML model and/or the INSPIRE registry indicate if a codelist is extensible.

A common approach for extending codelists is to create a new codelist file and duplicate similar terms from the common codelist and link back to them with a `SameAs` link. Broader or Narrower concepts can be added with a broader or narrower link. 

## Content negotiation

When a human arrives at a codelist file, the syntax with https://example.org/#concept opens the full file, and does not point to the relavant concept, because the web browser does not understand the file format. The mechanism of content negotiation can identify web browsers and present them an alternative format (html). Content negotiation can be set up in an intermediary webserver layer, the transformation from SKOS/iso19135 to html should be managed by an extra utility (such as [SKOSMOS](./virtuoso.md)).

## Multilingual concept labels

Both SKOS and ISO19135 support the option to provide labels for concepts in multiple languages.
