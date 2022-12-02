
# **View services**

The [TG View services](https://inspire.ec.europa.eu/documents/technical-guidance-implementation-inspire-view-services-1) prescribes the adoption of view services, which offer the capability of visualization of spatial data, possibly in a portal, GIS software or webpage. The service provides a quick view on the data, without the need to transfer the data itself to the client. The [TG Soil](https://inspire.ec.europa.eu/id/document/tg/so) prescribes that for each measured soil parameter a view service `layer` is made available online. Layers can relate to actual site observations (soil profiles) as well as parameter distribution grids or vector maps.

### Minimal

In a minimal implementation the Web Map Tiling Service (WMTS) standard is used to provide view services. Tile services have little risk with respect to the Quality of Service requirements. The alternative option, Web Map Service (WMS), is quite prone to exceed the performance limits in cases when it has to 'draw' a lot of data at once.

Tile services are however not optimal for dynamic data and may require a large (tile) storage. Also consider that the adoption of WMTS is less wide spread then WMS in GIS clients.

The getFeatureInfo (gfi) operation is not mandatory for INSPIRE (however useful for end users). Without getFeatureInfo, data used as a source for the view service can be minimal (geometry only).

| Product | Description |
| --- | --- |
| [Mapserver](https://mapserver.org/) | C based FastCGI WMS/WFS/WCS server implementation configured using 'mapfiles' |
| [Mapproxy](https://mapproxy.org/) | Python based tile (cache) server implementation, delegates on the fly rendering to a WMS server |
| [QGIS server](https://docs.qgis.org/3.16/en/docs/server_manual/index.html#qgis-server-manual) | The open source desktop GIS client deployed as a server application |

### Traditional

Most current view services are based on the Web Map Service (WMS) standard. These services are usually easy to set up on top of an existing traditional Web Feature Service or Web Coverage service implementation.

Examples are in the paragraph about download services.

### Experimental

OGC API Tiles is an upcoming standard for map visualization. The Open Geospatial Consortium (OGC) is preparing the final standardization documents, however initial implementations are available in. There is no good practice document for adoption of OGC API Tiles within INSPIRE in preparation yet.

| Product | Description |
| --- | --- |
| [GeoServer](https://geoserver.org/) | OGC API Tiles is available via the OGC API community plugin |
| [pygeoapi](http://pygeoapi.io/) | Python package which exposes a cache of tiles as OGC API Tiles |
| [LDProxy](https://github.com/interactive-instruments/ldproxy) | Java based opensource OGC API implementation |

Within the sector there is a shift to the use of Vector tiles for vector map visualization. Vector tiles usually require less bandwidth and provide a sharper view on the data, especially on mobile devices with high resolution. INSPIRE does not provide Guidance on the use of vector tiles yet. The [MapBox Vector tiles specification](https://github.com/mapbox/tilejson-spec) is a common API used to publish vector tiles.
