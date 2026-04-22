I read the two PPTX files together, treating Target Datalake 20260302.pptx as the newer steering view and cdp_migration 2_20260420.pptx as the earlier migration-study / estimation view. They are aligned at a high level, but the newer datalake deck makes one important correction: it narrows the Ali target and explicitly protects Azure 9DL as the primary enterprise center.  ￼  ￼

Bottom line

The proposed target is not “move the whole data platform from Azure to Ali.”
It is:

* Keep Azure 9DL as the main enterprise lakehouse and governance center
* Add a lean Ali-side data capability only for CDP-local / Ali-native workloads
* Move selected CDP processing and platform components to Ali-native services
* Avoid building a second full enterprise data lake on Ali
* Keep CDH for now, despite its obsolescence, under a waiver / transitional stance.  ￼  ￼  ￼

What is proposed to change

1) CDP-side runtime components move from self-hosted / Azure-VM style to Ali-native managed services

The newer datalake deck explicitly says the CDP application upgrade includes:

* MongoDB VM → Aliyun MongoDB
* ES VM → Shared ES
* Kafka VM → Serverless Kafka
* Azure storage account → OSS
* plus a PE custom pipeline adjustment.  ￼

This is broadly consistent with the migration deck’s “Option B” direction, which also proposed:

* MongoDB VM → PaaS
* ES VM → PaaS
* Kafka VM → PaaS
* Azure storage account → OSS.  ￼

So at the application/platform layer, the direction is clear:
replace VM-heavy supporting components with Ali managed services where practical.  ￼  ￼

2) CDP data processing for the Ali side moves from Azure tooling to Ali tooling

The newer deck explicitly calls out the data solution upgrade as:

* Databricks → EMR Serverless Spark
* Storage Account → OSS
* Data Factory → Dataworks
* with cross-cloud orchestration & integration.  ￼

And the target architecture adds Ali-side components such as:

* Dataworks
* OSS / OSS-HDFS
* EMR Serverless Spark
* Flink + Fluss
* Hive Metastore
* Hologres.  ￼  ￼

So the data-plane change is:
CDP-local ingestion, ETL, and serving gain an Ali-native processing path.  ￼  ￼

3) Consumer/CDP workloads are intended to be placed on Ali when they are Ali-sourced and Ali-used

The design principles in the newer deck say:

* if data is sourced from Ali and only used by CDP, it should be processed only on Ali
* for Consumer/CDP data, corresponding ETL jobs should be removed from Azure to Ali-only.  ￼  ￼

That is a substantive workload-placement change. It means:
the consumer/CDP domain is being pushed closer to Ali-native systems, but within a bounded scope.  ￼

4) Azure 9DL itself is still being modernized

The newer deck also proposes Azure-side enhancement, not just Ali-side migration:

* Enable Unity Catalog
* Complete N3 migration
* Adopt Iceberg as standard
* Integrate with CDL directly
* Decommission SQL Server and use ADB SQL Warehouse as report DB
* later move toward Power BI semantic models and governed datasets.  ￼

So “no change” does not mean Azure is frozen.
It means Azure remains the main center, while being modernized in parallel.  ￼

What is proposed to not change

1) Azure 9DL remains the primary enterprise data lake / lakehouse

This is the clearest message in the newer deck:

* “keeping Azure 9DL unchanged as the primary enterprise lakehouse”  ￼
* “Azure as the primary lakehouse and governance platform”  ￼
* “Keep Azure 9DL as the enterprise data lake center”  ￼

So the main non-change is:
the enterprise center of gravity stays on Azure.  ￼

2) The initiative is not meant to create a second enterprise lake on Ali

The newer deck says the Ali side should be:

* “a constrained domain platform, not a second enterprise lake”
* “a single-center lakehouse with a bounded Ali extension”.  ￼

That is a deliberate correction to the more open-ended feeling in the earlier migration study, where the CDH replacement analysis could be read as broader Ali re-platforming. The newer deck tightens the scope:
Ali is an extension, not a peer enterprise platform.  ￼  ￼

3) Centralized governance remains Azure-led

The newer deck repeatedly emphasizes:

* centralized governance
* governance and KPI consistency can be centralized
* the challenge is avoiding metric fragmentation and split access control across clouds.  ￼  ￼

So governance is not being decentralized to Ali.
Instead, the plan is:
workload decentralization, governance centralization.  ￼

4) BI/reporting still remains Azure-centered by default

The newer deck says:

* if BI/reports still need CDP-returned data, sync it daily from Ali back to Azure
* use copy-as-delivery
* sync only Gold/Serving layer by default.  ￼  ￼

So reporting is not being primarily relocated to Ali.
The default assumption is:
Ali computes local consumer/CDP outputs; Azure remains the broader reporting and governed serving center.  ￼

The most important correction from the newer datalake deck

The earlier migration deck spends more energy on CDH replacement study and compares:

* Kudu/Impala → StarRocks
* Spark → Serverless Spark
* Azkaban → DataWorks
* Hive → DLF
* HDFS → OSS HDFS
* HBase → Ali HBase,
    while noting a decision point between:
* Option A: modernize to new architecture
* Option B: keep CDH.  ￼  ￼

The newer datalake deck reframes that significantly:

* Keep CDH & apply security waiver
* use Lean Ali Data port (CDP scope) + Single Main Center on Azure.  ￼

That is the big update.

So the newer position is not:
“replace CDH immediately with a fully modern Ali data architecture.”

It is:
“for this migration phase, keep CDH, modernize selected components, add a lean Ali data path, and do not destabilize the enterprise center.”  ￼

Clean summary

Proposed changes

* CDP supporting middleware becomes more Ali managed-service based
* CDP-local data processing gets an Ali-native ETL/storage path
* Consumer/CDP ETL that is Ali-sourced and Ali-used shifts to Ali-only
* Azure-side lakehouse is also modernized further
* cross-cloud orchestration and selective delivery back to Azure are introduced.  ￼  ￼  ￼

Proposed non-changes

* Azure 9DL remains the primary enterprise lakehouse
* Azure remains the governance anchor
* Ali is not a second enterprise lake
* enterprise reporting / governed serving remains Azure-led
* CDH is kept for now rather than fully replaced in this phase.  ￼  ￼



