Here’s a comprehensive guide to SQL queries focusing on date and time usage, ranging from basic to advanced functions, using the current date of **Thursday, January 09, 2025, 7 PM IST** as a reference.

### Basic Date and Time Queries

1. **Retrieve Current Date and Time**
   ```sql
   SELECT NOW(); -- Returns current date and time
   ```

2. **Retrieve Current Date**
   ```sql
   SELECT CURDATE(); -- Returns current date (YYYY-MM-DD)
   ```

3. **Retrieve Current Time**
   ```sql
   SELECT CURTIME(); -- Returns current time (HH:MI:SS)
   ```

4. **Extract Date from DateTime**
   ```sql
   SELECT DATE('2025-01-09 19:00:00') AS DatePart; -- Extracts date part
   ```

5. **Extract Time from DateTime**
   ```sql
   SELECT TIME('2025-01-09 19:00:00') AS TimePart; -- Extracts time part
   ```

### Intermediate Date and Time Functions

6. **Add Days to a Date**
   ```sql
   SELECT DATE_ADD('2025-01-09', INTERVAL 10 DAY) AS NewDate; -- Adds 10 days
   ```

7. **Subtract Days from a Date**
   ```sql
   SELECT DATE_SUB('2025-01-09', INTERVAL 5 DAY) AS NewDate; -- Subtracts 5 days
   ```

8. **Calculate Difference Between Two Dates**
   ```sql
   SELECT DATEDIFF('2025-01-19', '2025-01-09') AS DaysDifference; -- Returns number of days between two dates
   ```

9. **Extract Specific Parts of a Date**
   ```sql
   SELECT EXTRACT(YEAR FROM '2025-01-09') AS YearPart; -- Extracts year
   SELECT EXTRACT(MONTH FROM '2025-01-09') AS MonthPart; -- Extracts month
   SELECT EXTRACT(DAY FROM '2025-01-09') AS DayPart; -- Extracts day
   ```

10. **Find Rows Between Two Dates**
    ```sql
    SELECT * FROM events WHERE event_date BETWEEN '2025-01-01' AND '2025-01-31'; -- Finds events in January 2025
    ```

### Advanced Date and Time Queries

11. **Find Rows Created Within the Last Week**
    ```sql
    SELECT * FROM events WHERE event_date > (CURDATE() - INTERVAL 7 DAY); -- Events from the last week
    ```

12. **Find Events Scheduled for a Specific Time Range**
    ```sql
    SELECT * FROM events 
    WHERE event_date BETWEEN '2025-01-09 19:00:00' AND '2025-01-09 23:59:59'; -- Events on January 9, 2025, after 7 PM
    ```

13. **Get the First Day of the Month**
    ```sql
    SELECT DATE_FORMAT(NOW() ,'%Y-%m-01') AS FirstDayOfMonth; -- Returns the first day of the current month
    ```

14. **Get the Last Day of the Month**
    ```sql
    SELECT LAST_DAY(NOW()) AS LastDayOfMonth; -- Returns the last day of the current month
    ```

15. **Get Weekday Name from a Date**
    ```sql
    SELECT DAYNAME('2025-01-09') AS WeekdayName; -- Returns the name of the weekday (e.g., Thursday)
    ```

16. **Get Week Number of the Year**
    ```sql
    SELECT WEEK('2025-01-09') AS WeekNumber; -- Returns week number for the given date
    ```

17. **Get Quarter of the Year**
    ```sql
    SELECT QUARTER('2025-01-09') AS QuarterNumber; -- Returns quarter number (1 to 4)
    ```

18. **Convert UTC to Local Time (if applicable)**
    ```sql
    SELECT CONVERT_TZ(NOW(), '+00:00', '+05:30') AS LocalTime; -- Converts UTC to IST (UTC+5:30)
    ```

### Formatting Dates

19. **Format Date Output**
    ```sql
    SELECT DATE_FORMAT('2025-01-09', '%W, %M %d, %Y') AS FormattedDate; -- Outputs formatted date (e.g., Thursday, January 09, 2025)
    ```

20. **Custom Time Formatting**
    ```sql
    SELECT DATE_FORMAT(NOW(), '%H:%i:%s') AS FormattedTime; -- Outputs time in HH:MM:SS format
    ```

### Miscellaneous Functions

21. **Check if a Date is Valid**
    ```sql
    SELECT STR_TO_DATE('2025-02-30', '%Y-%m-%d') IS NOT NULL AS IsValidDate; -- Checks if date is valid (returns FALSE)
    ```

22. **Get Current Timestamp in UTC**
    ```sql
    SELECT UTC_TIMESTAMP(); -- Returns current UTC timestamp 
    ```

23. **Find Age Based on Birthdate**
    ```sql
    SELECT FLOOR(DATEDIFF(CURDATE(), '1990-05-15') / 365) AS Age; -- Calculates age based on birthdate 
    ```

24. **Calculate Future or Past Dates Using INTERVAL**
    ```sql
    SELECT NOW() + INTERVAL 1 MONTH AS FutureDate; -- Adds one month to current date and time 
    ```

25. **Using CASE with Dates for Conditional Logic**
    ```sql
    SELECT CASE 
        WHEN event_date < CURDATE() THEN 'Past Event'
        WHEN event_date = CURDATE() THEN 'Today'
        ELSE 'Future Event'
        END AS EventStatus 
      FROM events;
    ```

### Conclusion

This list provides a comprehensive range of SQL queries related to date and time usage, from basic retrieval to advanced manipulation and formatting techniques. These queries can help you effectively manage temporal data in your SQL databases! If you have any specific queries or need further examples, feel free to ask!

Citations:
[1] https://www.geeksforgeeks.org/sql-date-functions/
[2] https://popsql.com/learn-sql/sql-server/how-to-query-date-and-time-in-sql-server
[3] https://www.atlassian.com/data/sql/dates
[4] https://stackoverflow.com/questions/6119369/simple-datetime-sql-query
[5] https://www.geeksforgeeks.org/how-to-write-a-sql-query-for-a-specific-date-range-and-date-time/