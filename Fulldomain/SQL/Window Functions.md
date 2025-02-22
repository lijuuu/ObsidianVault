### What Are Window Functions?

Window functions allow you to perform calculations across a set of rows related to the current row. Unlike traditional aggregate functions that return a single value for a group of rows, window functions return a value for each row while still allowing access to the individual row data.

### Why Use Window Functions?

- **Retain Row Detail**: Unlike aggregate functions, you can retain the original row data while performing calculations.
- **Complex Calculations**: They simplify complex calculations like running totals, moving averages, and rankings.
- **Performance**: Often more efficient than subqueries or self-joins for similar tasks.

### Components of Window Functions

1. **Function Type**: The type of calculation you want to perform (e.g., `SUM`, `AVG`, `ROW_NUMBER`, etc.).
2. **OVER Clause**: Defines how to partition and order the data.
   - **PARTITION BY**: Divides the result set into smaller sets (partitions) to which the window function is applied.
   - **ORDER BY**: Determines the order of rows within each partition.
   - **ROWS or RANGE**: Specifies the frame of rows used for calculations.

### Common Window Functions

1. **Aggregate Functions**:
   - `SUM()`
   - `AVG()`
   - `COUNT()`

2. **Ranking Functions**:
   - `ROW_NUMBER()`: Assigns a unique sequential integer to rows within a partition.
   - `RANK()`: Similar to `ROW_NUMBER()`, but can assign the same rank to ties.
   - `DENSE_RANK()`: Similar to `RANK()`, but does not leave gaps in ranking.

3. **Offset Functions**:
   - `LAG()`: Accesses data from a previous row in the same result set without needing a self-join.
   - `LEAD()`: Accesses data from a subsequent row in the same result set.

4. **NTILE(n)**: Divides an ordered partition into n buckets and assigns a bucket number to each row.

Here are some basic MySQL window function queries that are commonly asked, along with explanations for each. These examples will help you understand how to use window functions effectively in simple scenarios.

### Basic Queries Using Window Functions

#### 1. Using `ROW_NUMBER()`

To assign a unique sequential integer to each row within a partition:

```sql
SELECT employee_id, 
       first_name, 
       last_name,
       ROW_NUMBER() OVER (ORDER BY hire_date) AS row_num
FROM employees;
```
**Explanation**: This query assigns a row number to each employee based on their hire date, starting from the earliest hire.

#### 2. Using `RANK()`

To rank employees based on their salaries:

```sql
SELECT employee_id,
       first_name,
       salary,
       RANK() OVER (ORDER BY salary DESC) AS salary_rank
FROM employees;
```
**Explanation**: This query ranks employees by salary, with the highest salary receiving rank 1. Ties will receive the same rank.

#### 3. Using `DENSE_RANK()`

To rank products while avoiding gaps in ranking for ties:

```sql
SELECT product_id,
       product_name,
       price,
       DENSE_RANK() OVER (ORDER BY price DESC) AS price_rank
FROM products;
```
**Explanation**: Similar to `RANK()`, but if two products have the same price, they will receive the same rank without skipping numbers.

#### 4. Calculating a Running Total with `SUM()`

To calculate a running total of sales:

```sql
SELECT order_id,
       order_date,
       amount,
       SUM(amount) OVER (ORDER BY order_date) AS running_total
FROM orders;
```
**Explanation**: This query calculates a cumulative total of amounts ordered over time, showing how sales accumulate.

#### 5. Using `LAG()` to Compare Current and Previous Values

To find the difference between current and previous month sales:

```sql
SELECT order_date,
       amount,
       LAG(amount, 1) OVER (ORDER BY order_date) AS previous_amount,
       amount - LAG(amount, 1) OVER (ORDER BY order_date) AS difference
FROM orders;
```
**Explanation**: This query retrieves the amount from the previous row and calculates the difference from the current row.

#### 6. Using `LEAD()` for Future Comparison

To compare current sales with future sales:

```sql
SELECT order_date,
       amount,
       LEAD(amount, 1) OVER (ORDER BY order_date) AS next_amount
FROM orders;
```
**Explanation**: This query retrieves the amount from the next row based on order date, allowing comparisons with future sales.

#### 7. Calculating Average Salary by Department

To find the average salary within each department:

```sql
SELECT employee_id,
       first_name,
       department_id,
       salary,
       AVG(salary) OVER (PARTITION BY department_id) AS avg_salary
FROM employees;
```
**Explanation**: This query calculates the average salary for each department and displays it alongside each employee's details.

### Questions for Understanding

1. **What is the purpose of using `ROW_NUMBER()` in a query?**
2. **How does `RANK()` differ from `DENSE_RANK()`?**
3. **In what scenarios would you use `LAG()` and `LEAD()` functions?**
4. **How does partitioning affect the results of window functions?**
5. **Can you explain how to calculate a running total using window functions?**

