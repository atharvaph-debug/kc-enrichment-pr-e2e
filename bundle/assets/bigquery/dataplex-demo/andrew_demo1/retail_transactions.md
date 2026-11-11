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
  category: miscellaneous
  resource:
    name: projects/dataplex-demo/locations/us/entryGroups/@bigquery/entries/bigquery.googleapis.com/projects/dataplex-demo/datasets/andrew_demo1/tables/retail_transactions
    displayName: retail_transactions
    description: Context overlay for retail_transactions.
    parent: projects/dataplex-demo/locations/us-central1/entryGroups/democontextset/entries/assets/bigquery/dataplex-demo/andrew_demo1
  aspects:
    dataplex-types.global.document:
      type: table-context
      job:
        name: enrichment-agent/enrich-3a12f021f22b4475
        runTime: '2026-11-11T23:15:25Z'
---
# retail_transactions Overview

The `retail_transactions` table captures retail sales orders and their end-to-end lifecycle events, spanning initial purchase checkout, payment processing, outbound logistics, and downstream post-purchase activities such as returns and product exchanges. Each record represents an order transaction associated with a customer, product, and retail store location, capturing the transaction's financial amounts, fulfillment options, and reverse logistics costs.

## Purpose

The primary purpose of `retail_transactions` is to serve as an operational and analytical store of retail order transactions. It tracks sales volumes and financial metrics (order value, sales tax, and applied discounts) alongside complete post-order fulfillment states, including payment status, shipping methods, customer returns, and replacement exchange workflows. Metadata indicates that the table currently holds 0 rows [1].

## Columns & Metrics

### Core Identifiers
- **`transaction_id`** (`STRING`): Unique identifier for the retail transaction (documented with description `asdqweasdqwe123uniquedescription`). Represents the transaction key for the purchase record.
- **`customer_id`** (`STRING`): Identifier of the customer who completed the retail purchase.
- **`product_id`** (`STRING`): Identifier of the primary product purchased within the transaction.
- **`store_id`** (`STRING`): Identifier of the physical retail store or sales location where the transaction took place.

### Financial Amounts & Discounts
- **`total_price`** (`NUMERIC`): Total gross monetary amount charged for the transaction.
- **`tax`** (`NUMERIC`): Monetary tax amount assessed and collected for the transaction.
- **`discount`** (`NUMERIC`): Monetary value of promotional discounts or deductions applied against the purchase price.

### Payment Details
- **`payment_type`** (`STRING`): Classification or category of tender utilized for the transaction (e.g., credit card, cash, gift card).
- **`payment_method`** (`FLOAT`): Numerical code or identifier representing the specific payment mechanism or channel.
- **`payment_status`** (`STRING`): Processing state of the transaction's payment settlement.

### Outbound Fulfillment & Shipping
- **`shipping_method`** (`STRING`): Carrier, speed, or fulfillment mode designated for outbound delivery to the customer.
- **`shipping_cost`** (`NUMERIC`): Cost or fee charged to fulfill and ship the purchased product.

### Returns & Reverse Logistics
- **`return_status`** (`STRING`): Lifecycle or processing status of a customer product return request.
- **`return_reason`** (`STRING`): Customer-provided explanation or categorical reason for initiating the product return.
- **`return_shipping_cost`** (`NUMERIC`): Shipping and freight charges incurred to transport the returned item back to inventory.

### Exchanges & Replacements
- **`exchange_status`** (`STRING`): Operational status of a requested product replacement or exchange.
- **`exchange_product_id`** (`STRING`): Identifier of the new or alternate product requested or issued to replace the original purchase.
- **`exchange_shipping_cost`** (`NUMERIC`): Shipping cost incurred to dispatch the replacement item to the customer.
- **`exchange_return_status`** (`STRING`): Processing status of the original item returned as part of an exchange workflow.
- **`exchange_return_reason`** (`STRING`): Reason recorded for exchanging the original product.
- **`exchange_return_shipping_cost`** (`NUMERIC`): Shipping cost incurred to return the original item being replaced in an exchange.

## Usage

This table supports several analytical workflows across retail operations and customer behavior:
- **Revenue & Sales Performance**: Aggregating `total_price`, `discount`, and `tax` by `store_id`, `product_id`, or `customer_id` allows analysts to evaluate gross and net retail sales, discount penetration, and regional store performance.
- **Fulfillment & Logistics Cost Analysis**: Comparing outbound `shipping_cost` against delivery choices in `shipping_method` helps identify logistics margins and delivery carrier utilization.
- **Reverse Logistics & Customer Satisfaction**: Analyzing `return_status`, `return_reason`, and `return_shipping_cost` alongside exchange fields (`exchange_status`, `exchange_product_id`, `exchange_return_reason`) highlights problematic products with high defect or return rates, as well as the total operational overhead of managing return and replacement shipments.
- **Payment Operations**: Evaluating `payment_status` across various `payment_type` and `payment_method` values assists in monitoring transaction settlement rates and payment failure trends.

## Table Info

`dataplex-demo.andrew_demo1.retail_transactions`
