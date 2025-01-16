Here’s a comprehensive list of SQL string methods and keywords, grouped for easy reference:

### String Functions
- **CONCAT()**: Concatenates two or more strings.
  ```sql
  SELECT CONCAT('Hello', ' ', 'World');
  ```

- **CHAR_LENGTH() / CHARACTER_LENGTH()**: Returns the length of a string in characters.
  ```sql
  SELECT CHAR_LENGTH('Hello');
  ```

- **LENGTH()**: Returns the length of a string in bytes.
  ```sql
  SELECT LENGTH('Hello');
  ```

- **UPPER()**: Converts a string to uppercase.
  ```sql
  SELECT UPPER('hello');
  ```

- **LOWER()**: Converts a string to lowercase.
  ```sql
  SELECT LOWER('HELLO');
  ```

- **REPLACE()**: Replaces occurrences of a substring within a string.
  ```sql
  SELECT REPLACE('Hello World', 'World', 'SQL');
  ```

- **SUBSTRING() / SUBSTR()**: Extracts a substring from a string.
  ```sql
  SELECT SUBSTRING('Hello World', 1, 5);
  ```

- **LEFT()**: Extracts a specified number of characters from the left side of a string.
  ```sql
  SELECT LEFT('Hello World', 5);
  ```

- **RIGHT()**: Extracts a specified number of characters from the right side of a string.
  ```sql
  SELECT RIGHT('Hello World', 5);
  ```

- **INSTR()**: Finds the position of the first occurrence of a substring in a string.
  ```sql
  SELECT INSTR('Hello World', 'World');
  ```

- **TRIM()**: Removes leading and trailing spaces from a string.
  ```sql
  SELECT TRIM(' Hello World ');
  ```

- **REVERSE()**: Reverses the characters in a string.
  ```sql
  SELECT REVERSE('Hello');
  ```

- **SPACE()**: Returns a string consisting of the specified number of spaces.
  ```sql
  SELECT SPACE(7);
  ```

- **STRCMP()**: Compares two strings and returns an integer indicating their relationship.
  ```sql
  SELECT STRCMP('string1', 'string2');
  ```

Here’s an expanded overview of pattern matching in SQL, including the **LIKE** operator and regular expressions, along with additional techniques and examples.

### Pattern Matching Keywords

- **LIKE**: Searches for a specified pattern in a column.
  - **Wildcards**:
    - **%**: Represents zero or more characters "_".
  
  **Examples**:
  ```sql
  SELECT * FROM employees WHERE first_name LIKE 'J%'; -- Names starting with 'J'
  SELECT * FROM employees WHERE last_name LIKE '%son'; -- Names ending with 'son'
  SELECT * FROM employees WHERE first_name LIKE '_a%'; -- Names where the second character is 'a'
  ```

- **NOT LIKE**: Excludes entries that match a specified pattern.
  
  **Examples**:
  ```sql
  SELECT * FROM employees WHERE first_name NOT LIKE 'A%'; -- Names not starting with 'A'
  SELECT * FROM employees WHERE last_name NOT LIKE '%er'; -- Names not ending with 'er'
  ```

### Regular Expressions
- **REGEXP / RLIKE**: Used for advanced pattern matching using regular expressions (available in MySQL).
  
  **Examples**:
  ```sql
  SELECT * FROM products WHERE product_name REGEXP '^[A-Z]'; -- Names starting with an uppercase letter
  SELECT * FROM products WHERE product_name REGEXP '[aeiou]'; -- Products containing any vowel
  SELECT * FROM products WHERE product_name REGEXP 'a{2,}'; -- Products with two or more consecutive 'a' characters
  ```

### Advanced Pattern Matching Techniques

#### Using Square Brackets (T-SQL)
- In SQL Server, square brackets can specify a set of characters.
  
  **Examples**:
  ```sql
  SELECT 'Carson' LIKE '[C-K]arson'; -- TRUE, C is in the range C-K
  SELECT 'Karson' LIKE '[C-K]arson'; -- TRUE, K is in range
  SELECT 'Larson' LIKE '[CKL]arson'; -- TRUE, L is in the set [CKL]
  SELECT 'Parson' LIKE '[C-K]arson'; -- FALSE, P is out of range
  ```

#### Using the MATCH_RECOGNIZE Clause (Oracle SQL)
- Enables sophisticated row-pattern recognition within ordered datasets.
  
  **Example Usage**:
  ```sql
  SELECT *
  FROM sales
  MATCH_RECOGNIZE (
      PARTITION BY product_id
      ORDER BY sale_date
      MEASURES COUNT(*) AS total_sales
      PATTERN (A B)
      DEFINE A AS sale_price > PREV(sale_price),
             B AS sale_price < PREV(sale_price)
  );
  ```

### Combining Pattern Matching with Other Functions
- Integrating pattern matching with other SQL functions can yield powerful results.

#### Example of Combining Functions:
```sql
SELECT CONCAT(first_name, ' ', last_name) AS full_name 
FROM employees 
WHERE full_name LIKE '%Smith%';
```

### Performance Considerations
- To enhance the performance of pattern matching operations:
  - Ensure that columns frequently used in pattern matching queries are indexed. Indexes can significantly speed up data retrieval by allowing the database engine to quickly locate relevant rows without scanning the entire table.

### Summary of Key Techniques for Pattern Matching in SQL

1. **Using the LIKE Operator**: Basic pattern matching using wildcards `%` and `_`.
2. **Using Regular Expressions**: For complex searches and advanced pattern matching capabilities.
3. **Square Brackets in T-SQL**: For specifying sets of characters.
4. **MATCH_RECOGNIZE Clause**: For identifying patterns across multiple rows in Oracle SQL.
5. **Combining Functions**: Enhancing queries by integrating pattern matching with other SQL functions.

### Additional String Functions (if applicable)
- **FORMAT()**: Formats the value according to the specified format.
   ```sql
   SELECT FORMAT(1234567.89, 'C', 'en-US');
   ```

- **ASCII()**: Returns the numeric value of the leftmost character of a string.
   ```sql
   SELECT ASCII('A');
   ```

- **CHAR()**: Returns the character for an ASCII code.
   ```sql
   SELECT CHAR(65);
   ```
