---
type: dataplex-types.global.document
title: taxi_zone_geom
description: Context overlay for taxi_zone_geom.
generated:
  by: dataplex-enrichment-agent/1.0
resource: projects/dataplex-demo/locations/us/entryGroups/@bigquery/entries/bigquery.googleapis.com/projects/dataplex-demo/datasets/andrew_demo1/tables/taxi_zone_geom
sources:
- id: '1'
  resource: bq://dataplex-demo.andrew_demo1.taxi_zone_geom
  title: 'table metadata: dataplex-demo.andrew_demo1.taxi_zone_geom'
x-kcmd:
  name: assets/bigquery/dataplex-demo/andrew_demo1/taxi_zone_geom
  id: assets/bigquery/dataplex-demo/andrew_demo1/taxi_zone_geom
  type: dataplex-types.global.document
  category: warehouse-tables
  resource:
    name: projects/dataplex-demo/locations/us/entryGroups/@bigquery/entries/bigquery.googleapis.com/projects/dataplex-demo/datasets/andrew_demo1/tables/taxi_zone_geom
    displayName: taxi_zone_geom
    description: Context overlay for taxi_zone_geom.
    parent: projects/dataplex-demo/locations/us-central1/entryGroups/democontextset/entries/assets/bigquery/dataplex-demo/andrew_demo1
  aspects:
    dataplex-types.global.document:
      type: table-context
      job:
        name: enrichment-agent/enrich-d44fbe23b3bf415e
        runTime: '2026-11-11T23:19:21Z'
---
# taxi_zone_geom Overview

To maximize the practical value and analytical efficiency of transportation data, `taxi_zone_geom` serves as the primary spatial reference dimension for taxi operational zones. Connecting raw trip transactions to physical locations ensures that spatial metrics yield actionable insights for urban transit planning, route optimization, and resource allocation. By resolving point-based or identifier-based trip events into defined spatial boundaries and administrative hierarchies, it eliminates ambiguity and facilitates aggregations across urban sectors.

## Purpose

The primary purpose of `taxi_zone_geom` is to provide definitive geospatial boundaries and administrative attributes for taxi zones. Operating as a reference table, it enables analysts to link pickup and dropoff identifiers from trip transaction records to physical territories, supporting geospatial analysis, neighborhood-level aggregations, and regional mobility assessments.

## Columns & Metrics

- **zone_id** (`STRING`): The unique identifier for each taxi zone. This serves as the primary dimensional join key, corresponding directly to `pickup_location_id` and `dropoff_location_id` in related trip tables to attribute travel patterns to specific geographical locations.
- **zone_name** (`STRING`): The full descriptive name of the taxi zone, providing human-readable neighborhood or landmark identification for reporting and visualization.
- **borough** (`STRING`): The administrative borough that encompasses the taxi zone, allowing efficient macro-level aggregation and regional demographic comparisons.
- **zone_geom** (`GEOGRAPHY`): The geometric boundary defining the taxi zone's perimeter, structured for native BigQuery GIS spatial computations, containment evaluations, and map generation.

## Usage

To achieve the greatest analytical utility and prevent duplicate computational effort, use `taxi_zone_geom` as follows:

- **Dimensional Joins:** Join `zone_id` against trip fact tables using either `pickup_location_id` or `dropoff_location_id`. When evaluating end-to-end trip movements (origin-destination analysis), join this table twice—once for origins and once for destinations—to assign distinct names and geometries to both ends of the trip.
- **Hierarchical Aggregations:** Roll up high-volume trip metrics (such as trip counts, passenger totals, and fare revenues) by `borough` or `zone_name` to assess transit demand distributions across geographic sectors.
- **Spatial Computations:** Leverage `zone_geom` in native geospatial functions to determine whether external point coordinates (e.g., GPS pings or station locations) fall within specific zone boundaries, avoiding manual geocoding overhead.

## Data Quality

- The table contains an exact total of 263 records [1], representing the full catalog of defined taxi zone boundaries in this environment.

## Table Info

`dataplex-demo.andrew_demo1.taxi_zone_geom`
