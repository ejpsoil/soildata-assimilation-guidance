---
title: Data Standardisation (vector data)
summary: 
authors:
    - Paul van Genuchten
date: 2022-11-10
---

# Data Standardisation (vector data)

Data Standardisation is an aspect of step `4) data organization` in the [soil information workflow](https://www.isric.org/index.php/utilise/community-practice).

Data standardisation is the process of aligning one or more datasets to a common (standardised) data model. For the soil domain, [ISO 28258:2013 Soil quality — Digital exchange of soil-related data](https://www.iso.org/obp/ui/#iso:std:iso:28258:ed-1:v1:en) is a standardised conceptual model which has been developed by the soil community to facilitate the capture of soil plot and profile data. The core of the model is the [Observations and Measurements](https://www.ogc.org/standard/om/) model of the Open Geospatial Community. The ISO28258 model has proven to be generic to capture a lot of soil data use cases, and facilitates interoperability with partners. 

![Observations and Measurements](https://52north.github.io/sensor-web-tutorial/images/om1.png)

These days various encodings of the ISO28258 conceptual model are available
-	A xml/xsd oriented model 
-	A relational model ([PostGreSQL](https://iso28258.isric.org)) 
-	A semantic web ontology, called [GLOSIS Web Ontology](http://w3id.org/glosis/model) 

During implantation of ISO28258 limitations of the model are likely to be  discovered related to the local Use Cases. These limitations can usually be bypassed by extending the model. In recent years some extensions to ISO28258 have been published, which could be relevant to the your cases. Examples are [GLOSIS domain model](https://www.fao.org/global-soil-partnership/areas-of-work/soil-information-and-data/en/) and the [INSPIRE Soil data model](https://inspire.ec.europa.eu/id/document/tg/so).  [Annex D of TG Soil](https://github.com/INSPIRE-MIF/technical-guidelines/blob/2022.2/data/so/dataspecification_so.adoc#soil-data-model-extensions-informative) has a specific example on extending the model for a soil contamination use case. Options for model extensions vary per technology. Wetransform has a [dedicated section on model extension](http://inspire-extensions.wetransform.to) on their website, based on an [R&D project](https://www.geonovum.nl/uploads/documents/20161121-INSPIRE-Extensions.pdf) from 2016. 

An important activity related to Standardisation is the adoption of common code lists and extending those lists to capture regional conventions. The role of code lists is explained in a dedicated [codelists section](codelists.md). 

If you missed the initial EJP Training on Soil data good practices, you can still have a look at [a presentation about vector data standardisation](https://wur.yuja.com/V/Video?v=195126&node=829569&a=1133213006&autoplay=1).

This document lists various implementation options for data Standardisation. 

## Minimal

The [good practice on GeoPackage](https://github.com/INSPIRE-MIF/gp-geopackage-encodings) describes a relational database format to share standardised data. [GeoPackage](https://www.geopackage.org/) is a standardised format for storing relational data by the Open Geospatial Consorium, building on the SQLite database specification. Becuase many soil data is stored in the form of relational databases, the transformation to GeoPackage is relatively easy. The transformation process could for example be triggered by a series of database queries within a GIS Desktop client such as QGIS, in Python scripts or an ETL tool such as Hale Studio or FME. 

Pro's and Con's:

- The GeoPackage format is easy to consume by average users.
- To capture the hierarchical structure of the INSPIRE datamodels, a lot of tables are needed, resulting in a complex data-model. 
- The good practice is recent, so not a lot of community experience is available yet 
- Users download a full dataset, no (filering) api's are defined for GeoPackages yet

| Cookbook | Software | Description |
| --- | --- | --- |
| [INSPIRE in a relational database](cookbook/glosis-db.md) | [Geopackage](https://www.geopackage.org) | Standardise soil data using GeoPackage |

## Traditional

Tools like Hale Studio and FME are typically used to configure a conversion from data in a relational data model to data in a GML based INSPIRE model. The output is a big GML file which can be published using a WFS server or Atom download service. Below table links to detailed pages on various relevant technologies.

| Cookbook | Software | Description |
| --- | --- | --- |
| [Hale Studio](cookbook/hale-studio.md) | [Hale Studio](https://wetransform.to/halestudio/) | Humboldt Alignment Editor Studio is a Desktop tool to author 'data alignments'. |
| - | [FME](https://www.safe.com/fme/) | Feature Manipulation Engine is a visually oriented data integration platform |

You may not have considered before, but consuming a rich GML is not straight forward in common GIS clients like ArcGIS or QGIS. To consume a rich GML you need software which is able to traverse xml hierarchies and links. Tools like Hale Studio can also be used to read rich GML and convert it back to a relational database. Unfortunately you can not automatically reverse a ETL-configuration. But you can set up a new ETL configuration to read and transform the rich GML. A recipe is available which [imports INSPIRE Soil GML from the city of Berlin and converts it to a relational database](cookbook/hale-studio-consume-gml.md).

## Experimental

Alternative ETL procedures are based on Semantic Web technology. The INSPIRE community is [exploring various semantic web options](https://inspire-eu-rdf.github.io/inspire-rdf-guidelines/), but no good practice has been adopted yet.

See also the [presenation about semantic web (GLOSIS)](https://wur.yuja.com/V/Video?v=184392&node=785996&a=2121794774&autoplay=1) from the 2022 EJP Soil training.

| Product | Software | Description |
| --- | --- | --- |
| [Semantic Standardisation using TARQL](cookbook/tarql.md) | [TARQL](https://github.com/tarql/tarql) | command-line tool for converting CSV files to RDF using SPARQL 1.1 |
| [Semantic mapping using YARRRML](cookbook/rml.md) | [RML mapper](https://rml.io/) | Human readable RDF mappings for RML.io |
| [Publish data through semantic web](https://doi.org/10.15454/YJLFZI) | [Yed](https://www.yworks.com/products/yed) [Coby](https://forgemia.inra.fr/anaee-dev/coby) [BlazeGraph](https://blazegraph.com/) | Cookbook by INRAE on publishing soild data as RDF | 
tarql


