---
type: dataplex-types.global.document
title: retail_transactions
description: Context overlay for retail_transactions.
generated:
  by: dataplex-enrichment-agent/1.0
resource: projects/dataplex-demo/locations/us/entryGroups/@bigquery/entries/bigquery.googleapis.com/projects/dataplex-demo/datasets/andrew_demo1/tables/retail_transactions
sources:
- id: '1'
  resource: bq://dataplex-demo.andrew_demo1.retail_transactions
  title: 'table metadata: dataplex-demo.andrew_demo1.retail_transactions'
x-kcmd:
  name: assets/bigquery/dataplex-demo/andrew_demo1/retail_transactions
  id: assets/bigquery/dataplex-demo/andrew_demo1/retail_transactions
  type: dataplex-types.global.document
  category: warehouse-tables
  resource:
    name: projects/dataplex-demo/locations/us/entryGroups/@bigquery/entries/bigquery.googleapis.com/projects/dataplex-demo/datasets/andrew_demo1/tables/retail_transactions
    displayName: retail_transactions
    description: Context overlay for retail_transactions.
    parent: projects/dataplex-demo/locations/us-central1/entryGroups/democontextset/entries/assets/bigquery/dataplex-demo/andrew_demo1
  aspects:
    dataplex-types.global.document:
      type: table-context
      job:
        name: enrichment-agent/enrich-d44fbe23b3bf415e
        runTime: '2026-11-11T23:19:21Z'
---
# retail_transactions Overview

The `retail_transactions` table stores line-level retail transaction records, tracking customer purchases across retail stores along with fulfillment, payment, and post-purchase merchandise processing [1]. It models the complete purchase lifecycle from initial order placement through payment settlement, outbound shipping, customer returns, and replacement exchanges [1].

## Purpose

The primary purpose of `retail_transactions` is to serve as a consolidated operational and reporting log for retail sales events [1]. It captures:
- Transaction identification, customer links, product identifiers, and store locations.
- Financial metrics including transaction totals, taxes, promotional discounts, and fulfillment costs.
- Payment processing details, capturing payment types, numerical payment method codes, and transaction settlement statuses.
- Fulfillment logistics covering outbound shipping methods and delivery expenses.
- Reverse logistics workflows, tracking return events, reasons, shipping fees, product exchanges, and exchange return statuses.

## Columns & Metrics

- **transaction_id** (`STRING`): Unique identifier assigned to the retail transaction record (annotated in schema metadata as `asdqweasdqwe123uniquedescription`) [1].
- **customer_id** (`STRING`): Unique identifier representing the individual customer who completed the purchase [1].
- **product_id** (`STRING`): Identifier for the purchased retail product [1].
- **store_id** (`STRING`): Identifier for the brick-and-mortar store or retail channel where the transaction occurred [1].
- **total_price** (`NUMERIC`): Total gross monetary amount billed for the transaction, expressed in transactional currency units [1].
- **tax** (`NUMERIC`): Total sales tax or value-added tax applied to the transaction [1].
- **discount** (`NUMERIC`): Total promotional discount amount deducted from the gross purchase price [1].
- **payment_type** (`STRING`): Classification of the payment instrument utilized (e.g., credit card, cash, gift card) [1].
- **payment_method** (`FLOAT`): Numeric code or identifier representing the specific payment method used [1].
- **payment_status** (`STRING`): Settlement or processing state of the payment (e.g., authorized, completed, failed) [1].
- **shipping_method** (`STRING`): Fulfillment or carrier service tier selected for outbound shipping (e.g., standard, express) [1].
- **shipping_cost** (`NUMERIC`): Outbound shipping and handling fee charged for delivering the purchased merchandise [1].
- **return_status** (`STRING`): Processing status of an item return initiated for the transaction (e.g., pending, approved, refunded) [1].
- **return_reason** (`STRING`): Stated customer justification for returning the purchased item [1].
- **return_shipping_cost** (`NUMERIC`): Shipping cost incurred to transport returned items back to the warehouse or store [1].
- **exchange_status** (`STRING`): Current lifecycle status of an exchange request linked to the original purchase [1].
- **exchange_product_id** (`STRING`): Identifier of the substitute or replacement product selected as part of an exchange [1].
- **exchange_shipping_cost** (`NUMERIC`): Shipping cost incurred to dispatch the replacement exchange item [1].
- **exchange_return_status** (`STRING`): Logistics status of the original item being returned specifically in connection with an exchange [1].
- **exchange_return_reason** (`STRING`): Specific reason provided for returning the item in order to execute an exchange [1].
- **exchange_return_shipping_cost** (`NUMERIC`): Freight or postal charge incurred to return the original item being exchanged [1].

## Usage

This table is structured for retail analytics, fulfillment tracking, and financial reconciliation:
- **Sales and Revenue Reporting**: Aggregate gross and net sales across products, stores, and customers by evaluating `total_price`, `discount`, and `tax`.
- **Fulfillment and Reverse Logistics Analysis**: Monitor logistics expenses across outbound (`shipping_cost`), inbound returns (`return_shipping_cost`), and replacement dispatches (`exchange_shipping_cost`, `exchange_return_shipping_cost`) to evaluate net order profitability.
- **Customer Return & Exchange Insights**: Analyze return rates and common drivers by joining transaction records on `return_reason` and `exchange_return_reason`.

Within the `andrew_demo1` dataset, sibling tables such as `taxi_zone_geom` provide geographic boundaries for municipal transportation analysis and do not join or relate to this retail transaction entity.

## Table Info

`dataplex-demo.andrew_demo1.retail_transactions`
