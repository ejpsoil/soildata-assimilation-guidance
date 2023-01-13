# FROST server

*Status: review required*

[Frost](https://fraunhoferiosb.github.io/FROST-Server/) is an open source server implementation of [OGC Sensorthings](https://www.ogc.org/standards/sensorthings), a modern data exchange standard for Sensor Data. 
Because the INSPIRE Soil model is based on [Observations and Measurements](https://www.ogc.org/standards/om), the Sensorthings API can be used 
to provide sensor download services, with the soil profile and horizons as `FeatureOfInterest`. Sensorthings API is generally easier to set up for administrators and easier to consume by clients then INSPIRE Soil data in GML. INSPIRE has recently adopted a [good practice on Download services based on SensorThings API](https://inspire.ec.europa.eu/good-practice/ogc-sensorthings-api-inspire-download-service).

Kathi Schleidt has prepared a [workshop on inspire data in sensorthings API](https://datacoveeu.github.io/API4INSPIRE/dissemination/Workshop-2020-11-19.html). Also have a look at her sensor presentation in the [2022 edition of the training](https://wur.yuja.com/V/Video?v=184380&node=785951&a=1565884354&autoplay=1). After the 2022 training Kathy together with colleagues from Fraunhofer IOSB has put together a `SoilThings` variant of STA. The experiment has proven to be a most interesting use case, it has shown where flexibility has to be added in the STA model (these changes will be integrated in the upcoming 2.0 version of the standard). The cool thing about this API is that it allows you to do queries like the following: `give me all plots that contain a profile that contains a horizon on which pH H2O is measured`; while the query syntax can be a bit daunting, the other existing technologies for provision (WFS and the new OGC API) would require 5 separate requests to do this. Links: 

- Base SoilThings API: https://ogc-demo.k8s.ilt-dmz.iosb.fraunhofer.de/FROST-SoilThings/v1.1/ 
- Query on all plots that contain a profile that contains a horizon on which pH H2O is measured, including the measurements: 

    https://ogc-demo.k8s.ilt-dmz.iosb.fraunhofer.de/FROST-SoilThings/v1.1/SoilPlots?$count=true&$select=name&$filter=ObservedProfile/IsDescribedByHorizon/Datastreams/ObservedProperty/name%20eq%20%27pH%20H2O%27&$expand=ObservedProfile($select=name;$expand=IsDescribedByHorizon($select=name;$expand=Datastreams($select=name;$filter=ObservedProperty/name%20eq%20%27pH%20H2O%27;$expand=ObservedProperty($select=name),%20Observations))) 


## Read more

- Good practice Sensorthings: https://inspire.ec.europa.eu/good-practice/ogc-sensorthings-api-inspire-download-service
- Github repository: https://github.com/FraunhoferIOSB/FROST-Server
- Documentation: https://fraunhoferiosb.github.io/FROST-Server/
- Workshop: https://datacoveeu.github.io/API4INSPIRE/dissemination/Workshop-2020-11-19.html