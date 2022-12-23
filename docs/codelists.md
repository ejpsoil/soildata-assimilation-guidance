
The adoption of INSPIRE code lists has three steps:

- Collecting the code lists currently used
- Evaluation of the differences between local and the INSPIRE code lists
  - Some code lists are a full match
  - Some INSPIRE code lists need to be extended, or values mapped
  - Some code lists do not match with an INSPIRE code list
- In cases where the INSPIRE code list cannot (fully) be adopted, the code list needs to be published in a local repository

Adoption of a dedicated codelist is relevant for example for Soil classification. Many of the national soil classification systems have much more detail than the [World Reference Base](https://inspire.ec.europa.eu/codelist/WRBSpecifierValue), as suggested to be used by the [TG Soil](https://inspire.ec.europa.eu/id/document/tg/so).

| Please note that the harmonization meant here is harmonization of the description of the data, for example describing a soil observation of pH KCl with dilution 1:10 in the same way across Europe. The harmonization of the data itself, for example transforming pH KCl values to pH H2O values, is a separate step and not described in this wiki. More information on that harmonization can be found in D6.1 chapter 3.5 page 122. |
| --- |

The soil theme has a large number of code lists, ranging from soil type to ranges of grain size. Many code lists originate from the FAO soil classification and are published in the [INSPIRE registry](https://inspire.ec.europa.eu/registry/).

### Implementation options for extending a code list

#### Minimal

The most basic form of publishing an alternative or extended code list is to place a code list file on a web location and reference values in it as [http://example.com/codelist.xml#concept](http://example.com/codelist.xml#concept) (see for example [http://schemas.opengis.net/iso/19139/20070417/resources/Codelist/gmxCodelists.xml](http://schemas.opengis.net/iso/19139/20070417/resources/Codelist/gmxCodelists.xml))

#### Traditional

Extended code lists can be published in a local or national instance of the [Re3gistry](https://github.com/ec-jrc/re3gistry) software. This open source project is hosted by JRC to facilitate the INSPIRE registry.

#### Experimental

A standard for the definition of code lists is [Simple Knowledge Organization System](https://www.w3.org/TR/skos-reference/) (SKOS). Any SPARQL endpoint can be used to publish a code list based on SKOS. Software exists which facilitates the consumption of SKOS data from a SPARQL endpoint in a human friendly way. An example is [Skosmos](https://skosmos.org/).

A powerfull aspect of SKOS is that you can link from a concept to existing concepts in other codelists using link relations such as: sameAs, Broader, Narrower.
