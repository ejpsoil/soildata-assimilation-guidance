# OGC API Features with pygeoapi

*Status: in progress*

 In this recipe we'll set up an instance of [pygeoapi](https://pygeoapi.io) with some soil data. A good practice is available on how to provide an [INSPIRE download service based on OGC API Features](https://github.com/INSPIRE-MIF/gp-ogc-api-features/blob/master/spec/oapif-inspire-download.md). pygeoapi is an open source python server implementation of OGCAPI Features, Tiles, Maps, Coverages, Records and Processes.

## Quick start

The recipe is based on Docker. New to docker? Read more in the [Docker recipe](../utils/docker.md).

- With commandline in a new folder, run this command:

```
docker run -p 5000:80 geopython/pygeoapi:latest
```

- Navigate with your browser to http://localhost:5000 

If all went fine, you now see the default pygeoapi installation with sample data. In the next step we'll publish a new soil dataset.
pygeoapi's configuration is stored in a config file. The config file is encoded as [YAML](https://en.wikipedia.org/wiki/YAML). The first part configures the main settings of the service, in the second part individual datasets are configured.


- Download the Dutch INSPIRE dataset 'soil drills' from https://service.pdok.nl/bzk/brobhrpvolledigeset/atom/v1_1/downloads/brobhrpvolledigeset.zip
- Unzip the file to the work folder
- Create a local config file in the folder, download it from [here](https://github.com/geopython/pygeoapi/blob/master/pygeoapi-config.yml)
- Remove all the datasets from the config folder, and replace it for the following:

```yml
resources:
    bro:
        type: collection
        title: BRO
        description: Bro soil drills
        keywords:
            - soil
        links:
            - type: application/geopackage+sqlite
              rel: canonical
              title: source data
              href: https://service.pdok.nl/bzk/brobhrpvolledigeset/atom/v1_1/downloads/brobhrpvolledigeset.zip
              hreflang: en-US
        extents:
            spatial:
                bbox: [-180,-90,180,90]
                crs: http://www.opengis.net/def/crs/OGC/1.3/CRS84
        providers:
            -   type: feature
                name: OGR
                data:
                    source_type: GPKG
                    source: /pygeoapi/brobhrpvolledigeset.gpkg
                    gdal_ogr_options:
                        SHPT: POINT
                id_field: bro_id
                layer: borehole_research
```

- Mount config file in containter

```
docker run -p 5000:80 -v ${PWD}/pygeoapi-config.yml:/pygeoapi/local.config.yml -v ${PWD}/brobhrpvolledigeset.gpkg:/pygeoapi/brobhrpvolledigeset.gpkg  geopython/pygeoapi:latest
```


## Validation

JRC recently extended the [INSPIRE validator](https://inspire.ec.europa.eu/validator). It can now also validate an OGC API Features service.
Because docker runs locally, you need to set up a tunnel for the validator to access the local service. Read the [tunnel recipe](../utils/localtunnel.md) to see how to do that.

## Read more

At masterclass edition 2023 Tom Kralidis presented the geopython ecosystem, including pygeoapi.

<iframe title='Embedded Media titled: geopython' width="560"  height="315"  src="https://wur.yuja.com/V/Video?v=432913&node=1952041&a=194733222&preload=false" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen loading="lazy"></iframe>

The geopython community has prepared a [workshop on getting started with pygeoapi](https://dive.pygeoapi.io/).

- [Website](https://pygeoapi.io)
- [GitHub](https://github.com/geopython/pygeoapi)
- [Docker](https://hub.docker.com/r/geopython/pygeoapi)
- [Demo server](https://demo.pygeoapi.io/master)
- [Documentation](https://docs.pygeoapi.io)
- [OSGeo](https://www.osgeo.org/projects/pygeoapi) 
