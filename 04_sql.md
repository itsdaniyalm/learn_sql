### **Part 4: Using Aggregate Functions**

**Objective:**  
- Understand and use aggregate functions like `COUNT`, `SUM`, `AVG`, `MIN`, and `MAX` to perform calculations on data.

**Contents:**
1. **Introduction to Aggregate Functions**
   - Aggregate functions perform calculations on a set of values and return a single value.
   - Common aggregate functions include:
     - `COUNT()`: Returns the number of rows.
     - `SUM()`: Returns the total sum of a numeric column.
     - `AVG()`: Returns the average value of a numeric column.
     - `MIN()`: Returns the minimum value in a column.
     - `MAX()`: Returns the maximum value in a column.

2. **Using GROUP BY Clause**
   - The `GROUP BY` clause groups rows that have the same values in specified columns into summary rows, like "total sales per department."
   - Syntax:  
     ```sql
     SELECT column1, aggregate_function(column2)
     FROM table_name
     WHERE condition
     GROUP BY column1;
     ```

3. **Filtering Groups with HAVING Clause**
   - The `HAVING` clause is used to filter groups based on aggregate values.
   - It works similarly to the `WHERE` clause, but is used for groups.

---

#### **Example Queries**

**Example Query 1:**
```sql
SELECT COUNT(*) 
FROM employees;
```
*Explanation:* This query returns the total number of employees.

**Example Query 2:**
```sql
SELECT department_id, AVG(salary) 
FROM employees 
GROUP BY department_id;
```
*Explanation:* This query returns the average salary for each department by grouping the employees based on their department ID.

---

#### **Practice Questions:**

1. Write a query to find the total number of departments.
2. Retrieve the maximum salary from the `employees` table.
3. List the average salary of employees who work as 'SA_REP'.
4. Fetch the number of employees in each department.
5. Find the minimum salary of employees grouped by their job ID.

---

#### **Answers:**

1. ```sql
   SELECT COUNT(*) FROM departments;
   ```
2. ```sql
   SELECT MAX(salary) FROM employees;
   ```
3. ```sql
   SELECT AVG(salary) FROM employees WHERE job_id = 'SA_REP';
   ```
4. ```sql
   SELECT department_id, COUNT(*) FROM employees GROUP BY department_id;
   ```
5. ```sql
   SELECT job_id, MIN(salary) FROM employees GROUP BY job_id;
   ```
