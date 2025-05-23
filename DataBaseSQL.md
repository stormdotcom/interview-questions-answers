### SQL and Database Questions with Answers

#### 1. **What is the cardinality between library members and books in a library system where each book can be borrowed by multiple members, but each member can borrow only one copy of a book at a time?**

**Answer:** Many-to-Many

---

#### 2. **What is the cardinality between users and friends in a Facebook-like system where each user can have many friends, and each friend is also a user?**

**Answer:** Many-to-Many

---

#### 3. **How should the relationship between support tickets and the customer who raised them be represented in a customer support system?**

**Answer:** Include customer IDs in support ticket records.

---

#### 4. **How does an index impact `INSERT` and `UPDATE` operations?**

**Answer:** Slows down both `INSERT` and `UPDATE` operations.

---

#### 5. **What isolation level in a database is used when you want to ensure that, within a transaction, you consistently see the same snapshot of the data, even if other transactions are modifying the data concurrently?**

**Answer:** Repeatable Read

---

#### 6. **Which isolation level provides the highest level of data consistency but may lead to decreased concurrency?**

**Answer:** Serializable

---

#### 7. **Write an SQL query to retrieve distinct product categories with a quantity in stock less than 100. Include only those categories and order the result alphabetically.**

**Query:**

```sql
SELECT DISTINCT category
FROM ProductInventory
WHERE quantity_in_stock < 100
ORDER BY category ASC;
```

---

#### 8. **Find customers who have made at least 2 orders. Retrieve their first name and the total money spent (money_spent) and order by `money_spent` in descending order.**

**Query:**

```sql
SELECT c.first_name, SUM(p.price * o.qty) AS money_spent
FROM Customers c
JOIN Orders o ON c.id = o.cid
JOIN Products p ON o.pid = p.id
GROUP BY c.id
HAVING COUNT(o.id) >= 2
ORDER BY money_spent DESC;
```

---

#### 9. **Calculate the profit margin for each product and order results by `profit_margin` in descending order.**

**Query:**

```sql
SELECT sale_id, product_name, cost_price, selling_price,
       ROUND(((selling_price - cost_price) / cost_price) * 100, 4) AS profit_margin
FROM Sales
ORDER BY profit_margin DESC;
```

---

#### 10. **Find the youngest voter for each candidate and order the result alphabetically by candidate name and voter name.**

**Query:**

```sql
SELECT c.candidate_name, v.voter_name AS youngest_voter
FROM Votes vt
JOIN Voters v ON vt.voter_id = v.voter_id
JOIN Candidates c ON vt.candidate_id = c.candidate_id
WHERE v.voter_age = (
    SELECT MIN(v2.voter_age)
    FROM Votes vt2
    JOIN Voters v2 ON vt2.voter_id = v2.voter_id
    WHERE vt2.candidate_id = vt.candidate_id
)
ORDER BY c.candidate_name, youngest_voter;
```

---

#### 11. **Find the department names where the maximum bonus is less than the average bonus across all departments.**

**Query:**

```sql
WITH DepartmentMaxBonus AS (
    SELECT e.department_id, MAX(b.bonus_amount) AS max_bonus
    FROM Employees e
    JOIN Bonuses b ON e.employee_id = b.employee_id
    GROUP BY e.department_id
),
AverageBonus AS (
    SELECT AVG(bonus_amount) AS avg_bonus
    FROM Bonuses
)
SELECT d.department_name
FROM Departments d
JOIN DepartmentMaxBonus dmb ON d.department_id = dmb.department_id
JOIN AverageBonus ab
WHERE dmb.max_bonus < ab.avg_bonus;
```

---

#### 12. **Find the employee with the highest salary in each department and return results ordered by `department_id`.**

**Query:**

```sql
SELECT e.first_name, e.last_name, e.salary, e.department_id
FROM Employees e
JOIN (
    SELECT department_id, MAX(salary) AS max_salary
    FROM Employees
    GROUP BY department_id
) d ON e.department_id = d.department_id AND e.salary = d.max_salary
ORDER BY e.department_id ASC;
```

---

#### 13. **Write an SQL query to fetch all customers who bought a specific product and return their names.**

**Query:**

```sql
SELECT DISTINCT c.first_name, c.last_name
FROM Customers c
JOIN Orders o ON c.id = o.cid
JOIN Products p ON o.pid = p.id
WHERE p.name = 'Specific Product';
```

---

#### 14. **Retrieve all products with prices either above 50 or below 30, starting from the fourth matching product, and display 3 such products.**

**Query:**

```sql
SELECT *
FROM Products
WHERE price > 50 OR price < 30
ORDER BY product_id
LIMIT 3 OFFSET 3;
```

---

#### 15. **Find the total bonus amount for each department ordered by department ID.**

**Query:**

```sql
SELECT d.department_id, d.department_name, SUM(b.bonus_amount) AS total_bonus
FROM Departments d
JOIN Employees e ON d.department_id = e.department_id
JOIN Bonuses b ON e.employee_id = b.employee_id
GROUP BY d.department_id, d.department_name
ORDER BY d.department_id;
```

---

#### 16. **Find customers who didn’t place any orders and list their names.**

**Query:**

```sql
SELECT c.first_name, c.last_name
FROM Customers c
LEFT JOIN Orders o ON c.id = o.cid
WHERE o.id IS NULL;
```

---

#### 17. **Write an SQL query to retrieve all product categories that have a total stock quantity of more than 500.**

**Query:**

```sql
SELECT category
FROM ProductInventory
GROUP BY category
HAVING SUM(quantity_in_stock) > 500;
```

---

#### 18. **Fetch all employees earning a salary above the average salary in their department.**

**Query:**

```sql
SELECT e.first_name, e.last_name, e.salary, e.department_id
FROM Employees e
JOIN (
    SELECT department_id, AVG(salary) AS avg_salary
    FROM Employees
    GROUP BY department_id
) avg_salaries ON e.department_id = avg_salaries.department_id
WHERE e.salary > avg_salaries.avg_salary;
```

---

#### 19. **Retrieve the most expensive product in each category.**

**Query:**

```sql
SELECT category, product_name, MAX(price) AS max_price
FROM Products
GROUP BY category;
```

---

#### 20. **Find duplicate customer records based on their email address.**

**Query:**

```sql
SELECT email, COUNT(*) AS occurrences
FROM Customers
GROUP BY email
HAVING COUNT(*) > 1;
```

---

**Question:**  
How can you find duplicate emails along with their associated first names in a SQL table named `users` with columns `id, email, firstName, lastName, phoneNumber`?

**Answer:**  
You can use a subquery to identify emails that appear more than once, and then select rows with those emails. Here's an example SQL query that accomplishes this:

```sql
SELECT email, firstName
FROM users
WHERE email IN (
  SELECT email
  FROM users
  GROUP BY email
  HAVING COUNT(*) > 1
)
ORDER BY email;
```

**Explanation:**

- **Subquery:**

  ```sql
  SELECT email
  FROM users
  GROUP BY email
  HAVING COUNT(*) > 1
  ```

  This subquery groups the rows by the `email` field and filters out those groups that have a count greater than one, which identifies duplicate emails.

- **Main Query:**
  ```sql
  SELECT email, firstName
  FROM users
  WHERE email IN ( ... )
  ORDER BY email;
  ```
  The main query selects the `email` and `firstName` from the `users` table where the email exists in the list of duplicate emails provided by the subquery. The results are then ordered by email for easier review.
