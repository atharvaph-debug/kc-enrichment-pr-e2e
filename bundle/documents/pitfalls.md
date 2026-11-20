---
type: knowledge-base
title: Pitfalls that silently produce wrong answers
description: What common traps, redundant daily aggregate tables, or join edge cases
  silently distort ridership counts and station metrics?
generated:
  by: dataplex-enrichment-agent/1.0
resource: projects/dataplex-demo/locations/us-central1/catalog/documents/pitfalls
x-kcmd:
  v: 1
  entryId: documents/pitfalls
  name: documents/pitfalls
  entryType: projects/dataplex-types/locations/global/entryTypes/document
  parentEntry: projects/dataplex-demo/locations/us-central1/entryGroups/atharvaphtest1/entries/documents
  aspects:
    dataplex-types.global.document:
      job:
        name: enrichment-agent/enrich-2d509cb5893143af
        runTime: '2026-11-20T20:35:16Z'
---
# Pitfalls that Silently Produce Wrong Answers

## Purpose
This guide addresses common query traps, data type mismatches, and redundant aggregate tables that silently distort ridership metrics or break joins across municipal bike-share tables. Use this page to select the correct system of record, resolve join keys between trips and stations, and avoid unsegmented daily rollups.

## How to Query

### Canonical Daily Ridership
When calculating daily trip volume, aggregate directly from the operational transaction table `bikeshare_trips` rather than using one of the pre-computed summary tables.

```sql
SELECT
  DATE(start_time) AS trip_date,
  COUNT(trip_id) AS total_trips,
  COUNT(DISTINCT bike_id) AS active_bikes,
  AVG(duration_minutes) AS avg_duration_minutes
FROM `austin_bikeshare.bikeshare_trips`
GROUP BY 1
ORDER BY trip_date DESC;
```

### Joining Trips to Docking Stations
`start_station_id` is an `INTEGER`, whereas `end_station_id` is stored as a `STRING`. To join `bikeshare_stations` (where `station_id` is `INTEGER`) on both origin and destination stations, explicitly cast `end_station_id`.

```sql
SELECT
  t.trip_id,
  t.start_time,
  start_station.name AS origin_station,
  start_station.number_of_docks AS origin_docks,
  end_station.name AS destination_station,
  end_station.number_of_docks AS destination_docks
FROM `austin_bikeshare.bikeshare_trips` AS t
LEFT JOIN `austin_bikeshare.bikeshare_stations` AS start_station
  ON t.start_station_id = start_station.station_id
LEFT JOIN `austin_bikeshare.bikeshare_stations` AS end_station
  ON SAFE_CAST(t.end_station_id AS INT64) = end_station.station_id;
```

## Traps

- **Joins on trip destination station fail with a type mismatch or silently drop records.** In `bikeshare_trips`, `start_station_id` is typed as `INTEGER` while `end_station_id` is typed as `STRING`. Joining `bikeshare_stations.station_id` (`INTEGER`) directly to `end_station_id` without `SAFE_CAST(end_station_id AS INT64)` or casting `station_id` to `STRING` causes SQL type mismatch errors or failed joins.
- **Station, subscriber, or bike-level breakdowns return empty or missing columns.** You queried one of the pre-aggregated daily tables (`bikeshare_trips_daily_counts`, `daily_bikeshare_trips`, `daily_ride_counts`, or `daily_trip_counts`). These tables contain only calendar dates and aggregate counts; they do not retain station identifiers, bike types, subscriber classifications, or trip durations. Always query the granular transaction table `bikeshare_trips` for operational or demographic splits.
- **Metrics disagree across daily ridership reports.** The catalog contains four parallel daily aggregate tables (`bikeshare_trips_daily_counts`, `daily_bikeshare_trips`, `daily_ride_counts`, and `daily_trip_counts`) with varying column names (`trip_date` vs. `ride_date`, `trip_count` vs. `num_trips` vs. `daily_rides`) and no pipeline metadata establishing operational authority. To prevent conflicting numbers, compute daily volume directly from `bikeshare_trips` using `COUNT(trip_id)` grouped by `DATE(start_time)`.
- **Dock capacity or station footprint metrics are missing from trip analysis.** Trip logs in `bikeshare_trips` track trip events and station names, but do not track station infrastructure attributes such as physical size, power source, or capacity. Join `bikeshare_trips` to `bikeshare_stations` to retrieve operational infrastructure columns like `number_of_docks`, `status`, `footprint_length`, and `footprint_width`.

## Related Pages
- `bikeshare_trips` — granular system of record for completed bike trips, durations, subscriber types, and routing between docking stations.
- `bikeshare_stations` — dimension table containing physical dock counts, operational statuses, kiosk locations, and council districts.
- `bikeshare_trips_daily_counts`, `daily_bikeshare_trips`, `daily_ride_counts`, and `daily_trip_counts` — derived date-level aggregate rollups.
