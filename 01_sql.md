### **SQL for Beginners: Course Outline Using Oracle Live SQL Human Resources Schema**

We'll begin with basic concepts and gradually advance in complexity.

---

### **Part 1: Introduction to SQL and the HR Schema**

**Objective:**  
- Understand the basics of SQL.
- Familiarize yourself with the Oracle HR schema.

**Contents:**
1. **What is SQL?**
   - SQL (Structured Query Language) is used to manage and manipulate relational databases.
   - It enables users to query, update, and manage databases.

2. **Oracle Live SQL and the HR Schema**
   - Oracle Live SQL is an online platform to practice SQL queries.
   - The HR schema contains tables like `employees`, `departments`, `jobs`, and more.

3. **Basic SQL Query Structure**
   - `SELECT` statement for retrieving data.
   - `FROM` clause to specify the table from which to retrieve the data.

---

#### **Example Queries**

**Example Query 1:**
```sql
SELECT first_name, last_name 
FROM employees;
```
*Explanation:* This query retrieves the first and last names of all employees from the `employees` table.

**Example Query 2:**
```sql
SELECT department_name 
FROM departments;
```
*Explanation:* This query retrieves the names of all departments from the `departments` table.

---

#### **Practice Questions:**

1. Write a query to retrieve all job titles from the `jobs` table.
2. Retrieve the email addresses of all employees.
3. List the department IDs and names from the `departments` table.
4. Fetch the employee ID and job ID from the `employees` table.
5. Retrieve the names of all employees whose last name is 'King'.

---

#### **Answers:**

1. ```sql
   SELECT job_title FROM jobs;
   ```
2. ```sql
   SELECT email FROM employees;
   ```
3. ```sql
   SELECT department_id, department_name FROM departments;
   ```
4. ```sql
   SELECT employee_id, job_id FROM employees;
   ```
5. ```sql
   SELECT first_name, last_name FROM employees WHERE last_name = 'King';
   ```
