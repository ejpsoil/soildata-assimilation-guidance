---
title: Data harmonization (vector data)
summary: 
authors:
    - Paul van Genuchten
date: 2022-11-10
---

# Data harmonization (vector data)

A main aspect of INSPIRE is the harmonization of environmental data throughout Europe. Alinging the format, structure and content of your data to match a common model, so the data can be integrated with other datasets in Europe. And to describe aspects of the data which differ from the common model in such a way, that the differences can be understood by others. 

Data harmonization is an aspect of step `4) data organization` in the [soil information workflow](https://www.isric.org/index.php/utilise/community-practice).

An important activity related to harmonization is the adoption of INSPIRE code lists and extending those lists to capture regional conventions. The role of code lists is explained in a dedicated [codelists section](codelists.md). 

INSPIRE datamodel extension is another aspect to consider as part of data harmonization. Harmonization should not lead to loss of data (because some data doesn't fit the target model). Instead the target model should be extended to capture these aspects. [Annex D of TG Soil](https://github.com/INSPIRE-MIF/technical-guidelines/blob/2022.2/data/so/dataspecification_so.adoc#soil-data-model-extensions-informative) has a specific example on extending the model for a soil contamination use case. Options for model extensions vary per technology. Wetransform has a [dedicated section on model extension](http://inspire-extensions.wetransform.to) on their website, based on an [R&D project](https://www.geonovum.nl/uploads/documents/20161121-INSPIRE-Extensions.pdf) from 2016. 

If you missed the initial EJP Training on Soil data good practices, you can still have a look at [a presentation about vector data harmonization](https://wur.yuja.com/V/Video?v=195126&node=829569&a=1133213006&autoplay=1).

This document lists various implementation options for data harmonization. 

## Minimal

The [good practice on GeoPackage](https://github.com/INSPIRE-MIF/gp-geopackage-encodings) describes a relational database format to share harmonised data. [GeoPackage](https://www.geopackage.org/) is a standardised format for storing relational data by the Open Geospatial Consorium, building on the SQLite database specification. Becuase many soil data is stored in the form of relational databases, the transformation to GeoPackage is relatively easy. The transformation process could for example be triggered by a series of database queries within a GIS Desktop client such as QGIS, in Python scripts or an ETL tool such as Hale Studio or FME. 

Pro's and Con's:

- The GeoPackage format is easy to consume by average users.
- To capture the hierarchical structure of the INSPIRE datamodels, a lot of tables are needed, resulting in a complex data-model. 
- The good practice is recent, so not a lot of community experience is available yet 
- Users download a full dataset, no (filering) api's are defined for GeoPackages yet

| Cookbook | Software | Description |
| --- | --- | --- |
| [Glosis as a database](cookbook/glosis-db.md) | - | Harmonise soil data using GeoPackage |

## Traditional

Tools like Hale Studio and FME are typically used to configure a conversion from data in a relational data model to data in a GML based INSPIRE model. The output is a big GML file which can be published using a WFS server or Atom download service. Below table links to detailed pages on various relevant technologies.

| Cookbook | Software | Description |
| --- | --- | --- |
| [Hale Studio](cookbook/hale-studio.md) | [Hale Studio](https://wetransform.to/halestudio/) | Humboldt Alignment Editor Studio is a Desktop tool to author 'data alignments'. |
| [FME & INSPIRE](https://www.safe.com/integrate/inspire-gml/) | [FME](https://www.safe.com/fme/) | Feature Manipulation Engine is a visually oriented data integration platform |

You may not have considered before, but consuming a rich GML is not straight forward in common GIS clients like ArcGIS or QGIS. To consume a rich GML you need software which is able to traverse xml hierarchies and links. Tools like Hale Studio can also be used to read rich GML and convert it back to a relational database. Unfortunately you can not automatically reverse an existing database to GML ETL-configuration. But you can set up a new ETL configuration to read and transform the rich GML. A recipe is available which [imports INSPIRE Soil GML from the city of Berlin and converts it to a relational database](cookbook/hale-studio-consume-gml.md).

Alternatively some server tools offer on the fly transformation as part of the download service, the data mapping is defined within the service configuration.

| Cookbook | Software | Description |
| --- | --- | --- |
| [GeoServer](cookbook/geoserver.md) | [GeoServer](https://geoserver.org) | Java based server implementation |
| [deegree](cookbook/deegree.md) | [deegree](https://www.deegree.org) | Java based server implementation |
| [Xtraserver](cookbook/xtraserver.md) | [xtraserver](https://www.interactive-instruments.de/en/xtraserver/)  | Java based server implementation, also distributed as [ArcGIS for INSPIRE Classic](https://enterprise.arcgis.com/en/inspire/10.8/get-started/what-is-arcgis-for-inspire.htm) |

## Experimental

Alternative ETL procedures are based on Semantic Web technology. The INSPIRE community is [exploring various semantic web options](https://inspire-eu-rdf.github.io/inspire-rdf-guidelines/), but no good practice has been adopted yet.

See also the [presenation about semantic web (GLOSIS)](https://wur.yuja.com/V/Video?v=184392&node=785996&a=2121794774&autoplay=1) from the 2022 EJP Soil training.

| Product | Software | Description |
| --- | --- | --- |
| [Semantic harmonization using TARQL](cookbook/tarql.md) | [TARQL](https://github.com/tarql/tarql) | command-line tool for converting CSV files to RDF using SPARQL 1.1 |
| [Semantic mapping using YARRRML](cookbook/rml.md) | [RML mapper](https://rml.io/) | Human readable RDF mappings for RML.io |
| [Publish data through semantic web](https://doi.org/10.15454/YJLFZI) | [Yed](https://www.yworks.com/products/yed) [Coby](https://forgemia.inra.fr/anaee-dev/coby) [BlazeGraph](https://blazegraph.com/) | Cookbook by INRAE on publishing soild data as RDF | 
tarql


