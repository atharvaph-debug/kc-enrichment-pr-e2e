---
type: table-context
title: daily_bikeshare_trips
description: Context overlay for daily_bikeshare_trips.
generated:
  by: dataplex-enrichment-agent/1.0
resource: projects/dataplex-demo/locations/us/entryGroups/@bigquery/entries/bigquery.googleapis.com/projects/dataplex-demo/datasets/austin_bikeshare/tables/daily_bikeshare_trips
sources:
- id: '1'
  resource: about:sanitized
  title: 'table metadata: dataplex-demo.austin_bikeshare.daily_bikeshare_trips'
x-kcmd:
  v: 1
  entryId: assets/bigquery/dataplex-demo/austin_bikeshare/daily_bikeshare_trips
  name: assets/bigquery/dataplex-demo/austin_bikeshare/daily_bikeshare_trips
  entryType: projects/dataplex-types/locations/global/entryTypes/document
  parentEntry: projects/dataplex-demo/locations/us-central1/entryGroups/atharvaphtest1/entries/assets/bigquery/dataplex-demo/austin_bikeshare
  aspects:
    dataplex-types.global.document:
      job:
        name: enrichment-agent/enrich-2d509cb5893143af
        runTime: '2026-11-20T20:35:16Z'
---
# daily_bikeshare_trips Overview

The `daily_bikeshare_trips` table stores daily aggregate trip volume for municipal bike-share operations. Each record represents a single calendar date alongside the total number of trips taken across the Austin bike-share network.

## Purpose

The table provides a pre-aggregated daily summary of rider trip activity, tracking daily system-wide bike utilization over time across 3,851 recorded dates [1]. It serves high-level reporting and time-series analysis where trip-level granularity (such as docking station routing or trip duration) is not required.

## Columns & Metrics

- **trip_date** (`DATE`)
- **num_trips** (`INTEGER`)

## Usage

### System of Record vs. Derived Summary

- **Primary System of Record (`bikeshare_trips`)**: For operational trip activity, rider trip duration, and docking station infrastructure utilization (station-to-station routing, start and end docks), `bikeshare_trips` is the authoritative operational system of record. It records individual trips with complete station attributes (`start_station_id`, `end_station_id`, `start_station_name`, `end_station_name`), equipment identifiers (`bike_id`, `bike_type`), user categories (`subscriber_type`), and timestamps (`start_time`, `duration_minutes`).
- **Derived Daily Aggregates**: `daily_bikeshare_trips` is a derived aggregate table that summarizes network-wide volume at the date grain. It is suitable for trend monitoring and daily demand reporting, but omits station-level infrastructure context and trip-level mechanics.

### Sibling Aggregate Tables

The dataset contains multiple sibling tables that model the identical daily ride aggregation grain:
- `daily_bikeshare_trips` (`trip_date`, `num_trips`)
- `bikeshare_trips_daily_counts` (`trip_date`, `trip_count`)
- `daily_trip_counts` (`trip_date`, `trip_count`)
- `daily_ride_counts` (`ride_date`, `daily_rides`)

These four daily summary tables are indistinguishable in authority from the metadata available in the catalog; none carries explicit authority designations or distinct pipeline documentation. Identifying the active production ETL pipeline or reporting dashboard dependencies would settle which aggregate copy is maintained as canonical for downstream consumers.

## Table Info

`dataplex-demo.austin_bikeshare.daily_bikeshare_trips`
