# Consumer of Soil Data

In each of the articles we aim to describe the producer and consumer aspect of a topic. However in many cases we mainly describe the producer aspect. 
On this page we provide some specific consumer guidance and reference a number of articles which have explicit sections on the consumer aspect of discovering, accessing and downloading Soil Data.

Consuming and assimilating soil data has various challenges. 

- Discovery of data; not much data is advertised and on various platforms. In many cases the search engine is the only option to find something. In other cases there's too much similar results, which prevent you from easily finding the gems between the others. 
- Soil data is quite complex by nature; samples representing a soil horizon at a location, being analysed in some laboratory. These observations are used to derive a region sharing a common value, being vizualised on a map. Capturing this complexity in a standardised model has been quite a challenge. It resulted in [iso28258](https://www.iso.org/standard/44595.html) and derived models such as GLOSIS and the INSPIRE model. The process of adopting the standard requires expert skills, consider that working with this type of models is challenging, especcially in generic GIS tools such as QGIS/ArcGIS. It resulted in the fact that many organisations haven't fully adopted these models and provide the data in a local model or that the harmonised data is a subset of the original dataset. As a consumer it is hard to assess the level of implementation of the standard. 
- INSPIRE identified WFS as a relevant exchange mechanism for rich data such as soil data. However the industry has not moved with those efforts and hardly any tooling exists which is able to use WFS to explore the richness of WFS's providing rich (soil) data.
- As part of the harmonisation it is important to adopt common code lists, or, for unique concepts, extend existing code lists in a proper way. Many implementations have failed to follow this principle, resulting in a multitude of code list references which are redundant or under documented. In many cases a consumer will need to harmonize code list values as part of using the data.

Below some guidance on how to face some of these challenges:

## Discovery of data

## Multiple source data models

- [Hale Studio to import gml](tools/hale-studio-consume-gml.md) 

## Importing WFS data

- The [GDAL utility](utils/gdal.md) supports rich GML (GML Application Schema) and is able to import it from WFS and store it in for example a database.


## Code list mappings
