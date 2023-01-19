# deegree

*Status: contribution required*

An open source java server implementation of WMS, WMTS, CSW, WCS, WFS, WPS.

Deegree has 2 options to publish rich GML data. 

- Using a relational database and a mapping configuration to generate the GML
- Using a `blob` storage to provide individual features without any processing

The second is easy to setup and efficient when users often request full datasets. The second approach may get problematic if users use advanced filters to select subsets of the dataset.

## Get started with deegree

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

## Featured implementations

Some implementations of INSPIRE Soil data services based on deegree

- [Baden Württemberg, Germany](https://lgrbwissen.lgrb-bw.de/bodenkunde)
- [Brandenburg, Germany](https://geoportal.brandenburg.de/de/cms/portal/geodaten/diensteanbieter/dienste/psv/landesamt-fuer-bergbau-geologie-und-rohstoffe-lbgr/bGFuZC1sYmdyLWJi)


## Read more

deegree is maintained by a company called [LatLon](https://www.lat-lon.de/) and others

- Website: http://www.deegree.org/
- Documentation: https://download.deegree.org/documentation/3.4.32/html/
- Download: https://www.deegree.org/download/
- Docker: https://hub.docker.com/r/deegree/deegree3-docker/

