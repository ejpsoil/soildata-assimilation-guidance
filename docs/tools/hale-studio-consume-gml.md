# Consume Soil GML with Hale Studio

*Status: in progress*

Hale Studio is a familiar tool to transform data from a relational datamodel to INSPIRE Soil GML. However you can also use Hale Studio to connect to an existing WFS or load a GML file from a atom service and use Hale Studio to transform the data to a relational database model, so you can easily combine it with other relational databases.

!!!note

    If you're not interested in a specific target model, the [GMLAS functionality within OGR](https://gdal.org/drivers/vector/gmlas.html) may be sufficient for you. GMLAS will create a arbitrary relational model from any GML. With GDAL installed, and a gml file called *soil.gml*, run the following from commandline:

    ogrinfo -ro GMLAS:soil.gml

    ogr2ogr -f SQLite tmp.sqlite GMLAS:soil.gml -dsco SPATILIATE=YES -nlt CONVERT_TO_LINEAR -oo EXPOSE_METADATA_LAYERS=YES


In this recipe we will transform INSPIRE Soil GML from the city of Berlin to a relational database (GeoPackage).

- (Install and) Start the Hale Studio tool
- Import soil data from the Berlin Soil at https://fbinter.stadt-berlin.de/fb/atom/SO/SO_KrBwBoF2015.zip
- unzip the file to a new folder
- In hale studio, at File > Import > Source model, select the soil.xml included in the zip file
- At File > Import > Source data, select the `INSPIRE GML...gml` included in the zip file, select default options on the import wizard
- At File ...



