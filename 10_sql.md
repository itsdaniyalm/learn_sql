### **Part 10: Understanding Transactions in SQL**

**Objective:**  
- Learn what transactions are, their properties, and how to manage them using SQL commands.

**Contents:**
1. **Introduction to Transactions**
   - A transaction is a sequence of one or more SQL operations that are treated as a single unit of work.
   - Transactions ensure data integrity and consistency in the database.

2. **ACID Properties**
   - Transactions are governed by the ACID properties:
     - **Atomicity**: Ensures that all operations within a transaction are completed; if one fails, the entire transaction fails.
     - **Consistency**: Ensures that a transaction brings the database from one valid state to another.
     - **Isolation**: Ensures that transactions do not interfere with each other.
     - **Durability**: Ensures that the results of a completed transaction are permanently recorded in the database.

3. **Managing Transactions**
   - Common SQL commands for transaction management:
     - **BEGIN**: Starts a new transaction.
     - **COMMIT**: Saves all changes made in the transaction.
     - **ROLLBACK**: Undoes all changes made in the transaction.
   - Syntax:
     ```sql
     BEGIN;
     -- SQL operations
     COMMIT; -- or ROLLBACK;
     ```

4. **Example of a Transaction**
   - Example: Transferring funds between accounts.
     ```sql
     BEGIN;
     UPDATE accounts SET balance = balance - 100 WHERE account_id = 1;
     UPDATE accounts SET balance = balance + 100 WHERE account_id = 2;
     COMMIT;
     ```

---

#### **Example Queries**

**Example Query 1: Starting a Transaction**
```sql
BEGIN;
```
*Explanation:* This command starts a new transaction.

**Example Query 2: Committing a Transaction**
```sql
COMMIT;
```
*Explanation:* This command saves all changes made during the transaction.

**Example Query 3: Rolling Back a Transaction**
```sql
ROLLBACK;
```
*Explanation:* This command undoes all changes made during the transaction if an error occurs.

---

#### **Practice Questions:**

1. Write a transaction to deduct 200 from one employee's salary and add it to another employee's salary.
2. Create a transaction that inserts a new employee record, and if it fails, rolls back any changes.
3. Explain the importance of using `ROLLBACK` in transactions.
4. Write a transaction to transfer money between two accounts, ensuring both updates occur or neither does.
5. Describe what happens to a transaction if an error occurs after a `COMMIT`.

---

#### **Answers:**

1. ```sql
   BEGIN;
   UPDATE employees SET salary = salary - 200 WHERE employee_id = 101;
   UPDATE employees SET salary = salary + 200 WHERE employee_id = 102;
   COMMIT;
   ```
2. ```sql
   BEGIN;
   INSERT INTO employees (first_name, last_name, job_id) VALUES ('John', 'Doe', 'IT_PROG');
   -- If an error occurs:
   ROLLBACK; 
   ```
3. `ROLLBACK` is important in transactions as it allows you to undo changes if an error occurs, maintaining data integrity.
4. ```sql
   BEGIN;
   UPDATE accounts SET balance = balance - 100 WHERE account_id = 1;
   UPDATE accounts SET balance = balance + 100 WHERE account_id = 2;
   COMMIT;
   ```
5. If an error occurs after a `COMMIT`, the changes made in that transaction are permanent, and you cannot roll them back.