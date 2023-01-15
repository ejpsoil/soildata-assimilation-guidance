# A Pythonic metadata workflow

*status: in progress*

This recipe presents a minimalistic, however integrated and standardised approach to metadata management. Each data file on the file system will be accompagnied by a minimal YML metadata file. Automated pipelines will pick up these metadata files and publish them as valid iso19139 (or other metadata models) documents.

The recipe uses an incremental approach to extend the functionality of the data management system step by step.

## Quick start

The inital step assumes a folder of data files on a network drive, sharepoint or git repository. Many datasets are stored on a database, we'll not consider these for now.

For each data file in the folder we will create a `metadata control file` (MCF). [MCF](https://geopython.github.io/pygeometa/reference/mcf/) is a convention from the [pygeometa](https://geopython.github.io/pygeometa) community. It is a [YAML](https://en.wikipedia.org/wiki/YAML) encoded subset of iso19139:2007. YAML is easy to read by humans and optimal for versioning.

```
pip install pygeometa
```

```
pygeometa export 
```

Idea of this approach is to manually capture as little metadata as needed for a file, auto derive as much as possible from the spatial file itself (format, extent, crs) and merge with higher level metadata to capture generic aspects (contact details, usage constraints, etc.)

we've prepared a docker image including Python scripts to work efficiently with pygeometa

```
docker run /isric/
```



Publish records on a WebDav location or publish them for example in pycsw


