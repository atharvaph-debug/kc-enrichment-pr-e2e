---
type: table-context
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
  v: 1
  entryId: assets/bigquery/dataplex-demo/andrew_demo1/retail_transactions
  entryType: projects/dataplex-types/locations/global/entryTypes/document
  parentEntry: projects/jasoneliu-joonix-test-project/locations/us-central1/entryGroups/atharva-github-pr-e2e/entries/assets/bigquery/dataplex-demo/andrew_demo1
  aspects:
    dataplex-types.global.document:
      job:
        name: enrichment-agent/enrich-be09cba622934dbd
        runTime: '2026-11-12T21:24:42Z'
---
# retail_transactions Overview

The `retail_transactions` table serves as a granular log of retail sales and order fulfillment activities. It captures point-of-sale and online purchasing events, linking customers, products, and retail store locations with financial amounts, payment parameters, and fulfillment details. In addition to primary purchase transactions, the schema tracks the end-to-end post-purchase lifecycle, including product returns, exchange requests, associated customer reasons, and reverse-logistics shipping costs.

## Purpose

The primary purpose of `retail_transactions` is to record and monitor retail purchase operations, settlement statuses, and downstream order adjustments. Each record tracks item-level or basket-level transactions along with price components (gross totals, taxes, and applied discounts), payment execution, and fulfillment logistics. It also functions as the operational tracking mechanism for customer service events such as returns, replacements, and exchanges, allowing retail analysts and store operations teams to reconcile revenue, monitor payment success, and evaluate return and exchange rates across products and stores.

## Columns & Metrics

### Transaction & Entity Identifiers
- **transaction_id** (`STRING`): Unique identifier for the individual retail transaction.
- **customer_id** (`STRING`): Identifier representing the customer initiating the transaction.
- **product_id** (`STRING`): Identifier for the primary product purchased in the transaction.
- **store_id** (`STRING`): Identifier for the physical retail store or digital channel where the transaction occurred.

### Financials & Pricing Metrics
- **total_price** (`NUMERIC`): Total monetary amount charged for the transaction, expressed as a standard currency numeric value.
- **tax** (`NUMERIC`): Tax amount assessed and collected on the transaction.
- **discount** (`NUMERIC`): Total discount or promotional deduction applied against the purchase price.

### Payment Processing
- **payment_type** (`STRING`): High-level category or channel of payment used (e.g., credit, debit, gift card, or digital wallet).
- **payment_method** (`FLOAT`): Numeric code or identifier representing the specific payment instrument or payment gateway configuration.
- **payment_status** (`STRING`): Processing state of the transaction settlement (e.g., authorized, completed, or failed).

### Fulfillment & Logistics
- **shipping_method** (`STRING`): Delivery service level or fulfillment mechanism selected (e.g., standard, expedited, or in-store pickup).
- **shipping_cost** (`NUMERIC`): Outbound shipping and handling fee charged to the customer or absorbed for fulfillment.

### Returns Management
- **return_status** (`STRING`): Operational status of any return workflow initiated for the purchased product.
- **return_reason** (`STRING`): Customer-reported reason or classification code for returning the merchandise.
- **return_shipping_cost** (`NUMERIC`): Freight or postage cost incurred for the return shipment.

### Product Exchanges & Reverse Logistics
- **exchange_status** (`STRING`): State of an exchange request initiated for the transaction.
- **exchange_product_id** (`STRING`): Identifier of the replacement product selected in the exchange.
- **exchange_shipping_cost** (`NUMERIC`): Shipping cost incurred to fulfill and transport the replacement merchandise.
- **exchange_return_status** (`STRING`): Status of the return process specifically tied to the original item being exchanged.
- **exchange_return_reason** (`STRING`): Specific reason noted for initiating an exchange rather than a standard return.
- **exchange_return_shipping_cost** (`NUMERIC`): Shipping and reverse-logistics cost incurred to return the original item during an exchange.

## Usage

The `retail_transactions` table supports core retail reporting and operational analytics workflows:
- **Net Revenue & Sales Reporting**: Combining `total_price`, `tax`, and `discount` allows finance and merchandising teams to evaluate gross sales, promotional impact, and net realized revenue by `store_id` and `product_id`.
- **Payment Reconciliation**: Grouping by `payment_type`, `payment_method`, and `payment_status` helps identify gateway failure rates, preferred customer tender types, and settlement anomalies.
- **Reverse Logistics & Defect Analysis**: Monitoring `return_status`, `return_reason`, `exchange_status`, and `exchange_return_reason` enables quality assurance and merchandising teams to identify frequently returned products, quantify total reverse shipping expenditures, and isolate high-return physical or online store locations.

## Data Quality

The table metadata records an exact row count of 0 rows [1].

## Table Info

`dataplex-demo.andrew_demo1.retail_transactions`
