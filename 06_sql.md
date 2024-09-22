### **Part 6: Subqueries and Nested Queries**

**Objective:**  
- Learn how to use subqueries (also known as inner queries or nested queries) to perform more complex SQL operations.

**Contents:**
1. **Introduction to Subqueries**
   - A subquery is a query within another SQL query, used to return data that will be used in the main query as a condition to further refine the data retrieval.
   - A subquery can be used in various clauses like `SELECT`, `FROM`, `WHERE`, and `HAVING`.

2. **Types of Subqueries**
   - **Single-row subquery**: Returns a single row. Used with comparison operators like `=`, `<`, `>`, etc.
   - **Multi-row subquery**: Returns multiple rows. Used with operators like `IN`, `ANY`, `ALL`.
   - **Correlated subquery**: A subquery that references columns from the outer query. It is executed once for each row processed by the outer query.

3. **Using Subqueries in the WHERE Clause**
   - Syntax:
     ```sql
     SELECT columns
     FROM table
     WHERE column = (SELECT column FROM table WHERE condition);
     ```
   - Example:
     ```sql
     SELECT first_name, last_name
     FROM employees
     WHERE department_id = (SELECT department_id FROM departments WHERE department_name = 'Sales');
     ```

4. **Using Subqueries in the SELECT Clause**
   - Syntax:
     ```sql
     SELECT column, (SELECT column FROM table WHERE condition) AS alias
     FROM table;
     ```
   - Example:
     ```sql
     SELECT first_name, last_name, 
     (SELECT department_name FROM departments WHERE departments.department_id = employees.department_id) AS department_name
     FROM employees;
     ```

5. **Using Subqueries in the FROM Clause**
   - Syntax:
     ```sql
     SELECT columns
     FROM (SELECT columns FROM table WHERE condition) AS subquery_alias;
     ```
   - Example:
     ```sql
     SELECT subquery.first_name, subquery.last_name
     FROM (SELECT first_name, last_name FROM employees WHERE salary > 10000) AS subquery;
     ```

---

#### **Example Queries**

**Example Query 1: Single-Row Subquery in WHERE Clause**
```sql
SELECT first_name, last_name 
FROM employees 
WHERE salary = (SELECT MAX(salary) FROM employees);
```
*Explanation:* This query retrieves the first and last names of the employee(s) with the highest salary.

**Example Query 2: Multi-Row Subquery in WHERE Clause**
```sql
SELECT first_name, last_name 
FROM employees 
WHERE department_id IN (SELECT department_id FROM departments WHERE location_id = 1700);
```
*Explanation:* This query retrieves the names of employees who work in departments located in location 1700.

---

#### **Practice Questions:**

1. Write a query to find the names of employees who have the same job title as the employee with ID 100.
2. Retrieve the department name and location of the department with the highest number of employees.
3. List the names of employees whose salaries are above the average salary of the company.
4. Fetch the first and last names of employees who work in the same department as 'Alexander'.
5. Find the names of employees who earn less than the average salary in their department.

---

#### **Answers:**

1. ```sql
   SELECT first_name, last_name 
   FROM employees 
   WHERE job_id = (SELECT job_id FROM employees WHERE employee_id = 100);
   ```
2. ```sql
   SELECT department_name, location_id 
   FROM departments 
   WHERE department_id = (SELECT department_id FROM employees GROUP BY department_id ORDER BY COUNT(*) DESC FETCH FIRST 1 ROWS ONLY);
   ```
3. ```sql
   SELECT first_name, last_name 
   FROM employees 
   WHERE salary > (SELECT AVG(salary) FROM employees);
   ```
4. ```sql
   SELECT first_name, last_name 
   FROM employees 
   WHERE department_id = (SELECT department_id FROM employees WHERE first_name = 'Alexander');
   ```
5. ```sql
   SELECT first_name, last_name 
   FROM employees 
   WHERE salary < (SELECT AVG(salary) FROM employees WHERE department_id = employees.department_id);
   ```