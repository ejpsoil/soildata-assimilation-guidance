Code-lists
==========

INSPIRE
-------

Code-lists specified for the Soil domain within the INSPIRE directive are
described in the report [D2.8.III.3 Data Specification on Soil – Technical
Guidelines](https://inspire.ec.europa.eu/documents/Data_Specifications/INSPIRE_DataSpecification_OI_v3.0rc3.pdf).
A brief overview of these code-lists is offered below.

- **[LayerGenesisProcessStateValue](http://inspire.ec.europa.eu/codelist/LayerGenesisProcessStateValue)**
  - an indication of whether the process specified in layerGenesisProcess is
    ongoing or ceased in the past.
- **[LayerTypeValue](http://inspire-registry.jrc.ec.europa.eu/clr/LayerTypeValue)**
  - classification of a layer according to the concept that fits the purpose,
    e.g. "topsoil".
- **[ProfileElementParameterNameValue](http://inspire.ec.europa.eu/codelist/ProfileElementParameterNameValue)**
  [extensible] - list of properties that can be observed to characterize the
profile element.
- **[SoilDerivedObjectParameterNameValue](http://inspire.ec.europa.eu/codelist/SoilDerivedObjectParameterNameValue)**
  [extensible] - list of soil related properties that can be derived from soil
and other data.
- **[SoilInvestigationPurposeValue](http://inspire.ec.europa.eu/codelist/SoilInvestigationPurposeValue)**
  - list of terms indicating the reasons for conducting a survey.
- **[SoilPlotTypeValue](http://inspire.ec.europa.eu/codelist/SoilPlotTypeValue)**
  - list of possible values that give information on what kind of plot the
    observation of the soil is made.
- **[SoilProfileParameterNameValue](http://inspire.ec.europa.eu/codelist/SoilProfileParameterNameValue)**
  [extensible] - list of properties that can be observed to characterize the
soil profile.
- **[SoilSiteParameterNameValue](http://inspire.ec.europa.eu/codelist/SoilSiteParameterNameValue)**
  [extensible] - list of properties that can be observed to characterize the
soil site.
- **[WRBQualifierPlaceValue](http://inspire.ec.europa.eu/codelist/WRBQualifierPlaceValue)**
  - list of values to indicate the placement of the Qualifier with regard to the
    WRB reference soil group (RSG), according to naming rules of the World
reference base for soil resources 2006, first update 2007.
- **[WRBQualifierValue](http://inspire.ec.europa.eu/codelist/WRBQualifierValue)**
  - list of possible qualifiers (i.e. prefix and suffix qualifiers of the World
    Reference Base for Soil Resources 2006, first update 2007).
- **[WRBReferenceSoilGroupValue](http://inspire.ec.europa.eu/codelist/WRBReferenceSoilGroupValue)**
  - list of possible reference soil groups (i.e. first level of classification
    of the World Reference Base for Soil Resources 2006, first update 2007).
- **[WRBSpecifierValue](http://inspire.ec.europa.eu/codelist/WRBSpecifierValue)**
  - list of possible specifiers, comprising only the values specified in the
    World Reference Base for Soil Resources 2006, first update 2007.

These code-lists are all available on-line through a
[r3gistry](https://ec.europa.eu/isa2/solutions/re3gistry_en/) instance. Each
item in these code-lists is dereferenceable by URI. 

Four of these lists are extendable, those expressing properties associated with
the different features of interest. These code-lists are design to serve as
umbrella structures for further specialisation according to local practices.
Extension is made in an hierarchical fashion, meaning that each additional item
must be a narrower definition of one of the existing items.

Besides these curated code-lists, the INSPIRE domain model also creates space
for code-lists of physio-chemical procedures of soil analysis. These are to be
referenced from the Observation instances related to the properties referred
above.

There is no practical guidance in the Technical Guidelines document on how to
extend or create new code-lists towards INSPIRE compliance. This document
provides broad guidelines on how to do so. 

GloSIS
------


Extending code-lists
--------------------

### SKOS

### Extend an INSPIRE code-list with SKOS

### Extend a GloSIS code-list


Publishing your own code-list
------------------------------
