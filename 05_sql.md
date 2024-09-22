### **Part 5: Joining Tables**

**Objective:**  
- Learn how to combine data from multiple tables using different types of joins.

**Contents:**
1. **Introduction to Joins**
   - Joins are used to combine rows from two or more tables based on a related column between them.
   - Common types of joins include:
     - **INNER JOIN**: Returns only the rows where there is a match in both tables.
     - **LEFT JOIN (or LEFT OUTER JOIN)**: Returns all rows from the left table, and the matched rows from the right table. If no match, NULL values are returned for columns from the right table.
     - **RIGHT JOIN (or RIGHT OUTER JOIN)**: Returns all rows from the right table, and the matched rows from the left table. If no match, NULL values are returned for columns from the left table.
     - **FULL OUTER JOIN**: Returns all rows when there is a match in one of the tables. Returns NULL for non-matching rows.

2. **Using INNER JOIN**
   - Syntax:
     ```sql
     SELECT columns
     FROM table1
     INNER JOIN table2
     ON table1.column = table2.column;
     ```
   - Example:
     ```sql
     SELECT employees.first_name, employees.last_name, departments.department_name
     FROM employees
     INNER JOIN departments
     ON employees.department_id = departments.department_id;
     ```

3. **Using LEFT JOIN**
   - Syntax:
     ```sql
     SELECT columns
     FROM table1
     LEFT JOIN table2
     ON table1.column = table2.column;
     ```
   - Example:
     ```sql
     SELECT employees.first_name, employees.last_name, departments.department_name
     FROM employees
     LEFT JOIN departments
     ON employees.department_id = departments.department_id;
     ```

4. **Using RIGHT JOIN and FULL OUTER JOIN**
   - Similar to LEFT JOIN but with different results depending on which table's rows are fully returned.

---

#### **Example Queries**

**Example Query 1: INNER JOIN**
```sql
SELECT employees.first_name, employees.last_name, departments.department_name
FROM employees
INNER JOIN departments
ON employees.department_id = departments.department_id;
```
*Explanation:* This query retrieves the first and last names of employees along with their department names, but only for employees who have a department.

**Example Query 2: LEFT JOIN**
```sql
SELECT employees.first_name, employees.last_name, departments.department_name
FROM employees
LEFT JOIN departments
ON employees.department_id = departments.department_id;
```
*Explanation:* This query retrieves the first and last names of all employees along with their department names. If an employee does not have a department, the department name will be NULL.

---

#### **Practice Questions:**

1. Write a query to find the job title and department name of all employees using an INNER JOIN.
2. Retrieve the names of all departments and the number of employees in each department using a LEFT JOIN.
3. List the names of all employees and their managers (use `employees` table to join with itself).
4. Fetch all job titles along with the names of employees holding those jobs using an INNER JOIN.
5. Find the names of employees and their department names, including employees without a department using a RIGHT JOIN.

---

#### **Answers:**

1. ```sql
   SELECT employees.first_name, employees.last_name, jobs.job_title, departments.department_name
   FROM employees
   INNER JOIN jobs ON employees.job_id = jobs.job_id
   INNER JOIN departments ON employees.department_id = departments.department_id;
   ```
2. ```sql
   SELECT departments.department_name, COUNT(employees.employee_id) 
   FROM departments
   LEFT JOIN employees ON departments.department_id = employees.department_id
   GROUP BY departments.department_name;
   ```
3. ```sql
   SELECT e.first_name AS Employee, m.first_name AS Manager
   FROM employees e
   LEFT JOIN employees m ON e.manager_id = m.employee_id;
   ```
4. ```sql
   SELECT jobs.job_title, employees.first_name, employees.last_name
   FROM jobs
   INNER JOIN employees ON jobs.job_id = employees.job_id;
   ```
5. ```sql
   SELECT employees.first_name, employees.last_name, departments.department_name
   FROM employees
   RIGHT JOIN departments ON employees.department_id = departments.department_id;
   ```

