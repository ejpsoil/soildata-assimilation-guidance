# Appschema WFS in GeoServer

*Status: contribution required*

GeoServer is an open source java imlementation of WFS, WCS, WPS, WMS, CSW. Various OGC API endpoints are available via 
a [OGCAPI community plugin](https://docs.geoserver.org/latest/en/user/community/ogc-api). WMTS is available via a default plugin called `GeoWebCache`.

GeoServer is a popular server component because of the initial ease of setup and configuration in a webbased environment. It includes an authentication and authorisation system and advanced styling options. Configuration via a webinterface also has some negative aspects related to reproducability and scaling. GeoServer is able to provide INSPIRE data via the [appschema plugin](https://docs.geoserver.org/latest/en/user/data/app-schema/index.html) and (INSPIRE plugin)[https://docs.geoserver.org/stable/en/user/extensions/inspire].

Onegeology has prepared [a workshop](https://onegeology.github.io/documentation/providingdata/server_setup/geoserver.html) on how to set up an appschema dataset in GeoServer. This is an advanced workshop. 

At Foss4G 2022 in Florence one of the maintainers of GeoServer, [GeoSolutions](https://www.geosolutionsgroup.com/), announced a [new approach to appschema in GeoServer](https://speakerdeck.com/simboss/publishing-inspire-datasets-in-geoserver-made-easy-with-smart-data-loader-and-features-templating-foss4g-2022-edition), based on templating. I have not been able to test it yet, but it may resolve some of the challenges of the appschema approach.