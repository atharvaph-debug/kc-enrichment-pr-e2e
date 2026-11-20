---
type: table-context
title: daily_ride_counts
description: Context overlay for daily_ride_counts.
generated:
  by: dataplex-enrichment-agent/1.0
resource: projects/dataplex-demo/locations/us/entryGroups/@bigquery/entries/bigquery.googleapis.com/projects/dataplex-demo/datasets/austin_bikeshare/tables/daily_ride_counts
sources:
- id: '1'
  resource: about:sanitized
  title: 'table metadata: dataplex-demo.austin_bikeshare.daily_ride_counts'
x-kcmd:
  v: 1
  entryId: assets/bigquery/dataplex-demo/austin_bikeshare/daily_ride_counts
  name: assets/bigquery/dataplex-demo/austin_bikeshare/daily_ride_counts
  entryType: projects/dataplex-types/locations/global/entryTypes/document
  parentEntry: projects/dataplex-demo/locations/us-central1/entryGroups/atharvaphtest1/entries/assets/bigquery/dataplex-demo/austin_bikeshare
  aspects:
    dataplex-types.global.document:
      job:
        name: enrichment-agent/enrich-2d509cb5893143af
        runTime: '2026-11-20T20:35:16Z'
---
# daily_ride_counts Overview

`daily_ride_counts` is a reporting table in the `austin_bikeshare` dataset that records aggregate daily bicycle trip counts across the municipal bike-share system. The table contains 3,851 rows [1] at a grain of one record per calendar date.

## Purpose

The table provides a pre-aggregated summary of system-wide ridership volume by date, enabling macro-level monitoring of municipal bike-share usage and multi-year trip demand trends without requiring full scans of granular trip logs [1].

## Columns & Metrics

- **`ride_date`** (`DATE`)
- **`daily_rides`** (`INTEGER`)

## Usage

### Analytical Context

The table supports high-level ridership time-series analysis, such as evaluating day-of-week demand patterns, holiday usage shifts, and long-term volume trends across the Austin bike-share network.

Because this table contains only date and volume figures, it cannot answer operational questions regarding docking station capacity, station asset distributions, subscriber categories, or individual bike utilization. Queries requiring station infrastructure context must query `bikeshare_stations` (using attributes like `station_id`, `status`, and `number_of_docks`), while route and duration analyses require granular trip logs.

### Sibling Table Comparison and Authority Ranking

The `austin_bikeshare` dataset contains multiple tables that model bike-share trip activity:

1. **Granular System of Record vs. Daily Aggregates:**
   `bikeshare_trips` is the primary granular system of record for trip activity. It captures individual ride events with atomic details including `trip_id`, `start_time`, `start_station_id`, `end_station_id`, `bike_id`, `bike_type`, `subscriber_type`, and `duration_minutes`. For detailed operational reporting, station turnaround analysis, or custom cohort segmentation, `bikeshare_trips` outranks `daily_ride_counts`. `daily_ride_counts` is a convenient derived aggregate for queries that only require network-wide daily totals.

2. **Sibling Daily Aggregate Tables:**
   The dataset contains four near-duplicate daily aggregation tables:
   - `daily_ride_counts` (columns: `ride_date`, `daily_rides`)
   - `bikeshare_trips_daily_counts` (columns: `trip_date`, `trip_count`)
   - `daily_bikeshare_trips` (columns: `trip_date`, `num_trips`)
   - `daily_trip_counts` (columns: `trip_date`, `trip_count`)

   **Authority Ranking:** None of these four daily tables carry explicit authority designations, descriptive comments, or documentation in their schema metadata. As a result, they are indistinguishable in documented standing based on warehouse metadata alone. Determining which table is the primary production aggregate requires inspecting the upstream pipeline build jobs or verifying synchronization freshness against `bikeshare_trips`. For authoritative operational counts where pipeline provenance is unverified, aggregating directly from `bikeshare_trips` provides the verified ground truth.

## Table Info

`dataplex-demo.austin_bikeshare.daily_ride_counts`
