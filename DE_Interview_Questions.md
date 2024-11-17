# Interview-Spark/Data Engineering

**Question 1:**
You're monitoring Spark jobs, and one job is taking more time to complete but hasn't failed. What are the possible reasons for this Spark job running very slowly?

**Question 2:**
In Spark, if you have one large table and one small table, which join would you apply, and why? How does it work internally?

**Question 3:**
You are the only one managing ETL jobs and need to design a cluster to process 500 GB to 1 TB of data every day. You have resources of 8 nodes, each with 32GB RAM and 8 CPU cores. How would you configure executors, and what would be the memory and cores allocation for each executor? Explain the different categories of memory with the exact amount each occupies.

**Question 4:**
You deployed a Spark ETL job today in production, and it was working fine. Unfortunately, it broke the next day because two columns were unexpectedly added to the dataset (from 50 columns to 52 columns). This happened in production. How would you handle this situation?

**Question 5:**
In Spark, when you execute the code, it will create:

- Stages

- Jobs

- Tasks
Could you please explain how these are created?

**Question 6:**
There are many file formats available, but in Spark, we often use Parquet. What are the reasons for using Parquet over other file formats like JSON, ORC, CSV, and TXT?

**Question 7:**
If you have one table with 100 TB and another table with 1 GB, and you are performing joins, how would you try to optimize this?

**Question 8:**
If you are using an on-premise cluster, how do you check how much memory and cores are allocated to each team?

**Question 9:**
You mentioned you have a 100 TB table and are joining it with a 1 GB table. How much time would that job take to complete?

**Question 10:**
You need to process a 100 TB data file. You have 8 nodes, each with 64GB RAM and 8 CPU cores. How would you handle this 100 TB file using this cluster size?

**Question 11:**
Imagine you need to join two large datasets in Spark, but one of the datasets cannot fit into memory. How would you approach this situation?

**Question 12:**
For unit testing, what framework are you using, and what scenarios are you checking as part of unit testing?

 **Question 13:**
You have cleaned your data and are now trying to store it in your data warehouse. If you use the overwrite mode, what happens? If you use the append mode, what happens? If you need to maintain historical data, how do you maintain it?

-------------------------------------------------------------------------------
**Interviewer**: You're running a Spark job on a large dataset stored in HDFS. Suddenly, you notice that the job is taking longer than usual to complete. How would you troubleshoot ?

**Candidate**: When faced with a slowdown in a Spark job, several factors could be contributing to the issue. Here's how I would approach:

**Interviewer**: What would be your initial steps in troubleshooting the slow Spark job?

 I would check the Spark UI to gather information about the job's execution, including task progress, stage durations, and resource utilization. This can help identify bottlenecks and performance issues within the job.

**Interviewer**: Could you provide some specific metrics or indicators you'd look for in the Spark UI?

I'd focus on metrics such as task duration, shuffle read/write times, executor CPU and memory utilization, and garbage collection activity. These metrics can provide insights into potential performance bottlenecks, such as data skew, resource contention, or inefficient task execution.

**Interviewer**: If you notice high shuffle read/write times in the Spark UI, how would you investigate further?

High shuffle read/write times often indicate issues with data skew or inefficient shuffle operations. I would drill down into the stage details in the Spark UI to identify tasks with disproportionately high shuffle read/write times. Analyzing the data distribution and partitioning strategy can help pinpoint the cause of the skew and optimize the shuffle operations accordingly.

**Interviewer**: What steps would you take if you suspect resource contention as the cause of the slowdown?

If resource contention is suspected, I would examine executor CPU and memory utilization to identify any resource bottlenecks. Increasing executor memory or adjusting the number of executors can help alleviate resource contention and improve job performance. Additionally, optimizing resource allocation and task scheduling parameters in the Spark configuration can further optimize resource utilization.

**Interviewer**: Suppose you've optimized resource utilization, but the job is still running slower than expected. What other factors would you consider?

If resource utilization is optimized, I would investigate other potential factors impacting job performance, such as inefficient data processing logic, data skew, or suboptimal partitioning strategies. Analyzing the job's DAG  and execution plan can provide insights into the data processing flow and identify opportunities for optimization.

**Interviewer**: How would you ensure the stability and reliability of the Spark job after troubleshooting and optimization?

After troubleshooting and optimization, I would conduct thorough testing to validate the stability and reliability of the Spark job under varying workload conditions and data scenarios. This includes performance testing, stress testing, and fault tolerance testing to ensure the job performs reliably and efficiently in production environments.

-------------------------------------------------------------------------------------------

 # 𝐃𝐄 𝐈𝐧𝐭𝐞𝐫𝐯𝐢𝐞𝐰📢 𝐒𝐩𝐚𝐫𝐤 ⌛ 𝟏-𝐌𝐢𝐧-𝐑𝐞𝐚𝐝
🔍 𝐖𝐡𝐞𝐧 𝐜𝐚𝐧 𝐮𝐬𝐢𝐧𝐠 𝐂𝐨𝐚𝐥𝐞𝐬𝐜𝐞 𝐥𝐞𝐚𝐝 𝐭𝐨 𝐟𝐚𝐢𝐥𝐮𝐫𝐞 𝐢𝐧 𝐒𝐩𝐚𝐫𝐤?

🧔🏽‍♂ **Interviewer**: Explain when Coalesce can lead to failure in Spark?
👨‍🦰 **Interviewee**: Coalesce is a Spark transformation used to reduce the number of partitions in a DataFrame or RDD. While it's generally efficient, there are scenarios where using Coalesce can cause issues.

🧔🏽‍♂ **Interviewer**: Could you provide an example of such a scenario?
👨‍🦰 **Interviewee**: When reducing the number of partitions using Coalesce, Spark combines data from multiple partitions into a smaller number of partitions. If the combined data exceeds the memory limits of the executor nodes, it can lead to out-of-memory errors or even executor failures.

🧔🏽‍♂ **Interviewer**: How can this situation be avoided?
👨‍🦰 **Interviewee**: One approach is to use repartition instead of coalesce when you need to increase the number of partitions. Repartition shuffles data across partitions more evenly, reducing the risk of data skew and memory issues. Additionally, monitoring the memory usage of executor nodes and adjusting partition sizes accordingly can help prevent failures.

🧔🏽‍♂ **Interviewer**: Are there any other considerations when using Coalesce?
👨‍🦰 **Interviewee**: Yes, another consideration is data skew. If there's significant data skew in the original partitions, Coalesce may not evenly distribute the data across the reduced number of partitions. This can lead to uneven processing and performance issues, especially in downstream operations.

----------------------------------------------------------------------

# Interview Questions- Expected Answers
**Apache Spark**
1. Which version(s) of Apache Spark have you worked with?
A: "I have worked with Spark 2.4 and 3.0."
Big Data ETL Pipelines
2. Have you developed ETL pipelines for big data? If yes, could you describe one?
A: "Yes, I developed a pipeline using Apache Spark to process streaming data from Kafka and batch data from HDFS."
Data Management
3. What is the approximate size of data you handle in the ingest layer of your ETL pipelines?
A:"We handle around 10-100 TB of data in the ingest layer."
Job Nature
4. Do you work with batch jobs or streaming jobs?
A:"I work with both, but primarily with streaming jobs for real-time data processing."
Migration and Optimization
5. Have you had experience migrating back to on-premise systems from AWS? How do you optimize jobs in Spark?
A:"Yes, during a migration project from AWS to on-prem, I optimized Spark jobs by tuning the executor memory and cores."
Operational Details
6. How often do your Spark jobs run and what data formats do you commonly handle?
"Our jobs run hourly, handling formats like Parquet and JSON."
Spark Performance
7. How does Spark read data and what optimization techniques do you use?
A:"Spark reads data using Data Frame APIs optimized with partitioning and caching strategies."
8. When data is written in more than one partition, why might the sizes vary, and how does this affect performance?
A:"Partition size varies due to data skew. It affects performance by causing uneven load on cluster nodes."
Elasticsearch
9. Can you retrieve partially processed data from a failed job in Spark to avoid reprocessing?
A:"Yes, by maintaining state information or checkpoints in the pipeline, we can process only the necessary data again."
Checkpointing is a mechanism to save the state of your application at a given point in time, allowing you to recover from failures without reprocessing all the data.
How to Implement Checkpointing
	• Enable Checkpointing: You need to set a checkpoint directory where Spark will save the RDDs. This can be done using
spark.sparkContext.setCheckpointDir("path/to/checkpoint/dir")
	· Apply Checkpointing: Use the checkpoint() method on RDDs or DataFrames at strategic points in your processing pipeline. For example:
rdd.checkpoint()
	· Recovery: In the event of a failure, Spark will automatically load the data from the checkpoint instead of recomputing the entire lineage.

#### Apache Kafka

10. What have you used Apache Kafka for in your projects?
A:"I've used Kafka for real-time data ingestion and as a buffer between data sources and processing engines."

-----------------------------------------------------------------
# Recently asked Interview Question in EPAM
Technologies for Data Engineer (5+ years exeprience)
1. Coding Questions: Pyspark:
You've been given some CSV files like karnataka.csv
and maharashtra.csv in an ADLS location, each
containing columns for first_name, last_name, age,
sex, and location.
Your task is to add a new column called state to each
DataFrame. The state column should contain the
state name extracted from the filename.
For example:
For karnataka.csv, the state column should contain
the value 'karnataka'.
For maharashtra.csv, the state column should contain
the value 'maharashtra'.
Your solution should utilize PySpark to efficiently
handle large-scale data processing tasks.
2. Coding Question: Python/ DSA:
A. Reverse a string without using reverse function
B. Write a python program to implement following.
Given a pattern and a string. If string matches the
pattern return true else return false.
Ex:
Pattern - "abba", String - "dog cat cat dog" will return
true.
-
Pattern "aba", String - "dog dog cat" will return
false.
3. Coding Question: SQL
Find the 3-month rolling average of total revenue from
purchases given a table with users, their purchase
amount, and date purchased (YYYY-MM-DD). Output
the year-month (YYYY-MM) and 3-month rolling
average of revenue, sorted from earliest month to latest month.
4. Explain Spark Architecture.
5. What is Z-ordering?
6. Difference between Datamart, Datawarehouse and
Deltalake
7. Compare performance of Managed and External
Table
8. Difference between blob Store and ADLS Gen2

-------------------------------------------------------------------
1. Can you provide an overview of your experience working with PySpark and big data processing?

2. What motivated you to specialize in PySpark, and how have you applied it in your previous roles?

3. Explain the basic architecture of PySpark.

4. How does PySpark relate to Apache Spark, and what advantages does it offer in distributed data processing?

5. Describe the difference between a DataFrame and an RDD in PySpark.

6. Can you explain transformations and actions in PySpark DataFrames?

7. Provide examples of PySpark DataFrame operations you frequently use.

8. How do you optimize the performance of PySpark jobs?

9. Can you discuss techniques for handling skewed data in PySpark?

10. Explain how data serialization works in PySpark.

11. Discuss the significance of choosing the right compression codec for your PySpark applications.

12. How do you deal with missing or null values in PySpark DataFrames?

13. Are there any specific strategies or functions you prefer for handling missing data?

------------------------------------------------------------------

# For architect role

# LTI 5-5.30 Dt: 09.05.2024
1) Intro and Project
2) How many tables u     have in your project
3) Let's say,if u have 100gb of data movement,how do u decide the cluster size 
4) How do u do the incremental load if there's no date field
5) If u r joining large tables of size 100GB,what precautions do u take in terms of performance
6) Schema evaluation and schema enforcement,what's the difference and which one do u prefer.

# TCS | 16.05.24 | 11.30-12.15
1) Intro and Project 
2) What if I have multiple types of files such  as .txt,.CSV,.json etc.. I have to copy only .CSV files from the container to a storage location.whats the procedure using ADF 
3) What all activities u know in ADF 
4) Difference between Cache and persist 
5) Diff between System managed identity and User managed identity 
5) How do u call a notebook from another notebook
6) What are the different ways to access a storage account from ADF
7) What's the difference between SAS and access keys
8) Imagine if the target is another region and source is in another region, how do u copy the data
9) Due to any calamity if the Azure is down,how do u tackle that
10) Y u used databricks in your project ?
11) What's rbac and y we use it

-----------------------------------------------------------------


# Deloitte interview questions for Data Engineer 2024.

1. Can you explain your project flow and architecture?
2. What is the default file format used in Spark?
3. Why is Parquet commonly used in Spark?
4. What optimization techniques have you implemented in your projects?
5. Can you explain the difference between `groupByKey` and `reduceByKey` in Spark? Which one is more efficient?
6. What do you understand by rack awareness in Hadoop?
7. What file formats do you typically use in your data processing workflows?
8. How does fault tolerance work in Spark?
9. How would you handle and ignore null values while loading data?
10. How would you find the 3rd highest salary in a dataset?
11. Given a dataset with positive and negative invoice values, how would you convert the positive values to negative while keeping the negative values unchanged?
12. How can you convert a date like "20/04/1963" to an integer format?
13. Given a dataset containing alphanumeric values and integers, how would you extract specific alphanumeric sequences like "ML," "GM," and "LTR" and create a new DataFrame to view only these sequences in Spark?
14. What kind of questions have you encountered related to data modeling in your projects?
---------------------------------------------------------------------------------------
# Spark / PySpark / Databricks Interview Questions

1. Describe the PySpark architecture.
2. What are RDDs in PySpark?
3. Explain the concept of lazy evaluation in PySpark.
4. How does PySpark differ from Apache Hadoop?
5. What are DataFrames in PySpark?
6. How do you initialize a SparkSession?
7. What is the significance of the SparkContext?
8. Describe the types of transformations in PySpark.
9. What is Azure Databricks.
10. Explain the role of Apache Spark in Azure Databricks.
11. How do you configure a Spark cluster in Azure Databricks?
12. What are the advantages of using PySpark in Azure Databricks for data processing?
13. Describe the concept of notebooks in Azure Databricks.
14. How do Azure Databricks workspaces enhance collaboration?
15. What is the Databricks File System (DBFS), and how is it used?
16. How do you schedule jobs in Azure Databricks?
17. Explain the significance of Delta Lake in Azure Databricks.
18. How do you read a CSV file into a PySpark DataFrame?
19. What are actions in PySpark, and how do they differ from transformations?
20. How can you filter rows in a DataFrame?
21. Explain how to perform joins in PySpark.
22. How do you aggregate data in PySpark?
23. What are UDFs (User Defined Functions), and how are they used?
24. How can you handle missing or null values in PySpark?
25. How do you repartition a DataFrame, and why?
26. Describe how to cache a DataFrame. Why is it useful?
27. How do you save a DataFrame to a file?
28. What is the Catalyst Optimizer?
29. Explain the concept of partitioning in PySpark.
30. How can broadcast variables improve performance?
31. What are accumulators, and how are they used?
32. Describe strategies for optimizing PySpark jobs.
33. What is the significance of the Tungsten execution engine?
34. How does PySpark handle data skewness?
35. What are the best practices for managing memory in PySpark?
36. How can you monitor the performance of a PySpark application?
38. Explain how checkpointing works in PySpark.
39. What is delta lake
40. What is data lakehouse architecture.


