

# Data harmonization (vector data)

A main aspect of INSPIRE is the harmonization of environmental data throughout Europe. Alinging the format, structure and content of your data to match a common model, so the data can be integrated with other datasets in Europe. And to describe aspects of the data which differ from the common model in such a way, that the differences can be understood by others. INSPIRE does not require to restructure your work processes to fit the INSPIRE conventions, however in case your data infrastructure goes through a major refactor, INSPIRE conventions should be introduced.

One of the most important activities related to harmonization is the adoption of INSPIRE code lists and extending those lists to capture regional conventions. The role of code lists is explained in a dedicated [codelists section](codelists.md). 

This document lists various implementation options for data harmonization

## Minimal

The [good practice on GeoPackage](https://github.com/INSPIRE-MIF/gp-geopackage-encodings) describes a relational database format to persist harmonised data. GeoPackage is a standard by OGC building on the SQLite relational database. Since many soil data is persisted in the form of relational databases, the transformation to GeoPackage is relatively easy. The transformation process could for example be triggered by a series of database queries within a GIS Desktop client such as QGIS or Python scripts. 



Pro's and Con's:

- The GeoPackage format is easy to consume by average users.

- To capture the hierarchical structre of the INSPIRE datamodels, a lot of tables are needed, resulting in a complex data-model. 
- The good practice is recent, so not a lot of community experience is available yet 
- Users download the full dataset, no (filering) api's are defined for GeoPackages yet

## Traditional

Tools like Hale Studio and FME are typically used to configure a conversion from data in a relational data model to data in a UML based INSPIRE model. The output is a big GML file which can be published using a WFS server or Atom download service. Below table links to detailed pages on various relevant technologies.

| Product | Description |
| --- | --- |
| [FME](tools/fme.md) | Feature Manipulation Engine is a visually oriented data integration platform |
| [Hale Studio](tools/hale.md) | Humboldt Alignment Editor Studio is a Desktop tool to author 'data alignments'. |

Alternatively some server tools offer on the fly transformation as part of the download service, the data mapping is defined within the service configuration.

| Product | Description |
| --- | --- |
| [GeoServer](tools/geoserver.md) | java based server implementation |
| [deegree](tools/deegree.md) | java based server implementation |
| [Xtraserver](tools/xtraserver.md) | java based server implementation, also distributed as ArcGIS for INSPIRE Classic |

Pro's and Con's:

- The approach is well established, availability of documentation and validation tooling.
- The model captures the richness of soil data well

- Environment is hard to set up and maintain and is resource intensive (memory and cpu)
- GML is difficult to consume by average users

## Experimental

Since the soil theme substantially depends on [Observations and Measurements](https://www.ogc.org/standards/om) (O&M), the use of [Sensor Observation Service](https://www.ogc.org/standards/sos) (SOS) as a download service is a proper alternative to WFS. Various tools offer SOS, or its follow-up, [SensorThings API](https://www.ogc.org/standards/sensorthings), directly on top of a relational database. Katharina Schleidt provides some interesting work on [setting up SensorThings API to provide INSPIRE data](http://www.datacove.eu/inspire/).

| Product | Description |
| --- | --- |
| [52 north](https://52north.org/software/software-projects/sos/) | Java based open source SOS 2.0 implementation |
| [Frost server](https://fraunhoferiosb.github.io/FROST-Server/) | Java based implementation of Sensorthings API |
| [istSOS](http://istsos.org/) | Python based open source SOS 1.0 implementation |

Various groups prefer to work with semantic web technology over UML/XSD to publish environmental data. Various tools exist which expose relational models as sematic graph. INRAE provides an interesting cookbook on how to [publish soil data using semantic technology](https://doi.org/10.15454/YJLFZI).

| Product | Description |
| --- | --- |
| [Ontop](https://ontop-vkg.org/) | Exposes the content of arbitrary relational databases as knowledge graphs |
| [D2RQ](http://d2rq.org/) | Accessing relational databases as virtual, read-only RDF graphs |
| [TopBraid](https://www.topquadrant.com/doc/7.1/scripting/importing.html) | Desktop tool to manage graphs and relational data imports |
