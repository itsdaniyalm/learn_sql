### **Part 8: Using Views in SQL**

**Objective:**  
- Understand what views are and how to create, use, and manage them in SQL.

**Contents:**
1. **Introduction to Views**
   - A view is a virtual table based on the result set of a SQL query. It does not store data physically; instead, it dynamically retrieves data from the underlying tables.
   - Views can simplify complex queries, enhance security, and provide a level of abstraction.

2. **Creating a View**
   - Syntax to create a view:
     ```sql
     CREATE VIEW view_name AS
     SELECT column1, column2, ...
     FROM table_name
     WHERE condition;
     ```
   - Example:
     ```sql
     CREATE VIEW employee_details AS
     SELECT first_name, last_name, department_id
     FROM employees;
     ```

3. **Using a View**
   - You can query a view just like a regular table:
     ```sql
     SELECT * FROM employee_details;
     ```

4. **Updating a View**
   - If the view is updatable (based on the underlying tables), you can use `INSERT`, `UPDATE`, or `DELETE` statements:
     ```sql
     UPDATE employee_details
     SET department_id = 50
     WHERE last_name = 'Smith';
     ```

5. **Dropping a View**
   - To remove a view, use:
     ```sql
     DROP VIEW view_name;
     ```
   - Example:
     ```sql
     DROP VIEW employee_details;
     ```

---

#### **Example Queries**

**Example Query 1: Creating a View**
```sql
CREATE VIEW high_salary_employees AS
SELECT first_name, last_name, salary 
FROM employees 
WHERE salary > 10000;
```
*Explanation:* This query creates a view that includes employees earning more than 10,000.

**Example Query 2: Using a View**
```sql
SELECT * FROM high_salary_employees;
```
*Explanation:* This query retrieves all records from the `high_salary_employees` view.

---

#### **Practice Questions:**

1. Write a query to create a view that shows all employees in department 30.
2. Retrieve the names and salaries of employees from the view created in question 1.
3. Create a view that includes employees who were hired after January 1, 2020.
4. Update the view to increase the salary of employees with the last name 'Johnson' by 10%.
5. Drop the view created in question 3.

---

#### **Answers:**

1. ```sql
   CREATE VIEW department_30_employees AS
   SELECT first_name, last_name FROM employees WHERE department_id = 30;
   ```
2. ```sql
   SELECT * FROM department_30_employees;
   ```
3. ```sql
   CREATE VIEW recent_hires AS
   SELECT first_name, last_name, hire_date FROM employees WHERE hire_date > '2020-01-01';
   ```
4. ```sql
   UPDATE recent_hires SET salary = salary * 1.10 WHERE last_name = 'Johnson';
   ```
5. ```sql
   DROP VIEW recent_hires;
   ```