# gdal

[OGR/GDAL](https://gdal.org) is a swiss army knife for spatial data. It can read u multitude of grid and vector formats and interact with OGC services. 

GDAL utilities interact with grids, OGR utilities interact with vector formats.


## Installation

- Windows; most easy install is [using Conda](https://gdal.org/download.html#conda). Other option is via [ms4w](https://ms4w.com/). Note that QGIS (C:\Program Files\QGIS 3.xx\bin\gdalinfo.exe) and [ArcMap](https://www.arcgis.com/home/item.html?id=1eec30bf5fa042a5a2227b094db89441) are also packaged with GDAL.
- Apple; [brew install gdal](https://formulae.brew.sh/formula/gdal)
- Ubuntu; [add-apt-repository ppa:ubuntugis/ppa && apt update && apt install gdal-bin](https://mothergeo-py.readthedocs.io/en/latest/development/how-to/gdal-ubuntu-pkg.html)
- Debian; Use Conda
- [Docker](https://hub.docker.com/r/osgeo/gdal)

## GDAL exersize

- Get details of a gridded dataset

'''
gdalinfo https://files.isric.org/soilgrids/latest/data/bdod/bdod_0-5cm_mean.vrt
'''

- Get details of a geojson file

```
ogrinfo https://github.com/gregoiredavid/france-geojson/raw/master/cantons-avec-outre-mer.geojson
```

- Convert geojson to shapefile

```
ogr2ogr cantons.shp https://github.com/gregoiredavid/france-geojson/raw/master/cantons-avec-outre-mer.geojson
```

## GML Application Schema

In 2017 a large work on GDAL introduced support for [GML Application Schema](https://gdal.org/drivers/vector/gmlas.html). GDAL will read the schema of the xml and generate a relational database schema required to store the data. Verify that the build of GDAL includes GMLAS, it needs a special library XERCES

- Convert a gml file to geopackage

```
ogr2ogr -f GPKG test.gpkg GMLAS:/path/to/the.gml
```

- Use [DBeaver](https://dbeaver.io) or similar to evaluate the contents of the GeoPackage

## GDAL and Python

GDAL includes [python bindings](https://gdal.org/api/python_bindings.html), but many prefer the [Fiona](https://fiona.readthedocs.io/) and [Rasterio](https://rasterio.readthedocs.io/) library, which do the same in a more `pythonic` way.

## GDAL and R

[RGDAL](https://cran.r-project.org/web/packages/rgdal/index.html) and [sf](https://cran.r-project.org/web/packages/sf/index.html) provide bindings to GDAL within R.

## Read more

- [Website](https://gdal.org)
- [Docker](https://hub.docker.com/r/osgeo/gdal)
- [GMLAS](https://gdal.org/drivers/vector/gmlas.html)
- [Presentation on FOSS4G Europe 2017](https://inspire.ec.europa.eu/sites/default/files/presentations/20170718_qgis_gmlas_toolbox_groundwater_monitoring_brgm_oslandia_0.pdf)
