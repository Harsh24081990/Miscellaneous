1.########### CITY US ################ 7-Sept-2024
Que: pyspark - Write a program to
	a. to read a csv "Employee"[EMP_ID,EMP_Name,DEPT_ID,Designation] and "Department"[DEPT_ID,DEPT_Name] 
	b. Join the both DataFrames/tables
	c. Add new Column "Dept_Desig" contains (DEPT_Name-Designation)
	d. For each "Dept_Desig", Count the number of Employees
	e. Sort the result in Descending of Employees count
==============================================================

2.########### LTI MindTree ################ 7-Sept-2024
Que: SQL -------input
city1   city2       fare
banglore chennai   2000
chennai  banglore  2000
banglore pune      4000
kolkatta banglore  6000
banglore klokatta  6000
----output
banglore chennai  2000
banglore pune     4000
kolkatta banglore 6000
==============================================================

3.####### Cognizant ######## 21-Sept-2024

Que 1: How to connect onprem to azure ADLS ? can we directly connect that ? Types of Integration Run Time ? What issue you faced ?
Ans: Lecture 14 (Azure Notes)
-------------------------------------------------------------------------------------
Que 2: If you created pipeline in ADF using ADB notebooks ? how to handle failure scenarios ? how to restart pipeline from the failed point? how to maintain incremental loading without loading the data from start ?
https://github.com/Harsh24081990/databricks/blob/main/handling%20failure%20of%20notebooks.md
-------------------------------------------------------------------------------------

Que 3: Can we connect ADLS directly to the data bricks using mount point ? As we can't allow ADLS to be connecting to public end points, then it will give error while making the connection between ADLS and ADB. Have you faced that and how do you resolve that ?

(possible answer --> check box on --> "allow azure services to access this server" under "set server firewall" section.) (faced issue while connecting to azure sql db and the issue was resolved by enabling this option)

https://github.com/Harsh24081990/azure/blob/main/ADLS%20to%20Databricks%20mount%20point.md
-------------------------------------------------------------------------------------
Que 4: How to implement SCD 2 using pyspark code ?
https://github.com/Harsh24081990/PySpark/blob/main/SCD2_in_DataBricks.md

using SQL:-
https://github.com/Harsh24081990/databricks/blob/main/SCD%20type2%20using%20delta%20lake%20merge%20and%20md5.md
-------------------------------------------------------------------------------------
Que 5: While implementing SCD 1 how you do the comparison between the rows to identify the new recodes ?
https://github.com/Harsh24081990/databricks/blob/main/SCD%20type%201%20using%20merge%20into%20and%20MD5%20to%20compare%20business%20columns.md
-------------------------------------------------------------------------------------
Que 6: Have you used MD5 function ?
YES. to generate a hash values by concatenating the important business columns, the columns which we want to compare between source and target. so rather than comparing columns one by one we can use MD5 to generate a combined hash value. 
-------------------------------------------------------------------------------------
Que 7: Explain the deployment process in your project end to end ?
Ans: Use 13 A and 13 B page of Azure Notes
-------------------------------------------------------------------------------------

Que 8: What is the difference between Cluster and Workspace in context of data bricks ?
Ans: Clusters are about compute resources and running tasks, while Workspaces are about organization, collaboration, and management of projects and notebooks.

A cluster is tied to a single workspace in Databricks and cannot be shared across multiple workspaces. However, you can share data and code across workspaces using unity catalog, but each workspace must manage its own clusters separately.

https://github.com/Harsh24081990/databricks/blob/main/Cluster%20Vs%20Workspace%20in%20databricks.md
-------------------------------------------------------------------------------------

Que 9: How to do partitioning on the delta tables in databricks ?
# Write DataFrame to Delta Table with partitioning df.write.format("delta").mode("overwrite").partitionBy("date").save("/mnt/delta/my_partitioned_table")

CREATE TABLE my_partitioned_table 
USING delta PARTITIONED BY (date) 
AS 
SELECT id, date, category 
FROM …..
-------------------------------------------------------------------------------------

Que 10: Suppose you dropped the delta table, file is still present in the ADLS location. If you try to create table again with the changed schema using the old file ? what error you will get and how to handle that ?
Ans: 
	1. Check Current Schema of Files
	Before recreating the table, you can check the existing schema of the data files using the following command:
	# Read the old data files to see their schema
	old_data_df = spark.read.format("delta").load("path/to/old/files")
	old_data_df.printSchema()
	
	2. Create Table with REPLACE
	If you need to redefine the table with a new schema while keeping the old data, you can use REPLACE to overwrite the existing Delta table:
	spark.sql("""
	    CREATE OR REPLACE TABLE new_table_name
	    USING DELTA LOCATION 'path/to/old/files'
	    AS SELECT * FROM old_data_df
	""")
-------------------------------------------------------------------------------------
Que 11: There is a .DAT file. the header contain the number of records in the file. The rows are pipe delimited. the trailer contains the date. Using pyspark validate the file by matching the number of rows in the file with the number given in the header of the file and date should be the current date. If these 2 condition are satisfied print the message "File is OK".
Ans : use 
df.first().value or df.head(1)[0].value
df.last(1)[0].value
df.count()
datetime.now().strftime('%Y-%m-%d')
if condition

https://github.com/Harsh24081990/PySpark/blob/main/Validate_file.md
-------------------------------------------------------------------------------------

Que 12 : In storage event trigger in ADF, is it possible to give a condition like only if the 2 files are arrived in the storage directory , then only trigger the pipeline ? For example only if A.csv and B.csv both are present then only the pipeline should get trigger. 
ANS: 
• Step 1: Set up a storage event trigger in ADF for when files are created in the directory (e.g., for *.csv files).
• Step 2: Inside the pipeline, use 2 Get Metadata activity to check for the presence of A.csv and B.csv.
	- Get Metadata for A.csv (Check if A.csv exists)
	- Get Metadata for B.csv (Check if B.csv exists)
• Step 3: Use an If Condition activity. 
	If Condition: Check if both A.csv and B.csv exist.
	- True Branch: Proceed with the rest of the pipeline (e.g., copy data, process files, etc.).
	- False Branch: Exit or retry the process.
==============================================================================

4.####### Wolters Kluwer ######## 5-Oct-2024

	l Why dataframes are faster than RDD ?
	https://github.com/Harsh24081990/spark/blob/main/RDD_Vs_DataFrame.md

	l how to check the rejected rows while running a ADF pipeline ? how to send the notification mentioning the rows which got rejected ?
	https://github.com/Harsh24081990/azure/blob/main/Error_Handling_ADF.md

	l How to do data reconciliation between source and target in ADF ?
	https://github.com/Harsh24081990/azure/blob/main/Reconciliation%20in%20ADF.md

	l while working with the dataframes, one table is giving skewing data after each monthly load ? how would you fix it in pyspark ?
	Ans : Salting, Repartitioning, Bucketing, Skew Hints. 
	https://github.com/Harsh24081990/spark/blob/main/Handle_skewed_data.md

	l Partition by, cumulative sum, monthly sum using pyspark code ?
	https://github.com/Harsh24081990/PySpark/blob/main/sales_data_analysis.md

	l AVRO file format V/S Parquet file format ?
	https://github.com/Harsh24081990/Misc/blob/main/avro_vs_parquet.md
	Read : File Formats page in MISC Topics section. 

	l Have you created any custom activity in ADF ?
	Create the Custom Activity in ADF:
		• In the Azure Data Factory portal:
			○ Go to the Author section.
			○ Create a new pipeline.
			○ Add a Custom Activity from the activities pane.
			○ Configure the custom activity:
				§ For Azure Batch, specify the Azure Batch linked service, the pool, and the job settings.
				§ For Azure Functions, specify the function app and the function details.
	
	(we can give example of creating python script for reading the error log file and if error rows are present then send the notification mail ) (another example might be creating a cleanup script)
	https://github.com/Harsh24081990/azure/blob/main/ADF_performance_day2day_work.md#example-3-have-you-used-custom-activity-

	l What performance optimization activities you have worked on in ADF and in Data bricks ?
	ADF --> https://github.com/Harsh24081990/azure/blob/main/ADF_performance_day2day_work.md
	Databricks --> 
	https://github.com/Harsh24081990/databricks/blob/main/long%20running%20jobs.md
	        
	l Integration Run Time ?
	l Onprem to cloud, db migration ?
	l How to restrict access to various users to access azure portal ?
	https://github.com/Harsh24081990/azure/blob/main/user_access_control.md
	
	l What is IAAS, PAAS, SAAS ?
	https://github.com/Harsh24081990/Misc/blob/main/IAAS_PAAS_SAAS.md
	l Auto loader in databricks?
	spark.readStream
      .format("cloudFiles")
	---------------------------
	df.writeStream
          .format("delta")
	
	https://github.com/Harsh24081990/databricks/blob/main/AutoLoader.md
	
==============================================================

5.######## Deloitte ###### 25-Oct-2024

Have you used event hubs, stream analytics, HD insights etc. ??
Need to study from YouTube. 
In short:-
	• Event Hubs: A real-time data ingestion service to collect and stream millions of events per second (like Kafka in Azure).
	• Stream Analytics: A real-time analytics engine to process streaming data from sources like Event Hubs or IoT Hub using SQL-like queries.
	• HDInsight: A cloud service to run open-source big data frameworks like Hadoop, Spark, Hive, and Kafka on Azure-managed clusters.

======================================================

6.######## Ahvi Infotech ###### 25-Oct-2024
Normal Questions only. 

======================================================

7.######## Xebia ############## 02-Nov-2024
What will happen just next to this df.persist()
	1. Data will get persisted and loaded to memory
	2. Data will get persisted and loaded to disk
	3. Nothing
	
Ans : When you call df.persist() in PySpark or Databricks:
	• It does not immediately persist the data or load it into memory or disk.
	• Instead, it marks the DataFrame to be persisted later, based on the specified storage level (by default: MEMORY_AND_DISK).
	• The actual persistence only happens when an action is performed on the DataFrame — such as:
		○ .count()
		○ .collect()
		○ .show()
		○ .write(), etc.
--------------------------
Python
input                        
a = ['cat', 'act', 'god', 'dog', 'tca']                
output                     
{'act': [1, 2, 5], 'dgo': [3, 4]}
--------------------------
PySpark
input
a,b
c
d
e,f
g
output

a
b
c
d
e
f
g
--------------------------------
-- Difference between logical and physical plan in spark architecture ?
https://github.com/Harsh24081990/spark/blob/main/spark_terminologies.md#logical-execution-plan-vs-physical-execution-plan

--If driver is getting out of memory error suddenly on some peak business day ? what would you do ? --If executers are giving out of memory error ?
https://github.com/Harsh24081990/SPARK/blob/main/Out_Of_Mem_Issue.md

--Real time streaming have you worked on ? EventHub/Kafka
--what if Kafka stopped sending message suddenly ?
Azure Notes - Page 29

-- In an incremental load table, how would you update an old date values ? if the date is a partitioned column can you directly update the rows of some particular old date without deleting it ? can you overwrite partitioned column ?
https://github.com/Harsh24081990/SPARK/blob/main/update_old_values_in_incremental_load.md

-- have you used SFTP as source dataset in ADF ? what IR you will use if source is SFTP ?
https://github.com/Harsh24081990/AZURE/blob/main/SFTP_as_source_in_ADF.md

-- used default broadcasting then what is the size of your worker node ?
https://github.com/Harsh24081990/SPARK/blob/main/broadcast_size.md
==========================================================================

8.########## ZS associates ############ 08-Nov-2024

	- Explain project with medallion architecture in very detail.
	- what is DMS project mentioned in your resume.
	- what performance optimization you have worked on mentioned in resume ?
	- SQL - Dense Rank, Rank, rownumber, 3rd highest salary, empnames with same salary (display names separated by , )
	- what is COALESCE and not null function in SQL ?
	- If there are repeated logic you are writing in databricks cells, are you writing again and again the same logic for the multiple source tables ? 
	What is the ideal way to do it ?
	https://github.com/Harsh24081990/PySpark/blob/main/reusable_function.md
	
	- Have you used configuration file based setup to develop a more generic code?
	- If there are repeated logic you are writing in databricks cells, are you writing again and again the same logic for the multiple source tables ? 
	What is the ideal way to do it ?
	- Have you used configuration file based setup to develop a more generic code?
	
==========================================================================

9.####### Cognizant ######## 07-Dec-2024

	- What happens when you give infer schema = True while creating dataframe?
	- What is the exceptions you have handled while writing pyspark code ?
	- Spark optimization, Spark job execution steps ?
	- Why parquet format have less size than csv for the same file ?
	- How you handle access management while connecting to various sources ?
	- --------------------------------------------
	- Write a pyspark code to connect with some sql server db ?
	
	```
	CREATE TABLE
	USING JDBC
	OPTIONS (
	    url = "jdbc:{databaseServerType}://{jdbcHostname}:{jdbcPort}",
	    dbtable = "{jdbcDatabase}.table",
	    user = "{jdbcUsername}",
	    password = "{jdbcPassword}"
	)
	```
	- ---------------------------------------------
	- What are the actions and transformations you have used ?
	- what are escape characters and how to remove them while creating dataframe in pyspark ?
	https://github.com/Harsh24081990/PySpark/blob/main/escape_characters_handling.md
	- what is data size in your project ? what is the cluster size in your project ?
	- what version of spark / python you are using in your project ?
	Python ---> version 3.13
	Spark -----> version 3.5.1
	
==========================================================================

10.####### Gainwell ########## 10-Dec-2024
Q: in pyspark
bp_range
78/121
66/140
110/114
in pyspark, create 2 columns - low_bp and high_bp to mention these values.

Using PySpark :
```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import split, col

# Create a Spark session
spark = SparkSession.builder.appName("BP_Range_Split").getOrCreate()

# Sample Data
data = [("78/121",), ("66/140",), ("110/114",)]
columns = ["bp_range"]

# Create DataFrame
df = spark.createDataFrame(data, columns)

# Split the 'bp_range' column into two columns 'low_bp' and 'high_bp'
df_with_bp = df.withColumn("low_bp", split(col("bp_range"), "/")[0].cast("int")) \
               .withColumn("high_bp", split(col("bp_range"), "/")[1].cast("int"))

# Show the result
df_with_bp.show()
```

Another pyspark way :
```
df2 = df.select(
    col("bp_range"),
    split(col("bp_range"), "/")[0].alias("low_bp"),   # New column
    split(col("bp_range"), "/")[1].alias("high_bp")   # New column
)
```
Using SQL way :
```
SELECT
  bp_range,
  split(bp_range, '/')[0] AS low_bp,
  split(bp_range, '/')[1] AS high_bp
FROM bp_data
```
Note: Split function is directly available in PostgreSQL and PySparkSQL
--------------------------------------------------------------------------------------------
Q: in python - write a function to square a int by getting value from user
```python
def square_number():
    try:
        # Get input from the user and try to convert it to an integer
        num = int(input("Enter an integer: "))
        
        # Calculate the square of the number
        result = num ** 2
        
        # Return the result
        return result

    except ValueError:
        # Handle the case where the input is not a valid integer
        return "Error: Please enter a valid integer."

# Call the function and print the result
print(f"The square of the number is: {square_number()}")
```
==========================================================================

11.########### Inxite-out  ########## 10-Dec-2024
Q: there is a customer and order table. 
file1 = customre.csv  -- id, name , gender , joiningdate
file2 = order.csv  -- customer_id, orderid, order_date , order_date
write a query:
==> to know the customer who have never placed any orders.
```sql
SELECT c.id, c.name
FROM customer c
LEFT JOIN orders o ON c.id = o.customer_id
WHERE o.customer_id IS NULL;
```
-------------------------------------------------------
==> to know the customer who have never placed any orders in the first 90 days of their joining. 
```sql
SELECT c.id, c.name
FROM customer c
LEFT JOIN orders o 
  ON c.id = o.customer_id 
  AND o.order_date <= DATEADD(DAY, 90, c.joiningdate)
WHERE o.customer_id IS NULL;
```
-----------------------------------------------------------------
==> using Pyspark
```python
from pyspark.sql import SparkSession
from pyspark.sql.functions import col

# Create a Spark session
spark = SparkSession.builder.appName("FindCustomersWithNoOrders").getOrCreate()

# Load customer and orders data into DataFrames
customers_df = spark.read.option("header", "true").csv("customer.csv")
orders_df = spark.read.option("header", "true").csv("orders.csv")

# Perform a LEFT JOIN on the customer_id and filter for customers with no orders
customers_with_no_orders_df = customers_df.join(orders_df, customers_df.id == orders_df.customer_id, "left") \
    .filter(col("orders_df.customer_id").isNull()) \
    .select(customers_df.id, customers_df.name)

# Show the result
customers_with_no_orders_df.show()
```
==========================================================================

12.########### Cognizant  ########## 12-Dec-2024
Q: how to load a excel file with 3 sheets a, b, c into ADLS location as 3 separate files as a.csv, b.csv and c.csv using azure data factory ? 
Ans:
Step 1 :    While creating the source dataset (Blob --> File format: Excel), 
		Parameters tab => create a DS parameter named ds_param_filename
		Connection tab => worksheet mode : "Name" (Other option is "Index")
						Sheet name : (Add dynamic content) : @dataset().ds_param_filename
						
Step 2 :    Do same for sink dataset  (Blob --> File format: CSV), 
		Parameters tab => create a DS parameter named ds_param_filename
		Connection tab => File name : (Add dynamic content) :
					   @concat(dataset().ds_param_filename, 'csv')
		
Step 3:  Create a Pipeline --> ForEach Activity --> Setting --> Items --> (Add dynamic content) --> use @createArray function inside 'Add dynamic content'
@createArray('Sheet1', 'Sheet2', 'Sheet3')

Step 4:  Go inside ForEach activity --> Copy Activity --> select source and sink datasets in 'source' and 'sink' tabs.
--> in source dataset properties:-
ds_param_filename = (add dynamic content) @item()
(Do same for the sink as well)

Step 5 : Run the pipeline. 

https://github.com/Harsh24081990/azure/blob/main/Excel_to_CSV_using_ADF.md

how to do the same using pyspark code ?
Ans : 
Using pandas - which is a Python library. 
Using spark-excel - which is a JVM based library. 
https://github.com/Harsh24081990/databricks/blob/main/read_excel_file.md

Q: how to load data incrementally in a table ? for example if an employee's salary is revised and the new data is coming from a source file so we need to just update the salary in target table and don't need to insert the same employee details again. Do it in SQL and pyspark df way. 
ANS : SDC TYPE 1


Q: If we need to also keep the old salary record and mark the row as 'old' and new salary record as 'new', how to do it in SQL and in pyspark df ?
ANS : SCD Type 2
================================================================

13.########### Cognizant  ########## 26-April-2025
QUE : Read the csv file in a dataframe skipping the garbage lines at the top if there are any. 
#csv file
line1
line2
line3
id,name,age,gender
1,Harsh,22,M
2,Happy,33,M
3,Payal,32,F
ANS:
```
%fs head /FileStore/data/myfile.csv
```
	• This will print the first 1 KB of the file so you can manually count how many lines appear before the actual column headers.

# Read CSV into DataFrame
```
# Read CSV while skipping first 3 lines
df = spark.read.format("csv") \
    .option("skipRows", 3) \                   # skip first 3 lines
    .option("header", "true") \               # use the 4th line as header
    .option("inferSchema", "true") \     # infer column types
    .load("/dbfs/FileStore/data/myfile.csv")

# Show the DataFrame
df.show()
```
Important:
	• skipRows is available in Spark 3.2+. Make sure your Databricks cluster is using a compatible runtime (e.g., 10.x or higher).
	• You must still include header = true if the actual header is on the 4th line.
--------------------------
QUE: For Walmart warehouse design 3 tables. 
Items_table, city_table, state_table.
What is ERD, how these 3 tables will be connected to each other ?
============================================================

14.########### CapGemini  ########## 10-May-2025
	1. Project explanation.
	2. performance optimization of spark job.
	3. Tough scenario you have faced in your project. 
	4. Any custom functions you have used (for reusability of the code)

==========================================================================

15.########### CapGemini  ########## 17-May-2025
	1. sql - how may rows with all joins ? including null values. 
	Table A
	ID
	9
	6
	6
	2
	null
	 
	Table B
	ID
	2
	2
	9
	null
	null

	2. in spark dataframe solve the following problem :-
	compare each date price with previous date price and create the price_change column accordingly. 
	
 
ANS : 
using SQL --> https://github.com/Harsh24081990/sql/blob/main/compare_previous_row.md

using pySpark --> 



	3. Remove the special character using pyspark (Regexreplace) and using sql also. 
	Input - Harsh@123#
	Output - Harsh123
	Ans : use regexp_replace function
	
	from pyspark.sql.functions import regexp_replace
	df = spark.createDataFrame([("Harsh@123#",)], ["input"])
	df_clean = df.withColumn("output", regexp_replace("input", "[^a-zA-Z0-9]", "")) 
--> In input string find (which is not in a to z, A to Z and 0 to 9) and replace it with blank " "
	df_clean.show()
	
	Input - Harsh@123#
	Output - Harsh@123
	
	from pyspark.sql.functions import regexp_replace
	df = spark.createDataFrame([("Harsh@123#",)], ["input"])
	df_clean = df.withColumn("output", regexp_replace("input", "#", "")) 
--> in input string find # and replace with blank. 
	df_clean.show()
	

	4. In ADF, there is a ADLS container and inside it multiple CSV files are presnet in INPUTDATA folder. each file have different sizes.. give the steps to create a pipeline to copy the only files which are less than 10 MB.
https://github.com/Harsh24081990/azure/blob/main/copy_selected_files.md

	5. When your source file schema is changing frequently, how to handle this scenario in pyspark code using databricks ?
==========================================================================

16.########### Hexaware Technologies ########## 04-June-2025

	1. good morning Harsh, How are you today ? --> how to reverse this in python and pyspark ?
	2. a = 1,2,3,4,5 --> what datatype is this in python ?
	3. how to print just 3 form this a ?
	4. when to use partition and when to use bucketing ?
	5. what is the difference between parquet and delta format ? when to use what ? which one is faster for read/write and which one is faster for updating the data ? 
	6. does the new files created while updating the data or existing files gets updated ?
	7. Five Vs of BIg data ?
	8. Different types of data warehouse ? 
	9. what is difference in data warehouse and data lake house ?
==========================================================================

17.################ Coforge ##########################

	1. which cluster manager you are using ?
	2. if there are 100 tables in onprem db and want to copy only few (30) tables using ADF ? how we can do it ?
	3. if a spark job is taking huge amount of time, code is already tuned and basic performance optimization of the spark job is done. How to fix the issue without changing the cluster configuration like driver or executor memory ?
	4. How you handle schema evolution in your project ?
==========================================================================

18.########### Capco ########## 07-July-2025
	1. You have a DataFrame "sensor_data":
	sensor_id (string)
	timestamp (timestamp)
	temperature (double)
	
	The data may have missing temperature readings. Fill missing temperature values with the last known temperature per sensor (forward fill). Solve this using pyspark. 
	
	Ans : https://github.com/Harsh24081990/PySpark_Coding_Interview_Questions/blob/main/ForwardFill_MissingValues.py
	
	2. Account
	customer_id, account_id, status
	c1, a1, O
	c1, a2, C
	c2, a3, C
	c2, a4, C
	c3, a5, C
	.....
	.....
	Provide list of customers with all closed accounts , using pyspark.
	
	3. When to use parquet and when to use AVRO file format ?
==========================================================================

19.########### Wipro ########## 16-July-2025

	1. core difference between relational sql and BQ ? in term of storage and usages. 
	2. What is difference between Spark and PySpark ?
	3. main purpose of having unity catalog in databricks ?
	4. core difference between data warehouse and data lake ?
	5. what is z-ordering ? why we use Optimize ?
	6. what is Vacuum command used for in databricks ?
	7. Remove duplicate using window functions ?
	ID END-DT
	1 01/01/99
	1 01/01/25
	2 null
	2 02/01/24
	3 null
	
	8. I want total distance covered by each train between chennai to delhi. Solve using SQL and Pyspark df. 
	Input: 
	Source_city 	Dest_city 	Distance 	Train 
	Chennai 	Nagpur 	15000 	A 
	Nagpur 	Delhi 		12000 	A 
	Chennai 	UP 		17000 	B 
	UP 		Delhi 		6000 		B
	 
	output: ------- 
	Source_City   Dest_City   Train   Distance 
	Chennai         Delhi            A          27000 
	Chennai         Delhi            B          23000

	9. Which runtime you are using in databricks ?
	Ans : 
	Databricks Runtime 14.x
	Latest LTS (Long-Term Support): Databricks Runtime 14.3 LTS
	Base Apache Spark version: Spark 3.5.0
	10. How to handle schema evolution while working with spark in databricks ?
	11. What are the type of clusters you create in databricks ?
	Ans: 
	l All-purpose Cluster --> Development and interactive work. Always on but can be turned off manually. 
	l Job Cluster --> For production/Scheduled work. Automatically turns up when the job runs. 
==========================================================================

20.########### Deutsche Bank ########## 18-July-2025

	1. in python count the occurrence of numbers in the given list.
	input:-
	[2,3,2,1,1,2,4,5,6,2]
	output:-
	2 : 4
	3 : 1
	4 : 1
	
	
	2. Gsutil cp gs://dataprocessing/corporate_businessfiles/datefolder/*.csv 
	In the given GCP command, how to copy files in parallel to increase the performance of copy as there are huge number of CSV files. 

	3. Write a query which lists Items which are never get purchased.
	customer
	---------+-------+-------------------+          
	cust_id   | name  | contact_number  |      
	---------+-------+-------------------+ 
	Product
	-----------+----+---------------+---------          
	Product_id |name|Description    |Stock   |  
	-----------+----+---------------+--------- 
	Order
	-----------+-----------+----------------------+--------------------+------+--------+          
	Sr_No       | Order_id   |Cust_id|Product_id     |Transaction_date   | Rate  | Amount |  
	----------+-----------+-----------------------+-------------------+-------+---------+
	
	4. What is the schema changes required in order to migrate all three table into single one in BQ.(In new schema data should not be duplicated)
==========================================================================
	
21. ########### InfoBeans ########## 18-July-2025
	1. Que: Find the total active time in hours for each users. 
	data = [
	   ('c001', 1, '07:00:00'),
	   ('c001', 0, '09:30:00'),
	   ('c001', 1, '12:00:00'),
	   ('c001', 0, '14:30:00'),
	   ('c002', 1, '08:00:00'),
	   ('c002', 0, '09:30:00'),
	   ('c002', 1, '11:00:00'),
	   ('c002', 0, '12:30:00'),
	   ('c002', 1, '15:00:00'),
	   ('c002', 0, '16:30:00'),
	   ('c003', 1, '09:00:00'),
	   ('c003', 0, '10:30:00'),
	   ('c004', 1, '10:00:00'),
	   ('c004', 0, '10:30:00'),
	   ('c004', 1, '14:00:00'),
	   ('c004', 0, '15:30:00'),
	   ('c005', 1, '10:00:00'),
	   ('c005', 0, '14:30:00'),
	   ('c005', 1, '15:30:00'),
	   ('c005', 0, '18:30:00')
	]
	
	columns = ["cust_id", "state", "timestamp"]
	
	output:
	+-------+--------------------
	|cust_id|total_active_hours|
	+-------++------------------
	|   c001|               5.0|
	|   c002|               4.5|
	|   c003|               1.5|
	|   c004|               2.0|
	|   c005|               7.5|
	+-------+-------------------

	2. Q: Write a python function to find out the uses more than 18 years and currently active. 
users = [
   {"name": "John", "age": 17, "email": "john@example.com", "active": True},
   {"name": "Sara", "age": 21, "email": "sara@example.com", "active": True},
   {"name": "Bob", "age": 25, "email": "bob@example.com", "active": False},
]

	3. What is the difference between schema evolution and schema enforcement ?
	4. How to handle the situation if a file has arrived late (after the time to run your next job?) in ADF, how you would manage this situation to avoid any data loss or any duplicate issue in the target ?
==========================================================================

22. ########### KANINI ########## 18-July-2025

	1. print every 10th element using python.
	list = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]
	
	2. How to do rollback in case ADF pipeline fails in between ?
	3. what is databricks asset bundle (used for deployment) ?
	4. what is dead lock in SQL ?
	5. what is difference between parquet and delta lake format?
	6. How to implement SCD type2 in ADF ?
	7. Difference between repartitioning and Coalesce in spark ?
	8. What is auto loader in databricks ?
	9. what is shallow cloning and deep cloning in databricks ?
	https://github.com/Harsh24081990/databricks/blob/main/Deep_Vs_Shallow_clone.md
==========================================================================

23. ########### Persistent systems ########## 23-July-2025

Q: Spark architecture ? what happens when submitting spark job ?

Q: What is the steps you would take while you get Out of memory exception error while executing any spark job ?
https://github.com/Harsh24081990/spark/blob/main/Out_Of_Mem_Issue.md

Q: what will the result of append and extend in python ?
list1 = [1, 2, 3, 4, 5]
list2 = [3, 4, 5, 6, 7]
Ans: 
list1 = [1, 2, 3, 4, 5]
list2 = [3, 4, 5, 6, 7]

list1.append(list2)
print (list1)
Output: 
[1, 2, 3, 4, 5, [3, 4, 5, 6, 7]]

list3 = [1, 2, 3, 4, 5]
list4 = [3, 4, 5, 6, 7]
list3.extend(list4)
print (list3)
Output: 
[1, 2, 3, 4, 5, 3, 4, 5, 6, 7]

Q: string = "Hello"
How to find out the number of vowels in the given string ?
Ans :
string = "Hello"
vowels = "a,e,i,o,u,A,E,I,O,U"

count = 0

for i in string:
    if i in vowels:
        count = count + 1

print (count)


Q: what will the count of inner, left , right and full outer join in sql ?
Table X:
ID
10	  
20	  
30
40
NULL	  
 
Table Y:
ID
10	  
30	  
50
NULL
NULL
==========================================================================

24. ########### Hexaware ########## 26-July-2025

Q: if there is one json file having more than 500 lines of code, write a pyspark code to read the data from that file and create a dataframe. 
https://github.com/Harsh24081990/miscellaneous/blob/main/json_file_format.md

Q: If there are multiple json files present in a folder in ADLS location. write a pyspark code to read all the files to create a dataframe ?
https://github.com/Harsh24081990/miscellaneous/blob/main/json_file_format.md

Q: there are multiple folders in a ADLS containers. having multiple files in each folders.
How to create ADF pipeline for copying all the folders files based on some conditions. For example if conditon1 is satisfied then only copy the file from folder1, if condition 2 is satisfied then only copy from folder2 etc.. Write the steps /activities to achieve this using a single ADF pipeline. 
https://github.com/Harsh24081990/azure/blob/main/ADF_loading_multiple_folders_files.md

Q: difference between repartition and coalesce. 
https://github.com/Harsh24081990/spark/blob/main/Repartition_vs_coalesce.md

Q: syntax for broadcast join ?
Check 'Broadcasting' page in 'Spark' Section. 
from pyspark.sql.functions import broadcast
result_df = large_df.join(broadcast(small_df), large_df.id == small_df.id, "left")
or use
spark.conf.set("spark.sql.autoBroadcastJoinThreshold", 104857600)  # 100 MB 
(Default auto-broadcast size is 10 MB)

Q: Wide and narrow transformation with examples ? is count wide or narrow transformation ?
https://github.com/Harsh24081990/spark/blob/main/Wide_Vs_Narrow_Transformation.md

Q: How many types of join available in PySpark ? what is leftsemi join and leftanti join in spark ?
https://github.com/Harsh24081990/spark/blob/main/Joins_in_spark.md

Q: while running spark job there were 8 jobs created, out of which 6 completed very fast and 2 were taking exceptionally long time to finish. what might be the reason for these 2 jobs running log ? How to identify the reason and how to fix it ?

Q: If you have 25 GB of file how will you decide the number of partitions should be created to process the file efficiently ?
Ans: 
Rule of Thumb for Partitioning:
1 partition ≈ 128 MB (default block size in HDFS and optimal for most jobs)

Q: How to convert a given table into a dataframe in databricks, for converting the given sql query into pyspark code ?

Method	Use Case	Syntax Example
spark.table()	Load existing table from catalog/metastore	df = spark.table("mydb.my_table")
spark.sql()	Run SQL query and get DataFrame	df = spark.sql("SELECT * FROM my_table")
spark.createDataFrame()	Create DF from Python objects (list, dict)	df = spark.createDataFrame([("A", 1), ("B", 2)], ["name", "id"])
https://github.com/Harsh24081990/databricks/blob/main/running_SQL_in_databricks.md

Q: columns --> store_name, store_id, sales, year.
How to calculate the cumulative sum year wise for each store ?

Q: count of inner and full outer join col1 -- 2,2 col2 --2,2,2,2
Ans: inner:8 , left: 8 , right: 8, full: 8, left_semi: 2, left_anti: 0 
Notes: 
	1. Trick for full outer join --> inner join count + unmatched left table rows + unmatched right table rows.
	2. Null doesn't match and counted in case of inner join. But in left and right join NULLs will be present as it is in the output. similarly for Full outer join Nulls from both the tables will be presented as 'unmatched rows from left' + 'unmatched rows from right'.

Q: how to fetch the previous row of a table with respect to the current row ? explain with syntax ?

Q: what is first and last function used for ? explain in context of sql and pyspark. 
Q: what is the difference between Union and Join ?
==========================================================================

25. ########### Impetus ########## 28-July-2025

Q: We want to migrate the legacy oracle table having petabytes of data, into databricks keeping in mind the following criteria:- First of all the complete data should get copied, then it should update the table in near real time incrementally using databricks. 
what tools or technologies you would choose ?
What are the steps you would take to achieve this requirement to setup a pipeline ? 

Q: if there are 2 huge table (Ex. Customers and Transaction_details). both are huge in size. If we want to join these tables what are the techniques you would use to avoid shuffling while doing the join operation in spark ?

Q: What is time travel in databricks ?

Q: What is meant by liquid cluster and liquid clustering ?

Q: How exactly a catalyst optimizer work ?

Q: There is table having various countries of data in country column and in some other columns PII data is there. we have following 2 requirements : 1. we want to restrict country specific data for the people of respective country only. 2. we want to give access column wise (to avoid exposing the PII column data) to different users based on their role. How to achieve this RBAC in databricks (by commands or any other fetcher available in databricks to achieve this?) 

Also how to achieve the same RBAC in ADF ? 

Q: What are the advanced fetchers you have used in databricks ? explain them in short. 

Q: Do the following using PySpark and SQL:-
input --> emp.csv
id,name
1,harsh shrivastava
2,amit
3,aditya sharma
 
output
1,Harsh Shrivastava
2,Amit
3.Aditya Sharma


Q: Find out the second max salary using PySpark and SQL:-
input --> emp.csvcsv
name,sal
amit,1000
aditya,2000
sunil,3000
 
output
aditya , 2000

Q: Find out emp and their manager using SQL and PySpark
emp_table
id,name,m_id
1,aditya,null
2,amit,1
3,sunil,2
 
output
emp_name,manager_name

Ans:
SELECT 
  e.name AS emp_name, 
  m.name AS manager_name
FROM emp_table e
LEFT JOIN emp_table m
ON e.m_id = m.id;


Q: Explain the CICD process you follow ?
==========================================================================

26. ########### UTS ########## 29-July-2025

Q: How to rename column name to remove special character in ADF and in pySpark ?  col#1 to --> col_1
Ans : Inside ADF Data flow's "Derived Column" activity, we can use regexp_replace function to change the column name to remove # from the column name. 
regexpReplace(col#1, '[^a-zA-Z0-9]', '_')
or simple 'rename' function also we can use:-
rename(col#1, 'col_1')

Q: What is difference between SetVariable and AppendVariable activity in ADF ? what are limitations ?
ANS:
• SetVariable:
	• Only Assigns a single new value.
	• Can’t be used inside ForEach loop for array-building logic.
• AppendVariable:
	• Adds a new value to an existing array
	• Works only with array-type variables.
	• Appends string elements only (no complex objects).
• Example:-
SetVariable → var1 = "India"  
AppendVariable → var2 = ["USA"] → Append "UK" → ["USA", "UK"]


Q: Types of triggers and Integration Run time in ADF ?
Ans: 
Triggers --> Scheduled, Tumbling Window, Event Based, Manual. 
IRs --> AutoResolved, Azure, Self-Hosted, SSIS

Q: What are the activities you have used in ADF ? 

Q: What are the values you can get using getMetaData activity ?

Q: if there are 100 tables in source how to fetch them to optimize the overall pipeline run time ? In ForEach activity how many jobs can run in parallel ? 

Lookup -->  [ ForEach ---> Copy ]
inside Lookup activity use below sql query (If fetching form onprem sql server db)
SELECT table_name FROM information_schema.tables WHERE table_type = 'BASE TABLE'
---------------------------------------------------------------------------------------------------------
The default Batch Count in ForEach activity in ADF is 20
IsSequential = true --> This will ignore Batch count
• Use IsSequential = true when order matters.
• Use Batch Count = 1 when order doesn’t matter, but you want to throttle concurrency.
--------------------------------------------------------------------------------------

Q: What is difference between Blob and Data Lake Storage ?

Q: What are the fetchers of Delta Lake in databricks ?
https://github.com/Harsh24081990/databricks/blob/main/Delta_Lake_Format_Fetchers.md

Q: Schema enforcement Vs Schema evolution ?
Ans : Delta Lake automatically enforces schema when writing data. If incoming data doesn't match the table's schema, it throws an error.
df.write.format("delta").mode("append").save("/mnt/delta/sales")
-------------------------------------
To Allow Schema Evolution (optional) use .option as below :-
df.write.format("delta") \
  .option("mergeSchema", "true") \
  .mode("overwrite") \
  .save("/mnt/delta/sales")
-------
or define it at configuration level:-
spark.conf.set("spark.databricks.delta.schema.autoMerge.enabled", "true")
---------------------------------------------------------------------------------------------

Q: What is the difference between Parquet and delta lake ?

Q: What are the features of Unity Catalog in databricks ?
https://github.com/Harsh24081990/databricks/blob/main/unity_catalog.md

Q: How to identify and fix the data skewness issue in spark ?

Q: If there is no column names mentioned in a CSV file ? how you will create the column names while creating a dataframe using that file using databricks ? and also using ADF ?

In databricks:-
from pyspark.sql.types import StructType, StructField, StringType, IntegerType
Use --> header=False and use StructType and StructField or normal sql way to define the schema. 
----------------
In ADF:- 
Use --> In dataset -- Uncheck First row as header.
Define column names manually in the dataset schema (Column1, Column2, etc.)
-------------------------------------------

Q: Calculate the daily running total for each category using SQL:-
Table: SALES
sale_id (int)
category (varchar)
sale_date (date)
amount (decimal)

(1,"Electronics", "2024-04-01", 100),
(2,"Electronics", "2024-04-03", 150),
(3,"Electronics", "2024-04-05", 200),
(4,"Clothing", "2024-04-01", 50),
(5,"Clothing", "2024-04-04", 100)

Ans :
SELECT
  category,
  sale_date,
  amount,
  SUM(amount) OVER (
    PARTITION BY category
    ORDER BY sale_date
    ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW -- only needed in some dbs
  ) AS running_total
FROM SALES;



Q: Using pySpark and python do the following :-
Input: ["hello world", "apache spark", "map vs flatmap"]
Output: [['hello', 'world'], ['apache', 'spark'], ['map', 'vs', 'flatmap']]

PySpark:-
df_result = df.withColumn("words", split("text", " ")).select("words")
df_result.show
---------------------------
Python:-
way1:
input_list = ["hello world", "apache spark", "map vs flatmap"]
output = [x.split() for x in input_list]
print(output)
-----------------------
way2:
input_list = ["hello world", "apache spark", "map vs flatmap"]
output = []
for x in input_list: 
    words = x.split()
    output.append(words)
print(output)
------------------------------------------------------------------------------------------

Q: Using PySpark and Python do the following :-
input: [1,2,3,4]
output: [1,4,9,16]

Ans:
PySpark:-
df_squared = df.withColumn("squared", col("num") ** 2)
df_squared.show()
--------------------------------
Python:-
way1:
input_list = [1, 2, 3, 4]
output = [x**2 for x in input_list]
print(output)

way2:
input_list = [1, 2, 3, 4]
output = []
for number in input_list:
    square = number ** 2
    output.append(square)
print(output)


Q: Using PySpark and Python do the following :-
input: 'a|b|string', 'c|int'
output: 'a|b' 'string' , 'c' 'int'

==========================================================================

27. ########### Hinduja ########## 30-July-2025

QUE: what is meant by data governance in databricks ? how it is done ?
ANS: Data Governance in Databricks refers to managing data availability, usability, integrity, and security across the platform, ensuring the right people access the right data under the right conditions.
	Unity Catalog (core governance tool):
		○ Centralized metadata and data access control.
		○ Fine-grained permissions at table, column, row levels.
		○ Manages users, groups, and service principals.
----------------------------------------------------------------
QUE: How to maintain data quality, schema enforcement, schema evolution and failure case scenario in ADF ?

QUE: If we are following medallion architecture in a ADF - databricks setup. and we want to do the partitioning on the data files coming from the source, on which layer we should do the partitioning and how it is done ?

QUE: Find out using SQL 1. total_sales_amount 2. Second highest total sales amount 3. second highest total sales amount in each category ?
table name --> sales_order
columns --> order_id, order_date, emp_id, product_category, amount
==========================================================================

28. ########### Impetus (Round 2) ########## 30-July-2025

QUE: What are materialized view, when it is needed and must to use, give any practical example where you have used in your career ?
https://github.com/Harsh24081990/SQL_DB_Concepts/blob/main/Materialized_View.md

QUE: what are the normal forms generally implemented in a project using ADF and Databricks , while designing the tables ? How to model a schema and how to decide the normalization we should follow ?
https://github.com/Harsh24081990/Data_Modeling/tree/main

QUE: What is delta live table in databricks, it's use and how to create delta live table (with syntax) ?

QUE: What are the string functions you have used, both in SQL and in PySpark ? List all. 
https://github.com/Harsh24081990/sql/blob/main/common_string_functions.md

QUE:  Find out all the employees which have "an" in name. 
Table:Emp
COl:Name
Ankita
Pavan
Ankit
Nayan
Impetus
Vishal
jeevan
manish

ANS:
SELECT Name
FROM Emp
WHERE LOWER(Name) LIKE '%an%';

 
QUE: what is the exact output of this query ?
T1
C1
1
null
1
null
1
 
Select CASE 
	WHEN NULL=NULL THEN "Harsh" 
	ELSE "Impetus" END FROM T1;


QUE: Find out the duplicate without using duplicate keyword ?
T1
C1
1
2
9
0
1
2
9

ANS: 
SELECT C1
FROM T1
GROUP BY C1;
==========================================================================

29. ########### Wipro ########## 31-July-2025

QUE: What is meant by data pane in databricks ?
ANS: It is a term which refers to the "Data" tab available in the left side panel in the databricks UI. Used for Browsing tables, schemas, volumes, file systems (DBFS, Unity Catalog or Hive Metastore).
We can Browse and Explore:
	• Databases and tables (Hive Metastore or Unity Catalog).
	• Volumes, files in DBFS or external locations (ADLS, S3).
	• Schemas, columns, sample data. -->"Preview Table" (eye icon) — click it.
----------------------------------------------------------------------------------

QUE: What are type of clusters in databricks ? which one you have used and when ?
Cluster Type	Purpose
All-purpose cluster	For interactive analysis, ad-hoc notebooks, development work.
Job cluster	Auto-created by Databricks to run a specific job or workflow; auto-terminates.
SQL warehouse	Optimized compute for executing SQL queries and dashboards.
DLT cluster(managed)/	Used internally by Delta Live Tables pipelines. Not manually created.
workflows

QUE: How we can access the databricks clusters details which we have created, using azure CLI ?
ANS: 
Need to use Databrick PAT (Personal Access Token)
and use it in the curl command in azure CLI. (curl -X GET) command
https://github.com/Harsh24081990/databricks/blob/main/Get_Cluster_Details.md

QUE: What is meant by Schema in context of Informatica, Oracle, SQL server and Databricks ?

QUE: what is dynamic and scripted pipelines in Azure DevOps ?
https://github.com/Harsh24081990/azure/blob/main/Azure_devOps_Pipelines_types.md
==========================================================================

30. ########### Wipro ########## 1-Aug-2025

QUE: Get top selling product per region
Output --> region, product_id, product_name
Tables:
Customer – cust_id, cust_name
Product – product_id, product_name, product_price
Order – cust_id, product_id, order_date, order_quantity, order_status, region

QUE: How to you handle failure case scenarios in Azure Data Factory ?

QUE: How do you remove duplicates and NULL values in databricks using SQL and using PySpark ?
==========================================================================

31. ########### NCS ########## 1-Aug-2025

QUE: Write a query to find out the Nth highest salay from emp table.
emp table --> emp_id, sal

QUE: The count of inner ,left ,right and full outer and cross join for the below tables ?
colA	colB
1		1
1		2
2		null
3		3
null	           4
5		null
6		7

OUE: student table -->  student_id, attendence, date   
Attendence column will have 'PRESENT' and 'ABSENT' values only. 	 
Write a sql query to find out how many time any student was absent for 3 consecutive days.  
output --> student_id, consecutive_absent_day_count

QUE: Can databricks unity catalog overwrite the RBAC of azure user ? I mean if the user doesn't have access to the databricks workspace, can the unity catalog provide that user the access to one of the table present in the databrics ?

QUE: What is the difference between data warehouse and data lake and data lakehouse ?
==========================================================================

32. ########### Merkle (Dentsu) ########## 4-Aug-2025

QUE1: Do in python, pyspark , sql.
input string = INTERVIEW
output :-
E,0 = INT
E,1 = INTERVI
E,2 = Array out of bounds
I, 0 = Null
S,0 = Invalid entry
------------------------------
QUE2: Do it in sql.
SQL query to print the sum of n numbers. for example if number is 3. it should give 6 as result (3+2+1)
------------------------------
QUE: If there is a raw formatted data present in a CSV file. what will be your approach to create a table and load it keeping following points in mind:-
-- how to model the table structure ?
-- how to make sure it's ACID compliance ?
-- how to decide the normalization we should keep ?
-- how to decide the schema (start, snowflake etc.) ?
==========================================================================

33. ########### NCS (Round 2) ########## 8-Aug-2025
(Databricks to Delta Live Tables migration project at NCS Pune Phase1)

QUE: What will be the count of inner, left, right, full and cross join ?
Table1	Table2
1		1
1		1
1		2
2		2
2		2
3		4
NULL	NULL

QUE: 
input
+---+------+-----+
|pid|  date|price|
+---+------+-----+
|  1|26-May|  100|
|  1|27-May|  200|
|  1|28-May|  300|
|  2|29-May|  400|
|  3|30-May|  500|
|  3|31-May|  600|
+---+------+-----+
output
+---+------+-----+---------+
|pid|  date|price|new_price|
+---+------+-----+---------+
|  1|26-May|  100|      100|
|  1|27-May|  200|      300|
|  1|28-May|  300|      600|
|  2|29-May|  400|      400|
|  3|30-May|  500|      500|
|  3|31-May|  600|     1100|
+---+------+-----+---------+
Hint: For running total (Cumulative sum) we must do order by on date inside partition by clause. 
ANS:
select pid, date, price, sum(price) over(partition by pid order by date)
from product;
==========================================================================

34. ########### CGI (Round 1) ########## 8-Aug-2025

QUE: What is limitation of lookup and for each activity in ADF ?
QUE: Can we run a For each inside a for each activity ?
QUE: How to sue Azure monitor to setup failure alerts ?
QUE: What is the use of log analytics in ADF ?
QUE: What is difference between service principal and managed identity in Azure ?
QUE: How can we give row level, table level and column level access to specific users in data bricks ? how to restrict access to PII columns data ?
QUE: You have a large CSV (~200 GB) present in ADLS container with the following columns:-
order_id, customer_id, order_date, product_id, amount
Tasks:
1. Load it into a Delta table efficiently (handle schema inference, partitioning).
2. Optimize it for queries filtering on order_date and customer_id.
3. Write a query to find the top 5 customers by total spend in the last 90 days.
4. Show how you would compact small files in the Delta table.
QUE: If there are hundreds of tables present in onprem Postgress db and we want to copy them all to azure db, what should be the best approach to do that keeping in performance of the pipeline in mind ?

QUE: Suppose in a spark application there are 2 wide transformation and one action and handling 2 GB data. So, How many jobs, stages, task and Partitions will get created?
==========================================================================

35. ########### Optum Data Console ########## 9-Aug-2025

QUE : write sql to populate the end_date and it should be the one day prior to the start date of the next project. 
table --> project
project_id,     start_date,      end_date
1		01-01-2024
2		02-01-2025
3		05-02-2026

QUE : Do the same in PySpark as well using dataframes. 
==========================================================================

36. ################## EPAM ############# 10-Aug-2025

QUE : What are the type of indexes in SQL ?

QUE: customers, orders table. --> 
1. Find out the top 2 customer's name who placed maximum number of orders in last 3 months ? 
2. Find out the top 2 customer's name who placed maximum amount of orders in last 3 months ?

QUE: What is vacuum command in databricks ? what is default retention period of the files ?

QUE: What will be the result of select UNION and UNION ALL of these table ?
table1 --> col1 : 1,1,1,1,1
table2 --> col1: 1,1

QUE: What are different Panes in databricks architecture ? Explain databricks architecture. 
==========================================================================

37. ################ NTT DATA ################ 11 - Aug -2025

QUE: In Spark, what is core difference between partitioning and bucketing ? which one is better ?

QUE: If you are getting driver out of memory and in logs you can see lot of data spill related entries. what should be the approach to fix this without increasing the driver memory ?
Is there any use of checkpointing possible in performance improvement ? 

QUE: What is checkpoint in spark ? Why and how to use it ? Is it beneficial for performance ?
https://github.com/Harsh24081990/SPARK/blob/main/Checkpoint_usages.md

QUE: find customers who placed more than 3 orders in the last 6 months
orders(order_id, customer_id, order_date, total_amount) and 
customers(customer_id, customer_name, region)
Output-->  customer_id, customer_name, order_count, order_date

QUE: Features of Delta Live tables and Unity Catalog in databricks ? 
https://github.com/Harsh24081990/DATABRICKS/blob/main/Delta_Live_Tables.md

https://github.com/Harsh24081990/DATABRICKS/blob/main/unity_catalog.md


QUE: What is the role of catalyst optimizer in spark ?
https://github.com/Harsh24081990/DATABRICKS/blob/main/Catalyst_optimizer.md

QUE: Can we rollback delta table in databricks to one year older date ?
https://github.com/Harsh24081990/DATABRICKS/blob/main/Time_Travel_in_Delta_Tables.md
==========================================================================

38. ################ NTT DATA - Round 2 ################ 12 - Aug -2025

QUE: What is the toughest challenge you have faced recently in your project. Explain in detail at least 2 examples. 
==========================================================================

39. ############### Wipro L1 ############### 11-Aug-2025

QUE: Biggest files/source system you have in project, what is the size of that file ?

QUE: If only 8 million records are copied from your onprem sql server db to ADLS Gen2 landing zone container, how to find out and what is the action item you do ?

QUE: While working with huge file in databricks what are the performance measures you consider ?

QUE: In what scenario you would do Z-ordering in databricks ?
==========================================================================

40. ############### Altimetrik  ################ 12-Aug-2025

QUE: How we can run the spark job from AWS and from Azure Cloud platform ?

QUE: IF spark job is running for longer (stuck) and not failed, what will be your approach to solve this issue ?

QUE: If some bad data has been loaded into target table in databricks production environment, how you remove that data ?

QUE: SQL and PySpark coding Questions. 
https://nextleap.app/online-compiler/sql-programming
==========================================================================

41. ############### Wipro L2 ############### 13-Aug-2025

QUE: What should be the cluster configuration for processing 5 TB data in databricks ?
cluster type, RAM, number of nodes, executors, cores explain everything. 

QUE: What is cluster size in your project.

QUE: Explain end to end CICD process using azure devOps.

QUE: While fetching data from a huge onprem sql server table to Azure ADLS container in production environment, what are the steps involved ? How will you manage the authentication ? which authentication method you would use for connecting to your ADLS account ?
https://github.com/Harsh24081990/AZURE/blob/main/OnpremDB_to_ADLS_prod_setup.md

QUE: How would you do capacity planning for your project ?

QUE: SQL and pyspark questions.
==========================================================================

42. ############### Acuity ############### 13-Aug-2025 

QUE: databricks bitemporal ?

QUE: What is meant by outliers in databricks/ADF pipelines ? How do you handle it ?

QUE: SQL and Python question. 

QUE: How do you handle NULL values coming from source while loading in ADLS using ADF ? what do you do with those records ?

QUE: How do you handle Duplicate values coming from source while loading in ADLS using ADF ? what do you do with those records ?
==========================================================================

43. ############### Centricks ############### 14-Aug-2025 

	1. What is difference between varchar and nvarchar in sql ?
	2. What is difference between Delete and Truncate ? Why truncate if we can use delete from table without giving where condition ?
	ANS: TRUNCATE is faster for large tables because it doesn’t log every row deletion. Delete is DML and Truncate is DDL operation, but both can be rolled back if used inside a transaction and not committed. (Note: Oracle, you cannot rollback a TRUNCATE)
	3. What are the type of functions in sql ?
	4. What is the difference between functions and stored procedure in sql ?
	5. what is difference between clustered and non-clustered indexes in sql ? what are other types of indexes in sql ?
	6. Performance optimization techniques while writing sql or creating stored procedures
	7. SQL coding questions. 
==========================================================================

44. ############### Xebia ############### 14-Aug-2025

	1. Optimization you have used in databricks code ?
	2. How to design one to many relationship tables physically at db level ?
	3. How to handle duplicates values coming when joining 2 tables with many to many relationship ?
	4. SQL Questions.
	5. PySpark Question. 
==========================================================================

45. ###############  Synechron ############### 18-Aug-2025

	1. what is the optimization you have done in Integration Run Time side in ADF ?
	2. How to do incremental loading if there is no ID, Key or Timestamp related column in source table. what are the possible approaches you can think of ? (Tell for all, ADF and Databricks and in SQL.) 
	3. Design ADF pipeline to do Oracle db to azure sql db data migration. Consider incremental loading, partitioning, Fault tolerance, Alerting. Also If the pipeline fails in between a run and it loaded 700 out of 1000 records, it should restart from the 701th record and not from the beginning. 
	4. What is the data lineage in databricks, how you ever worked on it ?
	5. Difference between caching/persist, repartition/coalesce, partitioning/bucketing ?
	6. Types of Fact and Dimension table ?
	Dimensions --> Conformed, Junk, DD, Role Playing, SCD. 
	Facts --> Transactional, Periodic snapshot, Accumulating snapshot, Fact less. 
	
	7. Difference between fact and dim tables ?
	8. Difference between Data warehouse and Data Lakehouse ?
	9. Write SCD type 2 query in SQL Merge into statement. 
	10. PySpark code -- partitioned load in overwrite mode. 
	==========================================================================

46. ############### NTT DATA (Round-3) ############### 18-Aug-2025

QUE: Write a code using PySpark and SQL to read data from source file into raw_table then travel the data to bronze , silver and gold table using medallion architecture. 
How will you ensure that all the rows were processed in each layer ?

QUE: How have you managed security and access while sending and receiving data in/out of the HSBC firewall in your external data pattern project mentioned in your resume ?
==========================================================================

47. ############### NTT DATA (Round-4) ############### 19-Aug-2025

QUE: If you are running a VACCUM command on a table which was created and loaded 7 days before and no changes or updates on that table after that, what will happen to that file ?
QUE: If we use ---> VACUUM table_name RETAIN 0 HOURS ?

https://github.com/Harsh24081990/DATABRICKS/blob/main/Time_Travel_or_Rollback_Feature.md

QUE: What OPTIMIZE command used for ?
ANS: Compacting many small files into fewer large files (reduces file overhead of management and improves scan speed).

QUE: which spark library used while working with dataframes ?

QUE: What is the meant by resilient in RDD ?
ANS: In Resilient Distributed Dataset (RDD), the word resilient means:
	• Fault tolerance: If part of the data is lost due to node failure, Spark can automatically recompute it using the lineage (the sequence of transformations that created it).
	• Recovery without data replication: Instead of keeping multiple copies of the data, Spark stores how the RDD was derived. If a partition is lost, Spark recomputes only that partition from its source.
👉 In short: Resilient = ability to recover lost data automatically using lineage without full replication (which is the case for cloud storage fault tolerance i.e. 3 copies of each file).

- In Spark RDD / Delta Lake, data is not replicated multiple times by default for fault tolerance.
- If delta lake is built on top of cloud storage, it will have dual fault tolerance 1. From the spark (DAG + Lineage) 2. Cloud fault tolerance (three copies of each data and log files). 
==========================================================================

48. ###############  Persistent ############### 20-Aug-2025

QUE: What is resource/ Asset bundle in databricks (DAB) ?
https://github.com/Harsh24081990/DATABRICKS/blob/main/Asset_Bundles_in_Databricks.md

QUE: What is Bitemporal in databricks ?
https://github.com/Harsh24081990/DATABRICKS/blob/main/Bitemporal_in_databricks.md

QUE: What is the data lineage in databricks, how you ever worked on it ?
https://github.com/Harsh24081990/DATABRICKS/blob/main/Data_Lineage_in_databricks.md
==========================================================================

49. ############### Infinite ############### 20-Aug-2025

QUE: Which one is better for creating workflows ? ADF of Databricks ? 

QUE: Explain in brief the end to end steps while designing a Data Lake house using Azure and Databricks and following medallion architecture. Use ADF for data movement and orchestration and databricks for any other thing like transforming data, creating tables, business logic etc. Use SQL wherever possible. Give just the steps and not exact code.
==========================================================================

50. ############### NEUTRINO ############### 20-Aug-2025

QUE: If there are multiple source systems from where data has to come into one common data lakehouse (warehouse) which is to be developed from scratch using azure platform ? What are the end to end steps one should follow ? While designing the warehouse from scratch the main focus area should be security of the data as this is to be built for a banking application. 

QUE: If unstructured data is coming from multiple sources system and need to build a unified warehouse in azure which can be used for reporting. What will be your approach to do data modelling in this case ? 
==========================================================================

51. ############### Synechron ############### 21-Aug-2025

	1. Write a python program to find the prime numbers.
	2. Using SQL convert gender, count(*) columns to 2 columns --> Male, Female. And 1 row with the respective count. 
	3. if there are 2 huge dataframe with 2 columns (key, value) and data is highly skewed in both the key columns. How to join these dataframes ?
	==========================================================================

52. ############### Hexaware ############### 21-Aug-2025

	1. PySpark Coding.
	2. How will you create a pyspark dataframe by loading 100s of source files having different formats (like csv, json etc.) ? Files are present in ADLS location. Give syntax. 
	3. Delta live tables usages ?
	4. Which one is best for scheduling and orchestration ? ADF of Databricks workflows ?
==========================================================================

53. ############### NEUTRINO - Round 2 ############### 22-Aug-2025

Que: How to create a generic template in Azure/Databricks for doing some transformations on a given data, which we can use across cloud platform like Azure, AWS or GCP in a lift and shift manner ?

Que: How to design a ADF pipeline which can read a code (Macro) from a csv file, then do the logic implementation written in the code on a given source file, finally send the alert notification on completion of the pipeline. 
==========================================================================

54. ############### NTT DATA (Round-5) ############### 22-Aug-2025

Que: If reading a streaming source (Kafka) in databricks notebook and writing data to ADLS location, How would you schedule this notebook ? what cluster type will be used and where (Azure or Databricks clusters) ?
ANS:
For streaming, it’s common to use a long-running job cluster (because the Spark Structured Streaming job must continuously run).

QUE: If  running databricks notebooks from ADF pipeline and then scheduling it  using ADF scheduler,, which type of clusters are being used (ADF VMs only or databricks clusters are also utilized because we are running notebook code) ?
ANS: 
Databricks clusters are nothing but Azure VMs underneath – Databricks just manages them for you.
	• When you create a Databricks cluster, Databricks provisions Azure VMs (compute + storage + networking) behind the scenes.
	• execution happens on Databricks clusters, which are in turn built on Azure VMs.

QUE: In Informatica, the complete transformations are converted into what code at the backend for running the logics on the source systems ?

Que: What are the analytical functions?
==========================================================================

55. ############### Wipro ############### 23-Aug-2025

	1. How many Stage, Jobs and tasks  will be created?
	 
	- Read with infer schema
	- repartition
	- filter
	- select
	- group By
	- collect

	2. What is serialization and deserialization ? What are the types of serializers available in pySpark or python ?
	3. How to do schema evolution ?
	4. Explain spark submit command and it's parameters ?
==========================================================================

56. ############### NCS ############### 23-Aug-2025

QUE: SQL Questions. 

QUE: Is parquet format compatible for streaming data load in spark ?

QUE: Can we save incremental / SCD type 2 data in parquet format in spark ?
==========================================================================

57. ############### KPI Partners ############### 23-Aug-2025

QUE: SQL questions.

QUE: If there are 5 bugs in a ADF pipeline and we want to fix all in one day by assigning to 5 developers each bug. What will be the approach to deploy the fix in production ?

QUE: what is the default timeout duration for copy activity in ADF ?

QUE: Design a single ADF pipeline which copies data from 100 sql servers tables. 50 tables with full load, 30 with incremental load based on source timestamp column and 20 with incremental load based on the source ID columns. Do the reconciliation and alerting also for each table. 

QUE: How to do data quality checks using ADF ?

QUE: when to choose databricks workflows over ADF ?

QUE: Delta live table use cases ?
==========================================================================

58. ############### RSYSTEMS ############### 25-Aug-2025

QUE: In which pane the data gets saved in case of using external tables in databricks ? Why do you use external tables when you can save data in databricks managed tables ?

QUE: Is there any Data Quality framework available in databricks ? Where it is present and How to use it ? explain with example. 

QUE: SQL :How many users converted? find out from userlog activity tables ?
==========================================================================

59. ############### Wipro HR Round ############### 25-Aug-2025
==========================================================================

60. ############### Synechron HR Round ############### 25-Aug-2025
==========================================================================

61. #################### Persistent #################### 26-Aug-2025

QUE: this df is getting refreshed in each 5 mins.. but the reporting team is generating report every and want to see the latest data for that hour to fetch the latest o2 and co2 level in each city. Write a pyspark code to achieve this. 
event_df = cityid, cityname, timestamp, oxygen, co2
QUE: What is regression testing ?
QUE: What is the difference between Apache Spark and Databricks Spark ?
QUE: Why spark is fast ?
==========================================================================

62. #################### Neutrino HR Round #################### 28-Aug-2025
==========================================================================

63. #################### Wipro Client Round #################### 28-Aug-2025

Client : Humana (Health Care)
Oracle Hexadata to Azure Cloud migration project. 
Orchestration tool used --> Prefect

QUE: In Databricks why you are using external tables and not managed tables ?

QUE : What is meant by Liquid Clustering ?
==========================================================================

64. ################ Infinite computer solutions ################ 29-Aug-2025

QUE 1. How jobs, stages and tasks and partitions are created in spark while running any spark submit command or databricks notebook?

QUE 2. How to decide number of partitions to be used in repartition command to fix skewness issue?

QUE 3. If there are 100 nodes at work and 80 completed fast and 20 is showing running for longer time , what should be the approach to fix this, should we use repartition or coalesce in this case ?? When to use what ?

QUE 4. Out of 100 nodes if 20 have finished their work and 80 is in progress, what should we use repartition or coalesce? 
==========================================================================

65. ################ Infinite computer HR Round ################ 29-Aug-2025
==========================================================================

################ Other General Questions ################

Que: Can we update the base table using views created on it ?
==========================================================================

