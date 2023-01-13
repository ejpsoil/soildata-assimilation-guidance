# R

[r](https://www.r-project.org/) is a statistics utility commonly used in the soil statistics. R is typically extended with a series of libraries, like [GDAL](gdal.md) and [grassgis](https://grass.osgeo.org/). 
Due to the amount of plugins required, some with a difficult installation procedure and potential high use of resources, the use of virtualisation, such as Docker, is quite common.

## Soil Mapping spring school

R is used to generate [SoilGrids](https://soilgrids.org/) from the global Soil Profile database, [WoSIS](https://www.isric.org/index.php/explore/wosis).

At intervals ISRIC organises a [spring school on soil mapping using R](https://dev.isric.org/utilise/capacity-building/springschool) in case you're interested in this topic.

## Accessing SQL data from R.

Since many soil observation data is stored in relational databases, but processing in R requires a flat data view, it is relevant to have reproducable conventions to access sql data in R. David Rositter described an [approach to load soil profile data into R from sqlite](https://www.css.cornell.edu/faculty/dgr2/_static/files/R_PDF/R_HWSD.pdf) in 2017. For PostGreSQL a similar approach should be possible using [RPostres](https://github.com/r-dbi/RPostgres).  

## Read more

Website: https://www.r-project.org/
Docker: https://hub.docker.com/r/rocker/geospatial