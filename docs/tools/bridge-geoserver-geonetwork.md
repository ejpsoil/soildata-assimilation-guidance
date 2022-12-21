# Metadata and View Service with GeoCat Bridge, GeoNetwork and GeoServer

In this cookbook we use GeoCat Bridge to publish a View Service on a soil dataset in GeoServer, combined with connected metadata in a GeoNeonetwork instance. 


[GeoCat Bridge](https://www.geocat.net/bridge/) is a plugin for QGIS or ArcMap developed by GeoCat in Bennekom, the Netherlands. Its goal is to 
facilitate the complex process of data publication from 
a well known desktop environment. An introductionary video is available at https://www.youtube.com/watch?v=f-sZCVnR9dc

[GeoServer](geoserver.md) is a server application providing OGC services on various database backends.

[GeoNetwork](geonetwork.md) is a server application providing a search interface and various api's on a collection of metadata records.

## Contents of the cookbook:

- Deploy GeoServer and GeoNetwork using Docker
- Install and configure the Bridge plugin
- Publish the dataset

## Deploy GeoServer and GeoNetwork using Docker

This cookbook assumes you have docker installed, but you can also install each of the components directly on your system. We use the QGIS edition of Bridge, but an [edition for ArcMAP](https://geocat.net/bridge) is also available.

Download the file https://github.com/ejpsoil/ejpsoil-data-publication-guidance/docker/bridge-geoserver-geonetwork/docker-compose.yml into an empty folder.
Navigate to the folder using a shell client (windows powershell or Linux/Apple shell) and run:

```
docker compose up
```

The above statement will download and deploy docker containers for GeoServer, GeoNetwork, PostGreSQL and Elastic Search. When finished (it may take a long time), you can access GeoServer at https://localhost:8000/geoserver and GeoNetwork at https://localhost:8001/geonetwork.

GeoNetwork starts with an error, because the database is empty. Navigate to `http://localhost:8001/geonetwork/srv/eng/admin.console#/metadata`, login as user: `admin`, password: `admin`. Select the `iso19139:2007` profile and click `Load templates` and `Load samples`.

## Install and configure the Bridge plugin

With QGIS, open the QGIS plugins repository and search for the `GeoCat Bridge` plugin. Install it.

After succesfull installation, we will configure our GeoServer and GeoNetwork instances.

Find the Bridge module on the toolbar or in the `Web > GeoCat Bridge > Publish` menu. From the publish window, open the `Servers` tab.

In the bottom left click the `New server` option and select `GeoServer`. Populate the fields.

Click `New server` again and select `GeoNetwork`. Populate the fields.

You are now ready to publish your first dataset from QGIS.

## Publish the dataset

Open the dataset to be published. Configure the layer with relevant styling and labels.

Open the publish window from the menu (or toolbar). 

Select the layer to be published. A metadata editor will open in which you can configure some metadata. You can also import embedded metadata.

Select the target servers for the publisation and click the publish button.

In the publiction result window, you can click preview (meta)data to evaluate if the publication was successfull
