# WebDav & Atom

*Status: ready*

In the [technical Guidelines download services](https://inspire.ec.europa.eu/documents/technical-guidance-implementation-inspire-download-services) `INSPIRE atom services` are described to provide a light weight alternative to WFS and WCS, while fitting with all the aspects of a `webservice` as described in the implementing rules. 

This recipe describes a minimal approach which is based on placing a number of Atom-xml files along side the downloadable resources in a web accessible folder or webdav. Consider that WebDav is used as an example, any online file system would suffice. A plain apache webserver, Zenodo or even sharepoint or dropbox.

## WSGIDAV

Various webdav implmentations exist; [apache webdav](https://httpd.apache.org/docs/2.4/mod/mod_dav.html), [NGINX DAV](https://nginx.org/en/docs/http/ngx_http_dav_module.html), [SFTPGO](https://github.com/drakkan/sftpgo), [wsgidav](https://wsgidav.readthedocs.io/). For this recipe we'll use wsgidav, but others will work in a similar way.

WsgiDAV provides a docker image, with below statement you advertise the current folder via WebDAV.

```
docker run --rm -it -p 8080:8080 -v ${PWD}:/var/wsgidav-root mar10/wsgidav
```

Open http://localhost:8080 in your browser to see the file contents.

## ATOM files

Stop the container (ctrl-C). Create a new folder and copy your dataset(s) of choice into it. Create a file `service.atom.xml` and for each dataset a new text file with the same name, but the atom extension.

service.atom.xml is the `service feed` (comparable to the capabilities operation in OWS). The service feed will contain details about the service and link to each of the dataset feeds. Populate the service feed with (replace relevant sections):

```xml
<feed xmlns="http://www.w3.org/2005/Atom"
  xmlns:georss="http://www.georss.org/georss" 
  xmlns:inspire_dls="http://inspire.ec.europa.eu/schemas/inspire_dls/1.0" 
  xml:lang="en">
 <!-- feed title -->
 <title>XYZ Example INSPIRE Download Service</title>
 <!-- feed subtitle -->
 <subtitle>INSPIRE Download Service of Soil Properties data in Sahel region</subtitle>
 <!-- self-referencing link to this feed -->
 <link href="http://localhost:8080/service.atom.xml" rel="self" type="application/atom+xml"  hreflang="en" title="This document"/>
 <!-- link to Open Search definition file for this servicen (not implemented) 
<link rel="search" href="https://example.org/search/opensearchdescription.xml" type="application/opensearchdescription+xml" title="Open Search Description for XYZ download service"/> -->
 <!-- identifier -->
 <id>http://localhost:8080/service.atom.xml</id>
 <!-- rights, access restrictions -->
 <rights>Copyright (c) 2021, XYZ; all rights reserved</rights>
 <!-- date/time this feed was last updated -->
 <updated>2021-03-31T13:45:03Z</updated>
 <!-- author contact information -->
 <author><name>John Doe</name><email>doe@example.org</email></author>
 <category term="http://inspire.ec.europa.eu/metadata-codelist/SpatialDataServiceCategory/infoFeatureAccessService" scheme="http://inspire.ec.europa.eu/metadata-codelist/SpatialDataServiceCategory"/>
 <!-- entry for a "Dataset Feed" for a pre-defined dataset -->
 <entry>
    <!-- title for "Dataset Feed" for pre-defined dataset -->
    <title>soil properties ABC Dataset Feed</title>
    <!-- Spatial Dataset Unique Resource Identifier for this dataset-->
    <inspire_dls:spatial_dataset_identifier_code>wn_id1</inspire_dls:spatial_dataset_identifier_code> 
    <inspire_dls:spatial_dataset_identifier_namespace>https://example.org/</inspire_dls:spatial_dataset_identifier_namespace>
    <!-- link to dataset metadata record -->
    <link href="https://example.org/metadata/abcISO19139.xml" rel="describedby" type="application/xml"/>
    <!-- link to "Dataset Feed" for pre-defined dataset -->
    <link rel="alternate" href="http://localhost:8080/soilproperties.atom.xml" type="application/atom+xml"  hreflang="en" title="Feed containing the soil properties data"/>
    <!-- identifier for "Dataset Feed" for pre-defined dataset -->
    <id>http://localhost:8080/soilproperties.atom.xml</id>
    <!-- rights, access info for pre-defined dataset -->
    <rights>Copyright (c) 2002-2021, XYZ; all rights reserved</rights>
    <!-- last date/time this entry was updated -->
    <updated>2012-03-31T13:45:03Z</updated>
    <!-- summary -->
    <summary>This is the entry for soil properties ABC Dataset</summary>
    <!-- optional GeoRSS-Simple polygon outlining the bounding box of the pre-defined dataset described by the entry. Must be lat lon -->
    <georss:polygon>47.202 5.755 55.183 5.755 55.183 15.253 47.202 15.253 47.202 5.755</georss:polygon>
    <!-- CRSs in which the pre-defined Dataset is available -->
    <category term="http://www.opengis.net/def/crs/EPSG/0/4258" label="ETRS89"/>
 </entry>
</feed>
```

Notice that we're not implementing the actual opensearch search functionality yet. You can leave the `opensearchdescription` line empty for now. There are some external options to provide the opensearch, the Technical Guidance document actually includes a PHP script to facilitate opensearch.

Then for each dataset add a file `soilproperties.atom.xml`:

```xml
<feed xmlns="http://www.w3.org/2005/Atom"
 xmlns:georss="http://www.georss.org/georss" xml:lang="en">
    <!-- feed title -->
    <title>INSPIRE Dataset Soil properties Download</title>
    <!-- feed subtitle -->
    <subtitle>INSPIRE Download Service, of organisation XYZ providing dataset Soil Properties</subtitle>
    <!-- links to INSPIRE Spatial Object Type definitions for this predefined dataset -->
    <link href="https://inspire.ec.europa.eu/featureconcept/SoilProfile" rel="describedby" type="text/html"/>
    <!-- self-referencing link to this feed -->
    <link href="http://localhost:8080/soilproperties.atom.xml" rel="self" 
    type="application/atom+xml"
    hreflang="en" title="This document"/>
    <!-- upward link to the corresponding download service feed -->
    <link href="http://localhost:8080/service.atom.xml" rel="up" type="application/atom+xml" hreflang="en" title="The parent service feed document"/>
    <!-- identifier -->
    <id>http://localhost:8080/soilproperties.atom.xml</id>
    <!-- rights, access restrictions -->
    <rights>Copyright (c) 2021, XYZ; all rights reserved</rights>
    <!-- date/time this feed was last updated -->
    <updated>2021-03-31T13:45:03Z</updated>
    <!-- author contact information -->
    <author><name>John Doe</name><email>doe@xyz.org</email></author>
    <!-- download the pre-defined dataset in GML format in CRS EPSG:25832 --> 
    <entry>
        <title>soil properties in CRS EPSG:25832 (GML)</title>
        <link rel="alternate" href="http://localhost:8080/soilproperties_25832.gml" type="application/gml+xml;version=3.2" hreflang="en" length="34987" 
          title="soil properties dataset encoded as a GML 3.2 document in ETRS89 UTM zone 32N (http://www.opengis.net/def/crs/EPSG/0/25832)"/>
        <id>http://localhost:8080/soilproperties_25832.gml</id>
        <updated>2021-06-15T11:12:34Z</updated>
        <category term="http://www.opengis.net/def/crs/EPSG/0/25832" label="ETRS89 / UTM zone 32N"/>
    </entry>
    <!-- download the same pre-defined dataset in GML format in CRS EPSG:4258-->
    <entry>
        <title>soil properties in CRS EPSG:4258 (GML)</title>
        <!--file download link-->
        <link rel="alternate" href="http://localhost:8080/soilproperties_WGS84.gml" type="application/gml+xml;version=3.2" hreflang="en" length="37762" 
          title="soil properties encoded as a GML 3.2 document in WGS84 geographic coordinates (http://www.opengis.net/def/crs/OGC/1.3/CRS84)"/>
        <id>http://localhost:8080/soilproperties_WGS84.gml</id>
        <updated>2021-06-14T12:22:09Z</updated>
        <category term="http://www.opengis.net/def/crs/EPSG/0/4258" label="ETRS89"/>
    </entry>
    <!-- download the same pre-defined dataset in ShapeFile format in CRS EPSG:25832, ShapeFile is in a single zip archive.-->
    <entry>
        <title>soil properties in CRS EPSG:25832 (ShapeFile)</title>
        <link rel="alternate" href="http://localhost:8080/soilproperties_25832.zip" type="application/xshapefile" hreflang="en" length="89274" 
        title="soil properties dataset encoded as a ShapeFile in ETRS89 UTM zone 32N (http://www.opengis.net/def/crs/EPSG/0/25832)"/>
        <id>http://localhost:8080/soilproperties_25832.zip</id>
        <updated>2021-06-15T11:12:34Z</updated>
        <category term="http://www.opengis.net/def/crs/EPSG/0/25832" 
        label="ETRS89 / UTM zone 32N"/>
    </entry>
</feed>
```

Notice that you can provide multiple distributions for the same dataset (in various projections, translations or formats) to facilitate users.

Notice that the examples above incorperate ongoing work as described in https://github.com/INSPIRE-MIF/gp-data-service-linking-simplification/issues/63.

The docker container runs locally, so it can not be tested by the [INSPIRE Validator](https://inspire.ec.europa.eu/validator/test-selection/index.html). 
In [Local Tunnel](../utils/localtunnel.md) an approach is suggested to temporarily host a local service online, so you can run the validation.

Note that you have to update the self-references in atom files to use the tunneled web address. Then trigger the Atom validation:

![trigger the atom test](img/atom-test.png)

## Read more

An alternative Atom implementation exists in [GeoNetwork](https://geonetwork-opensource.org/). The approach is described at https://geonetwork-opensource.org/manuals/trunk/en/tutorials/inspire/download-atom.html and https://geonetwork-opensource.org/manuals/3.10.x/en/api/opensearch.html. GeoNetwork provides an internal and external mode, the external mode provides opensearch on a set of remote atom feeds. The internal mode generates the atom feeds from metadata records.

[Hale Studio](http://halestudio.org) provides an option to [generate a Atom feed](http://help.halestudio.org/latest/index.jsp?topic=%2Feu.esdihumboldt.hale.doc.user%2Fhtml%2Freference%2Fexport%2Finspiregml_data.html&resultof%3D%2522%2561%2574%256f%256d%2522%2520) while exporting a dataset to GML. The Hale Connect platform offers a [Atom based service endpoint](https://help.wetransform.to/docs/references/data/2018-03-07-reference-data-download-services) for every dataset published.

The [QGIS INSPIRE Atom plugin](https://plugins.qgis.org/plugins/inspireatomclient/) provides access to Atom services through QGIS.
