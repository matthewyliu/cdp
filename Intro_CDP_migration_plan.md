---
marp: true
html: true
theme: default
paginate: true
size: 16:9
header: 'CDP Application Migration — Infra Briefing'
footer: 'Michelin China · Consumer Data Platform'
style: |
  section {
    font-size: 24px;
    /* Extra bottom inset so dense slides clear footer + paginate (theme default ~56px is often too tight) */
    padding-bottom: 5.5rem !important;
    box-sizing: border-box;
  }
  section.lead {
    padding-bottom: 3.5rem !important;
  }
  footer {
    font-size: 11px;
    line-height: 1.2;
    color: #6b7280;
    opacity: 0.95;
  }
  /* Paginate number sits in footer area on default theme */
  section::after {
    font-size: 11px;
    line-height: 1.2;
    color: #6b7280;
  }
  h1 {
    color: #1f4e79;
  }
  h2 {
    color: #2e75b6;
    border-bottom: 2px solid #2e75b6;
    padding-bottom: 4px;
  }
  table {
    font-size: 22px;
  }
  code {
    background: #f4f4f4;
  }
  img[alt~="center"] {
    display: block;
    margin: 0 auto;
  }
  /* Slide "Why CDP — Business Context": smaller secondary lines */
  .context-footnote {
    font-size: 17px;
    line-height: 1.35;
    margin: 0.4em 0 0 0;
    color: #374151;
  }
  .context-footnote strong {
    color: #1f4e79;
    font-weight: 600;
  }
  /* Combined slide: layer summary (left) + system context diagram (right) */
  section.split-context h2 {
    margin-bottom: 0.35em;
  }
  section.split-context .split-row {
    display: grid;
    grid-template-columns: 42% 56%;
    gap: 1rem;
    align-items: start;
    margin-top: 0.15em;
  }
  section.split-context .split-left {
    font-size: 16px;
    line-height: 1.32;
    color: #1f2937;
  }
  section.split-context .split-layer-title {
    margin: 0.5em 0 0.08em 0;
    font-size: 17px;
    font-weight: 700;
    color: #1f4e79;
  }
  section.split-context .split-layer-title:first-child {
    margin-top: 0;
  }
  section.split-context .split-left ul {
    margin: 0 0 0.35em 0;
    padding-left: 1.05em;
  }
  section.split-context .split-left li {
    margin-bottom: 0.12em;
  }
  section.split-context .split-right {
    display: flex;
    align-items: flex-start;
    justify-content: center;
  }
  section.split-context .split-right img {
    width: 120%;
    max-height: 440px;
    object-fit: contain;
    margin: 0;
  }
  section.split-context .split-caption {
    font-size: 14px;
    line-height: 1.32;
    margin: 0.45em 0 0 0;
    color: #374151;
  }
  section.split-context .split-note {
    font-size: 13px;
    line-height: 1.3;
    margin: 0.3em 0 0 0;
    color: #6b7280;
  }
  section.split-context .split-bottom {
    margin-top: 0.35em;
  }
  /* 9DL on Azure: bullets (left) + reference architecture diagram (right) */
  section.arch-9dl h2 {
    margin-bottom: 0.2em;
  }
  section.arch-9dl .arch-9dl-lead {
    font-size: 16px;
    line-height: 1.3;
    color: #4b5563;
    margin: 0 0 0.35em 0;
  }
  section.arch-9dl .arch-9dl-row {
    display: grid;
    grid-template-columns: 32% 66%;
    gap: 0.9rem;
    align-items: start;
    margin-top: 0.1em;
  }
  section.arch-9dl .arch-9dl-left {
    font-size: 15px;
    line-height: 1.32;
    color: #1f2937;
  }
  section.arch-9dl .arch-9dl-left ul {
    margin: 0.12em 0 0 0;
    padding-left: 1.05em;
  }
  section.arch-9dl .arch-9dl-left li {
    margin-bottom: 0.1em;
  }
  section.arch-9dl .arch-9dl-right {
    display: flex;
    align-items: flex-start;
    justify-content: center;
  }
  section.arch-9dl .arch-9dl-right img {
    width: 100%;
    max-height: 420px;
    object-fit: contain;
    margin: 0;
  }
  section.arch-9dl .arch-9dl-caption {
    font-size: 12px;
    line-height: 1.3;
    color: #6b7280;
    margin: 0.35em 0 0 0;
  }
  /* As-is hybrid slide: compact text + diagram anchored at bottom */
  section.asis-hybrid {
    font-size: 18px;
    line-height: 1.28;
  }
  section.asis-hybrid h2 {
    margin-bottom: 0.2em;
    padding-bottom: 3px;
  }
  section.asis-hybrid > p {
    margin: 0.12em 0 0.18em 0;
  }
  section.asis-hybrid ul {
    margin: 0.08em 0 0.12em 0;
    padding-left: 1.05em;
  }
  section.asis-hybrid li {
    margin-bottom: 0.05em;
  }
  section.asis-hybrid .asis-impl {
    font-size: 16px;
    margin: 0.12em 0 0.2em 0;
    color: #374151;
  }
  section.asis-hybrid .asis-diagram-wrap {
    margin-top: 0.2em;
    padding-top: 0.15em;
    border-top: 1px solid #e5e7eb;
  }
  section.asis-hybrid .asis-diagram-wrap img {
    display: block;
    margin: 0 auto;
    max-height: 248px;
    max-width: 100%;
    width: auto;
    object-fit: contain;
  }
  section.asis-hybrid .asis-diagram-caption {
    font-size: 11px;
    line-height: 1.25;
    color: #6b7280;
    margin: 0.2em 0 0 0;
    text-align: center;
  }
  /* Pre-study slide: diagram (left) + effort (right), vertically centered on slide */
  section.prestudy-slide {
    font-size: 19px;
    line-height: 1.28;
    display: flex;
    flex-direction: column;
    justify-content: center;
    box-sizing: border-box;
  }
  section.prestudy-slide h2 {
    margin-bottom: 0.2em;
    padding-bottom: 3px;
    margin-top: 0;
  }
  section.prestudy-slide > p:first-of-type {
    font-size: 16px;
    color: #4b5563;
    margin: 0 0 0.45em 0;
  }
  section.prestudy-slide .prestudy-row {
    display: grid;
    grid-template-columns: 7fr 3fr;
    gap: 0.85rem;
    align-items: center;
    margin-top: 0;
  }
  section.prestudy-slide .prestudy-left img {
    display: block;
    margin: 0 auto;
    max-height: 340px;
    max-width: 100%;
    object-fit: contain;
  }
  section.prestudy-slide .prestudy-right {
    font-size: 15px;
    line-height: 1.32;
    padding-top: 0.1em;
  }
  section.prestudy-slide .prestudy-est {
    font-size: 15px;
    margin: 0;
  }
  section.prestudy-slide .prestudy-est ul {
    margin: 0.15em 0 0 0;
    padding-left: 1.05em;
  }
  section.prestudy-slide .prestudy-est li {
    margin-bottom: 0.1em;
  }
  /* Large diagram under h2 + lead line; h2 uses same base as other slides (global section 24px). */
  section.diagram-slide {
    line-height: 1.25;
  }
  section.diagram-slide h2 {
    margin-bottom: 0.15em;
    padding-bottom: 3px;
  }
  section.diagram-slide > p:first-of-type {
    font-size: 15px;
    color: #4b5563;
    margin: 0 0 0.3em 0;
  }
  section.diagram-slide img {
    display: block;
    margin: 0 auto;
    max-height: 430px;
    max-width: 100%;
    object-fit: contain;
  }
  /* 9CD / CDH component table (compact four columns) */
  section.cdh-slide h2 {
    margin-bottom: 0.2em;
    padding-bottom: 3px;
  }
  section.cdh-slide .cdh-lead {
    font-size: 16px;
    line-height: 1.32;
    color: #4b5563;
    margin: 0 0 0.35em 0;
  }
  section.cdh-slide table {
    width: 100%;
    margin: 0.15em 0 0 0;
    font-size: 14px;
    line-height: 1.28;
    border-collapse: collapse;
    table-layout: fixed;
  }
  section.cdh-slide th,
  section.cdh-slide td {
    border: 1px solid #d1d5db;
    padding: 0.28em 0.45em;
    text-align: left;
    vertical-align: top;
    word-wrap: break-word;
  }
  section.cdh-slide th {
    background: #eef2f7;
    color: #1f4e79;
    font-weight: 600;
  }
  section.cdh-slide th:nth-child(1),
  section.cdh-slide td:nth-child(1) {
    width: 10%;
  }
  section.cdh-slide th:nth-child(2),
  section.cdh-slide td:nth-child(2) {
    width: 16%;
  }
  section.cdh-slide th:nth-child(3),
  section.cdh-slide td:nth-child(3) {
    width: 24%;
  }
  section.cdh-slide tbody tr:nth-child(even) {
    background: #fafafa;
  }
  /* Domains A&B / C&D slides — aligned tables, spacing, footer clearance */
  section.domains-slide {
    font-size: 20px;
    line-height: 1.28;
  }
  section.domains-slide h2 {
    margin-bottom: 0.3em;
    padding-bottom: 3px;
  }
  section.domains-slide .domains-section-title {
    font-size: 18px;
    font-weight: 700;
    color: #1f4e79;
    margin: 0.4em 0 0.15em 0;
  }
  section.domains-slide .domains-section-title:first-of-type {
    margin-top: 0.1em;
  }
  section.domains-slide table {
    width: 100%;
    max-width: 900px;
    margin: 0 auto 0.45em auto;
    font-size: 17px;
    border-collapse: collapse;
    table-layout: fixed;
  }
  section.domains-slide table th:first-child,
  section.domains-slide table td:first-child {
    width: 44%;
  }
  section.domains-slide th,
  section.domains-slide td {
    border: 1px solid #d1d5db;
    padding: 0.3em 0.55em;
    text-align: left;
    vertical-align: top;
    word-wrap: break-word;
  }
  section.domains-slide th {
    background: #eef2f7;
    color: #1f4e79;
    font-weight: 600;
  }
  section.domains-slide tbody tr:nth-child(even) {
    background: #fafafa;
  }
  section.domains-slide .domains-after-tables {
    font-size: 16px;
    line-height: 1.32;
    color: #374151;
    margin: 0.2em auto 0 auto;
    max-width: 900px;
  }
  section.domains-slide .domains-list {
    margin: 0.15em auto 0.35em auto;
    padding-left: 1.15em;
    max-width: 900px;
    font-size: 17px;
  }
  section.domains-slide .domains-list li {
    margin-bottom: 0.12em;
  }
  section.domains-slide .domains-callout {
    font-size: 16px;
    line-height: 1.32;
    margin: 0.35em auto 0 auto;
    max-width: 900px;
    padding: 0.4em 0.55em;
    background: #f3f4f6;
    border-left: 4px solid #2e75b6;
    color: #1f2937;
  }
---

<!-- _class: lead -->
<!-- _paginate: false -->

# CDP Application Migration
## Heads-up & Context for the Infra Team

an early walkthrough of the planned change to the CDP application, so Infra has the big picture ahead of the migration project.


---

## Why CDP — Business Context

Michelin B2C is moving to a **Consumer Lifetime Value** model. Michelin China needs to:

- Deepen **direct** consumer relationships
- **Own** consumer data end-to-end
- Deliver a more **data-augmented** consumer experience

**The CDP application in scope is two layers working together**

| Layer | Role | Answers the question |
|-------|------|----------------------|
| **9DL** | Consumer **data lake** / data foundation | *How do we collect, clean, store, and serve China consumer data?* |
| **9CD** | Consumer **data platform** / activation layer | *How do we use that data to identify, segment, and engage consumers?* |

<p class="context-footnote"><strong>Coverage:</strong> 1st-party touchpoints + key 2nd/3rd-party ecosystems (Alibaba, Tencent, Bytedance, Bilibili, communities, selected offline).</p>

<p class="context-footnote"><strong>Note:</strong> 9CD is <em>both</em> a <strong>data source</strong> and a <strong>data consumer</strong> of 9DL — the two layers are tightly coupled.</p>

---

<!-- _class: split-context -->

## High-Level System Context Diagram

<div class="split-row">
<div class="split-left">
<p class="split-layer-title">9DL — Data foundation</p>
<ul>
<li>Centralize consumer data from all China touchpoints</li>
<li>Standardize dimensions, metrics, and data mappings</li>
<li>Cleanse and consolidate raw data</li>
<li>Expose curated datasets to <strong>CDP, BI, CRM</strong> and other consumers</li>
</ul>
<p class="split-layer-title">9CD — Activation</p>
<ul>
<li>Automatic <strong>consumer ID mapping &amp; merge</strong></li>
<li>Automatic <strong>tagging</strong> and <strong>segmentation</strong></li>
<li><strong>Journey orchestration</strong> (automated / personalized)</li>
<li><strong>Dynamic content</strong> across channels (WeChat, SMS, landing pages)</li>
</ul>
</div>
<div class="split-right">
<img src="design/diagram_system_context_cdp.png" alt="CDP high-level system context" />
</div>
</div>

---

<!-- _class: diagram-slide -->

## Overall Architecture — End-to-End Flow
- **Sources** → **lakehouse** on storage (Pre-ODS / ODS / DW / DM with Databricks + Delta) → **data services** (MySQL, Redis, Cloudera, Elastic, Cosmos DB, Kafka) → **CDP** → **MAP** → **touchpoints**
- Behavior data closes the loop back to CDP. 

![center w:1050](design/diagram_overall_architecture_layers.png)

---

<!-- _class: cdh-slide -->

## 9CD / CDH — Key platform components

<p class="cdh-lead">The <strong>9CD</strong> activation layer sits on a <strong>Cloudera Hadoop (CDH)</strong> cluster for large-scale storage and processing; these are the CDH-related building blocks from the component inventory (CDH and <code>CDH/…</code> services).</p>

| Component Code | Component | Component details | Description |
| ---------------- | --------- | ----------------- | ----------- |
| C20 | CDH | Cloudera Hadoop platform |  |
| C21 | CDH/Impala | Interactive query engine | Apache Impala is the open source, native analytic database for Apache Hadoop. |
| C22 | CDH/kudu | Distributed data store engine | Apache Kudu is an open source distributed data storage engine that makes fast analytics on fast and changing data easy. |
| C23 | CDH/spark | Big data processing engine | A fast and general compute engine for Hadoop data. Spark provides a simple and expressive programming model that supports a wide range of applications, including ETL, machine learning, stream processing, and graph computation. |
| C24 | CDH/hdfs | Distributed file system | A distributed file system that provides high-throughput access to application data. |
| C25 | CDH/hbase | Distributed data store | A scalable, distributed database that supports structured data storage for large tables. |
| C26 | CDH/YARN | Resource Management | A framework for job scheduling and cluster resource management. |
| C27 | CDH/Hive | Hadoop data store engine | A data warehouse infrastructure that provides data summarization and ad hoc querying. |
| C28 | CDH/Zookeeper | coordination service | A high-performance coordination service for distributed applications. |
| C29 | CDH/ClouderaManager | Hadoop management tool | Cloudera Manager is the industry's trusted tool for managing Hadoop in production. |

---

<!-- _class: arch-9dl -->

## 9DL — Data Lake Architecture (Azure China)
<br>
<p class="arch-9dl-lead">How the consumer <strong>9DL</strong> platform is put together: ingestion → lakehouse storage on <strong>ADLS Gen2</strong> (Delta) → serving.</p>
<br>

<div class="arch-9dl-row">
<div class="arch-9dl-left">
<ul>
<li><strong>Ingestion:</strong> batch via external receiver (Blob) and <strong>streaming</strong> via Event Hubs</li>
<li><strong>Orchestration &amp; compute:</strong> <strong>Data Factory</strong> (scheduler) and <strong>Databricks</strong> for transforms</li>
<li><strong>Storage (Gen2):</strong> <strong>Raw</strong> landing → <strong>ODS</strong> → <strong>datastore</strong> → <strong>Data mart</strong> — modeled as <strong>Delta Lake</strong> tables on ADLS</li>
<li><strong>Platform:</strong> <strong>Key Vault</strong> for secrets/encryption; <strong>CI/CD</strong> for release management</li>
<li><strong>Serving:</strong> <strong>CDP</strong>, <strong>CRM</strong>, SQL reporting (<strong>ChinaBI</strong>), <strong>Power BI</strong></li>
</ul>
</div>
<div class="arch-9dl-right">
<img src="design/diagram_9dl_azure_architecture.png" alt="9DL on Azure China: source to ADLS Gen2 zones and serving" />
</div>
</div>

---

<!-- _class: asis-hybrid -->

## As-Is Reality — Hybrid Chain
<br>
The real estate today is a hybrid **lake + warehouse + app-serving chain** with multiple delivery paths.

- **9DL ↔ 9CD is bidirectional.**  9DL/ADLS = secondary storage for 9CD/CDH.
- **9CD has its own data gravity.** Substantial processing happens inside 9CD — Kafka, CDH (Spark / HDFS / HBase / Kudu), MySQL, MongoDB, Redis, ElasticSearch — not always lake-first.
- **Parallel reporting chain** exists alongside the lake: **9RR Data Warehouse · SSIS · Talend · H5 Tomcat · Power BI**.
- **Six runtime patterns** observed in operations, ranging from 
  - `Source → Kafka → 9DL → Power BI` to 
  - `Source → ADF/Databricks → 9DL → 9RR → Talend → H5 → Power BI`.

<br>
<br>
<div class="asis-diagram-wrap">
<img src="design/diagram_asis_hybrid_chain.png" alt="As-is monitoring view: Source, Datalake and warehouse, Reports, and numbered scenarios" />
</div>

---

<!-- _class: prestudy-slide -->

## Migration Pre-study from Michael Zhao


<div class="prestudy-row">
<div class="prestudy-left">
<img src="design/migration_prestudy_architecture_michael_zhao.png" alt="Target architecture study: AS-IS CDH vs TO-BE Alibaba stack by layer" />
</div>
<div class="prestudy-right">
<div class="prestudy-est">
<strong>Rough effort (order-of-magnitude):</strong>
<ul>
<li><strong>DEV — Microservices</strong> (6 services): ~<strong>50</strong> dev MD</li>
<li><strong>DEV — ETL</strong> (all ETL adjustment): ~<strong>55</strong> dev MD</li>
<li><strong>E2E test</strong> (CI/CD): ~<strong>20</strong> tester MD + ~<strong>10</strong> dev MD</li>
<li><strong>Deployment</strong> (data migration): ~<strong>5</strong> dev MD</li>
<li><strong>Totals:</strong> ~<strong>20</strong> tester MD · ~<strong>120</strong> dev MD</li>
</ul>
</div>
</div>
</div>

---

<!-- _class: diagram-slide -->

## Proposed Due Diligence Study

*Scenario-based target view on Alibaba Cloud — separate scenarios instead of forcing one engine stack to do every job.*

![center w:1000](design/diagram_scenario_based_target_alibaba.png)

---

## Guiding Principles of Max Yang (based on above CDH plan)

**Bottom line:** *not* "move everything from Azure to Ali."

- Keep **Azure 9DL** as the **primary enterprise lakehouse** and **governance center**
- Add a **lean, bounded** Ali-side capability for CDP-local / Ali-native workloads
- Move **selected** CDP components to Ali-native managed services
- **Do not build a second enterprise data lake** on Ali
- Keep **CDH** for now, under security waiver — not replaced in this phase

**Guiding principle:** *workload decentralization, governance centralization.*

**What stays Azure-led (guardrails)**
9DL as primary lakehouse · centralized governance · enterprise BI / reporting · metric & KPI consistency · Ali is an **extension**, not a peer enterprise platform.

---

<!-- _class: diagram-slide -->

## Overall Architecture

*CDP overall architecture proposal — AliCloud (CDP MA, DataHub, lean Ali data port) + Azure (main lakehouse / BI); legend: green = new, yellow = to-change, white = no-change.*

![center w:1050](design/diagram_cdp_overall_architecture_proposal.png)

---

## Change Map — Four Domains at a Glance

| # | Domain | Summary of change |
|---|--------|-------------------|
| **A** | **CDP runtime middleware** | VM-based components → Ali **managed services** |
| **B** | **CDP data processing (Ali side)** | Azure tooling → **Ali-native** data path |
| **C** | **Azure 9DL (parallel)** | **Modernize** lakehouse — not freeze |
| **D** | **CDH disposition** | **Keep** under waiver; defer full replacement |

**Cross-cutting placement rule**
If data is **sourced from Ali** and **only used by CDP**, it is processed **on Ali only** — the corresponding ETL jobs are removed from Azure.

---

<!-- _class: domains-slide -->

## Domains A & B — Ali-Side CDP Changes

<p class="domains-section-title">A) Runtime middleware → Alibaba managed services</p>

| Current | Target (Alibaba) |
|---------|------------------|
| MongoDB VM | Aliyun MongoDB |
| ElasticSearch VM | Shared ES |
| Kafka VM | Serverless Kafka |
| Azure Storage Account | OSS |
| — | PE custom pipeline adjustment |

<p class="domains-section-title">B) CDP data processing → Alibaba-native path</p>

| Current (Azure) | Target (Alibaba) |
|-----------------|------------------|
| Databricks | EMR Serverless Spark |
| Storage Account | OSS / OSS-HDFS |
| Data Factory | DataWorks |
| — | **New:** Flink + Fluss · Hive Metastore · Hologres |

<p class="domains-after-tables">Plus <strong>cross-cloud orchestration &amp; integration</strong> between Azure and Alibaba for workloads that stay Azure-centered.</p>

---

<!-- _class: domains-slide -->

## Domains C & D — Azure Modernization + CDH Disposition

<p class="domains-section-title">C) Azure 9DL — modernize in parallel (not frozen)</p>

<ul class="domains-list">
<li>Enable <strong>Unity Catalog</strong></li>
<li>Complete <strong>N3 migration</strong></li>
<li>Adopt <strong>Iceberg</strong> as the standard table format</li>
<li>Direct integration with <strong>CDL</strong></li>
<li>Decommission SQL Server → use <strong>ADB SQL Warehouse</strong> as report DB</li>
<li>Move toward <strong>Power BI semantic models</strong> and governed datasets</li>
</ul>

<p class="domains-section-title">D) CDH — no replacement in this phase</p>

<ul class="domains-list">
<li><strong>Keep CDH</strong> under a security <strong>waiver / transitional stance</strong></li>
<li>Avoid destabilizing the enterprise center to chase CDH replacement now</li>
<li>Scenario-based future mapping — see <strong>Proposed Due Diligence Study</strong> slide (<strong>reference only</strong> for this phase)</li>
</ul>

<p class="domains-callout"><strong>Reporting back-flow:</strong> If BI needs CDP-computed data, <strong>daily sync Alibaba → Azure</strong>. <strong>Gold / Serving layer only.</strong> Copy-as-delivery.</p>

---

## Next Steps & Open Floor

**Now — your turn**

Questions, concerns, and early flags welcome. Anything that already looks risky or ambiguous from an infra standpoint, please raise it so we can factor it into the migration plan.
