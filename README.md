# dataplatform

 DataHub Reference Architecture
This reference architecture for DataHub Platform shows an end-to-end stream processing pipeline. This type of pipeline has four stages: ingest (Events), process (Transform, Aggregate and Enrich), store (Store Materialized Views), and analysis/reporting (Access patterns).

For this reference architecture, the pipeline ingests data from three sources typical databases with CDC enabled, performs a join on related records from each stream, enriches the result, and calculates an average in real time. The results are stored for further analysis.



Streaming Data Pipeline Reference Architecture
<< Insert Image>>


Architecture Components
The architecture consists of the following components.

Data sources/System of Records: The data sources are a real application that generate events or updates to the Database and generate CDC Events

Ingestion: Data Ingestion is a process where event data is streamed into Kafka Topics using CDC or collectors to get data into Stream Platform.

Stream Processing: Transform, Aggregate and Enriching data based on the Standardization, Core standardized data streams are made up of SoR entities that have been CDC’d, grouped, and standardized into canonical format. They MUST contain ONLY the SoR data that comprise a single entity. Any references to other entities must be by pointer. 
For example an Site Informaton would be a pointer from the Employee entity to the Site Information Entity.

Materialized Views:

Standard data streams are sequential access only and are therefore have limited use cases for querying the data inside them. To make the data access performant, resilient, and cost effective, three primary categories of materialized views are utilized.

- Specific Request/Response Access: API

- Reactive Access: Stream

- Reporting Access: Analytic
Access Patterns
API
When the types of queries are well known, low latency and high availability are prioritized, access is to a small number of records (<1000), and happen in response to some event then API query/response pattern is appropriate.

APIs are divided into three three categories

Core (All)
Foundation (3+)
Ecosystem (1-2)
An API belongs to the core category if all consumers of that type of data must go use it. It is foundation if three or more consumers use it, and it is considered an ecosystem API if less than three consumers use it.

Reactive
For event driven access or large scale data replication the reactive access pattern fits the bill. This is implemented using a stream which represents an in-order series of records. In either pattern, the stream is filtered down to the right records and attributes based on the use case. The stream is then made available to reactive consumers or periodically written into a file for legacy file based integrations.

Just like APIs, streams come in three flavors: core, foundation, and ecosystem based on targeted consumers.

Analytic
Many views can be used for ad-hoc reporting, analytic, and machine learning / AI access. Hadoop parquet files, graph databases, and in memory grids are just some examples of ways you might need to layout the data for specific use cases.
