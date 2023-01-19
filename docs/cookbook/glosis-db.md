# INSPIRE Soil in a relational database

This recipe describes an approach where data is harmonised to a common relational database.

The INSPIRE community has recently started an interesting activity to set up [guidelines on how to share INSPIRE data as a relational database](https://github.com/INSPIRE-MIF/gp-geopackage-encodings). More specifically a database in the [GeoPackage format](http://www.geopackage.org/), which is a specialisation of the [SQLite format](https://www.sqlite.org/). This will result in a series of new good practices on data harmonization for various INSPIRE themes and use cases. 

Idea behind the activity is that communities around a certain topic come together to develop a common relational model which substantially represents the INSPIRE UML model. 
This activity is supported by [a template](https://github.com/INSPIRE-MIF/2017.2/blob/master/template/template.md) that communities can use to share their work with the wider INSPIRE commuity. This template for example suggests to include a mapping which can facilitate a transformation of the data from the relational to the uml model and vice versa.

As soon as discussion has led to a conclusion, initial implementations have succeeded and the INSPIRE community confirmed the approach, then a typical harmonization effort would start from an empty database, following the `gpkg4soil` model. A user would insert their data using tools such as [r](../utils/r.md), [python](../utils/python.md), [FME](https://www.safe.com/fme/fme-desktop/), [Hale studio](./hale-studio.md), [DBeaver](https://dbeaver.io/), etc. or a dedicated (web) interface.

## SoilML in a PostGres database

As part of the [Soils4africa project](https://www.soils4africa-h2020.eu/) ISRIC and partners are experimenting with a SoilML model, similar to the INSPIRE Soil model, encoded in a relational PostGres database. It is interesting to evaluate in the masterclass if this effort can be ported to GeoPackage and form a starting point for the `gpkg4soil` effort.






