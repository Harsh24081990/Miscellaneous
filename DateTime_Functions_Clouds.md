In cloud data platforms, date functions are crucial for managing and querying time-based data. Here’s a comparison of commonly used date functions in Google Cloud Platform (GCP) and Azure.

### **Google Cloud Platform (GCP)**
In GCP, particularly when using BigQuery or Dataflow, here are some commonly used date functions:

1. **`CURRENT_DATE()`**:
   - Returns the current date.
   - Example: `SELECT CURRENT_DATE();`

2. **`CURRENT_TIMESTAMP()`**:
   - Returns the current timestamp including time.
   - Example: `SELECT CURRENT_TIMESTAMP();`

3. **`DATE_ADD(date, INTERVAL expr unit)`**:
   - Adds a specified time interval to a date.
   - Example: `SELECT DATE_ADD(CURRENT_DATE(), INTERVAL 30 DAY);`

4. **`DATE_SUB(date, INTERVAL expr unit)`**:
   - Subtracts a specified time interval from a date.
   - Example: `SELECT DATE_SUB(CURRENT_DATE(), INTERVAL 30 DAY);`

5. **`DATE_DIFF(date1, date2, unit)`**:
   - Calculates the difference between two dates in specified units.
   - Example: `SELECT DATE_DIFF(CURRENT_DATE(), DATE '2023-01-01', DAY);`

6. **`FORMAT_TIMESTAMP(format_string, timestamp)`**:
   - Formats a timestamp into a string based on the provided format.
   - Example: `SELECT FORMAT_TIMESTAMP('%Y-%m-%d %H:%M:%S', CURRENT_TIMESTAMP());`

7. **`PARSE_DATE(format_string, date_string)`**:
   - Parses a date string into a date object based on the format.
   - Example: `SELECT PARSE_DATE('%Y-%m-%d', '2023-07-26');`

8. **`EXTRACT(part FROM date)`**:
   - Extracts a specific part (year, month, day) from a date or timestamp.
   - Example: `SELECT EXTRACT(YEAR FROM CURRENT_DATE());`

9. **`DATE_TRUNC(date, part)`**:
   - Truncates a date or timestamp to the specified part (e.g., day, month).
   - Example: `SELECT DATE_TRUNC(CURRENT_DATE(), MONTH);`

### **Azure Data Factory (ADF) and Azure Synapse Analytics**
In Azure, date functions are used in Azure Data Factory (ADF) and Azure Synapse Analytics, and they are often used in expressions or queries:

1. **`utcnow()`**:
   - Returns the current UTC date and time.
   - Example: `@utcnow()`

2. **`addDays(startDate, numberOfDays)`**:
   - Adds a specified number of days to a date.
   - Example: `@addDays(utcnow(), -30)`

3. **`subDays(startDate, numberOfDays)`**:
   - Subtracts a specified number of days from a date.
   - Example: `@subDays(utcnow(), 30)`

4. **`formatDateTime(dateTime, format)`**:
   - Formats a datetime value to a specified format.
   - Example: `@formatDateTime(utcnow(), 'yyyy-MM-dd')`

5. **`dateDiff(endDate, startDate, unit)`**:
   - Computes the difference between two dates in specified units.
   - Example: `@dateDiff(utcnow(), '2024-01-01', 'Day')`

6. **`startOfMonth(dateTime)`**:
   - Returns the start of the month for a given datetime.
   - Example: `@startOfMonth(utcnow())`

7. **`endOfMonth(dateTime)`**:
   - Returns the end of the month for a given datetime.
   - Example: `@endOfMonth(utcnow())`

8. **`startOfYear(dateTime)`**:
   - Returns the start of the year for a given datetime.
   - Example: `@startOfYear(utcnow())`

9. **`endOfYear(dateTime)`**:
   - Returns the end of the year for a given datetime.
   - Example: `@endOfYear(utcnow())`

![image](https://github.com/user-attachments/assets/b000baaa-9172-4363-a805-a71825674fe5)
