# Virtuoso & Skosmos

*Status: in progress*

This recipe presents steps to publish a soil codelists using the SKOS ontology in Virtuoso and Skosmos. Virtuoso is an open source Triple store providing a SPARQL endpoint. 
Skosmos is an open source web application providing a human friendly browse interface for skos thesauri stored in a triple store.

The [skos ontology](https://www.w3.org/2004/02/skos/) supports the use of knowledge organization systems such as thesauri, 
classification schemes, subject heading lists and taxonomies within the framework of the Semantic Web (and beyond). For any concept (identified by a uri) a definition in multiple languages is modeled. For each concept a range of relation types is available to capture it's relation to other concepts, e.g. SameAs, Broader, Narrower, Affect, hasComponent, etc.

## Preparing the codelist

Excel is often used to create lists of concepts with their definition. But consider that tabular systems are less optimal when defining relations between concepts. For that reason the [Glosis codelists](https://github.com/rapw3k/glosis/blob/master/glosis_cl.ttl) are maintained as Turtle RDF files on GitHub.

For this recipe we assume the codelist to be published is available as a CSV. A range of tools is available to transform an excel to a skos RDF document. [Skos play](https://skos-play.sparna.fr/play/convert) offers for example a webbased conversion tool.

## Load SKOS RDF to virtuoso

We're using a docker compose orchestration to deploy virtuoso and skosmos locally. Copy the contents of the [virtuoso folder](https://github.com/ejpsoil/soildata-assimilation-guidance/blob/main/docker/virtuoso-skosmos) into an empty folder. Navigate to the folder with command line and run:

```
docker compose up
```

Load RDF data into Virtuoso ...


## Setup Skosmos

The file [config-docker.ttl](https://github.com/ejpsoil/soildata-assimilation-guidance/blob/main/docker/virtuoso-skosmos/config-docker.ttl) contains the configuration of SKOSMOS. You have to indicate which elements to select from the triple store.

## Extending an existing codelist



## Read more

Virtuoso

- Website: [virtuoso](https://virtuoso.openlinksw.com)
- GitHub: [github](https://github.com/openlink/virtuoso-opensource)
- Docker: [docker](https://hub.docker.com/r/openlink/virtuoso-opensource-7)
- Virtuoso at ISRIC: [isric](https://virtuoso.isric.org/)

Skosmos

- Website: [skosmos](https://skosmos.org)
- GitHub: [github](https://github.com/NatLibFi/Skosmos)
- Docker: [docker](https://hub.docker.com/r/ndslabs/skosmos)
- Skosmos examples: [glosis](https://glosis.isric.org), [agrovoc](https://agrovoc.fao.org), [agclass](https://agclass.nal.usda.gov)

Skos play

- Skos play: [skos play](https://skos-play.sparna.fr/play/convert)
