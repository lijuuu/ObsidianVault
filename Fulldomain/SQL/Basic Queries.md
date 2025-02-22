Here are numerous SQL queries to help you familiarize yourself with SQL syntax and operations:

### 1. Select all columns from a table
```sql
SELECT * FROM employees;
```

### 2. Select specific columns
```sql
SELECT name, age FROM employees;
```

### 3. Count total number of records
```sql
SELECT COUNT(*) FROM employees;
```

### 4. Find distinct values in a column
```sql
SELECT DISTINCT department FROM employees;
```

### 5. Filter records with a WHERE clause
```sql
SELECT * FROM employees WHERE age > 30;
```

### 6. Order results by a specific column
```sql
SELECT * FROM employees ORDER BY name ASC;
```

### 7. Group records and count them
```sql
SELECT department, COUNT(*) FROM employees GROUP BY department;
```

### 8. Join two tables
```sql
SELECT e.name, d.department_name 
FROM employees e 
JOIN departments d ON e.department_id = d.id;
```

### 9. Left join two tables
```sql
SELECT e.name, d.department_name 
FROM employees e 
LEFT JOIN departments d ON e.department_id = d.id;
```

### 10. Update a record in a table
```sql
UPDATE employees SET age = age + 1 WHERE name = 'John';
```

### 11. Delete a record from a table
```sql
DELETE FROM employees WHERE name = 'Alice';
```

### 12. Insert a new record into a table
```sql
INSERT INTO employees (name, age, department_id) VALUES ('Bob', 25, 1);
```

### 13. Calculate average age of employees
```sql
SELECT AVG(age) FROM employees;
```

### 14. Find maximum age of employees
```sql
SELECT MAX(age) FROM employees;
```

### 15. Find minimum age of employees
```sql
SELECT MIN(age) FROM employees;
```

### 16. Use CASE statement for conditional logic
```sql
SELECT name, 
       CASE 
           WHEN age < 30 THEN 'Young' 
           WHEN age BETWEEN 30 AND 50 THEN 'Middle-aged' 
           ELSE 'Senior' 
       END AS age_group 
FROM employees;
```

### 17. Find employees hired in the last year
```sql
SELECT * FROM employees WHERE hire_date >= CURDATE() - INTERVAL 1 YEAR;
```

### 18. Show top N records (e.g., top 5)
```sql
SELECT * FROM employees LIMIT 5;
```

### 19. Use subquery to find average salary by department
```sql
SELECT department_id, AVG(salary) 
FROM employees 
GROUP BY department_id 
HAVING AVG(salary) > (SELECT AVG(salary) FROM employees);
```

### 20. Find all employees with the same job title as 'Manager'
```sql
SELECT * FROM employees WHERE job_title = (SELECT job_title FROM employees WHERE name = 'John');
```

### 21. Use UNION to combine results from two queries
```sql
SELECT name FROM employees WHERE age < 30 
UNION 
SELECT name FROM contractors WHERE age < 30;
```

### 22. Find the total salary paid to all employees in each department
```sql
SELECT department_id, SUM(salary) AS total_salary 
FROM employees GROUP BY department_id;
```

### 23. Find the number of employees in each department with HAVING clause
```sql
SELECT department_id, COUNT(*) AS num_employees 
FROM employees GROUP BY department_id HAVING num_employees > 5;
```

### 24. Use COALESCE to handle NULL values in salary column
```sql
SELECT name, COALESCE(salary, 'Not Provided') AS salary_info FROM employees;
```

### 25. Create a temporary table and insert data into it
```sql
CREATE TEMPORARY TABLE temp_employees AS SELECT * FROM employees WHERE age > 30;
```

### 26. Find employees who do not have a department assigned
```sql
SELECT * FROM employees WHERE department_id IS NULL;
```

### 27. Find employees with a specific substring in their name
```sql
SELECT * FROM employees WHERE name LIKE '%John%';
```

### 28. Count distinct job titles
```sql
SELECT COUNT(DISTINCT job_title) FROM employees;
```

### 29. Get the first and last names of employees using concatenation
```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM employees;
```

### 30. Find employees whose names start with 'A'
```sql
SELECT * FROM employees WHERE name LIKE 'A%';
```

### 31. Calculate the total number of years each employee has worked
```sql
SELECT name, YEAR(CURDATE()) - YEAR(hire_date) AS years_worked FROM employees;
```

### 32. Find the most recently hired employee
```sql
SELECT * FROM employees ORDER BY hire_date DESC LIMIT 1;
```

### 33. Retrieve all records and sort by multiple columns
```sql
SELECT * FROM employees ORDER BY department_id ASC, name ASC;
```

### 34. Use a self-join to find employees who have the same manager
```sql
SELECT e1.name AS employee, e2.name AS manager 
FROM employees e1 
JOIN employees e2 ON e1.manager_id = e2.id;
```

### 35. Calculate the percentage of total salary for each employee
```sql
SELECT name, salary, 
       (salary / (SELECT SUM(salary) FROM employees) * 100) AS salary_percentage 
FROM employees;
```

### 36. Find employees hired on a specific date
```sql
SELECT * FROM employees WHERE hire_date = '2025-01-01';
```

### 37. Find all departments with no employees
```sql
SELECT d.department_name 
FROM departments d 
LEFT JOIN employees e ON d.id = e.department_id 
WHERE e.id IS NULL;
```

### 38. Update multiple records at once based on a condition
```sql
UPDATE employees SET salary = salary * 1.10 WHERE department_id = 2;
```

### 39. Delete records older than a specific date
```sql
DELETE FROM employees WHERE hire_date < '2020-01-01';
```

### 40. Insert multiple records at once
```sql
INSERT INTO employees (name, age, department_id) VALUES 
('Charlie', 28, 1), 
('David', 35, 2), 
('Eva', 40, 3);
```

### 41. Create an index on a column for faster searches
```sql
CREATE INDEX idx_name ON employees(name);
```

### 42. Drop an index from a table
```sql
DROP INDEX idx_name ON employees;
```

### 43. Use GROUP_CONCAT to combine values from multiple rows into one field
```sql
SELECT department_id, GROUP_CONCAT(name) AS employee_names 
FROM employees GROUP BY department_id;
```

### 44. Use EXISTS to check for related records in another table
```sql
SELECT name 
FROM employees e 
WHERE EXISTS (SELECT * FROM projects p WHERE p.employee_id = e.id);
```

### 45. Create a view for easier access to data
```sql
CREATE VIEW employee_salaries AS SELECT name, salary FROM employees;
```

### 46. Select from a view you created earlier
```sql
SELECT * FROM employee_salaries;
```

### 47. Update records in a view (if allowed)
```sql
UPDATE employee_salaries SET salary = salary * 1.05 WHERE name = 'Bob';
```

### 48. Use RANK() to assign ranks to salaries within departments (requires window functions)
```sql
SELECT name, salary, 
       RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS salary_rank 
FROM employees;
```

### 49. Use CTE (Common Table Expression) for recursive queries (if supported)
```sql
WITH RECURSIVE EmployeeCTE AS (
    SELECT id, name, manager_id FROM employees WHERE manager_id IS NULL 
    UNION ALL 
    SELECT e.id, e.name, e.manager_id FROM employees e 
    INNER JOIN EmployeeCTE cte ON cte.id = e.manager_id)
SELECT * FROM EmployeeCTE;
```

### 50. Use COALESCE to provide default values when NULL is encountered in queries.
```sql
SELECT name, COALESCE(salary, 'Not Provided') AS salary_info FROM employees;
```

Here’s an additional set of SQL queries to help you further develop your SQL skills. This collection includes a variety of operations, including data retrieval, manipulation, and advanced functions.

### 51. Find the total number of employees in each department
```sql
SELECT department_id, COUNT(*) AS total_employees 
FROM employees GROUP BY department_id;
```

### 52. Find employees with salaries above the average salary
```sql
SELECT * FROM employees WHERE salary > (SELECT AVG(salary) FROM employees);
```

### 53. Get the second highest salary from the employees table
```sql
SELECT MAX(salary) FROM employees WHERE salary < (SELECT MAX(salary) FROM employees);
```

### 54. Use LEFT JOIN to find all employees and their project assignments, if any
```sql
SELECT e.name, p.project_name 
FROM employees e 
LEFT JOIN projects p ON e.id = p.employee_id;
```

### 55. Find the total number of projects each employee is working on
```sql
SELECT e.name, COUNT(p.id) AS project_count 
FROM employees e 
LEFT JOIN projects p ON e.id = p.employee_id 
GROUP BY e.id;
```

### 56. Use a subquery to find employees who work in the same department as 'Alice'
```sql
SELECT * FROM employees WHERE department_id = (SELECT department_id FROM employees WHERE name = 'Alice');
```

### 57. Find all employees whose names contain 'e' and order them by age
```sql
SELECT * FROM employees WHERE name LIKE '%e%' ORDER BY age;
```

### 58. Calculate the total compensation (salary + bonus) for each employee
```sql
SELECT name, (salary + COALESCE(bonus, 0)) AS total_compensation FROM employees;
```

### 59. Retrieve the employee with the lowest salary in each department
```sql
SELECT department_id, MIN(salary) AS lowest_salary 
FROM employees GROUP BY department_id;
```

### 60. Find all departments that have more than three managers
```sql
SELECT department_id, COUNT(manager_id) AS manager_count 
FROM employees WHERE job_title = 'Manager' GROUP BY department_id HAVING manager_count > 3;
```

### 61. Create a stored procedure to add a new employee
```sql
CREATE PROCEDURE AddEmployee(IN emp_name VARCHAR(100), IN emp_age INT, IN emp_salary DECIMAL(10,2))
BEGIN
    INSERT INTO employees (name, age, salary) VALUES (emp_name, emp_age, emp_salary);
END;
```

### 62. Call the stored procedure to add an employee
```sql
CALL AddEmployee('Frank', 29, 60000);
```

### 63. Find the average salary for each job title in descending order
```sql
SELECT job_title, AVG(salary) AS average_salary 
FROM employees GROUP BY job_title ORDER BY average_salary DESC;
```

### 64. Use a trigger to automatically update a log table when an employee is added
```sql
CREATE TRIGGER after_employee_insert 
AFTER INSERT ON employees 
FOR EACH ROW 
BEGIN 
    INSERT INTO employee_log (employee_id, action) VALUES (NEW.id, 'Added'); 
END;
```

### 65. Retrieve all records from a specific year using DATE_FORMAT()
```sql
SELECT * FROM employees WHERE DATE_FORMAT(hire_date, '%Y') = '2025';
```

### 66. Use GROUP BY with multiple columns to find unique combinations
```sql
SELECT department_id, job_title, COUNT(*) AS count 
FROM employees GROUP BY department_id, job_title;
```

### 67. Find all projects that have not been assigned to any employee
```sql
SELECT * FROM projects WHERE id NOT IN (SELECT DISTINCT project_id FROM employee_projects);
```

### 68. Retrieve names and hire dates of all employees hired in January of any year
```sql
SELECT name, hire_date FROM employees WHERE MONTH(hire_date) = 1;
```

### 69. Use CROSS JOIN to create a combination of two tables’ records
```sql
SELECT e.name AS employee_name, d.department_name 
FROM employees e CROSS JOIN departments d;
```

### 70. Create an index on the hire_date column for faster searches
```sql
CREATE INDEX idx_hire_date ON employees(hire_date);
```

### 71. Drop a column from a table (e.g., remove bonus column)
```sql
ALTER TABLE employees DROP COLUMN bonus;
```

### 72. Rename a column in a table (e.g., rename age to years)
```sql
ALTER TABLE employees CHANGE age years INT;
```

### 73. Show the total number of records in multiple tables using UNION ALL
```sql
SELECT COUNT(*) AS total FROM employees 
UNION ALL 
SELECT COUNT(*) FROM contractors;
```

### 74. Use ROLLUP to get subtotals and grand totals in grouping results.
```sql
SELECT department_id, COUNT(*) AS total_employees 
FROM employees GROUP BY department_id WITH ROLLUP;
```

### 75. Find all unique combinations of first and last names in the employee table.
```sql
SELECT DISTINCT first_name, last_name FROM employees;
```

Here’s another batch of SQL queries to further enhance your familiarity with SQL operations. This collection includes a variety of query types, including data retrieval, manipulation, aggregation, and advanced SQL features.

### 76. Find employees hired in the last 30 days
```sql
SELECT * FROM employees WHERE hire_date >= CURDATE() - INTERVAL 30 DAY;
```

### 77. Get the total number of employees for each job title
```sql
SELECT job_title, COUNT(*) AS total_employees 
FROM employees GROUP BY job_title;
```

### 78. Retrieve employees with a salary between two values
```sql
SELECT * FROM employees WHERE salary BETWEEN 50000 AND 80000;
```

### 79. Find the employee with the highest salary in each department
```sql
SELECT department_id, MAX(salary) AS highest_salary 
FROM employees GROUP BY department_id;
```

### 80. Use EXISTS to check if an employee has any projects assigned
```sql
SELECT name 
FROM employees e 
WHERE EXISTS (SELECT * FROM projects p WHERE p.employee_id = e.id);
```

### 81. Find all employees who were hired before their manager
```sql
SELECT e1.name AS employee, e2.name AS manager 
FROM employees e1 
JOIN employees e2 ON e1.manager_id = e2.id 
WHERE e1.hire_date < e2.hire_date;
```

### 82. Retrieve the last five hires from the employees table
```sql
SELECT * FROM employees ORDER BY hire_date DESC LIMIT 5;
```

### 83. Use a subquery to find departments with more than ten employees
```sql
SELECT department_id 
FROM employees 
GROUP BY department_id 
HAVING COUNT(*) > 10;
```

### 84. Calculate the total number of years each employee has been with the company
```sql
SELECT name, TIMESTAMPDIFF(YEAR, hire_date, CURDATE()) AS years_with_company 
FROM employees;
```

### 85. Find all employees who have not been assigned to any project
```sql
SELECT e.name 
FROM employees e 
LEFT JOIN employee_projects ep ON e.id = ep.employee_id 
WHERE ep.project_id IS NULL;
```

### 86. Update salaries by a percentage increase for all employees in a specific department
```sql
UPDATE employees SET salary = salary * 1.05 WHERE department_id = 3;
```

### 87. Retrieve the average salary of all employees in each department and order by average salary descending
```sql
SELECT department_id, AVG(salary) AS avg_salary 
FROM employees GROUP BY department_id ORDER BY avg_salary DESC;
```

### 88. Use a temporary table to store intermediate results for analysis
```sql
CREATE TEMPORARY TABLE temp_salaries AS SELECT name, salary FROM employees WHERE salary > 60000;
```

### 89. Find all unique job titles from the employees table
```sql
SELECT DISTINCT job_title FROM employees;
```

### 90. Use a CASE statement to categorize salaries into brackets
```sql
SELECT name, salary,
       CASE 
           WHEN salary < 50000 THEN 'Low'
           WHEN salary BETWEEN 50000 AND 100000 THEN 'Medium'
           ELSE 'High'
       END AS salary_bracket 
FROM employees;
```

### 91. Find departments that have at least one employee with a specific job title (e.g., 'Developer')
```sql
SELECT DISTINCT d.department_name 
FROM departments d 
JOIN employees e ON d.id = e.department_id 
WHERE e.job_title = 'Developer';
```

### 92. Retrieve all projects along with their assigned employee names (if any)
```sql
SELECT p.project_name, e.name AS employee_name 
FROM projects p 
LEFT JOIN employee_projects ep ON p.id = ep.project_id 
LEFT JOIN employees e ON ep.employee_id = e.id;
```

### 93. Create an index on the salary column for faster searches on salaries.
```sql
CREATE INDEX idx_salary ON employees(salary);
```

### 94. Drop a view from the database.
```sql
DROP VIEW IF EXISTS employee_salaries;
```

### 95. Use GROUP BY to find the number of distinct job titles in each department.
```sql
SELECT department_id, COUNT(DISTINCT job_title) AS distinct_job_titles 
FROM employees GROUP BY department_id;
```

### 96. Find all records where the hire date is not specified (NULL).
```sql
SELECT * FROM employees WHERE hire_date IS NULL;
```

### 97. Retrieve names of all managers and their direct reports.
```sql
SELECT m.name AS manager_name, e.name AS employee_name 
FROM employees m 
JOIN employees e ON m.id = e.manager_id;
```

### 98. Use a correlated subquery to find employees earning more than their average departmental salary.
```sql
SELECT name FROM employees e1 
WHERE salary > (SELECT AVG(salary) FROM employees e2 WHERE e1.department_id = e2.department_id);
```

### 99. Get a list of all departments and their respective employee counts using LEFT JOIN.
```sql
SELECT d.department_name, COUNT(e.id) AS employee_count 
FROM departments d LEFT JOIN employees e ON d.id = e.department_id GROUP BY d.id;
```

### 100. Find all projects that are not associated with any active employee.
```sql
SELECT * FROM projects WHERE id NOT IN (SELECT project_id FROM employee_projects WHERE employee_id IN (SELECT id FROM employees WHERE status = 'Active'));
```
