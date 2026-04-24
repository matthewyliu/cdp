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
    width: 100%;
    max-height: 400px;
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
  /* Due diligence slide: scenario-based Alibaba target diagram */
  section.diligence-slide {
    font-size: 18px;
    line-height: 1.25;
  }
  section.diligence-slide h2 {
    margin-bottom: 0.15em;
    padding-bottom: 3px;
  }
  section.diligence-slide > p:first-of-type {
    font-size: 15px;
    color: #4b5563;
    margin: 0 0 0.3em 0;
  }
  section.diligence-slide img {
    display: block;
    margin: 0 auto;
    max-height: 430px;
    max-width: 100%;
    object-fit: contain;
  }
  /* Overall architecture proposal slide (Ali + Azure diagram) */
  section.overall-arch-slide {
    font-size: 18px;
    line-height: 1.25;
  }
  section.overall-arch-slide h2 {
    margin-bottom: 0.12em;
    padding-bottom: 3px;
  }
  section.overall-arch-slide > p:first-of-type {
    font-size: 15px;
    color: #4b5563;
    margin: 0 0 0.25em 0;
  }
  section.overall-arch-slide img {
    display: block;
    margin: 0 auto;
    max-height: 410px;
    max-width: 100%;
    object-fit: contain;
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

<!-- _class: asis-hybrid -->

## As-Is Reality — Hybrid Chain

The real estate today is a **hybrid lake + warehouse + app-serving chain** with multiple delivery paths.

- **9DL ↔ 9CD is bidirectional.** 9CD is both a source and a consumer of the lake; 9CD/CDH reads 9DL ADLS via service principal (ADLS = secondary storage for CDH).
- **9CD has its own data gravity.** Substantial processing happens inside 9CD — Kafka, CDH (Spark / HDFS / HBase / Kudu), MySQL, MongoDB, Redis, ElasticSearch — not always lake-first.
- **Parallel reporting chain** exists alongside the lake: **9RR Data Warehouse · SSIS · Talend · H5 Tomcat · Power BI**.
- **Six runtime patterns** observed in operations (from monitoring), ranging from `Source → Kafka → 9DL → Power BI` to `Source → ADF/Databricks → 9DL → 9RR → Talend → H5 → Power BI`.

<p class="asis-impl"><strong>Infra implication:</strong> scope spans <strong>9DL ↔ 9CD ↔ 9RR / reporting</strong> — not a single lift of the lake.</p>

<div class="asis-diagram-wrap">
<img src="design/diagram_asis_hybrid_chain.png" alt="As-is monitoring view: Source, Datalake and warehouse, Reports, and numbered scenarios" />
<p class="asis-diagram-caption">As-is (monitoring): Source → Datalake &amp; warehouse (ADF, Kafka, storage, SSIS/SQL) → Reports (Talend, H5, PBI) — numbered scenarios on the right.</p>
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

<!-- _class: diligence-slide -->

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

<!-- _class: overall-arch-slide -->

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
