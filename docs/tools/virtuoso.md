# Virtuoso & Skosmos

*Status: in progress*

This recipe presents steps to publish a soil codelists using the SKOS ontology in Virtuoso and Skosmos. Virtuoso is an open source Triple store providing a SPARQL endpoint. 
Skosmos is an open source web application providing a human friendly browse interface for skos thesauri stored in a triple store.

The [skos ontology](https://www.w3.org/2004/02/skos/) supports the use of knowledge organization systems such as thesauri, 
classification schemes, subject heading lists and taxonomies within the framework of the Semantic Web (and beyond). For any concept (identified by a uri) a definition in multiple languages is modeled. For each concept a range of relation types is available to capture it's relation to other concepts, e.g. SameAs, Broader, Narrower, Affect, hasComponent, etc.

## Preparing the codelist

Excel is often used to create lists of concepts with their definition. But consider that tabular systems are less optimal when defining relations between concepts. For that reason the [Glosis codelists](https://github.com/rapw3k/glosis/blob/master/glosis_cl.ttl) are maintained as Turtle RDF files on Github.

For this recipe we assume the codelist to be published is available as a CSV. A range of tools is available to transform an excel to a skos RDF document. [Skos play](https://skos-play.sparna.fr/play/convert) offers for example a webbased conversion tool.

## Load SKOS RDF to virtuoso

We're using a docker compose orchestration to deploy virtuoso and skosmos locally. Copy the [compose file](../../docker/virtuoso-skosmos/docker-compose.yml) into an empty folder. Navigate to the folder with a shell and run

```
docker compose up
```

## Setup Skosmos



## Extending an existing codelist



## Read more

Virtuoso

- Website: https://virtuoso.openlinksw.com/
- Github: https://github.com/openlink/virtuoso-opensource
- Docker: https://hub.docker.com/r/openlink/virtuoso-opensource-7
- Virtuoso at ISRIC: https://virtuoso.isric.org/

Skosmos

- Website: https://skosmos.org
- Github: https://github.com/NatLibFi/Skosmos
- Docker: https://hub.docker.com/r/ndslabs/skosmos
- Skosmos examples: https://glosis.isric.org/, https://agrovoc.fao.org, https://agclass.nal.usda.gov/

Skos play

- Skos play: https://skos-play.sparna.fr/play/convert