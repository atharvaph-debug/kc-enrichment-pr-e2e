---
type: table-context
title: bikeshare_trips
description: Context overlay for bikeshare_trips.
generated:
  by: dataplex-enrichment-agent/1.0
resource: projects/dataplex-demo/locations/us/entryGroups/@bigquery/entries/bigquery.googleapis.com/projects/dataplex-demo/datasets/austin_bikeshare/tables/bikeshare_trips
sources:
- id: '1'
  resource: about:sanitized
  title: 'table metadata: dataplex-demo.austin_bikeshare.bikeshare_trips'
x-kcmd:
  v: 1
  entryId: assets/bigquery/dataplex-demo/austin_bikeshare/bikeshare_trips
  name: assets/bigquery/dataplex-demo/austin_bikeshare/bikeshare_trips
  entryType: projects/dataplex-types/locations/global/entryTypes/document
  parentEntry: projects/dataplex-demo/locations/us-central1/entryGroups/atharvaphtest1/entries/assets/bigquery/dataplex-demo/austin_bikeshare
  aspects:
    dataplex-types.global.document:
      job:
        name: enrichment-agent/enrich-2d509cb5893143af
        runTime: '2026-11-20T20:35:16Z'
---
# bikeshare_trips Overview

The `bikeshare_trips` table stores individual bicycle trip records for the Austin municipal bike-share system [1]. It serves as the granular transaction log of rider activity across the docking station network, capturing the start and end stations, trip timing, trip duration, subscription classification, and bicycle identifier for each journey [1].

## Purpose

The table records completed bike-share trips, enabling analysis of rider travel patterns, docking station demand, fleet utilization, and trip duration metrics across the municipal transit network [1].

## Columns & Metrics

- **trip_id** (`STRING`): Numeric ID of bike trip [1].
- **subscriber_type** (`STRING`): Type of the Subscriber [1].
- **bike_id** (`STRING`): ID of bike used [1].
- **bike_type** (`STRING`): Type of bike used [1].
- **start_time** (`TIMESTAMP`): Start timestamp of trip [1].
- **start_station_id** (`INTEGER`): Numeric reference for start station [1].
- **start_station_name** (`STRING`): Station name for start station [1].
- **end_station_id** (`STRING`): Numeric reference for end station [1].
- **end_station_name** (`STRING`): Station name for end station [1].
- **duration_minutes** (`INTEGER`): Time of trip in minutes [1].

## Usage

### Analytical Use Cases

- **Docking Station Flow & Network Rebalancing**: Analyzing origin-destination station pairs (`start_station_id` to `end_station_id`) and temporal trends via `start_time` to identify net-inflow and net-outflow stations requiring bicycle rebalancing.
- **Rider Subscription & Trip Dynamics**: Comparing trip volume and `duration_minutes` across different `subscriber_type` tiers.
- **Fleet Asset Tracking**: Monitoring individual bicycle utilization across the network using `bike_id` and `bike_type`.

### Sibling Table Comparison & Authority

The dataset contains multiple tables reporting trip volumes:
- **`bikeshare_trips`**: The primary, trip-level table containing 2,271,152 individual journey records [1]. It is the authoritative source for trip-level attributes, route details, vehicle identification, and duration metrics.
- **Daily Aggregation Siblings (`bikeshare_trips_daily_counts`, `daily_bikeshare_trips`, `daily_ride_counts`, `daily_trip_counts`)**: These tables provide pre-aggregated daily ride counts (`trip_count`, `num_trips`, `daily_rides`) indexed by date. While convenient for day-over-day aggregate trend reporting without scanning trip rows, they do not contain station, subscriber, or bike-level dimensions. For operational queries, station infrastructure analyses, or granular rider journey investigations, `bikeshare_trips` is the required source.

### Station Infrastructure Joins

- **Origin Station Metadata**: `start_station_id` joins directly with `bikeshare_stations.station_id` on matching integer identifiers to obtain physical station attributes such as dock capacity (`number_of_docks`), power configuration (`power_type`), and geographic location.
- **Destination Station Metadata**: `end_station_id` references `bikeshare_stations.station_id`. Because `end_station_id` is stored as a `STRING` in `bikeshare_trips` while `bikeshare_stations.station_id` is typed as an `INTEGER`, queries joining the destination station must cast `end_station_id` to an integer or convert `station_id` to a string.

## Table Info

`dataplex-demo.austin_bikeshare.bikeshare_trips`
