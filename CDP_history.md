Based on the two design docs, the cleanest way to frame this is:

* 9DL = the consumer data lake / data foundation
* 9CD = the consumer data platform / activation layer built on top of that foundation

1) Project background and business objectives

Common business background

Both docs start from the same business driver: Michelin’s B2C business is shifting toward a Consumer Lifetime Value model, and Michelin China wants to deepen direct consumer relationships, own consumer data, and provide a more data-augmented consumer experience in China.  ￼  ￼

9DL business objective

The 9DL objective is to build a consumer data lake that can ingest, cleanse, consolidate, and stage China consumer data for downstream use by CDP and other business applications. It is explicitly positioned as the data backbone covering 1st-party touchpoints plus key 2nd/3rd-party ecosystems such as Alibaba, Tencent, Bytedance, Bilibili, communities, and selected offline touchpoints.  ￼

In practical terms, 9DL is meant to:

* centralize consumer data,
* standardize dimensions / metrics / data mappings,
* perform data cleansing and consolidation,
* expose processed data for CDP, BI, CRM, and similar consumers.  ￼

9CD business objective

The 9CD objective is to turn that consumer data into consumer understanding and personalized engagement capability. The stated goal is to enable personalized Michelin lifestyle offer delivery and a seamless consumer journey using consumer data and digital capabilities.  ￼

Its functional objectives are more business-facing:

* automatic consumer ID mapping,
* automatic tagging,
* segmentation,
* automated / personalized journey orchestration,
* dynamic content.  ￼

One-line relationship

So, in plain English:

* 9DL answers: “How do we collect, clean, store, and serve China consumer data?”
* 9CD answers: “How do we use that data to identify consumers, segment them, and run personalized marketing interactions?”

⸻

2) Data flow

Overall end-to-end flow across both docs

External / internal data sources
    -> 9DL ingestion and processing
    -> curated consumer datasets
    -> 9CD consumption and activation
    -> outbound consumer interactions / tracking
    -> events flow back into platform and lake

That is the intended loop, even if each document focuses on its own domain.

2.1 9DL data flow

The 9DL doc defines three zones: data source area, data process area, and data serve area.  ￼

Inbound

9DL ingests:

* batch data via file upload into Azure Storage Account / Blob,
* streaming data into Azure Event Hub,
* RDBMS data from databases via ADF + self-hosted Integration Runtime through the firewall.  ￼  ￼

The doc explicitly says inbound data includes identifiers, transactions, behavioral, demographic, and tracking data. Batch goes directly to the lake; real-time-only sources are streamed via API.  ￼

Processing

In the processing layer:

* Azure Data Factory (ADF) orchestrates data movement from Event Hub and Blob into ADLS,
* Azure Databricks performs transform / cleanse / aggregation,
* raw data is converted into more curated forms such as ODS, datastore, and data mart for downstream consumers.  ￼

Outbound / serving

The processed data is then exposed to:

* CDP
* China BI
* future CRM  ￼  ￼

9DL flow in one line

Files / APIs / DBs
 -> Blob / Event Hub / ADF IR
 -> ADF
 -> ADLS
 -> Databricks ETL / stream processing
 -> curated datasets (ODS / datastore / data mart)
 -> CDP / BI / CRM

⸻

2.2 9CD data flow

The 9CD doc is less of a generic pipeline and more of an application behavior flow.

Core inbound / runtime inputs

9CD receives and works with:

* consumer events from channels such as WeChat, landing pages, web/app tracking,
* data coming from / through 9DL / ADLS,
* internal operational definitions from admin users, such as journey rules, tag rules, segmentation rules, and dynamic content definitions.  ￼

Functional flows by capability

a) ID mapping

* consumer subscribes or enters mobile number,
* system checks for existing member identity,
* if a match exists, platform performs automatic ID mapping and merge.  ￼

b) Tagging / segmentation

* business user defines rules in admin UI,
* job schedule or Kafka event triggers calculation,
* Spark reads definitions from MySQL,
* results are stored into HDFS / HBase, and progress/status goes to MySQL / Redis.  ￼

c) Journey orchestration

* business user defines and activates journeys,
* consumer event is captured from channels,
* event goes to automation engine via Kafka,
* engine processes journey,
* footprint goes to MongoDB,
* statistics go to Kudu,
* execution comments/events continue through Kafka/event jobs.  ￼

d) Dynamic content

* business user defines dynamic content,
* content is linked to consumer properties,
* trigger goes out through WeChat template message,
* consumer clicks link,
* content service identifies the user and reads consumer properties,
* rendered content is returned.  ￼

Infrastructure-level ingress / egress

The doc also defines external traffic patterns:

* Ingress via Azure Application Gateway to private ingress on CaaS,
* Egress for outbound WeChat / article / SMS traffic,
* tracking callbacks and landing-page traffic come into the platform at fairly explicit TPS assumptions.  ￼

9CD flow in one line

Business rules + consumer events + 9DL data
 -> CDP microservices on Kubernetes
 -> Kafka / Spark / CDH / Redis / MySQL / MongoDB / Kudu / ES
 -> segmentation / journeys / content rendering
 -> WeChat / SMS / landing pages / APIs

⸻

3) Component diagram

Below is a synthesized logical component diagram from the two docs.

3.1 Combined logical view

                           +----------------------+
                           |   Business Users     |
                           |  (marketing/admin)   |
                           +----------+-----------+
                                      |
                                      v
                         +-----------------------------+
                         |          9CD Platform       |
                         |  Admin UI / APIs / Gateway  |
                         |  Journey / Tag / Segment    |
                         |  Dynamic Content / ID Map   |
                         +------+-----------+----------+
                                |           |
                reads curated   |           | processes runtime events
                consumer data   |           v
                                |   +------------------------------+
                                |   | Kafka / Redis / MySQL /      |
                                |   | MongoDB / ES / CDH           |
                                |   | Spark / HDFS / HBase / Kudu  |
                                |   +------------------------------+
                                |
                                v
+----------------+    +---------------------+    +----------------------+
| Source systems | -> |        9DL          | -> |   Data consumers      |
| OMS / CRMDP /  |    | Blob / Event Hub /  |    | 9CD / China BI / CRM |
| DMP / Tracking |    | ADF / ADLS /        |    +----------------------+
| SNX / MARS etc |    | Databricks / IR     |
+----------------+    +---------------------+

3.2 9DL logical component diagram

The 9DL component list and architecture clearly show these main components: Storage Account, Event Hub, Data Factory, Firewall, ADLS, Databricks, Integration Runtime, Key Vault, Azure AD, and source systems (DB/file/realtime).  ￼

Data Sources
  - DB sources
  - File sources
  - Real-time sources
        |
        v
+-------------------+      +------------------+
| Blob Storage      |      | Event Hub        |
| (batch landing)   |      | (stream ingest)  |
+---------+---------+      +---------+--------+
          \                       /
           \                     /
            v                   v
             +-------------------+
             | Azure Data Factory|
             | + Self-hosted IR  |
             +---------+---------+
                       |
                       v
              +-------------------+
              | ADLS Gen2         |
              | raw + curated     |
              +---------+---------+
                        |
                        v
              +-------------------+
              | Azure Databricks  |
              | cleanse / ETL /   |
              | aggregate         |
              +---------+---------+
                        |
                        v
        +----------------+-------------------+
        |                |                   |
        v                v                   v
      9CD            China BI             CRM

3.3 9CD logical component diagram

The 9CD doc describes a microservices-based CDP on Kubernetes, with:

* API gateway,
* admin frontend/backend,
* integration services,
* marketing automation services,
* customer/CDP services,
* Kafka,
* CDH stack,
* Redis,
* MySQL,
* MongoDB,
* ElasticSearch,
* CDN,
* Azure AD,
* Jenkins / GitLab / Artifactory in CI/CD context.  ￼  ￼

                     +----------------------+
                     |  Azure AD / OAuth2   |
                     +----------+-----------+
                                |
                                v
+-------------+        +-------------------------+        +------------------+
| Admin Users | -----> | API Gateway / Admin UI  | -----> | CDP Microservices|
+-------------+        +-------------------------+        +----+------+------+ 
                                                                  |      |
                                                                  |      |
                                                                  v      v
                                                           +---------+  +--------+
                                                           | Kafka   |  | Redis  |
                                                           +----+----+  +--------+
                                                                |
                                                                v
                  +-------------+   +---------+  +---------+  +---------+  +--------+
                  | MySQL       |   | MongoDB |  | ES      |  | CDH     |  | CDN    |
                  | metadata /  |   | journey |  | search  |  | Spark/  |  | static |
                  | config      |   | runtime |  | /index  |  | HDFS/   |  | content|
                  +-------------+   +---------+  +---------+  | HBase/  |  +--------+
                                                              | Kudu     |
                                                              +----+-----+
                                                                   |
                                                                   v
                                                           +---------------+
                                                           | 9DL / ADLS    |
                                                           | consumer data |
                                                           +---------------+

⸻

Executive summary

The two documents describe a two-layer China consumer data architecture:

* 9DL is the data platform layer: ingest, store, cleanse, and serve consumer data using Azure Blob, Event Hub, ADF, ADLS, Databricks, and self-hosted IR. Its consumers include 9CD, BI, and future CRM.  ￼  ￼  ￼
* 9CD is the activation / engagement layer: a Kubernetes-based microservices platform for ID mapping, tagging, segmentation, journey orchestration, and dynamic content, backed by Kafka, CDH, Redis, MySQL, MongoDB, ElasticSearch, and connected to 9DL / ADLS.  ￼  ￼

If you want, I can next turn this into a single comparison table: As-Is / 9DL / 9CD / End-to-end To-Be, or draw it as mermaid component and data-flow diagrams.