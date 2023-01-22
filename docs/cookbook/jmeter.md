# Capacity testing with jmeter

*status: in progress* 

[jmeter](https://jmeter.apache.org/) is a utility which can run a series of performance and capacity tests on a webservice.
The requirements for Capacity and Performance of an INSPIRE services are described in each of the technical guidelines for View, Download and Discoveryservices.
For example chapter 5 of [TG discovery services](https://inspire.ec.europa.eu/documents/Network_Services/TechnicalGuidance_DiscoveryServices_v3.1.pdf).

## Installation

Jmeter is a java program, which can run on most platforms (if java is installed). Download the latest version from the [apache website](https://jmeter.apache.org/download_jmeter.cgi).

## Web test plan

Jmeter is typically used to test the performance and capacity of a website or webservice. 

- Set up a web testing plan in jmeter by creating a list of sample requests (WMS/WFS/WCS, getcapabilities/getmap/getfeatere etc) 
- Run the test against the webservice
- Run the test with multiple users, notice the performance decrease of the service. Do not test against a production url, it wil severely impact the performance of that service. 

## Samples of requests:

- http://localhost:8080/geoserver/wms?request=getcapabilities
- http://localhost:8080/geoserver/ows?request=getcapabilities&version=2.0.0&service=wfs
- http://localhost:8080/geoserver/wcs?request=GetCapabilities&version=1.1.1&service=wcs
- http://localhost:8080/geoserver/gwc/service/wmts?REQUEST=getcapabilities
- http://localhost:8080/geonetwork/srv/eng/csw?REQUEST=GetCapabilities&version=2.0.1&service=CSW

## Read more

- [Website](https://jmeter.apache.org/)
- [Getting started with a web test plan](https://jmeter.apache.org/usermanual/build-web-test-plan.html)
- [Docker](https://hub.docker.com/r/justb4/jmeter)
- [Jmeter test module included in GeoNetwork](https://trac.osgeo.org/geonetwork/wiki/JMeterModule)