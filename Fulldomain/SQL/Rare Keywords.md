Here’s a list of some rarely heard SQL keywords and concepts that are often asked in interviews, categorized for easier reference:

### 1. Advanced SQL Functions
- **COALESCE()**: Returns the first non-null value in a list.
- **NULLIF()**: Returns NULL if two expressions are equal; otherwise, returns the first expression.
- **LEAD()**: Accesses data from the next row in the result set without the need for a self-join.
- **LAG()**: Accesses data from the previous row in the result set.
- **RANK()**: Assigns a unique rank to each row within a partition of a result set.
- **DENSE_RANK()**: Similar to RANK(), but does not leave gaps in ranking when there are ties.
- **NTILE(n)**: Divides an ordered result set into n buckets and assigns a bucket number to each row.

### 2. Query Techniques
- **CROSS JOIN**: Produces a Cartesian product of two tables.
- **SELF JOIN**: A table is joined with itself to compare rows within the same table.
- **UNION ALL**: Combines results from multiple SELECT statements, including duplicates.
- **INTERSECT**: Returns only the rows that are common to both SELECT statements.
- **EXCEPT**: Returns rows from the first SELECT statement that are not present in the second.

### 3. Data Manipulation Keywords
- **MERGE**: Combines INSERT and UPDATE operations into a single statement based on conditions (also known as UPSERT).
- **UPSERT**: A combination of UPDATE and INSERT, where it updates an existing record or inserts a new one if it doesn’t exist.

### 4. Transaction Control
- **SAVEPOINT**: Sets a point within a transaction to which you can later roll back.
- **SET TRANSACTION**: Configures properties for the current transaction.

### 5. Indexing and Performance
- **PARTITION BY**: Used in window functions to divide the result set into partitions.
- **INDEX HINTS**: Directs the query optimizer to use a specific index when executing a query.

### 6. Data Types and Constraints
- **ENUM**: A string object with a value chosen from a list of permitted values (used in MySQL).
- **SET**: A string object that can have zero or more values, each of which must be chosen from a list of permitted values (used in MySQL).
- **CHECK CONSTRAINTS**: Ensures that all values in a column satisfy certain conditions.

### 7. Miscellaneous Concepts
- **WITH ROLLUP**: Extends GROUP BY to include subtotals and grand totals in the result set.
- **WITH CUBE**: Generates subtotals for all combinations of specified dimensions.
- **TEMPORARY TABLES**: Tables that exist temporarily during a session or transaction.
  
### 8. Hierarchical Queries
- **CONNECT BY PRIOR** (Oracle): Used for hierarchical queries to establish parent-child relationships.
  
### 9. Dynamic SQL
- **EXECUTE IMMEDIATE**: Executes dynamically constructed SQL statements at runtime.

### 10. Other Keywords
- **ALIAS**: A temporary name given to a table or column for ease of reference.
- **TRUNCATE TABLE**: Removes all records from a table without logging individual row deletions.
  
### 11. Common Table Expressions (CTEs)
- **WITH ... AS**: Defines a CTE that can be referenced within SELECT, INSERT, UPDATE, or DELETE statements.

### 12. Window Functions
- **ROW_NUMBER()**: Assigns a unique sequential integer to rows within a partition of a result set.

### 13. Conditional Aggregation
- Using aggregate functions with CASE statements to conditionally sum or count values.

### 14. Data Modeling Concepts
- **Entity Relationship Model (ERM)**: Represents data entities and their relationships visually.

### 15. JSON Functions (in databases that support it)
- **JSON_AGG() / JSON_OBJECT()**: Aggregate data into JSON format.

This list covers various advanced SQL keywords and concepts that may not be commonly discussed but are valuable for interviews and practical applications. If you need more information on any specific keyword or concept, feel free to ask!

Citations:
[1] https://www.geeksforgeeks.org/uber-sql-interview-questions-with-answers-and-explanations/
[2] https://www.datacamp.com/blog/top-sql-interview-questions-and-answers-for-beginners-and-intermediate-practitioners
[3] https://www.testgorilla.com/blog/tricky-sql-interview-questions/
[4] https://upesonline.ac.in/blog/advanced-sql-interview-questions
[5] https://syndicode.com/blog/sql-tricky-questions-on-job-interview/