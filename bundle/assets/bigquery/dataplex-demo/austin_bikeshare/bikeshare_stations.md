---
type: table-context
title: bikeshare_stations
description: Austin Bikeshare Stations table
generated:
  by: dataplex-enrichment-agent/1.0
resource: projects/dataplex-demo/locations/us/entryGroups/@bigquery/entries/bigquery.googleapis.com/projects/dataplex-demo/datasets/austin_bikeshare/tables/bikeshare_stations
sources:
- id: '1'
  resource: about:sanitized
  title: 'table metadata: dataplex-demo.austin_bikeshare.bikeshare_stations'
x-kcmd:
  v: 1
  entryId: assets/bigquery/dataplex-demo/austin_bikeshare/bikeshare_stations
  name: assets/bigquery/dataplex-demo/austin_bikeshare/bikeshare_stations
  entryType: projects/dataplex-types/locations/global/entryTypes/document
  parentEntry: projects/dataplex-demo/locations/us-central1/entryGroups/atharvaphtest1/entries/assets/bigquery/dataplex-demo/austin_bikeshare
  aspects:
    dataplex-types.global.document:
      job:
        name: enrichment-agent/enrich-2d509cb5893143af
        runTime: '2026-11-20T20:35:16Z'
---
# bikeshare_stations Overview

The `bikeshare_stations` table is the station-level dimension table for the City of Austin's municipal bike-share system, tracking 101 station locations across the service area [1]. It provides docking station infrastructure attributes, physical footprint information, municipal council district alignments, and administrative identifiers needed to analyze bike availability, network coverage, and trip origination and destination patterns.

## Purpose

The table defines the physical and operational network of bike-share docking stations in Austin. It serves as the primary station dimension for municipal bike-share operations, enabling analysts to evaluate station infrastructure, correlate trip volumes with geographic locations, and link rider activity from checkout logs to physical kiosks.

## Columns & Metrics

- `station_id` (`INTEGER`): Numeric identifier for the bike-share station.
- `name` (`STRING`): Name of the station.
- `status` (`STRING`)
- `location` (`STRING`)
- `address` (`STRING`)
- `alternate_name` (`STRING`)
- `city_asset_number` (`INTEGER`)
- `property_type` (`STRING`)
- `number_of_docks` (`INTEGER`)
- `power_type` (`STRING`)
- `footprint_length` (`INTEGER`)
- `footprint_width` (`FLOAT`)
- `notes` (`STRING`)
- `council_district` (`INTEGER`)
- `image` (`STRING`)
- `modified_date` (`TIMESTAMP`)

## Usage

### Trip Activity Analysis and Joins
The table is designed to join with trip event records in `bikeshare_trips` to analyze rider origin and destination patterns across the Austin municipal network:
- **Origin Station Joins**: `station_id` (`INTEGER`) joins directly to `bikeshare_trips.start_station_id` (`INTEGER`), or `name` (`STRING`) joins to `bikeshare_trips.start_station_name` (`STRING`).
- **Destination Station Joins**: In `bikeshare_trips`, the destination reference `end_station_id` is typed as `STRING`. Joining `bikeshare_stations.station_id` to `end_station_id` requires explicit type conversion (casting `end_station_id` to integer or `station_id` to string), or joining on station name using `bikeshare_stations.name = bikeshare_trips.end_station_name`.

### Network Infrastructure and Coverage
The table facilitates spatial and operational analysis of the bike-share infrastructure across city council districts:
- Evaluating station density and dock capacity by council district.
- Assessing physical property placement types and power sources across operational kiosks.

## Table Info

`dataplex-demo.austin_bikeshare.bikeshare_stations`
