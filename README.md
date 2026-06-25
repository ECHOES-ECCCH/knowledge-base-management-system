# ECHOES Knowledge Base Management System (KBMS)

The **Knowledge Base Management System (KBMS)** is one of the central components of the ECHOES architecture, managing the querying, publishing, and editing of semantic data across a federated network of triplestores. It operates as a pure **RESTful API** (no graphical user interface is included in this repository) and is secured via **OAuth 2.0**.

## Core Features & Architecture

* **Federated Node & Registry Management:** Centralized registration, monitoring, and governance of federated triplestores, handled via a dedicated Administrative Repository.
* **Data Ingestion & Named Graphs:** RDF data is ingested exclusively via file uploads, with each upload creating a distinct Named Graph (NG) to ensure strict traceability and provenance guarantees.
* **Immutable Knowledge-Sharing Nodes:** Once a Named Graph is published to a production node, it cannot be modified in place. Updates or deletions trigger a replacement strategy that moves the old graph to a Recycle-bin node for rollback and snapshot versioning.
* **Collaborative Private Spaces:** Supports the creation of isolated, high-performance "temporary" Named Graphs on auxiliary triplestores. These spaces allow users to perform direct SPARQL-Updates and iterative editing without the overhead of live change-tracking before formal publication.
*  **Snapshot & Historical Versioning:** Supports historical state reconstruction by querying both active knowledge-sharing nodes and the recycle-bin triplestore. This allows users to pinpoint and retrieve the exact active Named Graph URIs and content as they existed during any specific date or timespan.

## API Documentation

The Swagger documentation for the API can be found at [Swagger UI](https://echoes-kb-api-route-echoes-graphs-production.apps.dcw1.paas.psnc.pl/swagger-ui/index.html).

> ⚠️ **Authentication Required:** To execute any service through the Swagger interface, a valid OAuth 2.0 token is required. You can obtain a valid access token directly from the [Token Generation Portal](https://aai-demo.egi.eu/token/).

## Current Deployment & Federated Nodes

The KBMS is currently operational and actively manages a federated environment consisting of **7 registered triplestores** used for testing and validation. These nodes are centrally governed through a dedicated **MongoDB** administrative database that handles system metadata, user roles, and workspace definitions.

The hosting infrastructure and node allocations are distributed as follows:
* **PSNC Infrastructure (6 Triplestores):**
  * **4 Public Nodes:** Dedicated public testing environments for hosting production-level RDF data.
  * **1 Private Space Node:** An isolated testing environment configured specifically to handle temporary Private Space RDF workloads.
  * **1 Recycle Bin Node:** Archival storage configured to store deleted or replaced Named Graphs, ensuring historical data integrity.
* **FORTH Infrastructure (1 Triplestore):**
  * **1 Registration Node:** Dedicated to hosting registration HDT data and relative system metadata.

> ⚠️ **Note:** This node configuration and infrastructure topology reflect the current testing phase and are subject to change as the federation scales and evolves.
