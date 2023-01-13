# R

[r](https://www.r-project.org/) is a statistics utility commonly used in the soil statistics. R is typically extended with a series of libraries, like [GDAL](gdal.md). 
Due to the amount of plugins required, some with a difficult installation procedure and potential high use of resources, the use of virtualisation, such as Docker, is quite common.

## Soil Mapping spring school

R is used to generate the [SoilGrids](https://soilgrids.org/) from the global Soil Profile database, [WoSIS](https://www.isric.org/index.php/explore/wosis).

At intervals ISRIC organises a [spring school on soil mapping using R](https://dev.isric.org/utilise/capacity-building/springschool).

## Accessing postgres data from R.

Since many spatial data is stored in PostGreSQL in a relational way, but processed in R, requiring a flat data view, it is relevant to have reproducable conventions to access PostGreSQL data in R.

## Read more

Website: https://www.r-project.org/
Docker: https://hub.docker.com/r/rocker/geospatial