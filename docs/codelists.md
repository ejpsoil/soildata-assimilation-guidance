
# Code Lists

Adoption of common code lists is an important aspect of data harmonization. For INSPIRE the [INSPIRE registry](https://inspire.ec.europa.eu/registry) is the source of common code lists. Other common codelists relevant to the soil domain are available in [FAO Agrovoc](https://agrovoc.fao.org/browse/agrovoc/en/), [GEMET](https://www.eionet.europa.eu/gemet/en/about/), [OGC definition server](https://www.ogc.org/def-server), [ISO TC211](http://www.isotc211.org/2005/resources/Codelist/gmxCodelists.xml), and [GLosis](https://github.com/rapw3k/glosis/blob/master/glosis_cl.ttl). At a national level [some countries](https://ec.europa.eu/isa2/solutions/re3gistry_en/) have implemented a national repository for common national codelists which may be relevant (either as a source or as a target, to publish an extended list).

The adoption of code lists has three aspects:

- Inventarisation of the code lists used in the source model
- Evaluation of the differences between local and common code lists
  - Some code lists are a full match
  - Some code lists need to be extended, or values mapped
  - Some local code lists do not (yet) have a common code list available
- In cases where the common code list cannot (fully) be adopted, the code list needs to be published in a local repository

Adoption of a dedicated codelist is relevant for example for Soil classification. Many of the national soil classification systems have much more detail than the [World Reference Base](https://inspire.ec.europa.eu/codelist/WRBSpecifierValue), as suggested to be used by the [TG Soil](https://inspire.ec.europa.eu/id/document/tg/so).

| Please note that the harmonization meant here is harmonization of the description of the data, for example describing a soil observation of pH KCl with dilution 1:10 in the same way across Europe. The harmonization of the data itself, for example transforming pH KCl values to pH H2O values, is a separate step and not described in this wiki. More information on that harmonization can be found in D6.1 chapter 3.5 page 122. |
| --- |

The soil theme has a large number of code lists, ranging from soil type to ranges of grain size. Many code lists originate from the FAO soil classification and are published in the [INSPIRE registry](https://inspire.ec.europa.eu/registry/).

## Implementation options for extending a code list

### Minimal

The most basic form of publishing an alternative or extended code list is to place a code list file on a web location and reference values in it as [http://example.com/codelist.xml#concept](http://example.com/codelist.xml#concept) (see for example [http://schemas.opengis.net/iso/19139/20070417/resources/Codelist/gmxCodelists.xml](http://schemas.opengis.net/iso/19139/20070417/resources/Codelist/gmxCodelists.xml))

| Cookbook | Software | Description |
| --- | --- | --- |
| [Code list as iso19135](tools/codelist-iso19135.md) | | Publish a xml file on a web location |


### Traditional

Extended code lists can be published in a local or national instance of the [Re3gistry](https://github.com/ec-jrc/re3gistry) software. This open source project is hosted by JRC to facilitate the INSPIRE registry.

| Cookbook | Software | Description |
| --- | --- | --- |
| [Code list in Re3gistry](tools/re3gistry.md) | [Re3gistry](https://ec.europa.eu/isa2/solutions/re3gistry_en/) | Publish a codelist in Re3gistry |

### Experimental

A standard for the definition of code lists is [Simple Knowledge Organization System](https://www.w3.org/TR/skos-reference/) (SKOS). Any SPARQL endpoint can be used to publish a code list based on SKOS. Software exists which facilitates the consumption of SKOS data from a SPARQL endpoint in a human friendly way. An example is [Skosmos](https://skosmos.org/).

A powerfull aspect of SKOS is that you can link from a concept to existing concepts in other codelists using link relations such as: sameAs, Broader, Narrower.

| Cookbook | Software | Description |
| --- | --- | --- |
| [SKOS codelist in semantic web](tools/virtuoso.md) | [Virtuoso](https://virtuoso.openlinksw.com/) [Skosmos](https://skosmos.org) | Publish a semantic web code list | 