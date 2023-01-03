# deegree

An open source java server implementation of WMS, WMTS, CSW, WCS, WFS, WPS.

Start a deegree instance locally using the docker hub image as:

```
docker run --name deegree -d -p 8080:8080 deegree/deegree3-docker
```

Initial start will take some time, then proceed with your browser to [http://localhost:8080/deegree-webservices](http://localhost:8080/deegree-webservices).

The deegree website contains a [detailed quick start](https://download.deegree.org/documentation/3.4.1/html/lightly.html) on how to import and operate a sample workspace

Setting up a database and importing GML Data is managed via a command line client. The command line client can be accessed via:

```
docker exec -w /opt deegree java -jar deegree-tools-gml.jar -help
```

The client tools are described in the [online manual](https://download.deegree.org/documentation/3.4.32/html/#deegree-gml-tools). An example call to export a database creation script to reflect the Soil.xsd schema:

```
docker exec -w /opt/ deegree java -jar deegree-tools-gml.jar SqlFeatureStoreConfigCreator --format=ddl --dialect=postgis --cycledepth=1 -schemaUrl=https://inspire.ec.europa.eu/schemas/so/4.0/Soil.xsd
```

## Read more

deegree is maintained by a company called [LatLon](https://www.lat-lon.de/) and others

- Website: http://www.deegree.org/
- Documentation: https://download.deegree.org/documentation/3.4.32/html/
- Download: https://www.deegree.org/download/
- Docker: https://hub.docker.com/r/deegree/deegree3-docker/

