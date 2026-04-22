Below is the As-Is, datalake-centered big picture for CDP-related data flows, using the two design docs as the primary source and the monitoring deck as a cross-check for the actual runtime patterns seen in operations. The core design intent is that 9DL is the central consumer data lake, ingesting data from multiple upstream systems, curating it, and serving downstream consumers such as CDP, China BI, and later CRM.  ￼  ￼

1) Executive view

At the highest level, the estate is not just “a data lake.” It is really three layers:

1. Source & ingestion
    * business systems and external sources send data as API/BLOB/file, DB extracts, or streaming events
    * 9DL ingests them mainly through Blob / Event Hub / ADF / SHIR.  ￼  ￼
2. Central lake processing
    * ADLS is the persistent lake store
    * Databricks does transform / cleanse / aggregate into curated datasets
    * the 9DL doc explicitly frames this as turning raw data into structures such as ODS, datastore, and data mart for consumers.  ￼
3. Consumption / downstream application
    * direct consumers include CDP, China BI, and future CRM
    * in practice, there is also a 9RR warehouse / SSIS / Talend / H5 / Power BI delivery chain that sits downstream of or alongside the lake for reporting and digital use cases. The monitoring deck makes that operationally visible.  ￼  ￼

2) Big-picture architecture

flowchart LR
    subgraph Sources["Source systems / touchpoints"]
        OMS[OMS]
        CRMDP[CRMDP]
        SNX[SNX CRM / SNX DB]
        MARS[MARS]
        DMP[DMP]
        Camp[Campaign tracking]
        Ads[Ads tracking]
        Other[Files / API / DB / real-time events]
        CDPsrc[CDP as source]
    end
    subgraph Ingestion["9DL ingestion layer"]
        Blob[Azure Blob / Storage Account]
        EH[Azure Event Hub]
        SHIR[Self-hosted Integration Runtime]
        ADF[Azure Data Factory]
    end
    subgraph Lake["9DL core lake"]
        ADLS[ADLS Gen2]
        DBX[Azure Databricks]
        Curated[ODS / Datastore / Data Mart]
    end
    subgraph Consumers["Consumers / downstream serving"]
        CDP[9CD / CDP]
        BI[China BI / Power BI]
        CRM[CRM future]
        RR[9RR Data Warehouse]
    end
    OMS --> Blob
    CRMDP --> Blob
    MARS --> Blob
    DMP --> Blob
    Camp --> Blob
    Ads --> Blob
    Other --> Blob
    Other --> EH
    CDPsrc --> Blob
    CDPsrc --> EH
    SNX --> SHIR --> ADF
    Blob --> ADF
    EH --> ADF
    ADF --> ADLS
    ADLS --> DBX
    DBX --> Curated
    Curated --> CDP
    Curated --> BI
    Curated --> CRM
    Curated --> RR

This diagram is a synthesis of the 9DL design: the document explicitly separates data source area, data process area, and data serve area, with blob / event hub → ADF → ADLS → Databricks → consumers as the core path.  ￼

3) What 9DL is supposed to do

The 9DL document is clear on the intent:

* consolidate structured + unstructured, timely + non-timely, behavior / engagement / event, and analysis / dimension data
* batch data lands mainly through blob
* streaming lands through event hub
* RDBMS data is extracted through ADF + self-hosted integration runtime
* CDP can access the data “on the lake,” and the lake should support computation needed for CDP processing.  ￼  ￼

That means 9DL is not just a passive store. It is the central ingestion and curation platform for consumer data.

4) How 9CD / CDP fits into that picture

The 9CD design shows that CDP itself is a fairly rich application/data platform with:

* microservices on CaaS
* Kafka
* CDH stack for data processing/query
* MongoDB, MySQL, Redis, ElasticSearch
* PowerBI Gateway
* services such as collectorentry, customer, etlv2, hadoopdts, cdhadapter, queryhub, data-extractor, etc.  ￼  ￼

Critically, the 9CD doc also says 9CD/CDH needs access to 9DL ADLS, using service principal-based access. It explicitly notes that ADLS in 9DL acts as a persistent storage layer that CDH can use as secondary storage.  ￼

So the practical relationship is:

* 9DL = central data lake and curated data platform
* 9CD = consumer-facing application/data platform that both feeds data into and consumes data from the lake
* CDH inside 9CD remains an important internal compute/store/query component in the as-is landscape

5) Datalake-centered CDP-relevant flows

The clearest way to read the as-is estate is as a few recurring flow families.

Flow A: source systems into 9DL for central curation

This is the canonical design flow.

flowchart LR
    S[Source systems / API / files / DB / tracking] --> B[Blob or Event Hub]
    DB[Private DBs] --> SHIR[SHIR]
    SHIR --> ADF[ADF]
    B --> ADF
    ADF --> ADLS[ADLS]
    ADLS --> DBX[Databricks]
    DBX --> C[Curated datasets]
    C --> CDP[CDP]
    C --> BI[China BI]
    C --> CRM[CRM future]

This is directly aligned with 9DL’s architecture text.  ￼

Flow B: CDP behavioral / operational events into CDP internals, then into big-data stores, then linked back to 9DL

The 9CD feature mapping shows examples such as:

* events captured from channels
* events sent to Kafka
* automation engine updates MongoDB
* statistics written to Kudu
* tagging / segmentation jobs use Spark + HBase + HDFS + MySQL + Redis.  ￼

A simplified view:

flowchart LR
    Touch[Wechat / mini-program / landing page / app / campaign events] --> MS[9CD microservices]
    MS --> K[Kafka]
    K --> CDH[CDH / Spark / HDFS / HBase / Kudu]
    MS --> MySQL[MySQL]
    MS --> Mongo[MongoDB]
    MS --> Redis[Redis]
    CDH --> Query[Query / customer / segment / tag services]
    Query --> Ops[Campaigns / journeys / dynamic content]
    CDH -. read/write integration .- ADLS[9DL ADLS]

This is not a full “lake-first” path. It shows that in the as-is world, CDP has its own data-processing center of gravity as well, with 9DL as a central but not exclusive data platform.

Flow C: 9DL to reporting and digital delivery

The monitoring deck makes the downstream reporting chain concrete. In operations, the lake often does not terminate directly in BI. There are intermediate hops.

flowchart LR
    Source[Source] --> ADF[ADF / Databricks]
    ADF --> DL[9DL Datalake]
    DL --> RR[9RR Data Warehouse]
    RR --> SSIS[SSIS / Procedures]
    SSIS --> Talend[Talend]
    Talend --> H5[H5 Tomcat / DCP]
    RR --> PBI[Power BI]
    DL --> PBI

This composite path is consistent with the six patterns in the monitoring deck.  ￼

6) The six actual runtime patterns seen in the monitoring deck

The deck is useful because it reveals the real operational shapes, not just the intended logical model.

Pattern 1

Source → Kafka → 9DL → Power BI.  ￼

Pattern 2

Source → API/BLOB → Data Factory + Databricks → 9DL → Power BI.  ￼

Pattern 3

Source → API/BLOB → SSIS + Procedures → 9RR Datawarehouse → Power BI.  ￼

Pattern 4

Source → API/BLOB → SSIS + Procedures → 9RR Datawarehouse → Talend → H5 Tomcat.  ￼

Pattern 5

Source → API/BLOB → Data Factory + Databricks → 9DL → BLOB → 9RR → Talend → H5 Tomcat → Power BI.  ￼

Pattern 6

Pattern 5 plus SSIS and procedures-in-ADF.  ￼

This is the important correction to any oversimplified architecture slide: the as-is estate is not just “source → lake → BI.” It is a mixed lake + warehouse + app-serving chain.

7) My recommended big-picture reading of the As-Is

The cleanest mental model is this:

flowchart TB
    subgraph Upstream["Upstream / capture"]
        U1[Business systems]
        U2[External platforms]
        U3[Tracking / campaign / ads]
        U4[CDP channels]
    end
    subgraph Core1["9DL central data platform"]
        I1[Blob / Event Hub / SHIR / ADF]
        I2[ADLS]
        I3[Databricks]
        I4[Curated data]
    end
    subgraph Core2["9CD application data platform"]
        C1[Microservices on CaaS]
        C2[Kafka]
        C3[CDH]
        C4[MySQL / Mongo / Redis / ES]
    end
    subgraph Serving["Serving / reporting"]
        S1[9RR Warehouse]
        S2[SSIS / Procedures]
        S3[Talend]
        S4[H5 Tomcat]
        S5[Power BI / China BI]
    end
    Upstream --> Core1
    Upstream --> Core2
    Core1 <--> Core2
    Core1 --> Serving
    Core2 --> Serving

That is the least misleading representation.

8) Key architectural conclusions

First, 9DL is the central consumer-data lake, but not the only place where data transformation and serving logic exists. The 9CD platform retains substantial internal processing and storage responsibilities.  ￼  ￼

Second, CDP is both upstream and downstream of the lake. The 9DL system context explicitly says CDP is both a data source and a data consumer of the lake.  ￼

Third, the actual downstream delivery path often includes 9RR, SSIS, Talend, H5, and Power BI, so the business-visible “CDP data flow” is broader than the 9DL diagram alone suggests.  ￼

Fourth, the monitoring deck indirectly confirms that these multi-hop flows are real, because the observed operational issues are exactly the kind you get in a hybrid lake + warehouse + report chain rather than a single clean lakehouse.  ￼

9) Bottom line

If I had to summarize the As-Is in one sentence:

9DL is the central Azure consumer data lake for ingestion, storage, and curation; 9CD is a parallel application/data platform that both feeds and consumes the lake; and business-facing delivery often continues through 9RR/SSIS/Talend/H5/Power BI rather than stopping at the lake boundary.  ￼  ￼  ￼

I can next turn this into either a cleaner single-slide architecture view or a table mapping each flow to its involved components and main purpose.