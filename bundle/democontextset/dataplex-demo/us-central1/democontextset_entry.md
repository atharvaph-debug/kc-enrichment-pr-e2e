---
type: dataplex-types.global.entrygroup
generated:
  by: dataplex-enrichment-agent/1.0
x-kcmd:
  name: democontextset/dataplex-demo/us-central1/democontextset_entry
  type: dataplex-types.global.entrygroup
---
# Retail Transactions Knowledge Base

The Retail Transactions Knowledge Base (`democontextset`) provides business documentation, asset metadata, and sample SQL queries covering the end-to-end retail sales order lifecycle. It supports reporting and analysis across checkout events, payment processing, fulfillment logistics, and post-purchase returns or product exchanges to evaluate sales volume, financial metrics, and reverse logistics performance. This collection is intended for data analysts, analytics engineers, and business stakeholders querying retail transactional data.

## Core Data Assets

The primary table documented in this group is `retail_transactions`. Its grain is one record per sales order transaction, identified by `transaction_id` and linked to customer, product, and physical store location dimensions. 

> **Data Notice:** According to current warehouse metadata, the `retail_transactions` table contains 0 rows.

## Structure and Navigation

The entry group is organized into two top-level directories:

* **`catalog/assets`**: Technical data assets and table overlays formatted as `assets/bigquery/<project>/<dataset>/<table>`. Dataset entries function as their own indexes; look up a dataset entry directly to view the tables it contains.
* **`catalog/documents`**: Cross-cutting reference documentation, including business domain overviews and curated sample SQL queries.

When querying this catalog, looking up an entry ID returns only the specific entry named (parent entries do not automatically include child entities). To explore the catalog, search for the target topic or dataset, then look up the specific entry IDs returned by the search.
