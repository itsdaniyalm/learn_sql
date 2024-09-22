### **Part 11: Advanced SQL Topics and Best Practices**

**Objective:**  
- Explore advanced SQL concepts and best practices for writing efficient and maintainable SQL code.

**Contents:**
1. **Advanced SQL Functions**
   - **Window Functions**: Used for performing calculations across a set of table rows related to the current row. Common examples include `ROW_NUMBER()`, `RANK()`, and `SUM() OVER()`.
     - Example:
       ```sql
       SELECT first_name, last_name, salary,
              RANK() OVER (ORDER BY salary DESC) AS salary_rank
       FROM employees;
       ```
   - **Common Table Expressions (CTEs)**: Temporary result sets that can be referenced within a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement.
     - Example:
       ```sql
       WITH high_earners AS (
           SELECT first_name, last_name, salary
           FROM employees
           WHERE salary > 10000
       )
       SELECT * FROM high_earners;
       ```

2. **Best Practices for Writing SQL**
   - **Consistent Naming Conventions**: Use clear and consistent naming conventions for tables and columns to improve readability.
   - **Commenting Code**: Add comments to explain complex queries or business logic.
   - **Avoid Hardcoding Values**: Use parameters in queries to enhance flexibility and security.
   - **Use Transactions**: Wrap multiple related operations in transactions to ensure data integrity.
   - **Review Execution Plans**: Regularly analyze execution plans to identify and optimize slow queries.

3. **Performance Tuning Techniques**
   - **Refactor Complex Queries**: Break down complex queries into simpler parts or use CTEs to improve readability and performance.
   - **Monitor Query Performance**: Use tools and logs to monitor slow queries and identify potential issues.
   - **Optimize Index Usage**: Regularly review and adjust indexes based on query patterns.

4. **Database Design Principles**
   - **Normalization**: Organize data to reduce redundancy and improve integrity.
   - **Denormalization**: In some cases, denormalization can improve read performance at the expense of write performance.
   - **Use of Foreign Keys**: Enforce relationships between tables to maintain data integrity.

---

#### **Example Queries**

**Example Query 1: Window Function**
```sql
SELECT first_name, last_name, salary,
       ROW_NUMBER() OVER (PARTITION BY department_id ORDER BY salary DESC) AS row_num
FROM employees;
```
*Explanation:* This query assigns a unique sequential integer to rows within each department based on salary.
Sure! Here are some additional example exercises for window functions:

### **Exercise 1: Employee Ranking**
**Task:** Write a query to rank employees based on their salaries within each department. Include the employee's name, department ID, and their rank.

**Example Solution:**
```sql
SELECT first_name, last_name, department_id,
       RANK() OVER (PARTITION BY department_id ORDER BY salary DESC) AS salary_rank
FROM employees;
```

---

### **Exercise 2: Moving Average**
**Task:** Calculate a moving average salary for employees over the last 3 months based on their hire date. Assume you have a column `hire_date` to use for ordering.

**Example Solution:**
```sql
SELECT first_name, last_name, salary, hire_date,
       AVG(salary) OVER (ORDER BY hire_date ROWS BETWEEN 2 PRECEDING AND CURRENT ROW) AS moving_avg_salary
FROM employees;
```

---

### **Exercise 3: Cumulative Salary Total**
**Task:** Write a query to display each employee's salary and the cumulative total salary of all employees up to and including that employee.

**Example Solution:**
```sql
SELECT first_name, last_name, salary,
       SUM(salary) OVER (ORDER BY employee_id) AS cumulative_salary
FROM employees;
```

---

### **Exercise 4: Percentage of Total Salary**
**Task:** Calculate the percentage of each employee's salary relative to the total salary of all employees.

**Example Solution:**
```sql
SELECT first_name, last_name, salary,
       (salary / SUM(salary) OVER ()) * 100 AS salary_percentage
FROM employees;
```

---

### **Exercise 5: Previous and Next Salaries**
**Task:** Write a query to show each employee's salary, the salary of the employee before them, and the salary of the employee after them in the ordered list by salary.

**Example Solution:**
```sql
SELECT first_name, last_name, salary,
       LAG(salary) OVER (ORDER BY salary) AS previous_salary,
       LEAD(salary) OVER (ORDER BY salary) AS next_salary
FROM employees;
```

---

### **Exercise 6: Employee Count by Department**
**Task:** Display the number of employees in each department alongside each employee's details.

**Example Solution:**
```sql
SELECT first_name, last_name, department_id,
       COUNT(*) OVER (PARTITION BY department_id) AS employee_count
FROM employees;
```

---

These exercises cover a range of window function applications, from ranking and cumulative totals to moving averages and percentages. Let me know if you need more examples or any specific adjustments!


**Example Query 2: Common Table Expression (CTE)**
```sql
WITH department_summary AS (
    SELECT department_id, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
)
SELECT * FROM department_summary;
```
*Explanation:* This CTE calculates the average salary for each department.

Here are additional example exercises for Common Table Expressions (CTEs):

### **Exercise 1: Employee Salary Summary**
**Task:** Write a CTE to summarize the total salary paid per department and then select all departments with a total salary above $100,000.

**Example Solution:**
```sql
WITH department_salary AS (
    SELECT department_id, SUM(salary) AS total_salary
    FROM employees
    GROUP BY department_id
)
SELECT department_id, total_salary
FROM department_salary
WHERE total_salary > 100000;
```

---

### **Exercise 2: Recursive CTE for Employee Hierarchy**
**Task:** Create a recursive CTE to display the hierarchy of employees, showing each employee along with their manager's name.

**Example Solution:**
```sql
WITH RECURSIVE employee_hierarchy AS (
    SELECT employee_id, first_name, last_name, manager_id
    FROM employees
    WHERE manager_id IS NULL
    UNION ALL
    SELECT e.employee_id, e.first_name, e.last_name, e.manager_id
    FROM employees e
    INNER JOIN employee_hierarchy eh ON e.manager_id = eh.employee_id
)
SELECT * FROM employee_hierarchy;
```

---

### **Exercise 3: Employee Tenure**
**Task:** Write a CTE to calculate each employee's tenure in years, and then select employees who have been with the company for more than 5 years.

**Example Solution:**
```sql
WITH employee_tenure AS (
    SELECT first_name, last_name, hire_date,
           TRUNC(MONTHS_BETWEEN(SYSDATE, hire_date)) AS tenure_years
    FROM employees
)
SELECT first_name, last_name, tenure_years
FROM employee_tenure
WHERE tenure_years > 5;
```

---

### **Exercise 4: Department Average Salary**
**Task:** Create a CTE that calculates the average salary per department and select departments with an average salary greater than the overall average salary.

**Example Solution:**
```sql
WITH department_avg AS (
    SELECT department_id, AVG(salary) AS avg_salary
    FROM employees
    GROUP BY department_id
),
overall_avg AS (
    SELECT AVG(salary) AS overall_average
    FROM employees
)
SELECT da.department_id, da.avg_salary
FROM department_avg da, overall_avg oa
WHERE da.avg_salary > oa.overall_average;
```

---

### **Exercise 5: Latest Hired Employees**
**Task:** Write a CTE to get the most recently hired employee in each department.

**Example Solution:**
```sql
WITH latest_hire AS (
    SELECT department_id, first_name, last_name, hire_date,
           RANK() OVER (PARTITION BY department_id ORDER BY hire_date DESC) AS hire_rank
    FROM employees
)
SELECT department_id, first_name, last_name, hire_date
FROM latest_hire
WHERE hire_rank = 1;
```

---

### **Exercise 6: Employees with High Salary and Bonus**
**Task:** Create a CTE that calculates the total compensation (salary + bonus) for each employee and select those whose total compensation is in the top 10%.

**Example Solution:**
```sql
WITH total_compensation AS (
    SELECT employee_id, first_name, last_name, 
           (salary + COALESCE(bonus, 0)) AS total_comp
    FROM employees
),
salary_threshold AS (
    SELECT PERCENTILE_CONT(0.90) WITHIN GROUP (ORDER BY total_comp) AS top_10_percent
    FROM total_compensation
)
SELECT employee_id, first_name, last_name, total_comp
FROM total_compensation
WHERE total_comp >= (SELECT top_10_percent FROM salary_threshold);
```

---

#### **Practice Questions:**

1. Write a query using a window function to find the top 3 highest salaries in the `employees` table.
2. Create a CTE that lists employees who have been with the company for more than 5 years.
3. Explain the importance of normalization in database design.
4. Describe how you would approach optimizing a slow-running query.
5. Write a SQL command to create an index on the `salary` column of the `employees` table.

---

#### **Answers:**

1. ```sql
   SELECT first_name, last_name, salary,
          RANK() OVER (ORDER BY salary DESC) AS salary_rank
   FROM employees
   WHERE salary_rank <= 3;
   ```
2. ```sql
   WITH long_term_employees AS (
       SELECT first_name, last_name, hire_date
       FROM employees
       WHERE hire_date <= ADD_MONTHS(SYSDATE, -60)
   )
   SELECT * FROM long_term_employees;
   ```
3. Normalization reduces data redundancy, improves data integrity, and makes the database more efficient by organizing data into related tables.
4. I would analyze the execution plan to identify bottlenecks, ensure proper indexing, rewrite complex queries for efficiency, and possibly break them into simpler queries.
5. ```sql
   CREATE INDEX idx_salary ON employees (salary);
   ```

---

That concludes our SQL course! Are there any specific topics you'd like to revisit or any final questions you have?