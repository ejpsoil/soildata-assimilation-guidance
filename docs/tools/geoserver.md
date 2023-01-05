# Appschema WFS in GeoServer

*Status: contribution required*

GeoServer is an open source java imlementation of WFS, WCS, WPS, WMS, CSW. Various OGC API endpoints are available via 
a [OGCAPI community plugin](https://docs.geoserver.org/latest/en/user/community/ogc-api). WMTS is available via a default plugin called `GeoWebCache`.

GeoServer is a popular server component because of the initial ease of setup and configuration in a webbased environment. It includes an authentication and authorisation system and advanced styling options. Configuration via a webinterface also has some negative aspects related to reproducability and scaling. GeoServer is able to provide INSPIRE data via the [appschema plugin](https://docs.geoserver.org/latest/en/user/data/app-schema/index.html) and (INSPIRE plugin)[https://docs.geoserver.org/stable/en/user/extensions/inspire].

## Run as docker container

```
docker run -p8080:8080 kartoza/geoserver:2.22.0
```

- Navigate to http://localhost:8080/geoserver
- Login as usr:admin pwd:geoserver

Load some data:

- create a workspace
- create a datastore of type `folder of shapefiles`
- create a layer

Preview the layer.

Consider that in this setup the configuration is lost at every restart of the container. In a normal scenario, you would mount a volume to persist the geoserver configuration. Optimally you place the volume under version control, so you can easily revert a previous situation.

## INSPIRE plugin

A GeoServer [INSPIRE plugin](https://docs.geoserver.org/latest/en/user/extensions/inspire/index.html) is available which adds some of the INSPIRE specific metadata properties to the OWS capabilities documents. For example a link to the service metadata. The main feature is that it adds a bbox for each of the available projection systems. GeoServer is known to list all projection systems (many) as part of the capabilities response. You need to limit this number to prevent the bounds be written in each of this projections.

## Appschema support

[Appschema](https://docs.geoserver.org/latest/en/user/data/app-schema) is a plugin for GeoServer which adds the capability to work with hierarchival GML data, such as the INSPIRE Soil data model.

Onegeology has prepared [a workshop](https://onegeology.github.io/documentation/providingdata/server_setup/geoserver.html) on how to set up an appschema dataset in GeoServer. This is an advanced workshop. 

At Foss4G 2022 in Florence one of the maintainers of GeoServer, [GeoSolutions](https://www.geosolutionsgroup.com/), announced a [new approach to appschema in GeoServer](https://speakerdeck.com/simboss/publishing-inspire-datasets-in-geoserver-made-easy-with-smart-data-loader-and-features-templating-foss4g-2022-edition), based on templating. I have not been able to test it yet, but it may resolve some of the challenges of the appschema approach.

## GeoServer as a View service

GeoServer also provides options to publish view services (WMS or WMTS). Read more about this topic in the recipe [GeoCat Bridge and GeoServer](bridge-geoserver-geonetwork.md).

## Read more

Website: https://geoserver.org
Github: https://github.com/geoserver/
Docker: https://docker.osgeo.org/geoserver
Issue management: https://osgeo-org.atlassian.net/projects/GEOS/summary
OSGeo: https://www.osgeo.org/projects/geoserver/