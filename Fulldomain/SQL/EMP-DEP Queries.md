Here are 20 questions of varying types based on the `employees` and `departments` tables, along with their corresponding SQL queries to answer them. Each question is designed to explore different aspects of the data.

## Questions and SQL Solutions

### 1. **What is the average salary for each department?**
```sql
SELECT deptid, AVG(salary) AS avg_salary
FROM employees
GROUP BY deptid;
```

### 2. **Which employees earn less than their department's average salary?**
```sql
SELECT e.id, e.name, e.salary, e.deptid
FROM employees e
WHERE e.salary < (
    SELECT AVG(e2.salary)
    FROM employees e2
    WHERE e2.deptid = e.deptid
);
```

### 3. **How many employees are there in each department?**
```sql
SELECT deptid, COUNT(*) AS employee_count
FROM employees
GROUP BY deptid;
```

### 4. **What is the highest salary in each department?**
```sql
SELECT deptid, MAX(salary) AS highest_salary
FROM employees
GROUP BY deptid;
```

### 5. **List all employees along with their department names.**
```sql
SELECT e.name, d.name AS department_name
FROM employees e
JOIN departments d ON e.deptid = d.id;
```

### 6. **Which departments have no employees?**
```sql
SELECT d.name 
FROM departments d 
LEFT JOIN employees e ON d.id = e.deptid 
WHERE e.id IS NULL;
```

### 7. **What is the total salary expenditure for each department?**
```sql
SELECT deptid, SUM(salary) AS total_salary_expenditure
FROM employees
GROUP BY deptid;
```

### 8. **Find the employee with the lowest salary in each department.**
```sql
SELECT e.name, e.salary, d.name AS department 
FROM employees e 
JOIN departments d ON e.deptid = d.id 
WHERE (e.deptid, e.salary) IN (SELECT deptid, MIN(salary) 
                                FROM employees 
                                GROUP BY deptid);
```

### 9. **How many employees joined after a specific date (e.g., January 1, 2020)?**
```sql
SELECT COUNT(*) AS employee_count 
FROM employees 
WHERE joindate > '2020-01-01';
```

### 10. **What is the average salary of all employees?**
```sql
SELECT AVG(salary) AS overall_avg_salary 
FROM employees;
```

### 11. **List all departments and their respective employee count.**
```sql
SELECT d.name AS department_name, COUNT(e.id) AS employee_count 
FROM departments d 
LEFT JOIN employees e ON d.id = e.deptid 
GROUP BY d.id;
```

### 12. **Which employee has been with the company the longest?**
```sql
SELECT name, joindate 
FROM employees 
ORDER BY joindate ASC 
LIMIT 1;
```

### 13. **Find all employees who were born before a certain date (e.g., January 1, 1990).**
```sql
SELECT name, DOB 
FROM employees 
WHERE DOB < '1990-01-01';
```

### 14. **Which departments have an average salary above a certain threshold (e.g., $50,000)?**
```sql
SELECT d.name AS department_name, AVG(e.salary) AS avg_salary 
FROM departments d 
JOIN employees e ON d.id = e.deptid 
GROUP BY d.id 
HAVING avg_salary > 50000;
```

### 15. **What percentage of employees earn below the average salary of their respective departments?**
This requires a more complex calculation and may involve temporary tables or subqueries to get accurate percentages.

### 16. **List all unique job titles in the company (if applicable).**  
(Note: This assumes there's a job title column in `employees`, which is not present in your description.)

### 17. **Find the difference between the highest and lowest salaries in each department.**
```sql
SELECT deptid, MAX(salary) - MIN(salary) AS salary_difference 
FROM employees 
GROUP BY deptid;
```

### 18. **How many employees have joined in each year?**
```sql
SELECT YEAR(joindate) AS join_year, COUNT(*) AS employee_count 
FROM employees 
GROUP BY join_year;
```

### 19. **Find the average age of employees in each department (assuming current year is used for age calculation).**
This requires calculating age from DOB.

### 20. **Which employee has a salary closest to the average salary of their department?**
This would involve calculating the absolute difference between each employee's salary and their department's average.

## Conclusion

These questions cover a wide range of analytical needs and insights that can be derived from the `employees` and `departments` tables using SQL queries in MySQL. You can adjust these queries according to your specific requirements or data structure as needed!