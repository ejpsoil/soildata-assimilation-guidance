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

Suppose you intend to publish results of chemical analysis appraising the
Zinc content of the soil. The INSPIRE code-lists do not presently include that
metal as property, therefore an additional code-list item must be created.

The first action is to identify in which code-list the item should be added.
Physio-chemical properties like Zinc content appear associated with the Horizon
or Layer class in soil ontologies, thus the appropriate code-list is [ProfileElementParameterNameValue](http://inspire.ec.europa.eu/codelist/ProfileElementParameterNameValue). Open that URI in your browser an go through the respective r3gistry record.

At the bottom of the page r3gistry lists the items for this code-list, in this
case they are [biological
parameter](http://inspire.ec.europa.eu/codelist/ProfileElementParameterNameValue/biologicalParameter),
[chemical
parameter](http://inspire.ec.europa.eu/codelist/ProfileElementParameterNameValue/chemicalParameter)
and [physical
parameter](http://inspire.ec.europa.eu/codelist/ProfileElementParameterNameValue/physicalParameter). Follow the URI to the chemical parameter, in that page there is another list of items, including other metals. The new item for Zinc should therefore be created at this same level in the hierarchy.

The list below presents a RDF document defining a new sub-item for Zinc within the physical parameter code-list.
The URI for this item is `http://example.com/my-soil/zincContent`. As this item
is not directly in a INSPIRE code-list, its URI must refer to an authority that
you control, i.e. you or your institution are the responsible party for the
code-list item, its definition and publication. For more on this, check the [URI strategy](uri.md) document. 

```turtle
@prefix skos: <http://www.w3.org/2004/02/skos/core#> .
@prefix inspire_cl_profile: <http://inspire.ec.europa.eu/codelist/ProfileElementParameterNameValue/> .
@prefix glosis_cl: <http://w3id.org/glosis/model/codelists#> .
@prefix my_soil: <http://example.com/my-soil/> . 

my_soil:zincContent a skos:Concept;
        skos:prefLabel "Zinc content"@en ;
        skos:definition "Zinc content of the soil within a profile element." ;
        skos:broader inspire_cl_profile:physicalParameter ;
        skos:inScheme inspire_cl_profile: ;
        skos:related glosis_cl:physioChemicalPropertyCode-Zin .
```
 
The RDF above contains the basic SKOS elements: a Concept instance, a label, an
annotation defining the concept and a reference to the parent item with the
`skos:broader` code-list. The last two triples need a closer look. The item is
declared as belonging to a Scheme with the URI
`http://inspire.ec.europa.eu/codelist/ProfileElementParameterNameValue/`. While
the later is not actually declared as such in `r3gistry`, it is still important to
convey the nature of this item as part of structured INSPIRE code-list. Finally,
the `skos:related` predicated is employed to refer a similar property in the
GloSIS web ontology. 

### Extend a GloSIS code-list




Publishing your own code-list
------------------------------
