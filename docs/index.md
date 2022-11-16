
# Publishing Soil data on the Web, using common practices and standards

 
The [INSPIRE directive](https://inspire.ec.europa.eu/inspire-directive/2) offers a set of regulations to publish data on the web. In the INSPIRE community a number of conventions, tools and practices are available to publish data according to the directive. Initially JRC published a series of technical guidelines, these days ‘good practice’ documents, contributed by the INSPIRE community, adopted by JRC, are becoming common. By following these guidelines you are guaranteed to be compliant to directive. However you can still publish data in alternative ways, in that case you need to declare how you confirm to regulations with that implementation. 

This wiki aims to list a series of cookbooks on the various options for publishing data according to adopted good practices. The practices are categorised in 3 levels:

- Minimal, based on a minimal effort 
- Traditional, following initial guidelines based on CSW, WMS, WFS, WCS 
- Experimental, following good practices, such as OGC API Features, Geopackage, RDF 

The practices are clustered in 6 topics: 
- Identification, namespaces and URI strategy
- Metadata & discovery 
- Data harmonization and Codelists
- View services
- Download services
- Quality of service

## Identification, namespaces and URI strategy  
An important aspect of publication on the web is identifier-persistence. To keep identification of metadata records, service endpoints, geometric features, etc. unchanged over time. To prevent broken links in websites or applications that link to aspects of the service.  
Within INSPIRE any identifier is combined with a namespace for that identifier. Or both aspects are combined into a single URI for the object. Namespaces need to be authoritative, but should not be likely to change. E.G. A project name is not a good namespace, because the project is bound to end after a certain period. Good namespaces are w3id.org, doi.org, data.gouv.fr.     
Some countries have a registry of nationally used namespaces, select a namespace from that registry, or have your namespaces be added to that registry. After adopting a namespace, you need to implement the aspect that requests to objects in that namespace resolve to your (INSPIRE) infrastructure. 

 
## Metadata & discovery 
The initial goal of any SDI is to describe its content, so potential users are aware what data is available, if the data is relevant and how they can fetch it, or who to contact for more details. Metadata of datasets and services is described in documents, which are made accessible via a discovery service. 

### Minimal 
In a minimal implementation you can describe your dataset as well as your service in a single document based on ISO19139. This ‘good practice’ is described in https://github.com/INSPIRE-MIF/gp-data-service-linking-simplification. Basic metadata editors exist, of which the most basic is Notepad++. 
These metadata documents can be placed in a Web Accessible Folder. Products exist which are able to ingest documents from such a folder and expose it as a CSW discovery service. Such an ingest point could be installed at a national level, to facilitate the European INSPIRE GeoPortal. 

### Traditional 
Traditionally INSPIRE defines documents which describe a dataset which are linked to other records which describe the service via which the datasets are exposed. This approach is described in the technical guidelines Metadata. These documents need to be exposed as a CSW discovery service using products such as GeoNetwork, ArcGIS Portal, pyCSW, deegree, Hale connect. The OGC CSW specification is extended with some specific INSPIRE elements, for multilinguality. 

### Experimental 
A good practice exists related to Geo-DCAT-ap. It relates to offering Geo-DCAT-ap as an additional metadata format. Currently use of ISO19139 is still required by all guidelines. However it is expected that it will also be possible to offer metadata in a DCAT ontology only. DCAT (if setup in a proper way) facilitates to let records be discoverable via google dataset search (and other search engines). 

Currently no ‘good practice’ exists to offer discovery services in alternative protocols then CSW. A good practice to adopt OGC API Records is being prepared. Opensearch, OData and SPARQL could be alternative discovery service protocols 
Data harmonization & code lists 

## Data harmonization and Codelists

The main aspect of INSPIRE is the harmonization of environmental data throughout Europe. INSPIRE does not requires you to refracture your work processes to fit the INSPIRE conventions, however in case your data infrastructure goes through a major refactor, INSPIRE conventions should be introduced. 
An important activity related to harmonisation is the adoption of INSPIRE codelists. This process has three steps: 
-	Inventarisation of codelists currently used 
-	Evaluation of the differences between local and INSPIRE codelists 
o	Some codelists are a full match 
o	Some codelists need to be partially extended, or values mapped 
o	Some codelists do not match with a INSPIRE codelist 
-	In cases where the INSPIRE codelist can not (fully) be adopted, the codelist needs to be published in a local repository 

### Minimal 
GeoPackage is an upcoming format to persist harmonised data. Since it is a relational database, the transformation from alternative relational models is relatively easy. 
The most basic form of publishing a codelist is to place a single file for the complete list on a web location and reference values in it as http://example.com/codelist.xml#concept (see for example http://schemas.opengis.net/iso/19139/20070417/resources/Codelist/gmxCodelists.xml) 

### Traditional 
Tools like Hale Studio and FME can be used to set up an alignment from data in a relational datamodel to a UML XSD based INSPIRE model. 
Some tools (deegree, geoserver, extraserver) offer on the fly transformation as part of the download service, the alignment is then defined in the service configuration. 

### Experimental 
Since the soil theme is heavily O&M oriented it makes sense to use Sensor Observation Service as a download service (in stead of WFS). Various tools (52 north, frostserver, istSOS) offer SOS, or its follow-up SensorThings API directly on any relational database. 
Various groups prefer to work with RDF/OWL over UML/XSD these days. Various tools exist which map relational models to RDF (Ontop, Coby, R2DQ, TopBraid). 

## View services 
View services offer a visualisation of the soil data on a map. The TG prescribes that for each measured soil parameter a map layer is made available. Map layers can relate to actual site obervations (soil profiles) as well as derived soil grids. 

### Minimal 
In a minimal implementation the WMTS (tiling) standard is used to provide view services. The featureinfo operation is not mandatory (however very usefull for endusers), so it can be left out, since it is quite complex to set up in case the data behind the service is harmonised. 
Tile services have very low risk in respect to Quality of Service and scale very well. Tile services are not optimal for dynamic data. Adoption of WMTS is not wide in geospatial clients. 
Various products offer WMTS, such as QGIS, Mapproxy, GeoServer, ArcGIS. Note that the required INSPIRE extension in the getcapabilities response can be implemented using a tailored xml document, separate from the service. 

### Traditional 
Most view services are based on WMS, which are quite easy to set up in products such as GeoServer, ArcGIS Server, MapServer, Extraserver, deegree, Hale Connect. 

### Experimental 
OGC API Tiles is the upcoming standard for map visualisation. There is no good practice for adoption of OGC API Tiles in preparation yet. Vector tiles would be an interesting alternative view service practice. 

## Download services  
Facilitates to download data 

### Minimal 
The INSPIRE Atom Service is a minimal service implementation on a series of downloadable files placed in a web accessible folder 

### Traditional 
WFS and WCS are commonly used to download Featurecollections and Coverages 

### Experimental 
SOS and SensorthingsAPI offer an alternative download option for themes such as Soil 
SPARQL is the typical endpoint for downloading RDF data, however no good practice document exists yet describing this approach 

## Quality of Service 
Via the quality of service conventions data providers report about the quality of their services. Aspects which are monitored are: 

- Availability (how many downtime did a service have in a period) 
- Performance and capacity (a period in which performance and capacity requirements are not met, is considered downtime) 
- Usage (how much is the service used) 

 

