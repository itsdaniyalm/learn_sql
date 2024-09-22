### **Part 2: Filtering Data with the WHERE Clause**

**Objective:**  
- Learn how to filter data using the `WHERE` clause to retrieve specific subsets of data from a table.

**Contents:**
1. **Introduction to the WHERE Clause**
   - The `WHERE` clause is used to filter records that meet certain conditions.
   - Syntax:  
     ```sql
     SELECT column1, column2, ...
     FROM table_name
     WHERE condition;
     ```

2. **Using Comparison Operators**
   - `=` (equal to)
   - `!=` or `<>` (not equal to)
   - `<` (less than), `>` (greater than)
   - `<=` (less than or equal to), `>=` (greater than or equal to)

3. **Combining Conditions with AND, OR**
   - Combine multiple conditions using `AND` (both conditions must be true) and `OR` (at least one condition must be true).

4. **Using BETWEEN, IN, LIKE, and IS NULL**
   - `BETWEEN`: Filters within a range.
   - `IN`: Filters for specific values in a list.
   - `LIKE`: Filters based on patterns (e.g., `%` for wildcards).
   - `IS NULL`: Filters for NULL (missing) values.

---

#### **Example Queries**

**Example Query 1:**
```sql
SELECT first_name, last_name 
FROM employees 
WHERE department_id = 90;
```
*Explanation:* This query retrieves the first and last names of employees who work in department 90.

**Example Query 2:**
```sql
SELECT first_name, last_name 
FROM employees 
WHERE salary BETWEEN 5000 AND 10000;
```
*Explanation:* This query retrieves the names of employees whose salaries are between 5000 and 10000.

---

#### **Practice Questions:**

1. Write a query to find all employees who work in department 50.
2. Retrieve the job IDs of employees who earn more than 8000.
3. List the names of employees whose last name starts with 'S'.
4. Fetch the employee ID and first name of employees who work as 'IT_PROG'.
5. Find all departments that are either in location 1700 or 1800.

---

#### **Answers:**

1. ```sql
   SELECT first_name, last_name FROM employees WHERE department_id = 50;
   ```
2. ```sql
   SELECT job_id FROM employees WHERE salary > 8000;
   ```
3. ```sql
   SELECT first_name, last_name FROM employees WHERE last_name LIKE 'S%';
   ```
4. ```sql
   SELECT employee_id, first_name FROM employees WHERE job_id = 'IT_PROG';
   ```
5. ```sql
   SELECT department_name FROM departments WHERE location_id IN (1700, 1800);
   ```