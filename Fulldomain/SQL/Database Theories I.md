Here’s a compilation of common relational database theories and concepts that are frequently asked in interviews, along with some system-level questions:

### Categories of SQL Queries
1. **DML (Data Manipulation Language)**: Insert, Update, Delete.
2. **DDL (Data Definition Language)**: Create, Alter, Drop.
3. **DCL (Data Control Language)**: Grant, Revoke.
4. **TCL (Transaction Control Language)**: Commit, Rollback, Savepoint.

### Normalization
5. **What is normalization?**: The process of organizing data to minimize redundancy and improve data integrity.
6. **Different normal forms**: 1NF, 2NF, 3NF, BCNF, 4NF, 5NF.
7. **Denormalization**: The process of combining tables to reduce complexity and improve read performance.

### ACID Properties
8. **What does ACID stand for?**: Atomicity, Consistency, Isolation, Durability.
9. **Importance of ACID**: Ensures reliable processing of database transactions.

### Indexing
10. **What is an index?**: A data structure that improves the speed of data retrieval operations on a database table.
11. **Types of indexes**: Unique index, Clustered index, Non-clustered index.
12. **How does indexing work?**: It creates a separate data structure that holds pointers to the actual rows in the table.

### Query Optimization
13. **How to find slow-running queries?**: Use query execution plans and performance monitoring tools (e.g., EXPLAIN statement).
14. **Common optimization techniques**: Indexing, query rewriting, avoiding SELECT *.

### Joins and Relationships
15. **What is a join?**: A SQL operation that combines rows from two or more tables based on a related column.
16. **Types of joins**: INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL OUTER JOIN.
17. **Database relationships**: One-to-One, One-to-Many, Many-to-Many.

### Data Integrity
18. **What are integrity constraints?**: Rules that ensure the accuracy and consistency of data in the database (e.g., primary keys, foreign keys).
19. **Referential integrity**: Ensures that relationships between tables remain consistent.

### Views and Stored Procedures
20. **What is a view?**: A virtual table based on the result set of a SQL query.
21. **What is a stored procedure?**: A precompiled collection of SQL statements that can be executed as a single unit.

### Triggers
22. **What is a trigger?**: A set of instructions that are automatically executed in response to certain events on a particular table.

### Concurrency Control
23. **How do you handle concurrency?**: Through locking mechanisms (pessimistic and optimistic locking) and transaction isolation levels.

### Database Architecture
24. **Two-tier vs Three-tier architecture**: Two-tier involves client-server communication directly; Three-tier adds an intermediary layer (application server).
25. **What is a data model?**: A conceptual representation of the data structures that are required by a database.

### Codd's Rules
26. **Codd's 12 rules for relational databases**: Fundamental principles defining what is required from a DBMS for it to be considered relational.

### Miscellaneous Concepts
27. **What is denormalization?**: The process of intentionally introducing redundancy into a database to improve performance.
28. **Difference between HAVING and WHERE clauses**: WHERE filters rows before aggregation; HAVING filters after aggregation.
29. **What is an entity-relationship model?**: A diagrammatic representation of entities and their relationships within a system.
30. **Data independence standards**: The ability to change the schema at one level without affecting other levels.

### Performance Tuning
31. **How can you improve query performance?**: Indexing, optimizing queries, using caching mechanisms.
32. **Explain the concept of partitioning in databases**: Dividing large tables into smaller, more manageable pieces while maintaining access through the same interface.

### System-Level Questions
33. **How does a database work?**: It stores data in structured formats (tables) and uses SQL for querying and managing that data.
34. **What are the key components of an RDBMS?**: Tables, records (rows), attributes (columns), schemas.
35. **Explain how transactions work in databases**: Transactions group multiple operations into a single unit to ensure consistency and reliability.

### Advanced Topics
36. **What is sharding in databases?**: Splitting a large database into smaller parts (shards) to distribute load and improve performance.
37. **Explain CAP theorem in distributed databases**: Consistency, Availability, Partition tolerance; states that not all three can be guaranteed simultaneously in distributed systems.

### Data Types and Structures
38. **Common data types used in SQL databases**: INT, VARCHAR, DATE, BOOLEAN.
39. **What are relations and relation schemas?**: Relations represent tables; relation schemas define the structure of those tables.

### Security Concerns
40. **How do you secure a database?**: Implementing user authentication and authorization protocols; using encryption for sensitive data.

### Backup and Recovery
41. **Importance of backup strategies in databases**: To prevent data loss due to failures or disasters; includes full backups, incremental backups.
42. **Explain point-in-time recovery in databases**: Restoring a database to its state at a specific moment using transaction logs.

### Query Languages
43. **Difference between SQL and NoSQL databases**: SQL databases use structured query language and are relational; NoSQL databases are non-relational and can handle unstructured data.

### Miscellaneous Concepts Continued
44. **What is an attribute in database terminology?**: A property or characteristic of an entity represented as a column in a table.
45. **Explain the term "degree of relationship" in databases**: Refers to the number of entities involved in a relationship (e.g., unary, binary).
=
### Additional Concepts
46. **What is an object-oriented model in databases?**: A model where data is represented as objects similar to object-oriented programming concepts.
47. **Describe what a query evaluation engine does in RDBMSs**: It processes SQL queries by parsing them into executable plans for retrieving results efficiently.

