### **Part 7: Set Operations (UNION, INTERSECT, MINUS)**

**Objective:**  
- Learn how to combine results from multiple queries using set operations like `UNION`, `INTERSECT`, and `MINUS`.

**Contents:**
1. **Introduction to Set Operations**
   - Set operations allow you to combine the results of two or more queries into a single result set.
   - The queries combined must have the same number of columns, and the corresponding columns must have compatible data types.

2. **Using UNION and UNION ALL**
   - **UNION** combines the results of two queries and removes duplicate rows.
   - **UNION ALL** combines the results and includes duplicates.
   - Syntax:
     ```sql
     SELECT column1, column2 FROM table1
     UNION
     SELECT column1, column2 FROM table2;
     ```

3. **Using INTERSECT**
   - **INTERSECT** returns only the rows that are common between two queries.
   - Syntax:
     ```sql
     SELECT column1, column2 FROM table1
     INTERSECT
     SELECT column1, column2 FROM table2;
     ```

4. **Using MINUS**
   - **MINUS** returns the rows from the first query that are not present in the second query.
   - Syntax:
     ```sql
     SELECT column1, column2 FROM table1
     MINUS
     SELECT column1, column2 FROM table2;
     ```

---

#### **Example Queries**

**Example Query 1: UNION**
```sql
SELECT department_id FROM employees WHERE job_id = 'IT_PROG'
UNION
SELECT department_id FROM employees WHERE job_id = 'ST_CLERK';
```
*Explanation:* This query returns the department IDs where employees work as either 'IT_PROG' or 'ST_CLERK', without duplicates.

**Example Query 2: MINUS**
```sql
SELECT employee_id FROM employees WHERE department_id = 10
MINUS
SELECT employee_id FROM employees WHERE job_id = 'AC_ACCOUNT';
```
*Explanation:* This query returns the IDs of employees who work in department 10 but do not have the job ID 'AC_ACCOUNT'.

---

#### **Practice Questions:**

1. Write a query to find all department IDs that have employees with either 'SA_REP' or 'SH_CLERK' jobs (use UNION).
2. Retrieve the names of employees who have the same first name in two different departments (use INTERSECT).
3. List the job titles that are held by employees in department 60 but not in department 90 (use MINUS).
4. Fetch the email addresses of employees who are either 'AD_VP' or 'AD_PRES', ensuring no duplicates (use UNION).
5. Find the employee IDs that are in the 'HR' department but not in the 'Finance' department (use MINUS).

---

#### **Answers:**

1. ```sql
   SELECT department_id FROM employees WHERE job_id = 'SA_REP'
   UNION
   SELECT department_id FROM employees WHERE job_id = 'SH_CLERK';
   ```
2. ```sql
   SELECT first_name FROM employees WHERE department_id = 10
   INTERSECT
   SELECT first_name FROM employees WHERE department_id = 20;
   ```
3. ```sql
   SELECT job_id FROM employees WHERE department_id = 60
   MINUS
   SELECT job_id FROM employees WHERE department_id = 90;
   ```
4. ```sql
   SELECT email FROM employees WHERE job_id = 'AD_VP'
   UNION
   SELECT email FROM employees WHERE job_id = 'AD_PRES';
   ```
5. ```sql
   SELECT employee_id FROM employees WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'HR')
   MINUS
   SELECT employee_id FROM employees WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'Finance');
   ```