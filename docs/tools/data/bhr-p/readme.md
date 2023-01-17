# BHR-P

This is an extract of [BRO - Bodemkundig booronderzoek (BHR-P)](https://nationaalgeoregister.nl/geonetwork/srv/dut/catalog.search#/metadata/562127a6-0381-46b3-9ed7-10e61ec5ecb5).

Bulk density and organic matter are relevant indicators of Carbon Stock.

Downloaded at 17-01-2023.

Datasets have been extracted using:

```sql
SELECT borehole_research_pk, bro_id, research_report_date, litter_layer_investigated, standardized_location, begin_depth, end_depth, analysis_report_date,  dry_bulk_density_determination.*
from borehole_research, dry_bulk_density_determination, investigated_interval, borehole_sample_analysis
where investigated_interval_fk=investigated_interval_pk
and borehole_sample_analysis_pk=borehole_sample_analysis_fk
and borehole_research_pk = borehole_research_fk 
and dry_bulk_density is not null;
```

```sql
SELECT borehole_research_pk, bro_id, research_report_date, litter_layer_investigated, standardized_location, begin_depth, end_depth, analysis_report_date,  organic_matter_content_determination.*
from borehole_research, organic_matter_content_determination, investigated_interval, borehole_sample_analysis
where investigated_interval_fk=investigated_interval_pk
and borehole_sample_analysis_pk=borehole_sample_analysis_fk
and borehole_research_pk = borehole_research_fk 
and organic_matter_content is not null;
```