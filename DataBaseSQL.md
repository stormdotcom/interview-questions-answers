## Database Interview Questions and Sample Answers for Fullstack (MERN) Developers

### MongoDB (NoSQL)

- **What are the key advantages of using MongoDB in fullstack development, compared to a relational database?**

  MongoDB provides a flexible schema, which allows developers to quickly adapt to changes in requirements. Its document-based model maps naturally to JavaScript objects in Node.js, making data handling seamless in MERN applications. Additionally, MongoDB scales horizontally with ease and is highly performant for unstructured or semi-structured data.

- **How does MongoDB handle indexing, and when should you create custom indexes?**

  MongoDB supports various index types, including single-field, compound, and text indexes. By default, it creates an index on the `_id` field. Custom indexes should be created on fields frequently used in query filters, sorting, or to enforce uniqueness, in order to improve read performance and query efficiency.

- **Explain the difference between replication and sharding in MongoDB. When would you use each approach?**

  Replication involves duplicating data across multiple servers for redundancy and availability. It's used primarily for high availability and disaster recovery. Sharding partitions data across multiple machines to distribute large datasets and high throughput operations, optimizing for scalability. Use replication for fault tolerance, and sharding for handling large data volumes or workloads.

- **How would you migrate data from a relational database (e.g., PostgreSQL) to MongoDB? What considerations are involved?**

  Migrating data involves extracting structured data from PostgreSQL, transforming it to JSON format, and inserting it into MongoDB collections. Schema differences must be accounted for, such as denormalizing relationships and deciding how to represent relational joins. Data consistency, validation, and minimizing downtime during migration are important considerations.

- **How do you optimize a slow-running query in MongoDB? What tools or commands would you use?**

  Use the `.explain()` method to analyze query execution plans. Slow queries are often caused by the lack of appropriate indexes or inefficient queries (such as those using `$regex` or large `$in` arrays). Adding indexes on fields frequently queried or sorted, and rewriting queries for efficiency, are common optimization methods.

- **Describe strategies for managing schema changes in MongoDB collections.**

  Schema changes can be handled by versioning documents, using optional fields, or running migration scripts to update documents in bulk. Using Mongoose schemas (in Node.js) helps enforce schema consistency, and migration tools like `migrate-mongo` can automate updates.

### PostgreSQL (Relational)

- **What is Multi-Version Concurrency Control (MVCC) and how does it work in PostgreSQL?**

  MVCC allows multiple transactions to access the database concurrently without blocking each other, providing a snapshot of the data at transaction start. It prevents dirty reads and increases database throughput by ensuring consistency without excessive locking.

- **How do you create and use indexes in PostgreSQL? What types of indexes are available?**

  Create indexes with the `CREATE INDEX` statement. PostgreSQL supports B-tree (default), hash, GIN, GiST, and BRIN indexes. Use B-tree for equality and range queries, GIN for array and full-text search, and hash for exact matches.

- **What is the difference between a foreign key and a unique key in PostgreSQL?**

  A foreign key enforces referential integrity between two tables, ensuring that a value in one table matches a value in another. A unique key enforces uniqueness within a column or group of columns, preventing duplicate values.

- **How would you handle database migrations and schema changes in a production PostgreSQL environment?**

  Use migration tools such as Knex, Sequelize, or Flyway to version and apply changes incrementally, ensuring safe and reversible schema evolution. Always back up the database and test migrations in staging before production.

- **Compare and contrast TRUNCATE vs. DELETE in PostgreSQL. When would you use each?**

  `TRUNCATE` quickly removes all rows from a table without scanning them, is not transactional, and may bypass triggers. `DELETE` allows conditional row removal, is transactional, and fires triggers. Use `TRUNCATE` for bulk removal when triggers and transactions aren't required; use `DELETE` for fine-grained or transactional deletions.

- **How do you perform a database backup and restore in PostgreSQL? What tools or commands are involved?**

  Use `pg_dump` to export a database and `pg_restore` or `psql` to import it. For full database restoration, use `pg_basebackup` for binary backups and Point-In-Time Recovery (PITR).

### Sequelize (ORM for SQL)

- **How do you define and use model associations in Sequelize?**

  Define associations using methods like `hasOne`, `hasMany`, `belongsTo`, and `belongsToMany` in your model definitions. This sets up the necessary foreign keys and enables eager/lazy loading of related data.

- **Explain the difference between eager and lazy loading in Sequelize. When would you use each?**

  Eager loading fetches associated data as part of the initial query using `include` options, ideal for reducing the number of database queries. Lazy loading fetches associations only when accessed, which offers flexibility but can cause the N+1 problem. Choose based on the required data and performance needs.

- **How are transactions managed in Sequelize? Provide a use case when transactions are important.**

  Transactions are managed using `sequelize.transaction()`. Critical operations, such as transferring funds between accounts, require transactions to ensure atomicity and consistent state in case of errors.

- **What are Sequelize migrations and how do you structure them in a project?**

  Migrations track schema changes over time in organized scripts. Typically, each migration file applies or reverts a structural change. Structure them in a chronologically-ordered migrations directory and use Sequelize CLI to run/revert them.

- **How can you execute raw SQL queries in Sequelize, and when is this approach appropriate?**

  Use `sequelize.query()` for raw queries, appropriate for complex operations not easily modeled via ORM functions or when performance optimizations are required.

- **Explain the use and benefits of Sequelize hooks.**

  Hooks allow execution of custom functions before or after certain model lifecycle events (e.g., beforeCreate, afterUpdate), useful for validation, auditing, or modifying records automatically.

### Knex.js (SQL Query Builder)

- **What is Knex.js and how does it fit into a Node.js fullstack application?**

  Knex.js is a SQL query builder for Node.js, supporting multiple database engines. It provides a fluent interface for constructing queries, managing migrations, and handling database connections in a backend application.

- **Describe how to perform schema migrations using Knex.js.**

  Use the built-in CLI to create migration files that define schema changes in JavaScript. Run migrations with `knex migrate:latest` to apply new changes or `knex migrate:rollback` to revert.

- **How do you parameterize queries in Knex.js to prevent SQL injection?**

  Knex parameterizes queries automatically using placeholders for values, e.g., `.where('username', username)`, ensuring user input doesn't get directly interpolated into SQL commands.

- **Give an example of how to perform a transactional operation using Knex.js.**

  Wrap operations in `knex.transaction(async trx => { ... })` and execute all database changes through the `trx` object, committing or rolling back as needed for atomicity.

- **Discuss how you would integrate Knex.js with either PostgreSQL or MySQL in a Node.js project.**

  Install the corresponding driver (`pg` for PostgreSQL, `mysql` for MySQL) and configure Knex’s connection settings with database details (host, user, password, database). Use Knex’s methods to interact with the chosen database.

### TypeORM (ORM for TypeScript/Node.js)

- **How do you define entities and relationships in TypeORM?**

  Define entities as TypeScript classes, using decorators like `@Entity`, `@Column`, `@OneToMany`, and `@ManyToOne` to specify relationships, columns, and constraints.

- **What are the steps to establish a database connection using TypeORM?**

  Import and configure TypeORM with the `DataSource` class (or `createConnection`), specifying database credentials, entities, and synchronization preferences, then initiate the connection.

- **Describe the process of running migrations in TypeORM and rolling back a migration.**

  Generate migration files using the CLI, run them with `typeorm migration:run`, and roll back with `typeorm migration:revert`, maintaining database version consistency.

- **How do you use TypeORM repositories and query builders for advanced queries?**

  Use repository methods (like `.find()`, `.save()`) for basic operations, or the query builder interface (`createQueryBuilder`) for complex joins, filtering, or aggregated queries.

- **What strategies are available in TypeORM for handling transactions and ensuring data consistency?**

  Manage transactions with the `@Transaction()` decorator, manual transaction queries, or by leveraging the `QueryRunner` API to execute a sequence of queries atomically, ensuring consistency in case of errors.

### General/Comparison

- **In a MERN stack application, how do you decide whether to use MongoDB or PostgreSQL for persistent data storage?**

  Choose MongoDB for flexible, unstructured data, rapid prototyping, and when your data model doesn't require strong ACID transactions or complex joins. PostgreSQL is preferable for structured, relational data, complex queries, and when transactional integrity is critical.

- **What are the trade-offs in using an ORM (like Sequelize or TypeORM) versus writing raw queries?**

  ORMs speed up development, provide abstraction, and reduce boilerplate, while raw queries offer maximum flexibility and performance optimization. However, ORMs may abstract away important database behaviors and may not support all advanced features.

- **As a fullstack developer, how do you ensure data integrity and consistency across microservices using different databases?**

  Employ database transactions where possible, implement distributed transaction patterns (like Saga or two-phase commit), and use consistent schema definitions and validation logic across services. Establish robust API contracts and validation layers to prevent inconsistent states.
