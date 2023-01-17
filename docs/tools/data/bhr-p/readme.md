# BHR-P

This is an extract of [BRO - Bodemkundig booronderzoek (BHR-P)](https://nationaalgeoregister.nl/geonetwork/srv/dut/catalog.search#/metadata/562127a6-0381-46b3-9ed7-10e61ec5ecb5), the Dutch National Database of Soil Profile analyses data (Licensed: CC-0).

Bulk density and organic matter are relevant indicators of Carbon Stock.

Downloaded at 17-01-2023.

- [Buld density](./bhr-p-bulk-dens.geojson) has been extracted via:

```sql
SELECT borehole_research_pk, bro_id, research_report_date, litter_layer_investigated, standardized_location, begin_depth, end_depth, analysis_report_date,  dry_bulk_density_determination.*
from borehole_research, dry_bulk_density_determination, investigated_interval, borehole_sample_analysis
where investigated_interval_fk=investigated_interval_pk
and borehole_sample_analysis_pk=borehole_sample_analysis_fk
and borehole_research_pk = borehole_research_fk 
and dry_bulk_density is not null;
```

- [Organic matter](./bhr-p-organic-matter.geojson) has been extracted via:

```sql
SELECT borehole_research_pk, bro_id, research_report_date, litter_layer_investigated, standardized_location, begin_depth, end_depth, analysis_report_date,  organic_matter_content_determination.*
from borehole_research, organic_matter_content_determination, investigated_interval, borehole_sample_analysis
where investigated_interval_fk=investigated_interval_pk
and borehole_sample_analysis_pk=borehole_sample_analysis_fk
and borehole_research_pk = borehole_research_fk 
and organic_matter_content is not null;
```

## Description of the dataset

| Attribute | Description |
| --- | --- |
| borehole_research_pk | identifier of the research |
| bro_id | alternative identifier of the research |
| research_report_date | Date of the fieldwork | 
| litter_layer_investigated | Indication if the litter layer was considered |
| geometry | lLocation of the research |
| begin_depth | Top of the layer |
| end_depth | Bottom of the layer |
| analysis_report_date | Date of the lab analyses |
| dry_bulk_density_determination_pk | Identifier of the analyses |
| investigated_interval_fk | Identifier of the layer |
| determination_procedure | Identifer of the procedure |
| determination_method | Identifier of the method |
| ring_diameter | Parameter of the specimen |
| ring_height | Parameter of the specimen |
| drying_temperature | Parameter of the analyses method |
| volume_water_saturated | Property of the sample |
| dry_bulk_density | Observed value |
| material_irregularity | Property of the sample |
