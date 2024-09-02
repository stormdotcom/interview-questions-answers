# Interview Questions and Answers

## Node.js Overview:

Node.js is a popular server-side technology that allows developers to use JavaScript, which was traditionally a client-side scripting language, on the server side as well. It is built on the V8 JavaScript engine, developed by Google, which compiles JavaScript directly into machine code, making Node.js applications fast and efficient.

Why Node.js is Adopted as a Server-Side Technology:

Single Language for Both Client and Server: With Node.js, developers can use JavaScript for both client-side and server-side development, streamlining the development process and allowing for better collaboration and code sharing.

High Performance: The V8 engine optimizes JavaScript execution, providing high performance by compiling code into highly optimized machine code.

Non-blocking Asynchronous Architecture: One of the key features of Node.js is its non-blocking, event-driven architecture. This means Node.js can handle multiple requests at the same time without waiting for one request to finish before starting another. This is ideal for I/O-heavy operations, such as reading from files or databases, or handling network requests.

Asynchronous Nature and Event Loop in Node.js:

Node.js operates in a single-threaded environment but achieves concurrency using the concept of asynchronous I/O and a mechanism known as the event loop. This event loop is a fundamental part of Node.js's architecture and is responsible for handling all asynchronous operations.

Understanding the Event Loop and libuv:

libuv: The event loop in Node.js is powered by libuv, a C library that provides the asynchronous I/O capabilities to Node.js. libuv allows Node.js to handle multiple connections concurrently by offloading operations to the underlying operating system, which can manage multiple threads or processes.

Event Loop Phases: The event loop in Node.js has several phases that it goes through to manage asynchronous operations. The major phases are:

Timers: This phase executes callbacks scheduled by setTimeout() and setInterval().

Pending Callbacks: Executes I/O callbacks deferred to the next loop iteration.

Idle, Prepare: Used internally by Node.js for performance optimization.

Poll: This phase retrieves new I/O events; node will block here when appropriate.

Check: Executes setImmediate() callbacks.

Close Callbacks: Executes callbacks for closed connections, such as socket.on('close', ...).

During each iteration, the event loop checks for pending callbacks and executes them in their respective phase. The non-blocking nature of Node.js comes from the fact that it doesn't wait for a function to complete; instead, it registers a callback and moves on to the next task.

## 1. User System Workflow

**Q:** What is the typical workflow of a user system?

**A:** In a typical user system workflow, these steps are commonly involved:

- **Registration:** Users create an account by providing their details. The system may validate the data and store it in a database.
- **Authentication:** When a user logs in, the system verifies their credentials (e.g., username and password) against stored data. Successful authentication generates a session or a token.
- **Authorization:** Determines what resources a user can access based on their role or permissions.
- **Session Management:** Maintains user sessions using cookies or tokens to keep users logged in.
- **Logout:** Ends the user's session and invalidates any tokens or session data.

## 2. Authentication

**Q:** What is authentication?

**A:** Authentication is the process of verifying the identity of a user. Common methods include:

- **Username and Password:** Users provide credentials that are checked against stored values.
- **Multi-Factor Authentication (MFA):** Adds an extra layer of security by requiring additional verification (e.g., SMS code, email verification).
- **OAuth:** A framework for token-based authentication allowing users to grant third-party applications access without sharing their credentials.

## 3. Refresh Token

**Q:** What is a refresh token?

**A:** A refresh token is used to obtain a new access token without re-authenticating the user. It allows for a long-lived session while keeping the access tokens short-lived for security. Typically used in OAuth implementations:

- **Initial Authentication:** The user logs in and receives an access token and a refresh token.
- **Access Token Expiry:** When the access token expires, the refresh token can be sent to the server to get a new access token.
- **Security:** Refresh tokens should be securely stored and protected, as they can be used to issue new access tokens.

## 4. Middleware

**Q:** What is middleware?

**A:** Middleware functions are used in web frameworks (like Express.js) to handle requests and responses. They act as a bridge between the server and request handlers. Middleware can:

- **Handle Requests:** Process incoming requests (e.g., logging, parsing JSON).
- **Authenticate Requests:** Check if the user is authenticated.
- **Modify Requests/Responses:** Add or modify headers, handle errors, etc.
- **Terminate Requests:** End the request-response cycle if certain conditions are met.

Example in Express.js:

```javascript
app.use((req, res, next) => {
  console.log("Middleware function");
  next(); // Pass control to the next handler
});
```

## 5. Asynchronous vs Synchronous Functions

**Q:** What is the difference between asynchronous and synchronous functions?

**A:**

- **Synchronous Functions:** Execute sequentially, blocking the execution of the following code until they complete. Example:

  ```javascript
  function syncFunction() {
    console.log("First");
    console.log("Second");
  }
  syncFunction(); // Outputs 'First', then 'Second'
  ```

- **Asynchronous Functions:** Allow other operations to run while waiting for a task to complete. This is achieved using callbacks, promises, or async/await. Example with `async/await`:
  ```javascript
  async function asyncFunction() {
    console.log("First");
    await new Promise((resolve) => setTimeout(resolve, 1000));
    console.log("Second");
  }
  asyncFunction(); // Outputs 'First', then 'Second' after 1 second
  ```

## 6. Array Iterators

**Q:** What are some common array iterators in JavaScript?

**A:** JavaScript arrays have several iterator methods:

- **forEach()**: Executes a function for each array element.

  ```javascript
  [1, 2, 3].forEach((num) => console.log(num)); // Outputs 1, 2, 3
  ```

- **map()**: Creates a new array with the results of calling a function on each element.

  ```javascript
  const doubled = [1, 2, 3].map((num) => num * 2); // [2, 4, 6]
  ```

- **filter()**: Creates a new array with elements that pass a test.

  ```javascript
  const evens = [1, 2, 3, 4].filter((num) => num % 2 === 0); // [2, 4]
  ```

- **reduce()**: Applies a function against an accumulator and each element to reduce it to a single value.
  ```javascript
  const sum = [1, 2, 3].reduce((acc, num) => acc + num, 0); // 6
  ```

## 7. MongoDB Aggregations

**Q:** What are MongoDB aggregations?

**A:** MongoDB aggregations process data records and return computed results. Common stages in an aggregation pipeline include:

- **$match:** Filters documents based on a condition.
- **$group:** Groups documents by a specified identifier and performs aggregation operations (e.g., sum, average).
- **$sort:** Sorts documents by a specified field.
- **$project:** Reshapes documents by including or excluding fields.

Example:

```javascript
db.collection.aggregate([
  { $match: { status: "active" } },
  { $group: { _id: "$category", total: { $sum: "$amount" } } },
  { $sort: { total: -1 } },
]);
```

## 8. Sequelize

**Q:** What is Sequelize?

**A:** Sequelize is an ORM (Object-Relational Mapping) for Node.js that works with SQL databases. It simplifies database interactions using JavaScript objects:

- **Define Models:** Create models that represent tables.

  ```javascript
  const User = sequelize.define("User", {
    name: Sequelize.STRING,
    email: Sequelize.STRING,
  });
  ```

- **Querying:** Perform CRUD operations.

  ```javascript
  User.findAll().then((users) => console.log(users));
  User.create({ name: "John", email: "john@example.com" });
  ```

- **Associations:** Define relationships between models (e.g., one-to-many, many-to-many).
  ```javascript
  User.hasMany(Post);
  Post.belongsTo(User);
  ```

## 9. Types of Relationships in RDBMS

**Q:** What are the types of relationships in a relational database management system (RDBMS)?

**A:** In an RDBMS, there are three primary types of relationships between tables:

- **One-to-One (1:1):** Each row in Table A is related to exactly one row in Table B, and vice versa. Example: A person has one passport, and each passport is assigned to one person.
- **One-to-Many (1:N):** A row in Table A can be related to multiple rows in Table B, but each row in Table B is related to only one row in Table A. Example: A department can have many employees, but each employee belongs to only one department.
- **Many-to-Many (M:N):** Rows in Table A can be related to multiple rows in Table B and vice versa. This is typically implemented using a junction table that contains foreign keys referencing both Table A and Table B. Example: Students and courses, where each student can enroll in multiple courses and each course can have multiple students.

## 10. Latency vs Throughput

**Q:** What is the difference between latency and throughput?

**A:**

- **Latency:** Measures the time it takes to process a single request or operation from start to finish. It is often referred to as "response time" and is crucial for applications where quick responses are needed. Example: The time taken for a web page to load.
- **Throughput:** Measures the number of requests or operations processed in a given amount of time. It indicates the capacity of a system to handle a load and is crucial for performance in high-load scenarios. Example: The number of transactions processed per second in a database.

## 11. Raw Query vs ORM

**Q:** When do we use raw queries, and when do we use an ORM (Object-Relational Mapping)?

**A:**

- **Raw Queries:** Used when performance is critical or when you need to execute complex queries that are difficult to express using ORM methods. Raw queries provide fine-grained control over the SQL executed against the database. They are also used when working with databases that are not well-supported by the ORM or for advanced database features not exposed by the ORM.
  Example:

  ```javascript
  const results = await db.query("SELECT * FROM users WHERE age > ?", [25]);
  ```

- **ORM (Object-Relational Mapping):** Used for simplicity and maintainability, as it abstracts away the database interactions into JavaScript objects. ORMs handle most common CRUD operations and relationships, making the code easier to write and understand. They also help in preventing SQL injection attacks by using parameterized queries.
  Example:

  ```javascript
  const users = await User.findAll({ where: { age: { [Op.gt]: 25 } } });
  ```

  In most cases, ORMs are used because they simplify code and reduce the likelihood of errors. However, raw queries are preferred for performance optimizations or complex operations.

## 12. Normalization and Normal Forms

**Q:** How do you normalize a database, and what are the three types of normal forms?

**A:** **Normalization** is the process of organizing a database to reduce redundancy and improve data integrity. The primary steps involve dividing large tables into

smaller, related tables and defining relationships between them.

### **Three Types of Normal Forms:**

1. **First Normal Form (1NF):**

   - **Requirement:** Eliminate repeating groups; ensure that each column contains only atomic (indivisible) values, and each column has a unique name.
   - **Example:** Convert a table with multiple values in a single column (e.g., multiple phone numbers in one cell) into separate rows.

2. **Second Normal Form (2NF):**

   - **Requirement:** Achieve 1NF and remove partial dependencies. Ensure that all non-key attributes are fully functionally dependent on the primary key.
   - **Example:** If a table has a composite key and some attributes depend on only part of the composite key, split it into separate tables to ensure that all attributes depend on the entire key.

3. **Third Normal Form (3NF):**
   - **Requirement:** Achieve 2NF and remove transitive dependencies. Ensure that all attributes are only dependent on the primary key and not on other non-key attributes.
   - **Example:** If a table has attributes that depend on other non-key attributes, separate these into different tables to ensure that each attribute depends only on the primary key.

Normalization aims to minimize redundancy and improve the efficiency and integrity of a database.

## **What are Git hooks?**

Git hooks are scripts that Git executes before or after events such as committing changes, merging branches, pushing commits, and more. These hooks are customizable and can automate tasks, enforce policies, and integrate with external systems. Examples include pre-commit hooks for linting code or post-commit hooks for deploying changes.

## **How can you return the names of people who are reported to (excluding null values), the number of members that report to them, and the average age of those members as an integer, ordered by names alphabetically?**

To achieve this, you can use the following SQL query:

```sql
SELECT ReportsTo AS Name,
       COUNT(*) AS NumberOfMembers,
       FLOOR(AVG(Age)) AS AverageAge
FROM Employees
WHERE ReportsTo IS NOT NULL
GROUP BY ReportsTo
ORDER BY ReportsTo;
```

This query selects the `ReportsTo` column, counts the number of members reporting to each person, calculates the average age (rounded down to the nearest integer), excludes null values, and orders the results alphabetically by `ReportsTo`.

```

```
