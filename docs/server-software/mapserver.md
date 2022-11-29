# Mapserver

Mapserver, originally UMN Mapserver, is an open source server component which provides OWS services on a variety of data sources.
Mapserver is commonly used to set up INSPIRE View Services. A detailed guidance on how to use Mapserver to set up INSPIRE View Services is available at https://mapserver.org/ogc/inspire.html.

MapServer supports WFS and WCS as data exchange mechanisms. Mapserver is not able to expose datasets having a hierarchical structure, as common in many INSPIRE datasets, which makes MapServer less suitable to provide INSPIRE download Services using WFS. Stored queries are supported. MapServer can be used to set up a WCS Download service.

Mapserver runs as a [CGI](https://en.wikipedia.org/wiki/Common_Gateway_Interface) executable. The progream will start up as soon as a request arrives at the server. This makes mapserver very suitable for situations where many datasets are incidentally queried.

Mapserver is configured using [map files](https://www.mapserver.org/mapfile/). These mapfiles contain metadata for each layer, connection details to the datasource and styling rules for the vizualisation. Various tools exist which create mapfiles automatically, from for example a QGIS layer. See https://plugins.qgis.org/plugins/geocatbridge/.

Mapserver does not provide tile services (WMTS) itself, but is often combined with a separate tool, [mapcache](https://mapserver.org/mapcache/), which provides tile service on top of a MapServer instance. Tile services are generally better from a Quality of Service perspective, but less dynamic in update and styling options. An interesting option is to use the WMS option of Mapcache, which uses a cache of tiles as a source to provide WMS services.

- Website: https://mapserver.org
- Support: https://geographika.net