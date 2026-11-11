---
type: dataplex-types.global.document
title: Pitfalls that silently produce wrong answers
description: Symptom-to-fix guide detailing common query mistakes, invalid join patterns,
  and silent calculation errors across operational and spatial datasets.
generated:
  by: dataplex-enrichment-agent/1.0
resource: projects/dataplex-demo/locations/us-central1/catalog/documents/pitfalls
x-kcmd:
  name: documents/pitfalls
  id: documents/pitfalls
  type: dataplex-types.global.document
  category: documents
  resource:
    name: projects/dataplex-demo/locations/us-central1/catalog/documents/pitfalls
    displayName: Pitfalls that silently produce wrong answers
    description: Symptom-to-fix guide detailing common query mistakes, invalid join
      patterns, and silent calculation errors across operational and spatial datasets.
    parent: projects/dataplex-demo/locations/us-central1/entryGroups/democontextset/entries/documents
  aspects:
    dataplex-types.global.document:
      type: knowledge-base
      job:
        name: enrichment-agent/enrich-d44fbe23b3bf415e
        runTime: '2026-11-11T23:19:21Z'
---
# Pitfalls that silently produce wrong answers

## Purpose
This guide addresses which cross-table joins, key mappings, and query assumptions silently corrupt query results across retail and municipal transit data. It identifies incompatible entity boundaries and prevents invalid dimensional joins before queries are executed.

## Traps
- You attempted to connect `retail_transactions` to `taxi_zone_geom` using store, transaction, or location identifiers. Sibling tables in `andrew_demo1` serve entirely distinct domains: `taxi_zone_geom` provides geospatial boundaries specifically for municipal transit analysis and does not relate or join to the retail transaction entity. Keep retail operational reporting separate from transit boundaries.
- **Trip locations fail to resolve or mismatch dimensional attributes.** You attempted to map spatial trip events using non-standard keys or non-transportation records. The `taxi_zone_geom` table must be joined strictly via its primary dimensional key `zone_id` to corresponding `pickup_location_id` or `dropoff_location_id` fields in related trip transaction tables to aggregate by `zone_name` or `borough`.
