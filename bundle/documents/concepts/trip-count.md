---
type: concept
title: 'Concept: trip_count (4 tables)'
description: 'What `trip_count` means in this catalog, quoted from each table that
  defines it: bikeshare_trips_daily_counts, daily_bikeshare_trips, daily_ride_counts,
  daily_trip_counts.'
generated:
  by: dataplex-enrichment-agent/1.0
resource: projects/dataplex-demo/locations/us-central1/catalog/documents/concepts/trip-count
x-kcmd:
  v: 1
  entryId: documents/concepts/trip-count
  name: documents/concepts/trip-count
  entryType: projects/dataplex-types/locations/global/entryTypes/document
  parentEntry: projects/dataplex-demo/locations/us-central1/entryGroups/atharvaphtest1/entries/documents/concepts
  aspects:
    dataplex-types.global.document:
      job:
        name: enrichment-agent/enrich-2d509cb5893143af
        runTime: '2026-11-20T20:35:16Z'
---
# Concept: trip_count (4 tables)

`trip_count` is used by 4 tables in this catalog. Each line below is quoted from that table's own page, where the claim was made and checked; follow the table id to read it in context.

## Definitions

- `dataplex-demo.austin_bikeshare.bikeshare_trips_daily_counts` — **`trip_count`** (`INTEGER`): The total count of completed bike trips recorded on the corresponding `trip_date`.
- `dataplex-demo.austin_bikeshare.daily_bikeshare_trips` — `bikeshare_trips_daily_counts` (`trip_date`, `trip_count`)
- `dataplex-demo.austin_bikeshare.daily_ride_counts` — `bikeshare_trips_daily_counts` (columns: `trip_date`, `trip_count`)
- `dataplex-demo.austin_bikeshare.daily_trip_counts` — **`trip_count`** (`INTEGER`): The total number of bike trips recorded on the specified date. Measures aggregate municipal bike-share ridership volume across all stations and bike types.

See also: `assets/bigquery/dataplex-demo/austin_bikeshare/bikeshare_trips_daily_counts` — the table entry for `dataplex-demo.austin_bikeshare.bikeshare_trips_daily_counts`.
See also: `assets/bigquery/dataplex-demo/austin_bikeshare/daily_bikeshare_trips` — the table entry for `dataplex-demo.austin_bikeshare.daily_bikeshare_trips`.
See also: `assets/bigquery/dataplex-demo/austin_bikeshare/daily_ride_counts` — the table entry for `dataplex-demo.austin_bikeshare.daily_ride_counts`.
