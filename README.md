# Azure DP 900 Notları
## Azure Data Fundamentals: Explore core data concepts
- Type: structured, semi-structured, or unstructured.
- Data stores : File stores ,Databases
- file Formats :
	-  Delimited text files
	-  JavaScript Object Notation (JSON) 
	- Extensible Markup Language (XML)
- Optimized File Format
    - Avro:  is a row-based format. It was created by Apache
    - ORC (Optimized Row Columnar format):  organizes data into columns developed by HortonWorks for  Apache Hive
    - Parquet is another columnar data format. It was created by Cloudera and Twitter very efficient compression and encoding schemes.
-databases
    - Relational databases
        - tables that represent entities
        - entity is assigned a primary key that uniquely identifies it
        - keys = Normalization = Remove Dups 
        - use SQL
    - Non-relational databases
        - Key-value databases
        - Document databases (JSON)
        - Column family databases (key , Columns )
        - Graph databases,
- Transactional data processing
    - specific events organization wants to track
    - Used in Money / Goods / services
    - The work performed by transactional systems  is Online Transactional Processing (OLTP).
    -  DB  optimized are both read and write operations
    - CRUD operation 
    - OLTP systems shd enforce ACID (Atomicity(entire transction happens at once or nothing happens),Consistency,Isolation,Durability (persisted)
- analytical data processing
    - read-mostly
    - files / OLTP > datalake > ETL > Warehouse-OLAP (Facts and Dim) > Analytics 
- Data lakes
    - file-based data must be collected and analyzed.
- Data warehouses 
    - relational schema 
    - read operations
    - Uses denormalizationfor performance ( Star Scheme)
- Key job roles 
    - Database administrators - manage databases,  permissions,  backup  ,policies
    - Data engineers - data integration, data cleaning routines,governance rules, and  pipelines
    - Data analysts -create visualizations 
    - Data scientists -  Build Model 
## Microsoft Azure Data Fundamentals: Explore relational data in Azure
### Explore fundamental relational data concepts
- collections of entities from the real world as table
- entity =record of information ie., objects and events
- Relational tables = structured data ie.,  each row in a table has the same columns
- Normalization 
    - Separate each entity into its own -TABLE.
    - Separate each discrete attribute into its own -COLUMN.
    - Uniquely identify each entity row using a -PRIMARY KEY.
    - FOREIGN KEY columns to link related entities.
    - Types:
        - 1st Normal Form (1NF): Make all cols only 1 value
        - 2nd Normal Form (2NF): Remove duplicates, create Foreign Key
        - 3rd Normal Form (3NF): move cols out of the tables which are not depending on primary key
- SQL (Structured Query Language)
    -  communicate with a relational database.        
- Type of SQl Language 
    - Transact-SQL :Microsoft SQL Server and Azure SQL services.
    - pgSQL- PostgreSQL.
    - PL/SQL- Oracle.
- Statement types
    - DDL (Data Definition Language) ie.,create,alter,rename,drop (dangerous)
    - DML (Data Manipluation) ie., select,insert,update ,delete
    - DCL (Data Control) ie., Grant,deny,revoke
    - TCL (Transaction control) ie., rollback
- Columns marked as NOT NULL are referred to as mandatory columns
- Views
    - virtual table
    - It is used to save a complex query and complex tables

   
		    CREATE VIEW Deliveries AS 
		    SELECT o.OrderDate,c.FirstName 
		    FROM Order AS o JOIN Customer AS c ON o.CustomerID = c.ID;

		    SELECT OrderDate, FirstName FROM Deliveries
	    
- Stored Procedure
    - SQL code that you can save, so the code can be reused

	        CREATE PROCEDURE procedure_name2
	        @ProductID INT
	        AS
	        SELECT * FROM SalesLT.Product where ProductID=@ProductID
	        GO;
	        EXEC procedure_name2 680;

- Index
    -  index =  index at the back of a book.
    -  database management system use index to fetch data quickly 
    - Primary key will have index hence faster
    - table can have > 1 indexes
    - Index = 1 or more cols
    - insert, update, or delete data , indexes table must be changed
    - 2 types of Indexes:
        - Clustered - Primary Key of a table
            - Table can have only 1 clustered index
            - Data is stored in the order of index 

        - non clustered - Created Seperatly
            - Index stored separatly with pointers 
            - create nonclustered index index_name on table (col_name);
    -Eg :
    CREATE INDEX idx_ProductName
    ON Product(Name);
- Unnormalized 
    - Data duplication exists
    - Because of Duplication it is hard to change data
    - not Recommended

### relational database services in Azure
- Azure SQL VM (IAAS) - Fully compatible with on-premises 
- Azure Managed Services (PAAS)
    - Azure SQL Database 
    - Azure SQL Managed Instance 
    - Azure Database open-source ie., My SQL, MariaDB,PostgreSQL 
- Azure SQL Edge (IOT)

#### Azure VM - IAAS
- virtual machine with installation of SQL Server
- Self Administered (OS , Updates etc., )
- "lift and shift" migration of existing on-premises
- Full Control - Mem ,CPU etc
#### Azure SQL VM Installation
- Search for "Virtual Machine" in portal
- New > Select images (SQL)
- U can ssh to virtualMachine in Cloudshell
or
- Search box "Azure SQL" 
- Under "SQL virtual machines"> select  "Free SQL Server Server 2019 Ubuntu " 
- Subscripption= Free, egion =Free,Image = Free ,Size = Least
- name = my-sql-server-vm
- create
- Save certificate to a folder when asked 
- Passed
- To connect to server from local  : ck on to resources page > settings >click on Connect 
#### Azure SQL Managed Instance
- PAAS
- All features of SQL server + Extra features
- Recommended in migration from on-prem
- Cross Database queries
- send emails
- SQL server Agents Eg: run jobs
- Virtual network (only for vCore)
- Supports Analysis , Reporting 
- Access to SQL Server Agent , Database Mail
- Linked servers, Service Broker 
#### Azure SQL Database
- platform as a service (PaaS)
- High availability
- Automatic Updates 
- Autobackups
- Serverless
- Flexible
- Auto Encryption( TDE)
- Authentication 
- Read Replica DB can be created ( for reporting against reporting Db)
- low Cost
- isn't fully compatible with on-premises SQL
- types : 
    - Single Database 
        - Default
         - charged per hour for the resources
        - Serverless 
            - shared by databases belonging to other Azure subscribers
            - automatically scales
    - Elastic Pool 
        - multiple databases can share the same resources
        - multiple-tenancy
        - For databases with resource requirements that vary over time, and can help you to reduce costs
- testdeepak/deepak/test-123 , SELECT * FROM SalesLT.Product;
#### Other DB ( all are almost same )
-  enable organizations  to move to Azure
- mySQL (oracle) : LAMP apps ie., linux  ,Apache, MySQL, and PHP
- Maria DB: Fork of MySQL
- Postgres ( uses pgsql , support custom datatype,manipulate geometric data)
- Types
    - Single Server :Basic, General Purpose, and Memory Optimized
    - Flexible Server :more control and server customizations,better cost optimization
    - Hyperscale :database is split across nodes. Data is split into chunks based on the value of a partition key or sharding key
- ports :
	- SQL - 1433
	- MYSQL = 3306
	- Postgrs = 5432
- Security
	- Transparent data encryption (TDE)- encrypting data at rest.
	- Transport Layer Security (TLS) to encrypt data that is transmitted across a network
	- Dynamic data masking (DDM) limits sensitive data exposure by masking it to non-privileged users. 


## Explore non-relational data in Azure

### Explore Azure Storage
- Azure Blob (Binary large objects Storage)
    - store massive amounts of unstructured data as binary large objects, or blobs
    - Uses container
    - can read and write blobs inside a container
    - virtual folders simialr to file system
    - types : Block , Page , Append
        - Block (100 MB) = Max of 50k Blocks = 4.7 TB
        - Page = Into Pages , Fast Read and Write , Max 8 TB
        - Append = Used for append operation ie.,logs . 4MB - 195 GB
    - 3 Access 
        - hot = high performance
        - cold = low performance , less charges
        - Archive = lowest storage cost  , long time to access data
- Azure DataLake Storage Gen2
    - newer ver of Gen1
    - Advantages = blob storage , cost-control of storage tiers, hierarchical namespace , analytics 
    - analytical data lakes
    - Integrate with Azure HDInsight, Azure Databricks, and Azure Synapse Analytics 
    - Data Lake Storage Gen2 = Azure Storage + hierarchical namespace checkbox (Under Advanced)
    - hierarchical namespace = Folder operations (rename , delete , copy etc.,)
    - By creating the storage account, or you can upgrade an existing Azure Storage account to support Data Lake Gen2
    - After Upgrading you can’t revert it to a flat namespace.
- Azure Files (File Share)
    - 100 TB of data in a single storage account.
    - maximum size of a single file is 1 TB
    - 2000 Concurrent operations
    - upload files using Azure portal, or  AzCopy utility.
    -  Azure File Sync service to synchronize local copy
    - 2 Types:
        - Standard :hard disk-based hardware in a datacenter,
        - Premium :uses solid-state disks , greater throughput
    - 2 file sharing protocols
        - Server Message Block (SMB) : used in all OS
        - Network File System (NFS) : Only in some mac and linux (Premium)
- Azure Table (No SQL , prefer cosmos instead)
  - Row = Key , Value 
  - each row holding the entire data for a logical entity
  - must have a unique key 
  - no concept of foreign keys, relationships, stored procedures, views,
  - denormalized
  - The number of fields in each row can be different
  - Partition Key 
	 - used to group related data 
	 - rows with same partition key are stored together
	 - They are independent in size
	 - Items in the same partition are stored in row key order.
	 - used for faster search and range queries  fetch contiguous block of rows
        
    - Ex

			+------+---------+------------+-----------+------------------+
			| Pkey | RowKey  | TimeStamp  | Property1 | Property2        |
			+------+---------+------------+-----------+------------------+
			| 1    | unique1 | 2022-01-01 | Deepak    | Bangalore, India |
			+------+---------+------------+-----------+------------------+
			| 2    | unique2 | 2022-01-01 | John      |                  |
			+------+---------+------------+-----------+------------------+
			| 2    | unique3 | 2022-01-01 |           | Newyork,India    |
			+------+---------+------------+-----------+------------------+
 

### Cosmos DB
- NoSQL DB
- Horz scaling ,High scalability
- Use Api to query Data
- no administraton
- Auto Scale (no limit)
- All features similar to SQL Server
- Can use SQL language to Query NoSQL data
- multi-region writes for globally distributed user local replica
- Creation:Account > DB > Container >item
Note :Seperate account is needed for each
- testdeepak/deepak/test-123 , SELECT * FROM SalesLT.Product;

#### Cosmos DB APIs
- Documents : 
    - Types : 
        - Core SQL  : JSON , SQL syntx
        -  Mongo (Binary JSON - BSON )
    - Ex: Person(name ,Address()).In RDBMS address will be seperate table
    - Core SQL :DB > Container > Item
    - Mongo : DB >Collection >Doc
- Table API
    - greater scalability and performance than Azure Table Storage.
    - Stucture similar to Azure Table
    - GET - https://endpoint/Customers(PartitionKey='1',RowKey='124')
- Column (Cassandra) 
    - rows and columns
    - Has 1 Primary Key Column
    - Other columns are grouped  as 1 column 
    - Eg:   (Pk=1 ,col2=(name="deepak",ph="123 )), 
            (Pk=2 ,col2=(name="ABC",email="abc@gmail" ))
    - compatible with Apache Cassandra,
    - not mandatory for every row to have the same columns.
    - KeySpace > Table >Row
    - SQL to Query (SELECT * FROM Employees WHERE ID = 2)
- Key Val :Map or Dict
- Gremlin (graph)
    - used to store complex relationship
    - Uses nodes and edges
    - Eg:Organization Charts 
    - Azure Cosmos , Gremlin
    - DB > Garph > Node , Edge

## Microsoft Azure Data Fundamentals: Explore data analytics in Azure
### Explore fundamentals of modern data warehousing
- Data ingestion pipelines
    - Data ingestion and processing -ETL,ELT
    - Analytical data store  - data warehouses, file-system based data lakes, and hybrid architectures
    - Analytical data model - cube , Facts and Dim ,Star Scheme
    - Data visualisation  -comparisons, dashboards , and key performance indicators (KPIs),reports
- Data ingestion pipelines
    -  Azure Data Factory or  Azure Synapse Analytics
    -  one or more activities 
    - Activities =  data flow that incrementally manipulates the data until an output dataset is produced.
    - Pipelines consist of one or more activities (built-in activities, linked service )
    - Eg : Azure Blob Store linked service to ingest the input dataset,
             Azure SQL Database to run a stored procedure,
            Run task on Azure Databricks or Azure HDInsight, or apply custom logic using an Azure Function.
- Data warehouse 
    - relational database ie ., stored in a schema
    - optimized for data analytics rather than transactional
    - denormalised into a schema
    - Facts and Dim
- Data lake
	- tabular schemas on semi-structured data files 
	- structured, semi-structured, and even unstructured data
- Hybrid approaches 
    - Used in Spark 
    -  data lakes and data warehouses in a lake database or data lakehouse.
    -  stored as files in a data lake > expose them as tables (templates ie., struct) >  queried using SQL using  SQL pools (Azure Synapse Analytics )
    - PolyBase :  query external tables 
- Azure services for analytical stores
    - Azure Synapse Analytics
        - unified data analytics solution
        - single service interface for multiple analytical capabilities
        - Pipelines similar  to Azure Data Factory.
        - Use SQL , Datawarehouse
        - Apache Spark 
        - Azure Synapse Data Explorer - data analytics using Kusto Query Language (KQL).
        - Not Support data Extraction from Multiple sources (use Datafactory)
        - MPP - Massive Parallel Process  - Computer nodes
    - Azure Databricks
        - Apache Spark data processing platform with SQL database semantics
        - notebook to query 
        - visualize data in web-based interface.
        - Multiple sources
    - Azure HDInsight
        - Apache Spark 
        - Apache Hadoop - a distributed system that uses MapReduce jobs 
        - Apache HBase - an open-source  large-scale NoSQL 
        - Apache Kafka - a message broker for data stream processing.
        - Apache Storm -  open-source  for real-time data processing 

### Fundamentals of real-time analytics
- 2 Types:
    - Batch processing
        - multiple data records are collected and stored processed 1 operation.
        - Eg : postpaid Bill
        - Adv : Large Volume of Data , Time can be schdeuled , For Complex Operations
        - DisAdv : Latency , Input Data needs to be prepared
    - Stream processing
        - source data is constantly monitored and processed in real time 
        - Adv : No Latency ,Real Time , No prep of data
        - Disav : Not for High Volume , Recent Data , Simple Operations 

- General architecture for stream processing
    - An event generates some data Eg:   a social media posts , a logs
    - data is captured  Eg: folder in a cloud data store or a table in a database , the source may be a "queue" 
    - The event data is processed by a perpetual query running in time window Eg:Count the number of sensor emissions per minute.
    - The results stored output sink Eg:  file, database table etc.,

- Azure Stream Analytics (PAAS) 
    - Ingest data from an input eg : Azure event hub, Azure IoT Hub, or Azure Storage blob container.
    - Process the data by using a SQL query 
    - Write the results - Gen 2, Azure SQL Database,  Synapse , Azure Functions,  event hub,  Power BI, or others.
    - created using Stream Analytics job 
    - Stream Analysis cluster = dedicated tenant for Stream Analytics job

- Spark Structured Streaming :
    - develop streaming for Apache Spark based services : Synapse  , Databricks, HDInsight.
- Delta Lake 
    - Datalake +transactional consistency + schema enforcement
    -  streaming and batch
    - Can be used as Source / Sink

- Azure Data Explorer: 
    - database ,
    - analytics 
    - ingesting querying batch , streaming data with a time-series element
    - a standalone Azure service 
    - Azure Synapse Data Explorer runtime in an Azure Synapse Analytics workspace.
    - Uses Kusto Query Language (KQL)
    - Query telemetry data that includes a timestamp attribute.
    - Example :
    

		    LogEvents
		    | where StartTime > datetime(2021-12-31) 
		    | where EventType == 'Error'
		    | project StartTime, EventType , Message
	    
	    

### Fundamentals of data visualization
- Microsoft Power BI
    - data analysts can use to build interactive data visualisations for business users
    - Dashboard - Single page coll of reports
    - Reports - Collection of visuals with more than 1 page
    - Powr BI report Builder = Author and publish paginated reports
    - Powr Bi Desktop - create interactive report for Dashboard
    - Power Bi Service = Desktop + Dashboard
    - Power BI Desktop 
        - import data from a wide range of data sources
        - combine and organize into analytics data model
        - create reports that contain interactive visualizations of the data.
    - Power BI service
        - reports can be published and interacted with by business users
        - basic data modeling using a web browser (limited functionality)
    -  Power BI phone app.
    - Users can consume reports, dashboards, and apps in the Power BI service 
- Concepts of data modeling
    - Facts and Dimensions 
    - numeric is called measures,entities is called dimensions
    - Eg :  table containing numeric measures for sales (such as revenue or quantity) and 
            dimensions for products, customers, and time.
    - model forms a multidimensional structure called cube
    - Denormalised Star Scheme (Best practise)
    - star Schema is  fact table is related to one or more dimension tables
    - Dim = Person Details  , Fact = Transaction done by Person
    - hierarchies = drill-up or drill-down to find aggregated values at different levels
    - model tab of Power BI Desktop to define your analytical model 

- Visualizations
	 - Tables and text: simplest way to communicate data
	 - Bar and column:  compare numeric values for discrete categories.
	 - Line:            examine trends, often over time.
	 - Pie:             visually compare categorized values as proportions of a total.
	 - Scatter:         compare two numeric measures, identify relationship or correlation
	 - Maps:            compare values for different geographic areas or locations.

- Create Reports
    1. PowerBi Destop > GetData > Web > add URl> OK
    2. Model Tab to Create Model ie., Format , Heirachy 
    3. enable Visualizations:
    File > Options and Settings> Security section> Use Map and Filled Map visuals> OK.
    4. Fields Pane contain the Model created 

- Visualizaton which can be pinned (gives No additional Data) = textbox ,Images,videos,streaming Data , Webcontent
- cannot be pinned in PowerBI = Interactive Reports , Datasets,Dashboards,Xlsx ,SSRS






================================== REFERENCES 




####

Descriptive  - averge Revenue
Diagnostic - Why avg rev low ?
Predictive - Avg revenue happens when covid
Presciptive - Youtube recommenede videos
Cognative  - AI , Self Driving Car

RDBMS 
SQL Server in VM - User installs the SQL server in VM
(Apply image on Container)
SQL Managed Instance  - Fully Managed by 
Azure SQL database (PaaS)
Azure Database ( other DBs than - MariaDB , PostgreSQL )



## DP-900 | Azure Data Fundamentals Certification (https://www.youtube.com/watch?v=0f9JLKgfFXM)
### DataStore Types
- RDBMS
- NoSQL
- Analytical DB
- Object/Blob/File

### WithoutCloud
- Buying infra is Expensive
- Utilization of entire Infra efficiently all the time ? 
- Team need to maintain

### With Cloud 
- On Demand provisioning ( pay per use)
- Scaling easier
- High Availiablity
- low Latency by adding more data center( users from other parts of the world)
- Maintainablity
- crash backup
- Going Global and CDS
- Security

### Terminalogy
- IAAS (Infra as Service) 
    - SQL (image) installed to VM by user
    - User is responsible for everything

- Paas (Platform as A Service) - Recommended
    - Cloud is responsible for everything
    - Eg: Azure SQL Db, Cosmos etc.,
    - Create SQL Db
        - Search for SQL Database in portal
        - Create new resource grp
        - Select eveything free ,
        - COnfigure db>Basic or (General Purpose > Serverless)
        - Select Local redundant 
        - (usn,admin)my-paas/Password123
        - Networking > Public (firewall settings)
        - Networking > Add current client IP address and Allow Azure services and resources to access this server = YES
    - Search for SQL Databases in portal or "Azure SQL" >  SQL Databses
    - Azure provides QUery Editor
- SAAS (Software as A Service)
    - Online Excel , Outlook , CRM , Box etc ., 
    - Serice Provider is responsible for runtime.

### DataFormats  
Structured (RDBMS)
- tables ,rows and cols
- Schema
- Relationship between other tables
- index = primary key , query efficiently
- Constraint = not null
- Used in OLTP (online transaction) 
    - Eg: online payments 
    - Heavy Writes
    - Azure SQL DB , DB for MySQL , DB for Postgresql
-  OLAP (Online Analytics Processin) 
    - Eg :ETL , Warehouse
    - data from other Dbs 
    - Azure Synapse Analytics 
- OLTP vs OLAP
    - OLTP is row data storage , OLAP is column wise storage (column is compressed bcoz of same type of data)  
    - OLTP data cannot be distributed , OLAP data (column data) can be distributed across mulitple nodes

Semi (JSON , key value )
- Fexible schema (schema not verified , no constraints)
- Horizontal Scaling possible
- Cosmos DB used for NoSQL , SemiStructured 

#### Azure Data Studio
- Create SQL server
    - Free
    - servername : my-sql-database-server-new ,c  azuser/Password123
    - Configure DbServer
        - General Purpose > Serverless
    - locally Redundant
    - Networking (public , all access , add client)
- Download Azure Data Studio
    - ck on new connection
    - server( server name from resource dashboard)
    - enter usn /password 
    - connect
 
#### Create new Cosmos SQL  :
- Data Stored as JSON but use SQL to fetch data
- Create
    - Free and Local redundant
    - account name = any unique name(cosmos-sql-udemy)
    - East Asia
    - Select limit the total amount option
    - Goto resource > Add Container
    - Mandatory = 
        - Db id
        - throughput= manual
        - Container id
        - partition key column  = "/pk"
    - Ro Run , open Dataexplorer 
        - cosmos-sql-udemy-db > core-sql-container > items > new item
        - save
        - Query "select * from c where c.name="deepak"

#### Create new Cosmos Mongo :       
- use mongo filter to pull data 
- container is called collection in Cosmos Mongo 
- Uses sharding (similar to  partition)
- sharding is split data across multiple shards
- shard key = partition key
- filter ="{"key":value}"

#### Serverless vs provision Throughput (RU)
- RU  is billed per hr , Serverless = usage
- RU no autoscale ,serverless= Autoscale
- RU =mulitregion ,Serverless= No
- RU = data unlimited , Serverless= 50Gb

### Azure Storage (ie., UnStructured - pictures)
- Similar to Harddisk,Fileshare 
- Azure Disks : additional storage acts like harddisk 
- Azure Files (File Storage) : File share
- Azure Blob (Object Storage) : REST API objects ,upload vis REST etc.,

### Azure Data Factory
-  define and schedule data pipelines 
- integrate your pipelines with other Azure services
- persist the results in another data store.
- ETL


### Azure Stream Analytics
- Streaming  ETL Engine 

### Azure Data Explorer
- in Azure Synapse Analytics.
-  querying of log and telemetry data
- Runtime

### Azure Purview
- map your data and track data lineage across multiple data sources and systems

### Microsoft Power BI
- analytical data modeling and reporting
- Power BI reports can be created by using the Power BI Desktop application
- published and delivered through Power BI service and Power BI mobile app

### Azure Region :
- Region is geo location to host service
- Region > Zone > Datacenter

### Azure Zone:
- Part of a region
- Region can have 1 or many zones at same or different location with 1 or more seperate Data Center

#### Purchase 
- 1.  vCore
    - Serverless 
        - Auto Scale
        - charged only on usage and data stored
    - Provisioned
        - Can be configured
        - charged based on memory and Compute 
- 2.  DTU :
    - Bundle (compute and Memory)
    - compute and Memory cannot be configured independently

#### Data Reduncany (replicating Data)
- LRS (Local Reduncany Storage)- 3 syned copies maintined in same Data Center
- ZRS (Zone)- 3 synced copies in different Availialibity Zones
- GRS (Geo)- LRS + 1 Async copy to secondary region
- GZRS (Geo Zone)- ZRS + 1 Async copy to secondary region (most expensive)

#### Block Storage 
- Harddisk to VM (SSD , HDD , premium SSD , )
- Use Azure Disk
- Add Resource > Virtual Machines > Add > Disks
- (alternate )Resources >Storage > select any disk name created > Datastorage >Containers (different from docker/kubetl)
- types : managed (By azure) , Unmanaged (By user)

### Sources for stream processing
Azure Event Hubs: manage queues of event data
Azure IoT Hub: Internet-of-things (IoT) devices.
Azure Data Lake Store Gen 2: A highly scalable storage service for batch /streaming data.
Apache Kafka: Use Apache Spark and also use Azure HDInsight to create a Kafka cluster.

### Sinks for stream processing
Azure Event Hubs: 
Azure Data Lake Store Gen 2 or Azure blob storage: 
Azure SQL Database or Azure Synapse Analytics, or Azure Databricks
Microsoft Power BI

### Spark on Microsoft Azure
Azure Synapse Analytics
Azure Databricks
Azure HDInsight

### Analytics Types
- Descriptive- what,SQL,averge Revenue
- Diagnostic - why,Why avg rev low ?
- Predictive (ML) - what will happen ,Avg revenue happens when covid
- Prescriptive - Use Predictive Analysis and take nest step),Youtube recommenede videos ,Auto Complete
- Cognitive ( AI + ML) ,AI , Self Driving Car

### Big Data
- 3V = Volumne,Varity, Velocity
- Storage
    - DataWarehouse
        - Processed Data 
        - SQL
    - DataLake 
        - Raw Data (Google Cloud , Azure Data Lake Storgae Gen2)
        - Blob Storage . Gen 2
        - parq format
        - Synapse can directly read from Datalake 

### Azure Specific Services
- Synapse (End to End Analytics)
    - Dataintegration + Load  DW + Data Analytics
    - Sql
    - Spark jobs
- Data Factory
    - Manged Serice
    - Serverless
    - ETL
    - Data pielines
- Power BI ( Visualization)

### Hadoop , Spark , Databricks
- Hadoop
    - Support variety of data
    - HDFS 
    - Map Reduce / parallelization in nodes
    - java Python
    - Hive (query)
    - spark  ( In Memory)
- Databricks
    - Web Based managed service for spark

### Parquet
- Storage Format
- opensource
- Column storage
- High Compression
- Azure Data Factory , Azure Data lake ,Blob Storage

### hadoop and Spark  Services
- Azure HDInsight (old)
- Azure Databricks - new (managed service) 
    - Read Data from Azure SQL Database, Cosmos,Event Hubs
- Synapse
- Datafactory

### Databricks
- Create 
    - Search Databricks > Give Resource Group and name > Create >Goto Resource> Launch Workspace
    - Name , Terminate after 10mins , workers=1
    - Create Notebook > Name
    - sample dataset - open browser "https://docs.microsoft.com/en-us/azure/open-datasets/dataset-catalog"
    - createorreplacetempview()
    - Use SQL query for Analysis 

### Massive Parallel Processing (MPP)
- compute across muliuplpe nodes
- Spark ,Synapse

### Pipelines 
Batch Piplines
- Huge 
- In groups
- Hours or No of Records
- high Latency

Streaming pipelines
- Small Number
- Use Event Hubs
- Realtime
- Low Latency

### Synapse 
- Target Data store itself is a transformation Engine
- Synapse Analytcs
- Linked Service ,Control Flow ,datMovement

### Synapse Analytics
- End to End Analytics 
- SQL 
- SPARK (spark jobs)
- Pipelines
- PowerBI,Cosmos,Azure ML,Azure Data Lake  ,GCp
- parq ,csv ,JSON
- Consumption Model : Dedicated ,Serverless
- Polybase : run SQL on external DataSources
- Data Explorer pools can be used to run near real-time analytics on large volumes of logs 

#### XXXX
- ARM Template (JSON) - Copy paste configuration of environments




- Synapse - Not Support data Extraction from Multiple sources 
- SQL mnaged Instance DB = Point to site VPN connections and Private endpoint
- Databricks = no streaming ,User cannot start stop cluster

- object Store - File / Audio ,Video Eg: Blob

- Control Node - responsible for intreacting with app 
- Azure Cosmos DB Data Migration tool - Migaration
