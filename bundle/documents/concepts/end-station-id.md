---
type: concept
title: 'Concept: end_station_id (2 tables)'
description: 'What `end_station_id` means in this catalog, quoted from each table
  that defines it: bikeshare_stations, bikeshare_trips.'
generated:
  by: dataplex-enrichment-agent/1.0
resource: projects/dataplex-demo/locations/us-central1/catalog/documents/concepts/end-station-id
x-kcmd:
  v: 1
  entryId: documents/concepts/end-station-id
  name: documents/concepts/end-station-id
  entryType: projects/dataplex-types/locations/global/entryTypes/document
  parentEntry: projects/dataplex-demo/locations/us-central1/entryGroups/atharvaphtest1/entries/documents/concepts
  aspects:
    dataplex-types.global.document:
      job:
        name: enrichment-agent/enrich-2d509cb5893143af
        runTime: '2026-11-20T20:35:16Z'
---
# Concept: end_station_id (2 tables)

`end_station_id` is used by 2 tables in this catalog. Each line below is quoted from that table's own page, where the claim was made and checked; follow the table id to read it in context.

## Definitions

- `dataplex-demo.austin_bikeshare.bikeshare_stations` — **Destination Station Joins**: In `bikeshare_trips`, the destination reference `end_station_id` is typed as `STRING`. Joining `bikeshare_stations.station_id` to `end_station_id` requires explicit type conversion (casting `end_station_id` to integer or `station_id` to string), or joining on station name using `bikeshare_stations.name = bikeshare_trips.end_station_name`.
- `dataplex-demo.austin_bikeshare.bikeshare_trips` — **Destination Station Metadata**: `end_station_id` references `bikeshare_stations.station_id`. Because `end_station_id` is stored as a `STRING` in `bikeshare_trips` while `bikeshare_stations.station_id` is typed as an `INTEGER`, queries joining the destination station must cast `end_station_id` to an integer or convert `station_id` to a string.

See also: `assets/bigquery/dataplex-demo/austin_bikeshare/bikeshare_stations` — the table entry for `dataplex-demo.austin_bikeshare.bikeshare_stations`.
See also: `assets/bigquery/dataplex-demo/austin_bikeshare/bikeshare_trips` — the table entry for `dataplex-demo.austin_bikeshare.bikeshare_trips`.
