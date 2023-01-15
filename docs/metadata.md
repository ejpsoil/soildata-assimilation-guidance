---
title: Overview Metadata & discovery
summary: 
authors:
    - Paul van Genuchten
date: 2022-11-10
---

# Overview Metadata & discovery

Discovery of available data is important for potential users to be aware what data is available, evaluate if the data is relevant for them and how they can fetch it, or who to contact for more details. Essentially, the initial goal of any Spatial Data Infrastructure (SDI) is to describe its content. Metadata of datasets and services is described in documents, which are made accessible via a discovery service as records in a catalogue.

Capturing metadata prior and during data collection is an aspect of step `4) data organization` in the [soil information workflow](https://www.isric.org/index.php/utilise/community-practice), publishing the metadata as part of the data dissemination is an aspect of step `6) data and info sharing`. Evaluating the findability of datasets and assessing broken links on existing metadata is an aspect of step `7) Soil Information User Consideration`.

In the soil domain we generally have 2 types of datasets, actual soil observations (calcium content in a horizon of a soil profile at a certain date or a soil profile field classification) and derived grids or polygon maps which represent parameter or soil type distribution for an area. For the second type of datasets describing the lineage (history) of the data is very important. Typically, you would describe the dataset with point observations in 1 document and link another document, describing the derived dataset, and link it as a parent-child relation. The document describing the derived dataset will contain 'processing-steps' describing the model that was used to calculate or derive the parameter or soil type distribution (D6.1 ch 5). This aspect is important for the usage of the derived dataset, to be able to evaluate if the estimate is valid for the envisioned use.

If you missed the initial EJP Training on Soil data good practices, you can still have a look at the [presentation about metadata and discovery](https://wur.yuja.com/V/Video?v=186423&node=793652&a=1324462841&autoplay=1).

This page lists various implementation options both for creating metadata, as well as setting up a discovery service.

## Minimal

In a minimal implementation you can describe your dataset as well as your services in a single metadata document. This 'good practice' is described in [https://github.com/INSPIRE-MIF/gp-data-service-linking-simplification](https://github.com/INSPIRE-MIF/gp-data-service-linking-simplification). Basic metadata editors exist, of which the most basic is Notepad++. In the Python domain exists the pygeometa and OWSLib projects, which offer capabilities to generate ISO19139 metadata from other formats.

These metadata documents can be placed in a [Web Accessible Folder](https://ioos.github.io/catalog/pages/registry/waf_creation/). Products exist which are able to ingest documents from such a folder and expose it as a CSW discovery service. Such an ingest point could be installed at a national level, to facilitate the European INSPIRE GeoPortal (which currently only supports ingests via CSW).

| Cookbook | Software | Description |
| --- | ---| --- |
| [A Pythonic metadata workflow](tools/pygeometa.md) | [pygeometa](https://geopython.github.io/pygeometa) | A minimalistic approach to data discovery |
| [Data in zenodo](tools/zenodo.md) | [zenodo](https://zenodo.org) | Zenodo is a data repository by CERN/Horizon2020, including rich metadata options |

## Traditional

The [TG metadata](https://inspire.ec.europa.eu/id/document/tg/metadata-iso19139) (Technical Guidelines metadata) defines 2 types of metadata; documents which describe a dataset which are linked to documents which describe the service via which the datasets are published.

The [TG discovery](https://inspire.ec.europa.eu/documents/technical-guidance-implementation-inspire-discovery-services-0) describes how the metadata documents need to be published as a CSW discovery service. The table below lists some products which can be used to set up such a service. Mind that the TG extends the OGC CSW specification with some specific INSPIRE elements, for identification and multilingualism.

| Cookbook | Software | Description |
| --- | ---| --- |
| [GeoNetwork](tools/geonetwork.md) | [GeoNetwork](https://www.geonetwork-opensource.org/) | A java based open source catalogue application widely used by member states for INSPIRE discovery. Provides a public portal application. Supports CSW, metadata authoring, validation and harvesting. |
| [pycsw](tools/pycsw.md) | [pycsw](https://pycsw.org/) | A Python based open source CSW server. Supports CSW, OGC API Records. Used in portal software such as [CKAN](https://github.com/ckan/ckanext-spatial)[Spatial](https://github.com/ckan/ckanext-spatial) and [GeoNode](https://geonode.org/). |
| [Geoportal server](tools/geoportal-server.md) | [ArcGIS Geoportal](https://github.com/Esri/geoportal-server) | A java based open source CSW implementation for the ArcGIS platform. A CSW client for ArcGIS desktop is included. Note that this package is not the same as ArcGIS Portal. |
| [Hale Connect](tools/hale-connect.md) | [Hale Connect](https://www.wetransform.to/products/haleconnect/) | A metadata authoring and CSW interface is provided as part of the HALE Connect SAAS offering. |

## Experimental

A good practice exists related to [Geo-DCAT-ap](https://inspire.ec.europa.eu/good-practice/geodcat-ap). It explains how to publish metadata using the Geo-DCAT-ap vocabulary as an additional metadata format. At present the use of ISO19139 is required by all guidelines. However, it is expected that it will soon be possible to offer metadata in a DCAT only. DCAT facilitates records to be discovered via google dataset search (and other search engines and semantic web platforms).

Currently no 'good practice' exists to offer discovery services in alternative protocols then CSW. A good practice to adopt [OGC API Records](https://ogcapi.ogc.org/records/) is being prepared. OpenSearch, OData and SPARQL could be alternative discovery service protocols.

| Cookbook | Software | Description |
| --- | ---| --- |
| [dcat](tools/dcat.md) | - | A dcat approach to dataset discovery |
