chawe use apply **apply changes into** avoids writing of duplicate records so we use it instead of **insert into** in some situations

 In PySpark, which of the following commands can you use to query the Delta table **employees** created in Spark SQL?

we can use 
```sql
spark.table("employees")
```
to query a table in pyspark 
***
 what of the following statement describe Auto loader 
`Auto loader monitors a source location, in which files accumulate, to identify and ingest only new arriving files with each command run. While the files that have already been ingested in previous runs are skipped.`
***
 The data engineer team has a DLT pipeline that updates all the tables once and then stops. The compute resources of the pipeline continue running to allow for quick testing.
Which of the following best describes the execution modes of this DLT pipeline ?

**The DLT pipeline executes in Triggered Pipeline mode under Development mode.**

note that --> A **DLT (Delta Live Table) pipeline** is a data pipeline in Databricks that is designed for building and managing data processing workflows in a simpler, scalable, and more reliable manner.

***
Which of the following code blocks can a data engineer use to query the existing streaming table **events** ?
```sql
  
spark.readStream.table("events")
```
 ***
 A data engineer has the following query in a Delta Live Tables pipeline:
```sql
CREATE LIVE TABLE aggregated_sales
AS
SELECT store_id, sum(total)
FROM cleaned_sales
GROUP BY store_id
```
The pipeline is failing to start due to an error in this query
Which of the following changes should be made to this query to successfully start the DLT pipeline ?

```sql
CREATE LIVE TABLE aggregated_sales
AS
SELECT store_id, sum(total)
FROM LIVE.cleaned_sales
GROUP BY store_id
```
 ***
 Which of the following is the benefit of using the Auto Stop feature of Databricks SQL warehouses ?

**Minimizes the total running time of the warehouse**

***
The data engineer team has a DLT pipeline that updates all the tables at defined intervals until manually stopped. The compute resources terminate when the pipeline is stopped.
Which of the following best describes the execution modes of this DLT pipeline ?

**The DLT pipeline executes in Continuous Pipeline mode under Production mode.**

***
A data engineer wants to create a relational object by pulling data from two tables. The relational object must be used by other data engineers in other sessions on the same cluster only. In order to save on storage costs, the date engineer wants to avoid copying and storing physical data.
Which of the following relational objects should the data engineer create?

**Global Temporary view**

***
Which of the following tasks is not supported by Databricks Repos (Git folders), and must be performed in your Git provider ?

 **delete branches**
 ***
 
 which of the following data engineer using to create a new table a long with a comment
```sql
CREATE TABLE payments
COMMENT "This table contains sensitive information"
AS SELECT * FROM bank_transactions
```

***
**Delta lake** -->One of the foundational technologies provided by the Databricks Lakehouse Platform is an open-source, file-based storage format that brings reliability to data lakes.
Which of the following technologies is being described in the above statement?

***
**JSON** --> is the primary format for the transaction log files
***
A junior data engineer uses the built-in Databricks Notebooks versioning for source control. A senior data engineer recommended using Databricks Repos (Git folders) instead.
Which of the following could explain why Databricks Repos is recommended instead of Databricks Notebooks versioning?

**Databricks Repos supports creating and managing branches for development work.**

***
A data engineer has a database named **db_hr**, and they want to know where this database was created in the underlying storage.
Which of the following commands can the data engineer use to complete this task?

**DESCRIBE EXTENDED db_hr**

****
Given the following commands:
```sql
CREATE DATABASE db_hr;
USE db_hr;
CREATE TABLE employees;
```
where the new table ***employees*** will be stored 

**dbfs:/user/hive/warehouse/db_hr.db**
***

Which of the following statements best describes the usage of `CREATE SCHEMA` command ?


**It’s used to create a database**

note that --> in HIVE in data bricks  **schemas** and **databases** are essentially the same concept, with the terms used interchangeably. Both commands create a namespace for tables and other objects within the environment.

SO create data db = create  schema database 
***
Which of the following statements is **Not** true about CTAS statements ?

**CTAS statements support manual schema declaration**
***
A junior data engineer uses the built-in Databricks Notebooks versioning for source control. A senior data engineer recommended using Databricks Repos (Git folders) instead.
Which of the following could explain why Databricks Repos is recommended instead of Databricks Notebooks versioning?

**Databricks Repos supports creating and managing branches for development work.**
****
A data engineer has a database named **db_hr**, and they want to know where this database was created in the underlying storage.
Which of the following commands can the data engineer use to complete this task?

**DESCRIBE DATABASE db_hr**
****
Given the following Structured Streaming query:
```sql
(spark.table("orders")
.withColumn("total_after_tax", col("total")+col("tax"))
.writeStream
.option("checkpointLocation", checkpointPath)
.outputMode("append")
.___________
.table("new_orders") )
```
Fill in the blank to make the query executes multiple micro-batches to process all available data, then stops the trigger.

**trigger(availableNow=True)**

****
A data engineer has defined the following data quality constraint in a Delta Live Tables pipeline:

  

`CONSTRAINT valid_id EXPECT (id IS NOT NULL) _____________`

  

Fill in the above blank so records violating this constraint cause the pipeline to fail.

**ON VIOLATION FAIL UPDATE**

***
Given the following Structured Streaming query:

  
```sql
(spark.readStream
.table("orders")
.writeStream
.option("checkpointLocation", checkpointPath)
.table("Output_Table")

```

**Every half second**

****
From which of the following locations can a data engineer set a schedule to automatically refresh a Databricks SQL query ?

**From the query's page in Databricks SQL**
***
In Databricks Jobs, which of the following approaches can a data engineer use to configure a linear dependency between **Task A** and **Task B** ?

**They can select the Task A in the Depends On field of the Task B configuration**

****
A data engineer uses the following SQL query:

  

`GRANT USAGE ON DATABASE sales_db TO finance_team`

  

Which of the following is the benefit of the **USAGE**  privilege ?

**No effect! but it's required to perform any action on the database**

****
In which of the following locations can a data engineer change the owner of a table?

***In Data Explorer, from the Owner field in the table's page***

****
A data engineer has ingested data from an external source into a PySpark DataFrame raw_df. They need to briefly make this data available in SQL for a data analyst to perform a quality assurance check on the data. Which of the following commands should the data engineer run to make this data available in SQL for only the remainder of the Spark session?

**raw_df.createOrReplaceTempView("raw_df")**

***

note that --> data bricks repos support multiple branches 
note that --> table is been saved in a physical location while view is not 
create streaming live table --> incrementally  
create live table --> static 
***

A data analysis team has noticed that their Databricks SQL queries are running too slowly when connected to their always-on SQL endpoint. They claim that this issue is present when many members of the team are running small queries simultaneously. They ask the data engineering team for help. The data engineering team notices that each of the team’s queries uses the same SQL endpoint.  
Which of the following approaches can the data engineering team use to improve the latency of the team’s queries?

**They can increase the maximum bound of the SQL endpoint’s scaling range.**

note that:
-Sequentially -> Increase cluster size 
-Concurrent --> Scale out cluster

***
A single Job runs two notebooks as two separate tasks. A data engineer has noticed that one of the notebooks is running slowly in the Job’s current run. The data engineer asks a tech lead for help in identifying why this might be the case.  
Which of the following approaches can the tech lead use to identify why the notebook is running slowly as part of the Job?

**They can navigate to the Runs tab in the Jobs UI and click on the active run to review the processing notebook.**

****
explanation: In Structured Streaming, if a data engineer wants to process all the available data in as many batches as required without any explicit trigger interval, they can use the option **trigger(availableNow=True)**. This feature, availableNow, is used to specify that the query should process all the data that is available at the moment and not wait for more data to arrive

note that --> trigger(processingTime="5 seconds")