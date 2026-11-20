---
type: concept
title: 'Concept: ride_date (4 tables)'
description: 'What `ride_date` means in this catalog, quoted from each table that
  defines it: bikeshare_trips_daily_counts, daily_bikeshare_trips, daily_ride_counts,
  daily_trip_counts.'
generated:
  by: dataplex-enrichment-agent/1.0
resource: projects/dataplex-demo/locations/us-central1/catalog/documents/concepts/ride-date
x-kcmd:
  v: 1
  entryId: documents/concepts/ride-date
  name: documents/concepts/ride-date
  entryType: projects/dataplex-types/locations/global/entryTypes/document
  parentEntry: projects/dataplex-demo/locations/us-central1/entryGroups/atharvaphtest1/entries/documents/concepts
  aspects:
    dataplex-types.global.document:
      job:
        name: enrichment-agent/enrich-2d509cb5893143af
        runTime: '2026-11-20T20:35:16Z'
---
# Concept: ride_date (4 tables)

`ride_date` is used by 4 tables in this catalog. Each line below is quoted from that table's own page, where the claim was made and checked; follow the table id to read it in context.

## Definitions

- `dataplex-demo.austin_bikeshare.bikeshare_trips_daily_counts` — `daily_ride_counts` (`ride_date`, `daily_rides`)
- `dataplex-demo.austin_bikeshare.daily_bikeshare_trips` — `daily_ride_counts` (`ride_date`, `daily_rides`)
- `dataplex-demo.austin_bikeshare.daily_ride_counts` — `daily_ride_counts` (columns: `ride_date`, `daily_rides`)
- `dataplex-demo.austin_bikeshare.daily_trip_counts` — `daily_ride_counts` (`ride_date`, `daily_rides`)

See also: `assets/bigquery/dataplex-demo/austin_bikeshare/bikeshare_trips_daily_counts` — the table entry for `dataplex-demo.austin_bikeshare.bikeshare_trips_daily_counts`.
See also: `assets/bigquery/dataplex-demo/austin_bikeshare/daily_bikeshare_trips` — the table entry for `dataplex-demo.austin_bikeshare.daily_bikeshare_trips`.
See also: `assets/bigquery/dataplex-demo/austin_bikeshare/daily_ride_counts` — the table entry for `dataplex-demo.austin_bikeshare.daily_ride_counts`.
