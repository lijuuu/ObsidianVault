Here’s a collection of 50 SQL queries focused on table manipulation, including commands for creating, altering, inserting, updating, and deleting data. 

### Creating Tables

1. **Create a new table**
   ```sql
   CREATE TABLE employees (
       employee_id INT PRIMARY KEY,
       first_name VARCHAR(50),
       last_name VARCHAR(50),
       hire_date DATE,
       salary DECIMAL(10, 2)
   );
   ```

2. **Create a table with foreign key**
   ```sql
   CREATE TABLE departments (
       department_id INT PRIMARY KEY,
       department_name VARCHAR(100)
   );

   CREATE TABLE employees (
       employee_id INT PRIMARY KEY,
       first_name VARCHAR(50),
       last_name VARCHAR(50),
       department_id INT,
       FOREIGN KEY (department_id) REFERENCES departments(department_id)
   );
   ```

3. **Create a temporary table**
   ```sql
   CREATE TEMPORARY TABLE temp_employees AS SELECT * FROM employees WHERE salary > 50000;
   ```

### Inserting Data

4. **Insert a single record**
   ```sql
   INSERT INTO employees (employee_id, first_name, last_name, hire_date, salary) 
   VALUES (1, 'John', 'Doe', '2023-01-01', 60000);
   ```

5. **Insert multiple records**
   ```sql
   INSERT INTO employees (employee_id, first_name, last_name, hire_date, salary) 
   VALUES 
   (2, 'Jane', 'Smith', '2023-02-01', 65000),
   (3, 'Mike', 'Johnson', '2023-03-01', 70000);
   ```

6. **Insert data from another table**
   ```sql
   INSERT INTO temp_employees (employee_id, first_name)
   SELECT employee_id, first_name FROM employees WHERE salary > 60000;
   ```

### Updating Data

7. **Update a single record**
   ```sql
   UPDATE employees SET salary = 75000 WHERE employee_id = 1;
   ```

8. **Update multiple records**
   ```sql
   UPDATE employees SET salary = salary * 1.10 WHERE hire_date < '2023-01-01';
   ```

9. **Update with a condition based on another table**
   ```sql
   UPDATE employees e 
   JOIN departments d ON e.department_id = d.department_id 
   SET e.salary = e.salary * 1.05 
   WHERE d.department_name = 'Sales';
   ```

### Deleting Data

10. **Delete a single record**
    ```sql
    DELETE FROM employees WHERE employee_id = 2;
    ```

11. **Delete multiple records**
    ```sql
    DELETE FROM employees WHERE hire_date < '2020-01-01';
    ```

12. **Delete records based on a condition in another table**
    ```sql
    DELETE FROM employees 
    WHERE department_id IN (SELECT department_id FROM departments WHERE department_name = 'HR');
    ```

### Altering Tables

13. **Add a new column to a table**
    ```sql
    ALTER TABLE employees ADD COLUMN email VARCHAR(100);
    ```

14. **Modify an existing column's datatype**
    ```sql
    ALTER TABLE employees MODIFY COLUMN salary DECIMAL(12, 2);
    ```

15. **Rename a column in a table**
    ```sql
    ALTER TABLE employees RENAME COLUMN last_name TO surname;
    ```

16. **Drop a column from a table**
    ```sql
    ALTER TABLE employees DROP COLUMN email;
    ```

17. **Add a primary key constraint to an existing column**
    ```sql
    ALTER TABLE employees ADD PRIMARY KEY (employee_id);
    ```

18. **Add a foreign key constraint to an existing column**
    ```sql
    ALTER TABLE employees ADD CONSTRAINT fk_department FOREIGN KEY (department_id) REFERENCES departments(department_id);
    ```

19. **Rename the table**
    ```sql
    RENAME TABLE employees TO staff;
    ```

20. **Change the name of the database**
    ```sql
    ALTER DATABASE old_database_name RENAME TO new_database_name;
    ```

### Dropping Tables

21. **Drop a table if it exists**
    ```sql
    DROP TABLE IF EXISTS temp_employees;
    ```

22. **Drop multiple tables at once**
    ```sql
    DROP TABLE IF EXISTS employees, departments;
    ```

### Selecting Data

23. **Select all columns from a table**
    ```sql
    SELECT * FROM employees;
    ```

24. **Select specific columns from a table**
    ```sql
    SELECT first_name, last_name FROM employees;
    ```

25. **Select with filtering conditions**
    ```sql
    SELECT * FROM employees WHERE salary > 60000;
    ```

26. **Select with ordering results**
    ```sql
    SELECT * FROM employees ORDER BY hire_date DESC;
    ```

27. **Select with grouping and aggregation functions**
    ```sql
    SELECT department_id, COUNT(*) AS total_employees 
    FROM employees GROUP BY department_id;
    ```

28. **Select distinct values from a column**
     ```sql
     SELECT DISTINCT department_id FROM employees;
     ```

### Other Manipulation Queries

29. **Use transactions to ensure data integrity while updating multiple tables**
     ```sql
     START TRANSACTION;

     UPDATE accounts SET balance = balance - 100 WHERE account_id = 1;
     UPDATE accounts SET balance = balance + 100 WHERE account_id = 2;

     COMMIT;
     ```

30. **Rollback transaction in case of an error**
     ```sql
     START TRANSACTION;

     UPDATE accounts SET balance = balance - 100 WHERE account_id = 1;

     -- If an error occurs:
     ROLLBACK;
     ```
     
31. **Create an index for faster searches on the salary column**
     ```sql
     CREATE INDEX idx_salary ON employees(salary);
     ```
     
32. **Drop an index from the table**
     ```sql
     DROP INDEX idx_salary ON employees;
     ```
     
33. **Create a view for easy access to employee data**
     ```sql
     CREATE VIEW employee_view AS SELECT first_name, last_name, salary FROM employees;
     ```
     
34. **Select data from the created view**
     ```sql
     SELECT * FROM employee_view;
     ```
     
35. **Update data through the view (if allowed)**
     ```sql
     UPDATE employee_view SET salary = salary + 5000 WHERE first_name = 'John';
     ```
     
36. **Drop the created view when no longer needed**
     ```sql
     DROP VIEW IF EXISTS employee_view;
     ```
     
37. **Use `ALTER` to add constraints on existing columns**  
      Example: Adding NOT NULL constraint.
      ```sql
      ALTER TABLE employees MODIFY COLUMN first_name VARCHAR(50) NOT NULL;
      ```
      
38. **Use `ALTER` to change default value of a column**  
      Example: Setting default for salary.
      ```sql
      ALTER TABLE employees ALTER COLUMN salary SET DEFAULT 50000;
      ```
      
39. **Set up cascading delete on foreign key**  
      Example: When deleting departments.
      ```sql
      ALTER TABLE employees ADD CONSTRAINT fk_department FOREIGN KEY (department_id) REFERENCES departments(department_id) ON DELETE CASCADE;
      ```
      
40. **Check the structure of the table**  
      Example: Describe command.
      ```sql
      DESCRIBE employees;
      ```
      
41. **Export data to CSV format**  
      Example: Exporting employee data.
      ```sql
      SELECT * INTO OUTFILE '/tmp/employees.csv' FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n' FROM employees;
      ```
      
42. **Import data from CSV format into the table**  
      Example: Importing employee data.
      ```sql
      LOAD DATA INFILE '/tmp/employees.csv' INTO TABLE employees FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n';
      ```
      
43. **Use `GRANT` to give permissions on the table**  
      Example: Granting select permission.
      ```sql
      GRANT SELECT ON employees TO user_role;
      ```
      
44. **Use `REVOKE` to remove permissions on the table**  
      Example: Revoking select permission.
      ```sql
      REVOKE SELECT ON employees FROM user_role;
      ```
      
45. **Create a trigger that logs changes made to the employee's salary**  
      Example: Trigger for logging updates.
      ```sql
      CREATE TRIGGER log_salary_change 
      AFTER UPDATE ON employees 
      FOR EACH ROW 
      BEGIN 
          INSERT INTO salary_log(employee_id, old_salary, new_salary) VALUES(OLD.employee_id, OLD.salary, NEW.salary);
      END;
      ```
      
46. **Drop a trigger when it's no longer needed**  
      Example: Dropping the trigger.
      ```sql
      DROP TRIGGER IF EXISTS log_salary_change; 
      ```
      
47. **Create stored procedure to insert new employee**  
       Example: Stored procedure creation.
       ```sql
       CREATE PROCEDURE AddEmployee(IN emp_first_name VARCHAR(50), IN emp_last_name VARCHAR(50), IN emp_salary DECIMAL(10,2))
       BEGIN 
           INSERT INTO employees (first_name, last_name, salary) VALUES (emp_first_name, emp_last_name, emp_salary); 
       END; 
       ```
       
48. **Call the stored procedure to add an employee**  
       Example: Calling stored procedure.
       ```sql 
       CALL AddEmployee('Sarah', 'Connor', 70000); 
       ```
       
49. **Use `SHOW TABLES` to list all tables in the database**  
       Example: Show all tables.
       ```sql 
       SHOW TABLES; 
       ```
       
50. **Use `SHOW COLUMNS` to describe columns in a specific table**  
       Example: Show columns in the employee table.
       ```sql 
       SHOW COLUMNS FROM employees; 
       ```

This comprehensive list includes various SQL commands related to manipulating tables and their data effectively! If you need further details or more queries on specific topics, feel free to ask!

Citations:
[1] https://snowflakemasters.in/data-manipulation-language-commands-in-sql/
[2] https://www.geeksforgeeks.org/sql-ddl-dql-dml-dcl-tcl-commands/
[3] https://www.javatpoint.com/dml-commands-in-sql
[4] https://codedamn.com/news/sql/creating-manipulating-tables-sql-step-by-step-guide
[5] https://opentextbc.ca/dbdesign01/chapter/chapter-sql-dml/
[6] https://365datascience.com/tutorials/sql-tutorials/operators-in-sql/