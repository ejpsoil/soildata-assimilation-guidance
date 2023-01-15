# Data Organisation

This article describes the `data organisation` step in the [Soil Information Workflow](https://www.isric.org/index.php/utilise/community-practice) and references various cookbook recipes related to this step in the workflow.

In this step a data curator prepares the organisation for incoming soil observations from field studies and laboratory work. Data from external organisations is prepared and made available to augment and/or validate local data. Relevant measures are put in place to authorise relevant staff, prevent data loss and data redundancy and assess privacy concerns. Concrete deliverables of this phase are: a data model materialised in a physical database, implemented procedures to prevent data loss, access grants to relevant staff, a metadata document in which these aspects are described, implemented procedures to evaluate quality of the data and infrastructure. 

Note that in this phase no effort is made to publish data to remote partners or the general public, but it does make sense to capture on the metadata if any access contraints apply which may prevent publication to a wider audience in a later stage.

Metadata documents are preferably based on a common ontology such as [DCAT](tools/dcat.md) or [ISO19139](tools/iso19139.md). Roughly 2 approaches, with various imlementation options, exist to maintain metadata in an organisation:

- Metadata is included in the data file or is stored as a sidecar file next to the actual data file. At intervals a crawler imports metadata to make the data findable from a central location.
- Metadata is captured in a separate system and linkage is maintained between the actual dataset and its metadata.

The second option is relatively easy to adopt, however it comes with a potential big effort to keep the metadata system in sync with the orginasation. In practice organisations tend to implement a combination of both options. 

Within this step is also the organisation of data arriving from external sources and the assimilation of that data with local data.
As soon as a user imports a remote dataset for use in a project, it is usefull to include a metadata record about that dataset in the local repository, so colleagues understand where/when the data was imported. If the dataset is available online, it is better to link to the remote dataset, so users would always use the latest version. As part of the assimilation a [data harmonisation to a locally used datamodel](tools/hale-studio-consume-gml.md) is relevant (See also [Data harmonization](etl.md)).

## Related recipes in this cookbook:

- [A Pythonic metadata workflow](tools/pygeometa.md)
- [A discovery service in GeoNetwork](tools/geonetwork.md) includes a section on metadata authoring in GeoNetwork
- [Metadata and View Service with GeoCat Bridge, GeoNetwork and GeoServer](tools/bridge-geoserver-geonetwork.md) includes a section on metadata management in QGIS
- [DCAT](tools/dcat.md)
- [Consume Soil GML with Hale Studio](tools/hale-studio-consume-gml.md)
