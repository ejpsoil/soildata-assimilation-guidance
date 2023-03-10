# A Pythonic metadata workflow

*status: in progress*

This recipe presents a minimalistic, however integrated and standardised approach to metadata management. Each data file on a file system will be accompagnied by a minimal YML metadata file. Crawler scripts will pick up these metadata files and publish them as iso19139 (or alternative models) on a catalogue. iso19139 is the metadata model currently [mandated by INSPIRE](https://inspire.ec.europa.eu/id/document/tg/metadata-iso19139) and very common in the GeoSpatial domain. Other communities tend to use different standards, such as [STAC](https://stacspec.org/en/about/stac-spec/) (Earth Observation), [DCAT](https://www.w3.org/TR/vocab-dcat-2/) (Open Data), [DataCite](https://schema.datacite.org/) (Academia), etc.

The recipe introduces you to a pythonic metadata workflow step by step.

## Initial

The inital step assumes a folder of data files on a network drive, sharepoint or git repository. Datasets stored on a database will not be considered for now, but can follow a similar workflow.

For each data file in the folder we will create a `metadata control file` (MCF). [MCF](https://geopython.github.io/pygeometa/reference/mcf/) is a convention from the [pygeometa](https://geopython.github.io/pygeometa) community. It is a [YAML](https://en.wikipedia.org/wiki/YAML) encoded subset of iso19139:2007. YAML is easy to read by humans and an optimal for content versioning (in git).

Consider to set up a virtual environment for the workshop:

```
virtualenv pygeometa && cd pygeometa && . bin/activate
```

Then install the pygeometa library.

```
pip install pygeometa
```

## Create an MCF

A minimal example of MCF is (see also a [more extended version](https://github.com/geopython/pygeometa/blob/master/sample.yml)):

```
mcf:
    version: 1.0

metadata:
    identifier: 3f342f64-9348-11df-ba6a-0014c2c00eab
    language: en
    hierarchylevel: dataset
    datestamp: 2023-01-01

spatial:
    datatype: grid

identification:
    language: eng
    title: Soilgrids sample Dataset
    abstract: This is a sample dataset for the EJP Soil Dataset Assimilation Masterclass
    dates:
        creation: 2023-01-01
    keywords:
        default:
            keywords: ["sample"]
    topiccategory:
        - geoscientificInformation
    extents:
        spatial:
            - bbox: [2,50,4,52]
              crs: 4326
    fees: None
    accessconstraints: otherRestrictions
    rights: CC-BY

contact:
    pointOfContact: 
        organization: ISRIC - World Soil Information
        url: https://www.isric.org
        city: Wageningen
        country: The Netherlands
        email: info@isric.org

content_info:
    type: image
    dimensions:
        - name: N
          units: g/m3
          min: 10
          max: 75
        - name: P
          units: mg/m3
          min: 30
          max: 75
        - name: K
          units: mg/m3
          min: 0.5
          max: 1.2

distribution:
    wms:
        url: https://maps.isric.org
        type: OGC:WMS
        rel: service
        name: soilgrids
```

- Use the above template to create a metadata file for a dataset. The file should have the same name as the dataset, but with an extension `.yml` or `.mcf`.

## Import existing metadata

- If the data file already has a metadata document (for example with a shapefile, if it contains a file with extension .shp.xml), you can try to import it using pygeometa. pygeometa requires to indicate the metadata schema in advance.

For iso19139:2007 use:

```
pygeometa metadata import path/to/file.xml --schema=iso19139
```

For fgdc (typically used with shapefiles) use: 

```
pygeometa metadata import path/to/file.xml --schema=fgdc
```

## Generate iso19139:2007

As soon as you have a folder of MCF's, you can use `pygeometa generate` to convert them to iso19139:2007.

```
pygeometa metadata generate path/to/file.yml --schema=iso19139 --output=some_file.xml
```

Or for a folder of files:

```
FILES="/path/to/*.yml"
for f in $FILES
do
  echo "Processing $f file..."
  pygeometa metadata generate $f --schema=iso19139 --output=$f.xml
done
```

Notice that you can also create your own template for the iso19139 generation. By using a customised template you're able to optimise the generated iso19139 records to facilitate for example better INSPIRE complience.

```
pygeometa metadata generate path/to/file.yml --schema_local=/path/to/my-schema --output=some_file.xml
```

## Import generated metadata to pycsw

[pycsw](https://www.pycsw.org) is a python based OGC reference implementation of [Catalog Service for the Web](https://www.ogc.org/standards/cat) and an early adaptor of [OGC API Records](https://ogcapi.ogc.org/records/) and [STAC Catalog](https://stacspec.org/en). We'll use pycsw via a [docker image](https://docs.pycsw.org/en/latest/docker.html) to publish the metadata records in a search service. We run it in `detach` mode so we can interact with the running container, type `docker stop pycsw` to stop the container.

```
docker run -d --rm --name pycsw -p 8000:8000 geopython/pycsw
```

We now have a running pycsw at http://localhost:8000/collections with some sample data. We will now remove the sample data and insert our metadata. For that reason we `mount` our current folder with xml files into the container

```
docker stop pycsw
docker run -d --rm --name pycsw -v ${PWD}:/metadata -p 8000:8000 geopython/pycsw
```

Now we can trigger pycsw admin to remove the default records and import our metadata. As part of the calls we reference the config file, which contains the connection details to the database.

```
docker exec -ti pycsw pycsw-admin.py delete-records -c /etc/pycsw/pycsw.cfg
docker exec -ti pycsw pycsw-admin.py load-records -c /etc/pycsw/pycsw.cfg -p /metadata -r
```

Check out the new content at http://localhost:8000/collections. Note that if you restart the container, all records are removed, because the database is currently not persisted on a volume.

Try to mount also a customised [configuration file](https://github.com/geopython/pycsw/blob/master/docker/pycsw.cfg) into the container, so you can optimise the configuration of the catalogue. Also have a look at the [INSPIRE extension](https://docs.pycsw.org/en/latest/profiles.html#inspire-extension) for pycsw.

## Evaluate Metadata and Discovery Service

You can evaluate individual iso19139 records in the [INSPIRE reference validator](https://inspire.ec.europa.eu/validator/home/index.html). Also you can evaluate the discovery service. If a service is running on localhost, use the [tunnel approach](../utils/localtunnel.md) to evaluate it.

## Access the service from QGIS

QGIS contains a default plugin called [MetaSearch](https://docs.qgis.org/3.22/en/docs/user_manual/plugins/core_plugins/plugins_metasearch.html) which enables catalogue searches from within QGIS. You can find the plugin in the `web` menu or on the toolbar as a set of binoculars. Open the plugin. First you need to set up a new service connection. On the services tab, click new, choose a name and add the url http://localhost:8080/csw. Click the `serviceinfo` button to view the metadata of the service. Now return to the `Search` tab and perform a search. Notice that if you select a search result, it highlights on the map and may trigger the `Add data` button in the footer (this depends on if QGIS recognises the protocol mentioned in the metadata). 

## Read more

At masterclass edition 2023 Tom Kralidis presented the geopython ecosystem, including pycsw.

<iframe title='Embedded Media titled: geopython' width="560"  height="315"  src="https://wur.yuja.com/V/Video?v=432913&node=1952041&a=194733222&preload=false" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen loading="lazy"></iframe>

- [github](https://github.com/geopython) the geopython community welcomes your questions and contributions.
- [pygeometa](https://geopython.github.io/pygeometa)
- [pycsw](https://pycsw.org)
- [pyGeoDataCrawler](https://github.com/pvgenuchten/pyGeoDataCrawler) is a set of scripts to manage MCF's. It supports importing MCF from a CSV, MCF inheritence, generate MCF from a data file, etc.
- [Model Driven Metadata Editor](https://github.com/osgeo/mdme) A web based GUI for populating MCF's.