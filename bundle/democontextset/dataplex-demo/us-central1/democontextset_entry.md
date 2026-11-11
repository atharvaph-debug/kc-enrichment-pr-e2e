---
type: dataplex-types.global.entrygroup
generated:
  by: dataplex-enrichment-agent/1.0
x-kcmd:
  name: democontextset/dataplex-demo/us-central1/democontextset_entry
  type: dataplex-types.global.entrygroup
---
# Dataset Analytics and Operations

The **Dataset Analytics and Operations** entry group (`democontextset`) is a catalog and operational knowledge base designed to support incrementally updating the context set. It serves data practitioners, analysts, and operators by organizing BigQuery table overlays alongside operational documentation and analytical guidelines.

## Contents and Navigation

The knowledge base is structured into technical assets and operational reference documents:

* **Assets (`catalog/assets`)**: Houses table overlays accessible via the path format `assets/bigquery/<project>/<dataset>/<table>`. Dataset entries serve as their own indexes; retrieve a specific dataset entry to identify the individual tables it contains.
* **Documents (`catalog/documents`)**: Contains cross-cutting operational and analytical reference pages, focusing on analytical guidelines and pitfalls for updating the context set.
* **Context Set Index (`democontextset`)**: Root-level index managing the context set configuration and associated materials.

### Lookup Guidance

A lookup returns only the specific entry requested; parent entries do not include child entries in their responses. To navigate the catalog effectively:
1. Search to identify the target dataset, tier, or document path.
2. Look up the specific entry by its ID to inspect its schema, overlays, or contents.
3. Expect a typical inquiry to require roughly three searches and three lookups to move from a high-level dataset or topic down to the underlying entries.
