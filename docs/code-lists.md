Code-lists
==========

INSPIRE
-------

Code-lists specified for the Soil domain within the INSPIRE directive are
described in the report [D2.8.III.3 Data Specification on Soil – Technical
Guidelines](https://inspire.ec.europa.eu/documents/Data_Specifications/INSPIRE_DataSpecification_OI_v3.0rc3.pdf).
A brief overview of these code-lists is offered below.

- **[LayerGenesisProcessStateValue](http://inspire.ec.europa.eu/codelist/LayerGenesisProcessStateValue)** - an indication of whether the process specified in layerGenesisProcess is
    ongoing or ceased in the past.
- **[LayerTypeValue](http://inspire-registry.jrc.ec.europa.eu/clr/LayerTypeValue)** - classification of a layer according to the concept that fits the purpose,
    e.g. "topsoil".
- **[ProfileElementParameterNameValue](http://inspire.ec.europa.eu/codelist/ProfileElementParameterNameValue)**
  [extensible] - list of properties that can be observed to characterize the
profile element.
- **[SoilDerivedObjectParameterNameValue](http://inspire.ec.europa.eu/codelist/SoilDerivedObjectParameterNameValue)**
  [extensible] - list of soil related properties that can be derived from soil
and other data.
- **[SoilInvestigationPurposeValue](http://inspire.ec.europa.eu/codelist/SoilInvestigationPurposeValue)** - list of terms indicating the reasons for conducting a survey.
- **[SoilPlotTypeValue](http://inspire.ec.europa.eu/codelist/SoilPlotTypeValue)** - list of possible values that give information on what kind of plot the
    observation of the soil is made.
- **[SoilProfileParameterNameValue](http://inspire.ec.europa.eu/codelist/SoilProfileParameterNameValue)**
  [extensible] - list of properties that can be observed to characterize the
soil profile.
- **[SoilSiteParameterNameValue](http://inspire.ec.europa.eu/codelist/SoilSiteParameterNameValue)**
  [extensible] - list of properties that can be observed to characterize the
soil site.
- **[WRBQualifierPlaceValue](http://inspire.ec.europa.eu/codelist/WRBQualifierPlaceValue)** - list of values to indicate the placement of the Qualifier with regard to the
    WRB reference soil group (RSG), according to naming rules of the World
reference base for soil resources 2006, first update 2007.
- **[WRBQualifierValue](http://inspire.ec.europa.eu/codelist/WRBQualifierValue)** - list of possible qualifiers (i.e. prefix and suffix qualifiers of the World
    Reference Base for Soil Resources 2006, first update 2007).
- **[WRBReferenceSoilGroupValue](http://inspire.ec.europa.eu/codelist/WRBReferenceSoilGroupValue)** - list of possible reference soil groups (i.e. first level of classification
    of the World Reference Base for Soil Resources 2006, first update 2007).
- **[WRBSpecifierValue](http://inspire.ec.europa.eu/codelist/WRBSpecifierValue)** - list of possible specifiers, comprising only the values specified in the
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

The [GloSIS web ontology](https://github.com/rapw3k/glosis) includes a large
range of code-lists that are relevant within within the INSPIRE context. GloSIS
follows the pattern of the [Sensor, Observation, Sample, and
Actuator](https://www.w3.org/TR/vocab-ssn/) (SOSA) ontology, which is the
Semantic Web counterpart of the [Observations &
Measurements](https://www.ogc.org/standards/om) standard (O&M). These code-lists
are expressed with the [Simple Knowledge Onrganisation System](https://www.w3.org/2004/02/skos/) (SKOS), described
briefly below.

The GloSIS code-lists spread along four main categories:

- Values meeting **Descriptive** properties (FAO Guidelines of Soil
  Description):
    - Site/Plot (40)
    - Layer/Profile (90)
    - Surface (5)
- **Physio-chemical** properties (circa 80 items)
- **Procedures** of physio-chemical analysis (circa 230 items).


Code-lists in GloSIS are gathered in a [generic
module](https://rapw3k.github.io/glosis/docs/glosis-cl-doc/index-en.html). With
physcio-chemical analysis procedures in a [specific
module](https://rapw3k.github.io/glosis/docs/glosis-pc-doc/index-en.html).

Extending code-lists
--------------------

### SKOS

The SKOS ontology is remarkably simple, actually one of its strengths. At its
core are five primitives:

- **Concept** - a unit of though, an idea, a meaning, a category or an object.
  They are identified with URIs.

- **Label** - a lexical string used to annotate a concept. The same concept may
  be annotated in different natural languages.

- **Relation** - an semantic association between two concepts, conveying
  hierarchy or simply connecting concepts in a network.

- **Scheme** - an aggregator of related concepts, usually forming a hierarchy.

- **Note** - provides further semantics or definition to a concept. Often used
  to associate a concept to other knowledge graphs or other external resources.

The listing below presents an item from the GloSIS code-list for [crop
classes](http://w3id.org/glosis/model/codelists#CropClassValueCode). Its URI is
[http://w3id.org/glosis/model/codelists#cropClassValueCode-Ce_Ba](http://w3id.org/glosis/model/codelists#cropClassValueCode-Ce_Ba),
abbreviated with the Turtle syntax to `glosis_cl:cropClassValueCode-Ce_Ba`. The
label for this item is "Barley" in the English language, an annotation also
indicates its short notation: "Ce_Ba". Two object properties provide semantic
associations, this item is a narrower definition of the
`glosis_cl:cropClassValueCode-Ce` item (the "Cereals" concept), and is part of
the scheme `glosis_cl:cropClassValueCode`.  

```turtle
glosis_cl:cropClassValueCode-Ce_Ba a skos:Concept, glosis_cl:CropClassValueCode;
        skos:prefLabel "Barley"@en ;
        skos:notation "Ce_Ba" ;
        skos:inScheme glosis_cl:cropClassValueCode ;
        skos:broader glosis_cl:cropClassValueCode-Ce .
```

The next listing shows the scheme integrating the "Barley" concept above.
This object is very similar, with a label providing its name and some notes
adding further definition. The literal "table 9" indicates the source of this
code-list within the FAO Guidelines for Soil Description.

```turtle
glosis_cl:cropClassValueCode a skos:ConceptScheme ;
        skos:prefLabel "Code list for CropClassValue - codelist scheme"@en;
        rdfs:label "Code list for CropClassValue - codelist scheme"@en;
        skos:note "This  code list provides the CropClassValue."@en;
        skos:definition "table 9" ;
        rdfs:seeAlso glosis_cl:CropClassValueCode .
```

Using this simple pattern, a hierarchical code-list can be developed further
simply using the predicates `skos:inScheme`, `skos:broader` and `skos:narrower`.
The predicates `skos:topConceptOf` and `skos:hasTopConcept` can be further use
to indicate the root items in a concept hierarchy. 

### Extend an INSPIRE code-list with SKOS

### Extend a GloSIS code-list


Publishing your own code-list
------------------------------
