# View services with QGIS server

*Status: contributions required*

QGIS started as a GIS desktop application. In recent years the community prepared a server edition of QGIS. The server provides WMS, WFS and since recently OGC API Features. 

The advantage of using QGIS both as a desktop and server component is that the maps generated on the server will be exactly the same as those prepared on a desktop client.

## Prepare a map service in QGIS Desktop

Name your project project.qgs

On project settings, open the WMS properties to add relevant metadata

## Publish a map service

We're running QGIS server as a docker container based on https://hub.docker.com/r/camptocamp/qgis-server

```
docker run -p 8080:80 --volume=$PWD:/etc/qgisserver camptocamp/qgis-server
```

Try the service via

```
http://localhost:8080/?SERVICE=WMS&REQUEST=GetCapabilities
```

## QGIS Desktop as a client for INSPIRE services

It can act as a client for WMS, WMTS, WCS, Sensorthings API and OGC API Features.

QGIS data model is based on data layers and is therefore less optimal for hierachical vector data as used in INSPIRE. There have been initiatives to bring hierarchical data to QGIS, such as [GMLAS](https://plugins.qgis.org/plugins/gml_application_schema_toolbox/) but adoption has been limited. The Application Schema functionality has been introduced in GDAL/OGR, the QGIS plugin builds on top of it. OGR converts the contents of the GML to a relational database. Individual tables from that database are loaded in the QGIS interface.



