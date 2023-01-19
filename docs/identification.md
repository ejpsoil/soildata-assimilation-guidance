---
title: Identification, namespaces and URI strategy
summary: 
authors:
    - Paul van Genuchten
date: 2022-11-10
---

# Identification, namespaces and URI strategy

An important aspect of publication of data on the web is universal identification of objects within the European INSPIRE infrastructure. Identifiers are constant, unique and authoritative.

Resource identificiation is an aspect of step `4) data organization` in the [soil information workflow](https://www.isric.org/index.php/utilise/community-practice).

Any identifier is typically combined with a namespace for that identifier, or both aspects are combined into a single [Universal Resource Identifier (URI)](./cookbook/uri.md) for the object. Namespaces need to be authoritative but should not be sensible to change. For example, a project name is not a good namespace, because the project is bound to end after a certain period. Examples of good namespaces are: w3id.org, doi.org, data.gouv.fr.

Some countries have a registry of national namespaces ([Netherlands](http://inspirelab.geonovum.nl/namespaces), [Germany](https://registry.gdi-de.org/register/namespace/)). Select a namespace from that registry, or consider to add your namespace to such a registry.

### Minimal implementation

In a minimal implementation you can concatenate the database identifier, the featuretype and a namespace to create the INSPIRE identification for the object. For example:

_https://data.gouv.fr/inrae/collections/{featuretype}/items/{id}_

To facilitate users to use the INSPIRE identification to open the object in a web browser, you can set up a routing mechanism to forward the request to the location where the catalogue or feature server is located.

An example of such a routing rule in Apache webserver:

``` 
RewriteRule
  "https://data.gouv.fr/inrae/collections/(.\*)/items/(.\*)$"
  "http://data.recover.inrae.fr:8081/geoserver/vulter/wfs?typeNames=$1&featureID=$2&request=GetFeature"
```

### Traditional

The Technical Guidelines have a long section on identification within INSPIRE, including dates indicating the validity of a feature. An interesting blog about the use of Namespaces and Identifiers is written by Thorsten Reitz at [https://www.wetransform.to/news/2018/02/12/best-practices-for-inspire-ids/](https://www.wetransform.to/news/2018/02/12/best-practices-for-inspire-ids/).

### Experimental

These days the INSPIRE community recommends the use of URI's to identify things. This aspect is described in [https://inspire.ec.europa.eu/implementation-identifiers-using-uris-inspire-%E2%80%93-frequently-asked-questions/59309](https://inspire.ec.europa.eu/implementation-identifiers-using-uris-inspire-%E2%80%93-frequently-asked-questions/59309).

The aspect of identification is one of the major benefits of the upcoming OGC API's over traditional WMS, WFS, WCS. By design any feature, coverage, record or tile in OGC API has a unique URI, including content negotiation to be able to request the object in one of the available encodings (xml, json, html, Geopackage)

### Common mistakes

In many cases catalogue records and service definitions are populated manually in separate locations. Verify that at each location the identification and namespace of links between metadata and services are correct. Initially JRC did not have testing procedures to test these linkages. In practice a lot of these links where not correct, causing users not to be able to download a dataset from a search result in the national and INSPIRE GeoPortal.

JRC provides the [resource linkage checker](https://inspire-geoportal.ec.europa.eu/linkagechecker.html) to evaluate linkage of resources.

## Read more

See also the article about [uri strategy](./cookbook/uri.md)