# Databricks Structured Streaming Study Note

## Introduction
Structured Streaming is a scalable and fault-tolerant stream processing engine built on the Spark SQL engine. It allows you to process real-time data streams with the same ease and simplicity as batch processing.

## Key Concepts

- **Stream vs Batch Processing**: Traditional batch processing works on a static dataset, while streaming processes data in real-time as it arrives.
- **DataFrame API**: Structured Streaming uses the DataFrame API for defining the streaming computation.
- **Fault Tolerance**: It guarantees fault tolerance through checkpointing and write-ahead logs.

## Setting Up Structured Streaming

1. **Create a Spark Session**: Initialize the Spark session.
2. **Read Stream**: Use `readStream` to connect to a data source (e.g., Kafka, socket, files).
3. **Transformations**: Use DataFrame transformations to process the incoming stream.
4. **Write Stream**: Output the processed stream to a sink (e.g., console, file, Kafka).

## Example: Word Count from Streaming Data

### Step 1: Create a Spark Session
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("Structured Streaming Example") \
    .getOrCreate()
```
### Step 2: Read stream
```python
lines = spark.readStream \
    .schema("key STRING, value STRING") \
    .csv("path/to/your/csv/source")  
```
### Step 3: Transformation
```python
from pyspark.sql.functions import explode, split

words = lines.select(
    explode(split(lines.value, " ")).alias("word")
)
```
### Step 4 : read Stream
```python
wordCounts = words.groupBy("word").count()

query = wordCounts.writeStream \
    .outputMode("complete") \
    .format("console") \
    .start()

query.awaitTermination()
```

```