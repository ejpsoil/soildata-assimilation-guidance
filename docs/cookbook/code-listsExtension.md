---
Author: Luis de Sousa
Date: 2023-01-18
Title: Extending Code Lists
---


Code-lists
==========

This recipe describes an approach to extend an INSPIRE codelist.


INSPIRE
-------

Code-lists specified for the Soil domain within the INSPIRE directive are
described in the report [D2.8.III.3 Data Specification on Soil – Technical
Guidelines](https://inspire.ec.europa.eu/documents/Data_Specifications/INSPIRE_DataSpecification_OI_v3.0rc3.pdf).
A brief overview of these code-lists is offered below.

| Code-list | Description |
|-----------|-------------|
| **[LayerGenesisProcessStateValue](http://inspire.ec.europa.eu/codelist/LayerGenesisProcessStateValue)** | An indication of whether the process specified in layerGenesisProcess is ongoing or ceased in the past. |
| **[LayerTypeValue](http://inspire-registry.jrc.ec.europa.eu/clr/LayerTypeValue)** | Classification of a layer according to the concept that fits the purpose,  e.g. "topsoil". |
| **[ProfileElementParameterNameValue](http://inspire.ec.europa.eu/codelist/ProfileElementParameterNameValue)** | [Extensible] List of properties that can be observed to characterize the profile element. |
| **[SoilDerivedObjectParameterNameValue](http://inspire.ec.europa.eu/codelist/SoilDerivedObjectParameterNameValue)** | [Extensible] List of soil related properties that can be derived from soil and other data. |
| **[SoilInvestigationPurposeValue](http://inspire.ec.europa.eu/codelist/SoilInvestigationPurposeValue)** | List of terms indicating the reasons for conducting a survey. |
| **[SoilPlotTypeValue](http://inspire.ec.europa.eu/codelist/SoilPlotTypeValue)** | List of possible values that give information on what kind of plot the observation of the soil is made. |
| **[SoilProfileParameterNameValue](http://inspire.ec.europa.eu/codelist/SoilProfileParameterNameValue)** | [Extensible] List of properties that can be observed to characterize the soil profile. |
| **[SoilSiteParameterNameValue](http://inspire.ec.europa.eu/codelist/SoilSiteParameterNameValue)** | [Extensible] List of properties that can be observed to characterize the soil site. |
| **[WRBQualifierPlaceValue](http://inspire.ec.europa.eu/codelist/WRBQualifierPlaceValue)** | List of values to indicate the placement of the Qualifier with regard to the WRB reference soil group (RSG), according to naming rules of the World reference base for soil resources 2006, first update 2007. |
| **[WRBQualifierValue](http://inspire.ec.europa.eu/codelist/WRBQualifierValue)** | List of possible qualifiers (i.e. prefix and suffix qualifiers of the World Reference Base for Soil Resources 2006, first update 2007). |
| **[WRBReferenceSoilGroupValue](http://inspire.ec.europa.eu/codelist/WRBReferenceSoilGroupValue)** | List of possible reference soil groups (i.e. first level of classification of the World Reference Base for Soil Resources 2006, first update 2007). |
| **[WRBSpecifierValue](http://inspire.ec.europa.eu/codelist/WRBSpecifierValue)** | List of possible specifiers, comprising only the values specified in the World Reference Base for Soil Resources 2006, first update 2007. | 


These code-lists are all available on-line through a
[r3gistry](https://ec.europa.eu/isa2/solutions/re3gistry_en/) instance. Each
item in these code-lists is a dereferenceable by URI. 

Four of these lists are extensible, those expressing properties associated with
the different features of interest. They are designed to serve as
umbrella structures for further specialisation according to local practices.
Extension is made in an hierarchical fashion, meaning that each additional item
must be a narrower definition of one of the existing items.

Besides these curated code-lists, the INSPIRE domain model also creates space
for code-lists of physio-chemical procedures of soil analysis. These are to be
referenced from the Observation instances related to the properties referred
above.

There is no practical guidance in the Technical Guidelines document on how to
extend or create new code-lists towards INSPIRE compliance. This document
provides broad guidelines on how to do so with the [Simple Knowledge
Organisation System](https://www.w3.org/2004/02/skos/) (SKOS), described ahead. 

GloSIS
------

The [GloSIS web ontology](https://github.com/rapw3k/glosis) includes a large
range of code-lists that are relevant within the INSPIRE context. GloSIS
follows the pattern of the [Sensor, Observation, Sample, and
Actuator](https://www.w3.org/TR/vocab-ssn/) (SOSA) ontology, which is the
Semantic Web counterpart of the [Observations &
Measurements](https://www.ogc.org/standards/om) standard (O&M). These code-lists
are expressed with SKOS.

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
physio-chemical analysis procedures in a [specific
module](https://rapw3k.github.io/glosis/docs/glosis-pc-doc/index-en.html).

Extending code-lists
--------------------

### SKOS

The SKOS ontology is remarkably simple, actually one of its strengths. At its
core are five primitives:

- **Concept** - a unit of thought, an idea, a meaning, a category or an object.
  Concepts are identified with URIs.

- **Label** - a lexical string used to annotate a concept. The same concept may
  be annotated in different natural languages.

- **Relation** - a semantic association between two concepts, conveying
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
@prefix skos:  <http://www.w3.org/2004/02/skos/core#> .
@prefix glosis_cl: <http://w3id.org/glosis/model/codelists#> .

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
@prefix rdfs:  <http://www.w3.org/2000/01/rdf-schema#> .
@prefix skos:  <http://www.w3.org/2004/02/skos/core#> .
@prefix glosis_cl: <http://w3id.org/glosis/model/codelists#> .

glosis_cl:cropClassValueCode a skos:ConceptScheme ;
        skos:prefLabel "Code list for CropClassValue - codelist scheme"@en;
        rdfs:label "Code list for CropClassValue - codelist scheme"@en;
        skos:note "This  code list provides the CropClassValue."@en;
        skos:definition "table 9" ;
        rdfs:seeAlso glosis_cl:CropClassValueCode .
```

Using this simple pattern, a hierarchical code-list can be developed further
simply using the predicates `skos:inScheme`, `skos:broader` and `skos:narrower`.
The predicates `skos:topConceptOf` and `skos:hasTopConcept` can be further used
to indicate the root items in a concept hierarchy. 

### Extend an INSPIRE code-list with SKOS

Suppose you intend to publish results of chemical analyses appraising the
Zinc content of the soil. The INSPIRE code-lists do not presently include that
metal as property, therefore an additional code-list item must be created.

The first action is to identify in which code-list the item should be added.
Physio-chemical properties like Zinc content appear associated with the Horizon
or Layer class in soil ontologies, thus the appropriate code-list is [ProfileElementParameterNameValue](http://inspire.ec.europa.eu/codelist/ProfileElementParameterNameValue). Open that URI in your browser an go through the respective `r3gistry` record.

At the bottom of the page `r3gistry` lists the items for this code-list, in this
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
convey the nature of this item as part of a structured INSPIRE code-list. Finally,
the `skos:related` predicated is employed to refer a similar property in the
GloSIS web ontology. This last triple is not at all mandatory, but provides
another dimension to the code-list item.

### Extend a GloSIS code-list

The GloSIS web ontology becomes particularly relevant in the sections of the
INSPIRE domain model for which code-lists do not yet exist. A prominent case is
the list of laboratory procedures to assess physico-chemical properties. As
mentioned above, GloSIS includes a specific module for procedures.

The listing below presents a RDF document with an extra item for the soil
texture procedures code list (SKOS scheme `glosis_proc:textProcedure`). Compared
to the previous example, the most remarkable aspect here is the declaration of a
`glosis_proc:TextProcedure` instance. The latter is a sub-class of the SOSA
Procedure class, making the bridge to the Observation instances declared in
other GloSIS modules.  

```turtle
@prefix skos: <http://www.w3.org/2004/02/skos/core#> .
@prefix glosis_proc: <http://w3id.org/glosis/model/procedure#> .
@prefix my_soil: <http://example.com/my-soil/> . 

my_soil:textureProcedure-SaSiCl_5-50-2000u a skos:Concept, glosis_proc:TextureProcedure ;
    skos:inScheme glosis_proc:textProcedure ;
    skos:topConceptOf glosis_proc:textureProcedure ;
    skos:prefLabel "SaSiCl_5-50-2000u"@en ;
    skos:notation "SaSiCl_5-50-2000u" ;
    skos:definition "Sand, silt and clay fractions as used in my country (5-50-2000um)" .
``` 

The remaining triples should all be familiar by now. The link to the SKOS scheme
is made with the `skos:inScheme` and `skos:topConceptOf` predicates. Then come
the annotations.

### Create a new code-list

INSPIRE and GloSIS cover quite a good deal of ground with their code-lists.
However, there might be circumstances where you may require an entire new
code-list to express a domain property specific to your institution or dataset.

The examples above already provide the necessary to build a code-list on your
own. In summary, these are the steps:

1. Devise a URI policy, encompassing the code-list and its items.

2. Create a Scheme instance to aggregate the code-list items. The Scheme
   provides a URI and annotation for the code-list.

3. Add in the top Concept instances with the predicates `skos:inScheme`,
   `skos:topConceptOf` and `skos:hasTopConcept`.

4. If necessary, add in narrower terms forming a hierarchy with `skos:broader`
   and `skos:narrower`.

5. Link items to similar concepts in other ontologies or vocabularies if possible.

Publishing your own code-list items
-----------------------------------

Now that you extended or even created a new code-list the next step is to
publish it on-line. There are three essentials ways of doing so, briefly
described below. 

1. **A simple on-line RDF file**. Save the items or code-list as a RDF document
   and deploy it to a web server. Fairly easy, but not the most user friendly. 

2. **A knowledge graph deployed to a triple store**. Load the RDF document to a
   triple store or directly create the code-list triples with SPARQL queries.
Triple stores usually provide end-points for interaction with SPARQL queries and
other mechanisms that facilitate user access/view of the code-list.
[Virtuoso](virtuoso.md) is a triple store providing these functionalities.

3. **A [SKOSMOS](skosmos.md) instance**. Load the code-list triples into a triple store and then
   link it to a [SKOSMOS](skosmos.md) instance. This software leverages
the SKOS ontology to presnnt code-lists in a
user friendly, browsable complex of HTML pages.

### Derreferenceable URIs

When publishing a code-list, it is important to facilitate the resolution of the
respective URIs. This promotes accessibility and use of the code-list. With a
simple deployment to a web server, the hypothetical URI used above:
`http://example.com/my-soil` can point directly to the RDF file. In this case it
is customary the use of the hash character (`#`) to distinguish different
resources within the same file. E.g.  `http://example.com/my-soil#zincContent`
for the Zinc item.

With more advanced software like SKOSMOS, a mid-layer mechanism is necessary to
translate the URIs declared in the RDF into the corresponding pages or services.
More about this topic in the [Identification](../identification.md) document. 





















