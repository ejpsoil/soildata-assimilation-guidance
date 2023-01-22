# View services with QGIS server

*Status: done*

[QGIS](https://qgis.org) started as a GIS desktop application. In recent years the community prepared a server edition of QGIS. The server provides WMS, WFS and since recently OGC API Features. 

The advantage of using QGIS both as a desktop and server component is that the maps generated on the server will display exactly the same as those prepared on a desktop client.

## Prepare a view service in QGIS Desktop

Use an existing QGIS project, or create a new project with some [sample data](https://data.isric.org).
If you include any data, place it in a folder within the current folder, so docker can access it as a docker mounted volume.

Name your project `project.qgs`.

On project settings, open the WMS properties to add relevant metadata.

## Publish a view service

Navigate with a console application to the folder which contains `project.qgs`.

We're running QGIS server as a docker container based on https://hub.docker.com/r/camptocamp/qgis-server. Run the QGIS container:

```
docker run -p 8080:80 --volume=$PWD:/etc/qgisserver camptocamp/qgis-server
```

Try the service via:

```
http://localhost:8080/?SERVICE=WMS&REQUEST=GetCapabilities
```

## Validate the view service

In order for the [INSPIRE validator](https://inspire.ec.europa.eu/validator/home/index.html) to access your local service, you need to set up a [tunnel](../utils/localtunnel.md).

## QGIS Desktop as a client for INSPIRE data

QGIS can act as a client for WMS, WMTS, WCS, CSW, Sensorthings API, OGC API Records and OGC API Features.

The QGIS data model is based on data layers and has minimalistic support for joins. QGIS is therefore less optimal for rich GML data as used in INSPIRE. There have been initiatives to bring hierarchical data to QGIS, such as [GMLAS](https://plugins.qgis.org/plugins/gml_application_schema_toolbox/) but adoption has been limited. The Application Schema functionality has been introduced in [GDAL/OGR](../utils/gdal.md), the QGIS plugin builds on top of it. OGR converts the contents of the GML to a relational database. Individual tables from that database are loaded in the QGIS interface.

