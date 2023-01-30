# INSPIRE Soil in a relational database

This recipe describes an approach where data is harmonised to a common relational database.

The INSPIRE community has recently started an interesting activity to set up [guidelines on how to share INSPIRE data as a relational database](https://github.com/INSPIRE-MIF/gp-geopackage-encodings). More specifically a database in the [GeoPackage format](http://www.geopackage.org/), which is a specialisation of the [SQLite format](https://www.sqlite.org/). This will result in a series of new good practices on alternative approaches for data harmonization for various INSPIRE themes and use cases. 

Idea behind the activity is that communities around a certain topic come together to develop a common relational model which substantially represents the INSPIRE UML model. This aspect can be validated by providing a mapping document which maps the relational model to the INSPIRE UML or GML model.
This activity is supported by [a template](https://github.com/INSPIRE-MIF/2017.2/blob/master/template/template.md) that communities can use to share their work with the wider INSPIRE community. 

After an initial effort of defining and describing the alternative model, a typical workflow to publish harmonised data is as follows:

- Users download the GeoPackage template as an empty database
- Users populate the database from various sources using their favourite tool ([r](../utils/r.md), [python](../utils/python.md), [FME](https://www.safe.com/fme/fme-desktop/), [Hale studio](./hale-studio.md), [DBeaver](https://dbeaver.io/))
- Users publish the database as an [Atom service](./webdav.md) or [OGC API Features](./pygeoapi.md).

## Sub models for dedicated use cases

The INSPIRE Model is able to capture a number of use cases, which are usually not combined in a single database. By creating a dedicated (minimal) database model for specific use cases, the database model will be smaller and easier to understand. The following use case can be identified:

- A Soilbody polygon map based on Derived Soil Profiles
- A point map of Observed Soil Profiles
- Grid data of derived soil property distribution

For each of the cases a Layer or Horizon oriented approach can be used. 

![Soil model](./img/soil-model.png)

## ISO25258 in a PostGres database

As part of the [Soils4africa project](https://www.soils4africa-h2020.eu/) ISRIC and partners are experimenting with a [ISO25258](https://www.iso.org/standard/44595.html) model, similar to the INSPIRE Soil model, encoded in a relational PostGres database. It is interesting to evaluate if this effort can be ported to GeoPackage and form a starting point for the initial effort.

## Read more

At the masterclass edition 2023 Stefania Morrone (Epsilon) presented an approach to use geopackage as an alternative encoding for Soil data download services.

<iframe title='use geopackage as an alternative encoding for Soil data download services' width="560"  height="315"  src="use geopackage as an alternative encoding for Soil data download services" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen loading="lazy"></iframe>

- [Good practice on GeoPackage](https://github.com/INSPIRE-MIF/gp-geopackage-encodings)
- [Model Transformation Rules for alternative encodings](https://github.com/INSPIRE-MIF/model-transformation-rules)




