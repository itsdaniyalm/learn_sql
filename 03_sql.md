### **Part 3: Sorting Data with the ORDER BY Clause**

**Objective:**  
- Learn to sort query results using the `ORDER BY` clause.

**Contents:**
1. **Introduction to ORDER BY**
   - The `ORDER BY` clause is used to sort the result set by one or more columns.
   - By default, the sorting is done in ascending order (from smallest to largest).

2. **Sorting in Ascending and Descending Order**
   - `ASC`: Sorts the data in ascending order (default).
   - `DESC`: Sorts the data in descending order.

3. **Sorting by Multiple Columns**
   - You can sort the result by multiple columns by separating them with commas.
   - The result is first sorted by the first column, and then by the second column for rows where the first column values are the same.

4. **Handling NULL Values in Sorting**
   - By default, NULL values appear last in ascending order and first in descending order.

---

#### **Example Queries**

**Example Query 1:**
```sql
SELECT first_name, last_name 
FROM employees 
ORDER BY last_name ASC;
```
*Explanation:* This query retrieves the first and last names of all employees, sorted by their last names in ascending order.

**Example Query 2:**
```sql
SELECT first_name, last_name, salary 
FROM employees 
ORDER BY salary DESC;
``}
*Explanation:* This query retrieves the first name, last name, and salary of employees, sorted by salary in descending order.

---

#### **Practice Questions:**

1. Write a query to list all job titles sorted alphabetically.
2. Retrieve the department IDs and names, sorted by department name in descending order.
3. List the first and last names of employees, sorted by their hire date in ascending order.
4. Fetch the names of employees who earn less than 3000, sorted by salary in ascending order.
5. List the employee IDs and job IDs, sorted by employee ID in descending order.

---

#### **Answers:**

1. ```sql
   SELECT job_title FROM jobs ORDER BY job_title ASC;
   ```
2. ```sql
   SELECT department_id, department_name FROM departments ORDER BY department_name DESC;
   ```
3. ```sql
   SELECT first_name, last_name FROM employees ORDER BY hire_date ASC;
   ```
4. ```sql
   SELECT first_name, last_name FROM employees WHERE salary < 3000 ORDER BY salary ASC;
   ```
5. ```sql
   SELECT employee_id, job_id FROM employees ORDER BY employee_id DESC;
   ```