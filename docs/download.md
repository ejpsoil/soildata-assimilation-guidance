---
title: Overview Download Services
summary: 
authors:
    - Paul van Genuchten
date: 2022-11-10
---

# Overview Download Services

Download services facilitate the download of vector, grid or sensor data. 

If you missed the initial EJP Training on Soil data good practices, you can still have a look at [a presentation about download services as Coverage and SensorThings](https://wur.yuja.com/V/Video?v=184380&node=785951&a=1565884354&autoplay=1) or [a presentation on Atom/WMS/WFS](https://wur.yuja.com/V/Video?v=184438&node=786146&a=1735271407&autoplay=1).

Setting up download services is an aspect of step `6) data and info sharing` in the [soil information workflow](https://www.isric.org/index.php/utilise/community-practice).

This page lists some implementation options for providing INSPIRE Download Services.

### Minimal

The INSPIRE Atom Service provides a minimal download service implementation on a series of downloadable files placed in a web accessible folder. For every file a 'dataset feed' document can be generated and linked to a service feed describing the 'service'. A metadata record points to the service feed to complete the implementation.

Alternatively, products like [GeoNetwork](https://geonetwork-opensource.org/manuals/3.10.x/en/tutorials/inspire/download-atom.html) and Hale Connect (Annex 1) can provide an Atom interface on top of a set of registered datasets. The [TG download services](https://inspire.ec.europa.eu/documents/technical-guidance-implementation-inspire-download-services) also provides some PHP scripts which create an Atom OpenSearch interface for a series of files.

| Cookbook | Software | Description |
| --- | --- | --- |
| [Webdav](tools/webdav.md) | [Wsgidav](https://wsgidav.readthedocs.io) | Setting up atom service using webdav |
| [GeoNetwork Atom](tools/geonetwork.md) | [GeoNetwork](https://geonetwork-opensource.org) | Atom download service from GeoNetwork |

### Traditional

[Web Feature Service](https://www.ogc.org/standards/wfs) (WFS) and [Web Coverage Service](https://www.ogc.org/standards/wcs) (WCS) are commonly used to download Featurecollections (vector) and Coverages (grids). Consider that most of the INSPIRE themes (including soil) require publication of hierarchical (app-schema) features, this aspect is not supported by many WFS server implementations. Some tools with this capability are listed in the table below. For WCS a [good practice](https://inspire-wcs.eu/) is available to facilitate implementation.

| Cookbook | Software | Description |
| --- | --- | --- |
| [GeoServer](tools/geoserver.md) | [GeoServer](https://geoserver.org/) | The app-schema plugin extends the WFS implementation with support for hierarchical features. On the fly transformation is managed from a configuration file. Marcus Sen (Onegeology) create a [cookbook for this approach](http://www.onegeology.org/docs/technical/OneGeologyWFSCookbook_v1.4.pdf). |
| [Get started with Hale Connect](https://help.wetransform.to/docs/getting-started/2018-04-28-quick-start) | [Hale Connect](https://www.wetransform.to/products/haleconnect/) | Optimized for performance, stores pregeneralised xml fragments in combination with an elastic search index for filtering |
| [Coverages with rasdaman](tools/rasdaman.md) | [Rasdaman](http://www.rasdaman.org/) | A Web Coverage Service implementation |

Consider that a product advertising WFS support does not automatically qualify for INSPIRE, the product has to support hierarchical GML.

### Experimental

As described in the harmonization paragraph, Sensor Observation Service and SensorThings API offer an alternative download option for themes including much observation data, such as Soil.

A good practice document has been adopted on the [use of OGC API Features as download service](https://inspire.ec.europa.eu/good-practice/ogc-api-%E2%80%93-features-inspire-download-service). With its 20 years of history WFS and GML are out of synch with current IT practices. OGC API is a new direction of standards within OGC adopting some of the latest IT conventions, such as Open API, Rest services, JSON encodings, content negotiation, etc. The use of OGC API will increase in coming years while OGC adopts more standards. Various products exist implementing the final and/or draft specifications. 

SensorThings API is a modern sensor standard. JRC adopted the good practice to provide download services using SensorThings API.


| Cookbook | Software | Description |
| --- | --- | --- |
| [OGC API Features via pygeoapi](tools/pygeoapi.md) | [pygeoapi](https://pygeoapi.io) | A python based open source implementation of OGC APIs including OGC API Features. Configuration is managed from a configuration file. |
| [Proxy a WFS as OGC API Features using LDProxy](tools/ldproxy.md) | [ldproxy](https://github.com/interactive-instruments/ldproxy) | A java based open source implementation of OGC APIs. Originally developed by Interactive Instruments as an easy way to consume API (proxy) on top of existing WFS. These experiments were a main driver for OGC in the direction of OGC API. Configuration is managed from a web interface. |
| [SensorThings API via Frost server](tools/frost-server.md) | [Frost server](https://fraunhoferiosb.github.io/FROST-Server/) | Soil observation data as sensor stream |
| [Soil data via GraphQL](tools/postgraphile.md) | [Postgraphile](https://www.graphile.org/postgraphile/) | Soil data from a postgres database via graphQL |


