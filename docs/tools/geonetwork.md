# A discovery service in GeoNetwork

*Status: in progress*

[GeoNetwork](https://geonetwork-opensource.org) is a catalogue for registering spatial datasets and services. GeoNetwork does support multiple [metadata models](https://github.com/metadata101) based on XML, but it is optimized for iso19139:2007 and iso19115-2:2018. This recipe uses [docker](../utils/docker.md) to run GeoNetwork locally. It will discuss aspects such as schema plugins, creating metadata records, set up codelists and harvest metadata.

## Schema plugins

GeoNetwork provides a dynamic system to pre load schema plugins providing support for a variety of metadata models, such as iso19139:2007, iso19115-2:2018, national profiles based on these, DCAT, SensorML, EML/GBIF, etc. Many of these plugins are made available via https://github.com/metadata101. Before creating or importing records, verify that the relevant profile is available in the GeoNetwork instance.

Creation of metadata records is based on templates. For each metadata model a series of templates is available. Users select a relevant template for their use case while creating a new record to describe a resource. Any template is based on a specific metadata model, which determines which properties need to be described and in which format the record will be stored. 

GeoNetwork provides a number of transformation options for crosswalks between metadata models, but you should always consider some loss of information in these crosswalks. Crosswalks occur for example when a user requests a record in DCAT, while it is stored as iso19139:2007 in the database.

## Quick Start


- Start a GeoNetwork instance locally (initial startup may take some time)
  
  ```
  docker run -p 8080:8080 geonetwork:3.12
  ```

- Navigate to [http://localhost:8080/geonetwork](http://localhost:8080/geonetwork)
- Let's load some sample data. Select `Login`; login as usr:`admin`, pwd:`admin`
- Select `Admin console` > `Metadata records and templates`; Select `iso19139:2007`, click on `load samples` and `load templates`
- On `Admin console` > `Settings`, set the title and url of the instance.
- Let's set up some code lists (which populate the pull downs on the editor). Select `Classification systems` from `Admin console`.
- Select `From registry` in `Add thesaurus`.
- Click `Use INSPIRE registry` for the `Url` field
- Select language(s) and `INSPIRE theme register` and click `Upload`
- Add another thesaurus from registry, select `INSPIRE metadata code list register` and then `Spatial scope`.
- Continue with other relevant code lists, notice that you can also create a new code list manually.

## Create records

- On `Contribute` Editor board, click `Add new record`
- Select a template (they we're loaded on the previous step) and click `create`
- On the editor notice the view (eye) button on top right, you can switch the editor view between `Simple`, `Full` and `XML`.
- Notice the `validate` button, which provides a report on the level of completion of the record
- The associated resources side panel displays links to remote resources, such as data files, data services and thumbnails
- Notice that you can also import a record from a local xml file
- Notice that you can collapse the `save` button to `save as template`, in this way others can use this record as a base to start a new record

## Harvest records

Harvesting is the process of importing records from remote sources at intervals.

- Open `harvesting` from `Admin console`
- Select `OGC CSW 2.0.2` from `Add thesaurus`
- Provide a name for the harvester
- `Action on UUID collision` determines the behaviour when similar records are found in multiple remote endpoints
- Provide the url of the remote endpoint (for example https://www.geocatalogue.fr/api-public/servicesRest?request=GetCapabilities&service=CSW)
- Add a filter `Anytext:Soil`
- Set a interval schedule for the harvest (`only one run`)
- Harvesters have many additional options, you can read about it in the [documentation](https://geonetwork-opensource.org/manuals/trunk/en/user-guide/harvesting/index.html)
- Click `Save` and on the next screen `harvest`, a spinner starts to run, the harvest may take some minutes, depending of the size of the remote catalogue
- Notice a list of harvest run logs at the bottom of the screen, you can click `log` to check in more detail.
- If you increase logging on `Settings` to `DEV`, the logging on `harvesting` will also provide more details (in case of non explainable errors)

## Discovery from QGIS

The `metasearch` plugin is a default plugin in QGIS. 
- Open the plugin from the `Web` menu (or toolbar). 
- Click `New connection`. Provide a name for the connection and the url http://localhost:8080/geonetwork/srv/eng/csw
- Switch to the find tab, and search some records. 
- Select a search result, for some search results the `load data` button (lower left) is activated and you can load some data to the map

## Atom download service from GeoNetwork

You can enable an ATOM download service in GeoNetwork. GeoNetwork provides an opensearch API and will use the metadata content to generate Atom service and dataset files. You can read more about this option in the [documentation](https://geonetwork-opensource.org/manuals/3.10.x/en/tutorials/inspire/download-atom.html).

## Read more

- Website: https://geonetwork-opensource.org/
- GitHub repository: https://github.com/geonetwork
- Docker composition: https://github.com/geonetwork/docker-geonetwork/blob/main/4.2.1/docker-compose.yml
- Documentation: https://geonetwork-opensource.org/manuals/4.0.x/en
- Tutorial: https://geonetwork-opensource.org/manuals/trunk/en/tutorials/introduction
