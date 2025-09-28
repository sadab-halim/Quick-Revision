# DBMS

<details>
  <summary>01: Introduction to DBMS</summary>

### Data, Information & Database

- **Data**: Raw, unorganized facts and figures that lack context. For example, `101`, `John Doe`, `Engineering`.
- **Information**: Data that has been processed, organized, and structured to provide context and meaning. For example, "Student with ID 101 is John Doe from the Engineering department."
- **Database**: An organized, persistent, and structured collection of interrelated data. It is designed for efficient access, management, and updating.
- **Analogy**: Think of a library. The individual words in all the books are **data**. A single, complete book is **information**. The entire organized library, with shelves, catalogs, and a system for checking books in and out, is the **database**.


### Types of Databases

- **Relational Databases (RDBMS)**: Store data in tables with rows and columns. They use SQL (Structured Query Language). Examples include MySQL, PostgreSQL, and Oracle.
- **Non-Relational Databases (NoSQL)**: Store data in formats other than tables. They are more flexible and scalable for certain use cases. Major types include Document, Key-Value, Column-Family, and Graph databases. Examples: MongoDB, Redis.
- **Object-Oriented Databases**: Store data in the form of objects, similar to object-oriented programming.
- **Hierarchical Databases**: Organize data in a tree-like structure with parent-child relationships. Example: IBM's IMS.
- **Network Databases**: Similar to hierarchical but allow each record to have multiple parent and child records, forming a graph-like structure.


### Database Management System (DBMS)

A DBMS is a software system that acts as an interface between the user and the database. It allows users to perform operations like creating, reading, updating, and deleting (CRUD) data while handling security, consistency, and concurrency.

### Need, Advantages & Disadvantages of DBMS

A DBMS is needed to overcome the issues of traditional file-based systems (like data redundancy, inconsistency, and poor security).


| Advantages                         | Disadvantages |
|:-----------------------------------| :-- |
| **Controls Redundancy**            | **High Cost** |
| **Enforces Data Consistency**      | **Complexity** |
| **Facilitates Data Sharing**       | **Performance Overhead** |
| **Provides Security**              | **Requires Skilled Staff** |
| **Offers Backup & Recovery**       | **Single Point of Failure** |
| **Enforces Integrity Constraints** |  |

### Data Abstraction in DBMS (IMP)

Data abstraction hides complex storage details from users. There are three levels:

- **Physical Level (Internal)**: The lowest level. It describes *how* the data is physically stored on storage devices (e.g., file organization, indexing methods). This is the most complex level, visible only to DBAs and developers.
- **Logical Level (Conceptual)**: The middle level. It describes *what* data is stored and the relationships between different data entities. It defines the entire database schema without concern for physical storage.
- **View Level (External)**: The highest level. It shows only a specific part of the database to a particular user group, hiding the rest. A single database can have multiple views. For example, a student might only see their own grades, not the entire university's grade data.

**Analogy**: A car.

- **Physical Level**: The engine mechanics, wiring, and transmission system.
- **Logical Level**: The engineering blueprint of the car showing all components and their connections.
- **View Level**: The driver's dashboard, steering wheel, and pedals—only what is needed to operate the car.


### DBMS Architecture (IMP)

- **1-Tier Architecture**: The database, DBMS, and application logic all reside on a single machine. It is rarely used in production. Example: A simple local database app using SQLite.
- **2-Tier Architecture**: A client-server model. The client (Tier 1) sends requests directly to the database server (Tier 2). The application logic can be on the client or server.
- **3-Tier Architecture**: The most common architecture for web applications. It separates layers for better scalability, security, and maintenance.
  - **Presentation Tier (Client)**: The user interface (e.g., web browser).
  - **Application Tier (Middle Tier)**: The server that contains the business logic (e.g., a Spring Boot application).
  - **Data Tier (Database Server)**: The DBMS that stores and manages the data.
- **Best Practice**: For most modern applications, a 3-tier (or N-tier) architecture is preferred as it decouples the presentation logic from the business logic, making the system more modular and scalable.


### Database Users and Interactions

- **Database Administrator (DBA)**: Has central control. Responsible for security, monitoring, performance tuning, backup, and recovery.
- **Database Designer**: Defines the logical schema, including tables, relationships, and constraints.
- **Application Programmer**: Writes applications (e.g., in Java, Python) that interact with the database using APIs or SQL.
- **End User**: Interacts with the database through an application. They can be:
  - **Naive Users**: Use a pre-built application with a graphical interface.
  - **Sophisticated Users**: Use query languages like SQL to access data directly.


</details>

---

<details>
  <summary>02: Data Models & ER Models</summary>

### DBMS Interfaces

A DBMS interface is the component that allows users to communicate with the database. Different interfaces are designed for different types of users and tasks.[^3_1]

- **Menu-Based Interfaces**: Present a series of options or menus to guide the user in formulating a request. This is common in web applications and removes the need to write complex queries.[^3_2][^3_1]
- **Forms-Based Interfaces**: Provide a form with fields for users to fill in. Ideal for data entry operations (e.g., a registration form). They are simple and structured for naive users.[^3_3][^3_1]
- **Graphical User Interfaces (GUI)**: Display the database schema visually (e.g., tables and relationships). Users can interact by clicking on objects. Tools like MySQL Workbench provide a GUI.
- **Natural Language Interfaces**: Allow users to query the database using plain language (e.g., "Show me all employees in the sales department"). The system translates this into a formal query.
- **DBA Interfaces**: Command-line or graphical interfaces with privileged commands for Database Administrators to manage the system, including user creation, security, and performance monitoring.[^3_2]


### Data Models & their Types

A data model defines the logical structure of a database. It describes how data is connected, processed, and stored.[^3_4]

- **Relational Model**: The most widely used model. Data is organized into tables (relations) made of rows and columns.[^3_5][^3_4]
- **Entity-Relationship (ER) Model**: A high-level, conceptual model that describes data as entities, attributes, and relationships. It's primarily a database design tool.[^3_6][^3_5]
- **Object-Oriented Model**: Data is stored as objects, which encapsulate both data (attributes) and behavior (methods).
- **Hierarchical Model**: Organizes data in a tree-like structure with a single root. Each record has exactly one parent.[^3_5]
- **Network Model**: An extension of the hierarchical model, allowing a record to have multiple parent records, forming a graph structure.[^3_5]


### ER Model & its Components (IMP)

The ER Model is like a blueprint for a database. It helps visualize the database structure before it's built. Its main components are:[^3_6]

- **Entity**: A real-world object or concept, such as a `Student` or a `Car`. Represented by a rectangle.[^3_7]
  - **Weak Entity**: An entity that cannot be uniquely identified by its attributes alone and depends on another entity (the "owner"). Represented by a double rectangle.[^3_7]
- **Attribute**: A property that describes an entity, such as `student_name` or `car_color`. Represented by an oval.[^3_7]
  - **Key Attribute**: Uniquely identifies an entity in a set (e.g., `student_id`). Represented by an underlined oval.[^3_7]
  - **Composite Attribute**: An attribute that can be broken down into smaller components (e.g., `Address` can be broken down into `Street`, `City`, `Zip`).[^3_7]
  - **Multivalued Attribute**: An attribute that can hold multiple values (e.g., `phone_number`). Represented by a double oval.[^3_7]
  - **Derived Attribute**: An attribute whose value can be calculated from other attributes (e.g., `Age` can be derived from `Date_of_Birth`). Represented by a dashed oval.[^3_7]
- **Relationship**: An association between two or more entities, such as a `Student` *enrolls in* a `Course`. Represented by a diamond.[^3_6]


### Types of Relationships in DBMS (IMP)

Relationships are defined by their cardinality, which specifies how many instances of one entity can be related to instances of another entity.


| Relationship Type | Description | Real-World Example | Implementation |
| :-- | :-- | :-- | :-- |
| **One-to-One (1:1)** | Each instance in Entity A is linked to at most one instance in Entity B, and vice-versa [^3_8]. | A `Person` has one `Passport` [^3_9]. | The primary key of one table is stored as a unique foreign key in the other. |
| **One-to-Many (1:N)** | An instance in Entity A can be linked to many instances in Entity B, but an instance in B is linked to only one in A [^3_8]. | A `Customer` can place many `Orders` [^3_8]. | The primary key of the "one" side is added as a foreign key to the "many" side. |
| **Many-to-Many (N:M)** | An instance in Entity A can be linked to many in B, and an instance in B can be linked to many in A [^3_8]. | A `Student` can enroll in many `Courses`, and a `Course` can have many `Students`. | Requires a third "junction" or "linking" table that contains foreign keys from both tables. |

### Extended ER Features (IMP)

These features enhance the ER model to represent complex database schemas more accurately.

- **Specialization**: A **top-down** approach. A higher-level entity is broken down into more specific sub-entities. For example, the entity `Person` can be specialized into `Student` and `Professor`. The sub-entities inherit attributes from the parent but may also have their own specific attributes.[^3_10][^3_11]
- **Generalization**: A **bottom-up** approach. Two or more lower-level entities with common attributes are combined to form a more general higher-level entity. For example, `Car` and `Truck` entities can be generalized into a `Vehicle` entity.[^3_11][^3_10]
- **Aggregation**: Treats a relationship set as a higher-level entity. It's used when a relationship itself needs to participate in another relationship.
  - **Analogy**: Imagine a `Doctor` *treats* a `Patient` at a `Hospital`. The entire "treatment" event (a relationship) might need to be evaluated by an `Auditor`. Aggregation allows you to model this by enclosing the `Doctor-treats-Patient` relationship in a box and treating it as a single entity that the `Auditor` relates to.


### Types of Inheritance

Inheritance refers to how specialization/generalization hierarchies are implemented in a relational database.

- **Single Table Inheritance**: All entities in the hierarchy are stored in a single table. A "discriminator" column is used to identify the type of each row. This is simple but can lead to many `NULL` values if sub-entities have different attributes.[^3_12]
- **Class Table Inheritance**: A separate table is created for the parent entity and for each child entity. The child tables only contain their specific attributes and a foreign key referencing the parent table. This avoids `NULL` values but requires joins.[^3_13]
- **Concrete Table Inheritance**: A separate table is created for each concrete class in the hierarchy. Each table includes all attributes of that class, including inherited ones. This offers good performance for queries on a specific subclass but can lead to data redundancy.


### Entity-Relationship Diagram (ERD) & Creation

An ERD is the visual representation of the ER model. To create one:[^3_6]

1. **Identify Entities**: Determine the main objects or concepts (e.g., `Product`, `Customer`).[^3_14][^3_15]
2. **Define Attributes**: List the properties for each entity (e.g., `product_id`, `name`).[^3_15]
3. **Specify Relationships**: Define how entities are associated (e.g., a `Customer` *buys* a `Product`).[^3_14]
4. **Add Cardinality**: Use notations like Crow's Foot to show the relationship type (1:1, 1:N, N:M).[^3_14]

### Relational Model

This is the model that ER diagrams are typically converted into for implementation. It represents data in two-dimensional tables called **relations**. Each table has rows (tuples) and columns (attributes). The relationships defined in the ER model are maintained through the use of keys.[^3_4]


</details>

---

<details>
  <summary>03: Relational Model & Normalization</summary>

### Intension and Extension

- **Intension (Schema)**: The constant part of the database. It's the description or structure of the database, including the name of the relation (table), its attributes (columns), and their data types. It doesn't change frequently.
- **Extension (Instance)**: The snapshot of the data in the database at a specific moment in time. It's the set of all tuples (rows) currently in a relation. It changes frequently as data is added, updated, or deleted.
- **Analogy**: The **intension** is the blueprint for a house, defining rooms and their functions. The **extension** is the actual furniture and people inside the house at any given time.


### Keys in DBMS (IMP)

Keys are attributes or sets of attributes that help uniquely identify rows in a table.

- **Super Key**: Any set of attributes that can uniquely identify a tuple (row) within a relation.
- **Candidate Key**: A minimal super key. It's a super key from which no attribute can be removed without losing its uniqueness. A table can have multiple candidate keys.
- **Primary Key**: One candidate key chosen by the database designer to be the main identifier for the table. It cannot contain `NULL` values and must be unique.
- **Alternate Key**: Any candidate key that is not selected as the primary key.
- **Foreign Key**: An attribute (or set of attributes) in one table that refers to the primary key of another table. It is used to link tables and enforce referential integrity.
- **Composite Key**: A key that consists of two or more attributes that together uniquely identify a record.


### Data Normalization (IMP)

Normalization is the process of organizing columns and tables in a relational database to minimize **data redundancy** and improve **data integrity**. It involves decomposing larger tables into smaller, well-structured ones to eliminate undesirable characteristics like Insertion, Updation, and Deletion Anomalies.[^4_3][^4_4][^4_5]

**Analogy**: Think of organizing a messy closet. You don't just throw everything in one big pile (un-normalized). Instead, you create separate sections for shirts, pants, and shoes (normalized tables) to find things easily and avoid having five identical red shirts.

#### Normal Forms

Normal forms are a series of guidelines to check if a database is well-designed.[^4_2]


| Normal Form | Rule | Problem Solved |
| :-- | :-- | :-- |
| **1NF** | Ensures all columns contain atomic (indivisible) values. Each cell must hold a single value [^4_1][^4_5]. | Removes repeating groups and multi-valued attributes [^4_7]. |
| **2NF** | Must be in 1NF. All non-key attributes must be fully functionally dependent on the entire primary key [^4_1]. | Eliminates partial dependencies on a composite primary key [^4_7]. |
| **3NF** | Must be in 2NF. There should be no transitive dependencies [^4_1]. | Eliminates dependencies where a non-key attribute depends on another non-key attribute [^4_7]. |
| **BCNF** | A stricter version of 3NF. For every non-trivial functional dependency `X -> Y`, `X` must be a super key. | Handles certain anomalies not addressed by 3NF where a table has multiple overlapping candidate keys. |

**Real-World Example**:

- **Un-normalized Table**:


| StudentID | StudentName | CourseIDs | CourseNames |
| :-- | :-- | :-- | :-- |
| 1 | John | C101, C102 | Java, Python |

- **1NF**: A single cell cannot hold multiple values.


| StudentID | StudentName | CourseID | CourseName |
| :-- | :-- | :-- | :-- |
| 1 | John | C101 | Java |
| 1 | John | C102 | Python |

*Pitfall*: Still has redundancy (`StudentName` is repeated).
- **2NF**: Decompose to remove partial dependencies. Assume `(StudentID, CourseID)` is the primary key. `StudentName` only depends on `StudentID`, which is a partial dependency.
  - **Students Table**:


| StudentID (PK) | StudentName |
| :-- | :-- |
| 1 | John |

    - **Enrollment Table**:


| StudentID (FK) | CourseID (FK) | CourseName |
| :-- | :-- | :-- |
| 1 | C101 | Java |
| 1 | C102 | Python |

- **3NF**: Decompose to remove transitive dependencies. In the `Enrollment` table, `CourseName` depends on `CourseID`, and `CourseID` depends on `StudentID`. This is a transitive dependency (`StudentID -> CourseID -> CourseName`).
  - **Students Table**: `(StudentID, StudentName)`
  - **Courses Table**:


| CourseID (PK) | CourseName |
| :-- | :-- |
| C101 | Java |
| C102 | Python |

    - **Enrollment Table**:


| StudentID (FK) | CourseID (FK) |
| :-- | :-- |
| 1 | C101 |
| 1 | C102 |


**Best Practice**: Aim for at least 3NF in most transactional database designs (OLTP). Higher normal forms are more academic and can sometimes degrade performance due to the need for more joins.

### Functional Dependency (FD)

A functional dependency `X -> Y` in a relation `R` means that the value of attribute set `X` uniquely determines the value of attribute set `Y`. If two tuples have the same value for `X`, they must also have the same value for `Y`.

### Armstrong's Axioms

A set of inference rules used to find all possible functional dependencies in a database.

1. **Reflexivity**: If `Y` is a subset of `X`, then `X -> Y`.
2. **Augmentation**: If `X -> Y`, then `XZ -> YZ` for any `Z`.
3. **Transitivity**: If `X -> Y` and `Y -> Z`, then `X -> Z`.

### Closure in Functional Dependencies

The closure of an attribute set `X`, denoted as `X+`, is the set of all attributes that can be functionally determined from `X` using Armstrong's axioms. It's used to find candidate keys and check dependencies.

### Denormalization

The intentional process of violating normalization rules to improve query performance. By adding redundant data back into tables, we can reduce the number of joins needed to retrieve data, which is often faster.

- **Use Case**: Commonly used in data warehousing and reporting databases (OLAP), where read performance is more critical than write efficiency.
- **Common Pitfall**: Denormalize with caution. It introduces data redundancy, which can lead to inconsistencies if not managed carefully (e.g., using triggers or application logic to keep redundant copies in sync).

</details>

---

<details>
  <summary>04: SQL & Query Optimization</summary>

### Database Languages

- **DDL (Data Definition Language)**: Defines the database schema.
  - **Commands**: `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME`.
  - **Example**: `CREATE TABLE Students (StudentID INT PRIMARY KEY, Name VARCHAR(100));`
- **DML (Data Manipulation Language)**: Used for accessing and manipulating data.
  - **Commands**: `SELECT`, `INSERT`, `UPDATE`, `DELETE`.
  - **Example**: `UPDATE Students SET Name = 'John Doe' WHERE StudentID = 1;`
- **DCL (Data Control Language)**: Manages access rights and permissions.
  - **Commands**: `GRANT`, `REVOKE`.
  - **Example**: `GRANT SELECT ON Students TO 'some_user'@'localhost';`
- **TCL (Transaction Control Language)**: Manages transactions in the database.
  - **Commands**: `COMMIT`, `ROLLBACK`, `SAVEPOINT`.


### SQL Operators

- **Arithmetic**: `+`, `-`, `*`, `/`, `%`
- **Comparison**: `=`, `!=` or `<>`, `>`, `<`, `>=`, `<=`
- **Logical**: `AND`, `OR`, `NOT`, `BETWEEN`, `LIKE`, `IN`, `EXISTS`, `ALL`, `ANY`, `IS NULL`


### Aggregates in SQL

Aggregate functions perform a calculation on a set of values and return a single value.

- `COUNT()`: Counts the number of rows.
- `SUM()`: Calculates the sum of values.
- `AVG()`: Calculates the average of values.
- `MIN()`: Returns the minimum value.
- `MAX()`: Returns the maximum value.
- **Common Pitfall**: Aggregate functions (except `COUNT(*)`) ignore `NULL` values. This can affect results, especially with `AVG()`.


### SQL Clauses

Clauses are keywords that perform specific tasks in SQL queries.

- `FROM`: Specifies the table to query.
- `WHERE`: Filters records based on a condition.
- `GROUP BY`: Groups rows that have the same values in specified columns into summary rows. Often used with aggregate functions.
- `HAVING`: Filters groups created by `GROUP BY`. `WHERE` filters rows *before* aggregation, while `HAVING` filters groups *after* aggregation.
- `ORDER BY`: Sorts the result set in ascending (`ASC`) or descending (`DESC`) order.
- `LIMIT` / `OFFSET`: Restricts the number of rows returned and specifies a starting point.


### SQL Joins (IMP)

Joins are used to combine rows from two or more tables based on a related column.


| Join Type | Description |
| :-- | :-- |
| **`INNER JOIN`** | Returns records that have matching values in both tables. |
| **`LEFT JOIN`** | Returns all records from the left table, and the matched records from the right table. The result is `NULL` from the right side if there is no match. |
| **`RIGHT JOIN`** | Returns all records from the right table, and the matched records from the left table. The result is `NULL` from the left side if there is no match. |
| **`FULL OUTER JOIN`** | Returns all records when there is a match in either the left or right table. It's a combination of `LEFT` and `RIGHT` joins. |
| **`CROSS JOIN`** | Produces the Cartesian product of the two tables, combining every row from the first table with every row from the second. |
| **`SELF JOIN`** | Joins a table to itself. Requires using table aliases. Useful for querying hierarchical data (e.g., finding an employee's manager in the same `Employees` table). |

### Unions in SQL

- **`UNION`**: Combines the result set of two or more `SELECT` statements but removes duplicate rows.
- **`UNION ALL`**: Combines the result set but includes all rows, including duplicates. It's faster than `UNION` because it doesn't need to check for duplicates.
- **Best Practice**: Use `UNION ALL` unless you specifically need to remove duplicates, as it offers better performance.


### Views in SQL

A view is a virtual table based on the result-set of an SQL statement.

- **Advantages**:
  - **Simplicity**: Can simplify complex queries.
  - **Security**: Can restrict access to data by showing users only specific columns or rows.
  - **Consistency**: Provides a consistent structure even if the underlying tables change.
- **Indexed Views (Materialized Views)** (IMP): A view where the result set is physically stored on disk and automatically updated when the underlying data changes.
  - **Use Case**: Greatly improves performance for complex and frequently executed queries (e.g., in data warehousing) because the join and aggregation logic is pre-computed.
  - **Common Pitfall**: Adds overhead to data modification operations (`INSERT`, `UPDATE`, `DELETE`) on the base tables because the view must also be updated.


### SQL Subqueries (IMP)

A subquery, or inner query, is a query nested inside another SQL query.

- **Scalar Subquery**: Returns a single value (one row, one column). Can be used anywhere a single value is expected.
- **Multi-row Subquery**: Returns multiple rows. Often used with operators like `IN`, `NOT IN`, `ANY`, `ALL`.
- **Correlated Subquery**: An inner query that depends on the outer query for its values. It is executed once for each row processed by the outer query.
  - **Performance Pitfall**: Correlated subqueries can be very slow because they execute repeatedly. It's often better to rewrite them as a `JOIN` if possible.
  - **Example**: Find employees whose salary is above the average for their department.

```sql
SELECT employee_name, salary
FROM employees e1
WHERE salary > (
    SELECT AVG(salary)
    FROM employees e2
    WHERE e2.department_id = e1.department_id -- Correlated on department_id
);
```


### Query Processing & Optimization (IMP)

The DBMS does not execute an SQL query as written. It first translates it into a relational algebra expression and then optimizes it to find the most efficient execution plan.[^5_1][^5_2]

1. **Parsing and Translation**: The SQL query is parsed for syntax, and translated into a relational algebra expression.
2. **Optimization**: The query optimizer generates multiple possible execution plans. It estimates the "cost" of each plan (based on CPU time, I/O, etc.) and chooses the one with the lowest cost.
3. **Execution**: The DBMS executes the chosen plan.

#### Relational Algebra for Optimization

The optimizer uses relational algebra equivalences to transform the initial query plan into a more efficient one. A key principle is to **reduce the size of intermediate results** as early as possible.

- **Example Optimization**:
  - **Bad Plan**: `Product(Employees, Departments) -> Select(dept_id = 5)`
    - First, create a huge Cartesian product of all employees and all departments. Then, filter. Very inefficient.
  - **Good Plan (Pushing down selections)**: `Select(dept_id = 5, Departments) -> Join(Employees)`
    - First, filter the `Departments` table to get only the relevant department. Then, join with `Employees`. This works on much smaller intermediate data sets.
- **Best Practice**: Always use `WHERE` clauses that are as specific as possible to allow the optimizer to use indexes and reduce the data set early.


</details>

---

<details>
  <summary>05: NoSQL Databases</summary>

### NoSQL Databases

NoSQL ("Not Only SQL") databases provide a mechanism for storage and retrieval of data that is modeled in means other than the tabular relations used in relational databases. They are known for their schema flexibility, horizontal scalability, and high performance.

#### RDBMS (SQL) vs. NoSQL Comparison (IMP)

| Feature | RDBMS (e.g., MySQL, PostgreSQL) | NoSQL (e.g., MongoDB, Redis, Cassandra) |
| :-- | :-- | :-- |
| **Data Model** | Structured data in tables with predefined schemas. | Unstructured, semi-structured, or structured data (documents, key-value, graph). |
| **Schema** | Schema-on-write (strict schema defined before data entry). | Schema-on-read (flexible, dynamic schema). |
| **Scalability** | Vertically scalable (increase resources on a single server). | Horizontally scalable (distribute load across multiple servers). |
| **Consistency** | Strong consistency (ACID properties). | Eventual consistency (BASE properties). |
| **Query Language** | SQL (Structured Query Language). | Varies by database (e.g., MQL for MongoDB, CQL for Cassandra). |
| **Best For** | Complex queries, transactional applications (e.g., banking, e-commerce). | Big data, real-time applications, content management, IoT. |

### BASE Properties (IMP)

While RDBMS databases adhere to ACID properties, many NoSQL databases follow the BASE model, which prioritizes availability over strict consistency.

- **Basically Available**: The system guarantees availability. There will be a response to any request (even if it's a failure message or outdated data).
- **Soft State**: The state of the system may change over time, even without input, due to eventual consistency.
- **Eventually Consistent**: The system will eventually become consistent once it stops receiving input. Data will be replicated to all nodes over time.
- **Analogy**: Imagine you and your friends are editing a shared Google Doc (NoSQL/BASE). If you both type in the same spot at the same time, you might see each other's changes appear with a slight delay. The document is **Basically Available** to both of you, its state is **Soft** as it syncs, and it will be **Eventually Consistent** once all changes are propagated. An RDBMS/ACID approach would be like locking the document file on a shared drive; only one person can edit at a time, ensuring absolute consistency but reducing availability.


### Types of NoSQL Databases (IMP)

| Type | Description | Example | Use Case |
| :-- | :-- | :-- | :-- |
| **Document Store** | Stores data in JSON, BSON, or XML documents. Schema is flexible. | **MongoDB** | Content management, user profiles, product catalogs. |
| **Key-Value Store** | The simplest model. Stores data as a collection of key-value pairs. | **Redis**, **DynamoDB** | Caching, session management, real-time leaderboards. |
| **Column-Family** | Stores data in columns rather than rows. Optimized for fast read/write of columns of data. | **Cassandra**, **HBase** | Big data analytics, logging, time-series data. |
| **Graph Database** | Stores data as nodes (entities) and edges (relationships). | **Neo4j**, **Amazon Neptune** | Social networks, fraud detection, recommendation engines. |

### Graph Databases

Graph databases excel at managing highly connected data.

- **Components**:
  - **Nodes**: Represent entities (e.g., a person, a place).
  - **Edges**: Represent relationships between nodes. They have a direction and a type (e.g., `(Person)-[:FRIENDS_WITH]->(Person)`).
  - **Properties**: Key-value pairs that describe nodes and edges.
- **Query Example (Cypher for Neo4j)**: Find all friends of a user named 'Alice'.

```cypher
MATCH (p1:Person {name: 'Alice'})-[:FRIENDS_WITH]-(p2:Person)
RETURN p2.name;
```


### In-Memory Databases

An in-memory database (IMDB) stores data in a computer's main memory (RAM) instead of on disk.

- **Advantages**: Blazing-fast performance due to the elimination of disk I/O.
- **Disadvantages**: Data volatility (data is lost if power is cut off, unless persistence mechanisms are used) and higher cost of RAM.
- **Example**: **Redis**, **SAP HANA**.
- **Use Case**: Real-time bidding, analytics, and caching layers where response time is critical.


### Partitioning in Databases

Partitioning is the process of splitting a large database table into smaller, more manageable pieces called partitions.

- **Why Partition?**
  - **Improved Performance**: Queries can scan only the relevant partitions instead of the whole table.
  - **Enhanced Manageability**: Maintenance tasks (like backups or index rebuilds) can be performed on individual partitions.
- **Types of Partitioning**:
  - **Horizontal Partitioning**: Divides a table by rows. Rows are distributed into different partitions based on a partition key.
    - **Range Partitioning**: Based on a range of values (e.g., partitioning sales data by month).
    - **List Partitioning**: Based on a list of discrete values (e.g., partitioning customer data by country).
    - **Hash Partitioning**: Based on a hash value of a key, ensuring an even data distribution.
  - **Vertical Partitioning**: Divides a table by columns. Some columns are stored in one partition and the remaining in another. Useful for separating frequently accessed columns from large, infrequently accessed ones (like `BLOB` or `TEXT` fields).


### Sharding in DBMS (IMP)

Sharding is a type of horizontal partitioning applied at the database level, not just within a single table. It involves splitting a database across multiple machines (servers). Each machine, or **shard**, contains a subset of the data.

- **Analogy**: Imagine a massive phone book (the database). Partitioning is like splitting it into sections A-M and N-Z within one building. Sharding is like putting the A-M phonebook in one library branch and the N-Z phonebook in another branch across town.
- **Advantages**:
  - **Horizontal Scalability**: To handle more load, you can just add more servers (shards).
  - **Increased Availability**: If one shard goes down, the other shards remain accessible.
- **Common Pitfall**:
  - **Increased Complexity**: Joins across shards are complex and expensive. Schema design must be done carefully to keep related data on the same shard.
  - **Hotspots**: If the shard key is not chosen well, one shard might get a disproportionate amount of traffic. For example, sharding users by their sign-up month might overload the current month's shard.

</details>

---

<details>
  <summary>06: Distributed Database Systems</summary>

### Database Lifecycle

The Database Lifecycle (DBLC) outlines the phases of designing, implementing, and maintaining a database system.

1. **Requirement Analysis**: Gathering business requirements for the database.
2. **Database Design**: Creating the conceptual, logical, and physical models (ER diagrams, schema definition).
3. **Implementation**: Writing the DDL statements to create the database schema and loading the initial data.
4. **Testing**: Verifying the database for accuracy, performance, and security.
5. **Deployment**: Putting the database into production.
6. **Maintenance**: Ongoing activities like performance tuning, backup, recovery, and security updates.

### Distributed Database Systems (DDBMS)

A distributed database is a single logical database that is physically spread across multiple computers (sites or nodes) connected by a network. From the user's perspective, it appears as a single database.

- **Transparency**: The main goal of a DDBMS is to provide transparency.
  - **Location Transparency**: Users don't need to know the physical location of the data.
  - **Replication Transparency**: Users are unaware if data is replicated across multiple nodes.
  - **Failure Transparency**: The system continues to operate even if some nodes fail.


### Architecture of Distributed Database Systems (IMP)

- **Shared Memory**: Multiple processors share a common memory space. This is not truly a distributed system but a tightly coupled multiprocessor system.
- **Shared Disk**: Each processor has its own private memory but has access to all disks on the network. This architecture provides a degree of fault tolerance.
- **Shared Nothing**: This is the most common architecture for DDBMS. Each node has its own processor, memory, and disk. Nodes communicate over the network. This model is highly scalable and fault-tolerant.


### Data Distribution Methods (IMP)

This describes how data is spread across the different sites in a distributed system.

- **Replication**: The system maintains identical copies (replicas) of the database at multiple sites.
  - **Advantages**: High availability and fast read performance (queries can be served by the nearest node).
  - **Disadvantages**: Slow write performance (updates must be propagated to all replicas) and increased storage cost.
- **Fragmentation (Partitioning)**: The database is divided into smaller pieces (fragments), and each fragment is stored at a different site.
  - **Horizontal Fragmentation**: Splits a table by rows (e.g., storing customer data for each region in a server located in that region).
  - **Vertical Fragmentation**: Splits a table by columns (e.g., storing `employee_id` and `name` in one fragment and sensitive `salary` data in a more secure, separate fragment).
- **Hybrid Approach**: A combination of replication and fragmentation. For example, a table might be fragmented, and then some of those fragments might be replicated for higher availability.


### Fault Tolerance in Distributed Databases (IMP)

Fault tolerance is the ability of the system to continue operating in the event of a failure of one or more of its components.

- **Replication**: The primary mechanism for fault tolerance. If a node with a data replica fails, requests can be redirected to another node that has a copy of the same data.
- **Commit Protocols**:
  - **Two-Phase Commit (2PC)**: A protocol to ensure that a transaction is either committed on all participating nodes or aborted on all of them (atomicity).

1. **Phase 1 (Voting Phase)**: The coordinator node asks all participating nodes (cohorts) to prepare to commit. Cohorts vote "yes" or "no".
2. **Phase 2 (Commit/Abort Phase)**: If all cohorts vote "yes," the coordinator sends a "commit" message. If even one votes "no," it sends an "abort" message.
  - **Common Pitfall**: 2PC can be a bottleneck and is susceptible to blocking if the coordinator fails.
- **Quorum-Based Protocols**: To perform a read or write, a client must get votes from a certain number of replicas (a "quorum"). For example, in a system with 5 replicas, a write might require acks from 3 replicas (`W=3`) and a read might require responses from 3 replicas (`R=3`). Since `W + R > N` (where `N` is the number of replicas), this guarantees that a read will see at least one up-to-date copy of the data.


### Load Balancing in Distributed Databases

Load balancing is the process of distributing client requests or network traffic across multiple servers to ensure no single server becomes a bottleneck.

- **Client-Side Load Balancing**: The client application is aware of the multiple database nodes and chooses one to connect to based on a specific logic (e.g., round-robin).
- **Proxy-Based Load Balancing**: A proxy server (like HAProxy or a dedicated middleware) sits between the clients and the database nodes, intercepting requests and routing them to the appropriate node.
- **DNS-Based Load Balancing**: A domain name (e.g., `db.myapp.com`) can resolve to multiple IP addresses of the different database nodes, and clients will be directed to different nodes.


</details>

---

<details>
  <summary>07: Transaction & Concurrency</summary>

### ACID Properties (IMP)

ACID is a set of properties that guarantees database transactions are processed reliably. This is a cornerstone of transactional systems (OLTP).

- **Atomicity**: "All or nothing." A transaction is an indivisible unit of work. Either all of its operations are completed successfully, or none of them are. If any part fails, the entire transaction is rolled back.
- **Consistency**: A transaction brings the database from one valid state to another. It ensures that any data written to the database must be valid according to all defined rules, including constraints, triggers, and cascades.
- **Isolation**: "One at a time." Concurrent transactions are executed in a way that makes it appear as if they are running sequentially. The intermediate state of a transaction is not visible to other transactions.
- **Durability**: "It will stick." Once a transaction has been committed, its changes are permanent and will survive any subsequent system failure (like a power outage or crash).
- **Analogy**: A bank transfer.
  - **Atomicity**: Money must be debited from Account A AND credited to Account B. If the credit fails, the debit must be undone.
  - **Consistency**: The total amount of money in both accounts remains the same before and after the transaction. No money is created or destroyed.
  - **Isolation**: If someone checks the balance of both accounts while the transfer is in progress, they won't see the money missing from Account A before it has appeared in Account B.
  - **Durability**: Once the bank confirms the transfer is complete, the new balances are permanent, even if the bank's server crashes immediately after.


### CAP Theorem (IMP)

The CAP theorem states that a distributed data store can only provide **two** of the following three guarantees simultaneously:

- **Consistency**: Every read receives the most recent write or an error. All nodes in the system have the same data at the same time.
- **Availability**: Every request receives a (non-error) response, without the guarantee that it contains the most recent write. The system is always operational.
- **Partition Tolerance**: The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes (i.e., a network partition).
- **In distributed systems, network partitions are a fact of life, so you must choose between Consistency and Availability.**
  - **CP (Consistency & Partition Tolerance)**: The system will return an error or time out if it cannot guarantee up-to-date data due to a network partition. (Example: Banking systems).
  - **AP (Availability & Partition Tolerance)**: The system will always return the most recent available version of the data, even if it's stale. (Example: Social media feeds, where eventual consistency is acceptable).


### Database Transactions

A transaction is a logical unit of work that consists of one or more database operations. It is managed by TCL commands: `COMMIT` (save the changes), `ROLLBACK` (undo the changes), and `SAVEPOINT` (create a point to roll back to).

### Concurrency Control in Database (IMP)

Concurrency control is the process of managing simultaneous operations on a database without them interfering with one another. Without it, several problems can occur:

- **Dirty Read**: A transaction reads data that has been written by another transaction that has not yet been committed.
- **Non-Repeatable Read**: A transaction reads the same row twice but gets different data each time because another transaction modified it in between.
- **Phantom Read**: A transaction re-executes a query and finds that the set of rows has changed because another transaction inserted or deleted rows.


### Locking Protocols

Locking is a mechanism to ensure that only one transaction can access a data item at a time.

- **Shared Lock (S-lock / Read Lock)**: Allows a transaction to read a data item. Multiple transactions can hold a shared lock on the same item simultaneously.
- **Exclusive Lock (X-lock / Write Lock)**: Allows a transaction to both read and write a data item. Only one transaction can hold an exclusive lock on an item at any given time. No other lock (shared or exclusive) can be placed.
- **Two-Phase Locking (2PL)**: A protocol that ensures serializability. It has two phases:

1. **Growing Phase**: The transaction can obtain locks but cannot release any.
2. **Shrinking Phase**: The transaction can release locks but cannot obtain any new ones.


### Deadlock in DBMS

A deadlock is a situation where two or more transactions are waiting indefinitely for each other to release locks.

- **Example**: Transaction T1 locks resource A and needs resource B. Transaction T2 locks resource B and needs resource A.
- **Deadlock Prevention**: Protocols that ensure the system will never enter a deadlock state (e.g., acquiring all locks at once, or enforcing a lock order).
- **Deadlock Detection & Recovery**: The system periodically checks for deadlocks. If one is found, it "kills" one of the transactions (the victim) to break the cycle.


### Isolation Levels (IMP)

Isolation levels define the degree to which a transaction must be isolated from the data modifications made by other transactions. SQL defines four levels:


| Isolation Level | Dirty Read | Non-Repeatable Read | Phantom Read |
| :-- | :-- | :-- | :-- |
| **Read Uncommitted** | Allowed | Allowed | Allowed |
| **Read Committed** | Not Allowed | Allowed | Allowed |
| **Repeatable Read** | Not Allowed | Not Allowed | Allowed |
| **Serializable** | Not Allowed | Not Allowed | Not Allowed |

- **Best Practice**: `Read Committed` is the default for many databases (like PostgreSQL and Oracle) and offers a good balance between performance and consistency. `Serializable` provides the highest level of isolation but can significantly reduce concurrency.


</details>


---

<details>
  <summary>08: Triggers \& Procedural Features</summary>

### Triggers in Databases (IMP)

A trigger is a special type of stored procedure that automatically runs when a specific event occurs in the database server. The event is typically a DML (Data Manipulation Language) statement like `INSERT`, `UPDATE`, or `DELETE` on a specified table.

- **Purpose**: Triggers are used to maintain data integrity, enforce complex business rules, and automate tasks.
- **Trigger Timing**:
  - **`BEFORE`**: The trigger action is executed *before* the triggering DML statement is run. Useful for validating or modifying data before it's written.
  - **`AFTER`**: The trigger action is executed *after* the triggering DML statement completes. Useful for actions that should only happen if the initial operation was successful, like logging or updating related tables.
- **Trigger Level**:
  - **Row-Level Trigger**: The trigger fires once for each row affected by the DML statement. Inside the trigger, you can access the data of the row being changed using special variables (e.g., `:new` and `:old` in Oracle/PostgreSQL).
  - **Statement-Level Trigger**: The trigger fires only once for the entire DML statement, regardless of how many rows it affects.

**Real-World Example**: Creating an audit trail.
Suppose you want to log every salary change in an `employees` table.

```sql
-- Create a table to store the audit history
CREATE TABLE salary_audit (
    employee_id INT,
    old_salary DECIMAL(10, 2),
    new_salary DECIMAL(10, 2),
    change_date TIMESTAMP
);

-- Create the trigger
CREATE TRIGGER after_salary_update
AFTER UPDATE OF salary ON employees
FOR EACH ROW
BEGIN
    INSERT INTO salary_audit(employee_id, old_salary, new_salary, change_date)
    VALUES (old.employee_id, old.salary, new.salary, NOW());
END;
```

Now, whenever a salary is updated in the `employees` table, this trigger will automatically fire and insert a record into the `salary_audit` table.

**Common Pitfalls**:

- **Cascading Triggers**: A trigger on one table might cause a change in another table, which in turn fires another trigger. This can lead to complex, hard-to-debug chains of events and even infinite loops if not designed carefully.
- **Performance Overhead**: Triggers add overhead to DML operations. Overuse or poorly written triggers can significantly slow down database performance.
- **Hidden Logic**: The business logic is hidden inside the database, which can make the application's behavior harder to understand and maintain compared to keeping logic within the application code.


### Stored Procedures in Databases

A stored procedure is a precompiled collection of one or more SQL statements and procedural logic that is stored in the database. It can be executed by name.

- **Purpose**:
  - **Encapsulate Business Logic**: Complex operations can be encapsulated into a single procedure.
  - **Improve Performance**: The procedure is compiled once and reused, reducing network traffic as the client only sends the procedure name and parameters instead of a long SQL script.
  - **Enhance Security**: Users can be granted permission to execute a stored procedure without having direct access to the underlying tables.

**Stored Procedures vs. Triggers**:


| Feature | Stored Procedure | Trigger |
| :-- | :-- | :-- |
| **Invocation** | Called explicitly by a user or application (`CALL procedure_name();`). | Invoked implicitly (automatically) by a DML event. |
| **Parameters** | Can accept input and return output parameters. | Cannot be passed parameters directly. |
| **Use Case** | Used for performing specific, reusable tasks (e.g., registering a new user, generating a report). | Used for enforcing rules and automating reactions to data changes. |
| **`COMMIT`/`ROLLBACK`** | Can typically contain transaction control statements. | Cannot usually contain `COMMIT` or `ROLLBACK`. |

**Example of a Stored Procedure**:
A procedure to add a new employee and assign them to a department.

```sql
CREATE PROCEDURE AddEmployee (
    IN emp_name VARCHAR(100),
    IN emp_salary DECIMAL(10, 2),
    IN dept_id INT
)
BEGIN
    -- This could contain more complex logic, validation, etc.
    INSERT INTO employees (name, salary, department_id)
    VALUES (emp_name, emp_salary, dept_id);
END;
```

To run it: `CALL AddEmployee('Jane Doe', 60000, 4);`

**Best Practices**:

- Use stored procedures to centralize and reuse complex business logic that is data-intensive.
- Use triggers for tasks that must always happen when data changes, such as auditing or maintaining data integrity that cannot be handled by constraints alone.


</details>


---

<details>
  <summary>09: Recovery & Backup</summary>

### Database Recovery Management

Database recovery is the process of restoring a database to a correct and consistent state after a failure. The primary goal is to uphold the **Atomicity** and **Durability** properties of ACID. Recovery techniques ensure that committed transactions are permanent and uncommitted transactions are completely undone.[^10_1][^10_7]

#### Types of Failures

- **Transaction Failure**: Occurs when a transaction fails to execute or reaches a point where it cannot continue (e.g., due to a logical error or data validation issue).
- **System Crash**: The system fails due to a hardware malfunction or a software bug (e.g., power outage, OS crash). Data in main memory (buffer) is lost, but data on stable storage (disk) is safe.
- **Disk Failure**: A disk block or the entire disk drive fails, leading to data loss. This is the most catastrophic type of failure.


### Recovery Techniques (IMP)

- **Log-Based Recovery**: This is the most common technique. The DBMS maintains a log file on stable storage that records all database modifications (`INSERT`, `UPDATE`, `DELETE`). The log contains records for the start, commit, and abort of transactions.[^10_1]
  - **Undo**: Reverses the changes made by uncommitted (aborted) transactions.
  - **Redo**: Reapplies the changes made by committed transactions to ensure they are durable.
  - **Immediate Update**: Allows database modifications to be written to disk before the transaction commits. Requires both `UNDO` and `REDO` during recovery.
  - **Deferred Update**: Defers all database modifications until the transaction commits. Only requires `REDO` during recovery.[^10_1]
- **Checkpointing**: A mechanism used to optimize log-based recovery. A checkpoint is a point in time where the DBMS forces all modified database buffers and all log records to be written to disk. When recovering from a crash, the system only needs to process the log from the last checkpoint onward, significantly reducing recovery time.[^10_1]
- **Shadow Paging**: This technique maintains two page tables during a transaction: a `current` page table and a `shadow` page table. The shadow table points to the consistent database state before the transaction started. Updates are made to copies of the pages, and the current table points to these new pages. If the transaction commits, the current table becomes the new shadow table. If it aborts, the current table is discarded, and the shadow table is reinstated. This avoids the need for `UNDO` or `REDO` operations.[^10_1]


### Database Backups (IMP)

A backup is a copy of database data that can be used to restore the database in case of data loss.[^10_2]


| Backup Type | Description | Pros | Cons |
| :-- | :-- | :-- | :-- |
| **Full Backup** | A complete copy of the entire database [^10_4]. | Simple restoration; only one backup file is needed. | Time-consuming; requires significant storage space [^10_4]. |
| **Differential Backup** | Copies all data that has changed since the last **full** backup [^10_5]. | Faster to restore than incremental because you only need the last full backup and the last differential backup [^10_5]. | Backup files grow larger over time until the next full backup. |
| **Incremental Backup** | Copies only the data that has changed since the last backup of **any type** (full or incremental) [^10_4]. | Very fast backups; requires the least storage space. | Restoration is complex, as it requires the last full backup plus all subsequent incremental backups in order [^10_4]. |

**Recovery Models**:

- **Simple Recovery**: The transaction log is automatically truncated, and log backups are not supported. Only full or differential backups can be used. You can only restore the database to the point when the backup was taken, meaning some data loss is possible.[^10_5]
- **Full Recovery**: All transactions are logged until the log is backed up. This model supports point-in-time recovery, allowing you to restore the database to a specific moment (e.g., right before an accidental `DELETE` statement was run).[^10_5]
- **Bulk-Logged Recovery**: A supplement to the full model that reduces log space usage for certain large-scale bulk operations (like `BULK INSERT`) by logging them minimally.[^10_5]

**Best Practices**:

- **Regularly schedule backups**. A common strategy is a weekly full backup, daily differential backups, and transaction log backups every 15-30 minutes.
- **Store backups in a separate physical location** to protect against disasters like fire or flood.
- **Regularly test your backups** by performing a trial restoration to ensure they are valid and the recovery process works as expected.


</details>

---

<details>
  <summary>10: Indexing & Performance Tuning</summary>

### Database Indexing (IMP)

An index is a data structure that improves the speed of data retrieval operations on a database table at the cost of additional writes and storage space. It allows the database to find rows matching specific criteria quickly, without having to scan the entire table.[^11_1][^11_6]

- **Analogy**: An index in a database is like the index at the back of a book. Instead of reading the entire book to find a topic (a full table scan), you look up the topic in the index, which tells you the exact page numbers (data pointers) where it's mentioned.

**Advantages of Indexing**:

- **Faster Query Performance**: Dramatically speeds up `SELECT` queries with `WHERE` clauses and `JOIN` operations.[^11_2][^11_5]
- **Efficient Sorting**: Speeds up `ORDER BY` and `GROUP BY` operations as the data can be retrieved in sorted order directly from the index.[^11_5][^11_2]
- **Enforces Uniqueness**: A unique index ensures that no two rows have the same value in the indexed column(s).[^11_1]

**Disadvantages of Indexing**:

- **Storage Overhead**: Indexes require additional disk space.[^11_1]
- **Slower DML Operations**: `INSERT`, `UPDATE`, and `DELETE` statements become slower because the database must update the indexes as well as the table data.[^11_1]


### Types of Database Indexing (IMP)

- **Single-Column Index**: An index created on a single column.
- **Composite (or Multi-column) Index**: An index created on two or more columns. The order of columns in the index is crucial.
  - **Best Practice**: For a query like `WHERE col1 = 'A' AND col2 = 'B'`, an index on `(col1, col2)` is very effective. An index on `(col2, col1)` would be less effective.

| Index Type | Description | Key Characteristic |
| :-- | :-- | :-- |
| **Clustered Index** | Determines the physical order of data in a table [^11_6]. The leaf nodes of the index contain the actual data rows. | Only **one** clustered index per table. Data is physically sorted on disk according to the index key [^11_1]. |
| **Non-Clustered Index** | The logical order of the index is separate from the physical storage of the rows [^11_2]. The leaf nodes contain pointers to the data rows. | A table can have **multiple** non-clustered indexes [^11_6]. This is like a book's index. |
| **Unique Index** | Enforces that all values in the index key must be unique. A primary key is automatically a unique, clustered index by default in many systems [^11_7]. | Prevents duplicate values [^11_6]. |

### Indexing Techniques

- **B-Tree \& B+ Tree (IMP)**: Most relational databases use B-Trees or B+ Trees for indexing. They are self-balancing tree data structures that maintain sorted data and allow for efficient insertion, deletion, and searching (in logarithmic time).
  - **B-Tree**: Can store data pointers at both internal nodes and leaf nodes.
  - **B+ Tree**: All data pointers are stored exclusively at the leaf nodes. The leaf nodes are also linked together in a doubly-linked list, which allows for very efficient range queries (e.g., `WHERE age BETWEEN 20 AND 30`). This is why B+ Trees are more commonly used for database indexing.
- **Hash Index**: Uses a hash function to compute the location of the data. Extremely fast for exact-match lookups (`WHERE id = 123`) but not useful for range queries (`WHERE id > 100`).[^11_8]
- **Bitmap Index**: Uses a string of bits (a bitmap) to represent the existence of a value for a column. Highly efficient for columns with low cardinality (few distinct values, e.g., 'Gender' with values 'Male', 'Female', 'Other') and often used in data warehouses.[^11_8]
- **Full-Text Index**: Designed for searching text data. It allows you to search for words and phrases within a text column efficiently, something `LIKE '%word%'` is very slow at.[^11_8]
- **Covering Index**: A composite index that includes all the columns needed to satisfy a query (in the `SELECT`, `WHERE`, and `JOIN` clauses). The database can answer the query using only the index, without ever having to access the table data itself, which is extremely fast.

**Best Practices for Indexing**:

- Index columns that are frequently used in `WHERE` clauses, `JOIN` conditions, and `ORDER BY` clauses.
- Do not over-index. Each index slows down DML operations.
- For composite indexes, place the most selective column (the one with the most unique values) first.
- Regularly monitor and maintain indexes. Unused indexes should be dropped.

</details>

---

<details>
  <summary>11: Database Monitoring & Caching</summary>

### Database Monitoring

Database monitoring is the process of tracking the performance, availability, and overall health of a database to ensure it operates efficiently and reliably. Proactive monitoring helps identify and resolve issues before they impact users.[^12_2][^12_6]

#### Key Performance Metrics to Monitor (IMP)

Monitoring can be broken down into key areas :[^12_4]

**1. Query Performance**

- **Query Throughput**: The number of queries executed per second. A sudden drop can indicate a bottleneck.[^12_7]
- **Query Latency / Response Time**: The time taken to execute a query. High latency is a direct indicator of poor performance.[^12_5]
- **Slow Queries**: Identifying the specific queries that take the longest to run is crucial for optimization efforts.[^12_5]

**2. Resource Utilization**

- **CPU Usage**: High CPU usage can indicate inefficient queries or an overloaded server. Consistent usage above 80% is a red flag.[^12_5]
- **Memory Usage**: Tracks how much memory is being used by the database. Insufficient memory leads to more disk I/O, which is slow.[^12_4]
- **Disk I/O**: Measures the read/write operations on the disk. High I/O rates can be a major bottleneck.[^12_5]

**3. Buffer Cache Performance**

- **Cache Hit Ratio**: The percentage of data requests that are served from the in-memory cache versus being read from disk. A high cache hit ratio (e.g., >99% for OLTP systems) is desirable.[^12_4]
- **Page Life Expectancy (PLE)**: The average time a data page stays in the buffer cache. A low PLE indicates memory pressure, as pages are being flushed from memory too quickly to be reused.[^12_4]

**4. Concurrency and Locking**

- **Locks and Blocks**: The number of active locks and blocking transactions. A high number of blocks indicates contention issues where transactions are waiting for others to release locks.[^12_4]
- **Deadlocks**: The number of deadlocks detected. While occasional deadlocks can happen, a frequent occurrence indicates a design problem.

**Popular Monitoring Tools**:

- **Native Tools**: Most databases come with built-in tools (e.g., Oracle Enterprise Manager, SQL Server Management Studio's Activity Monitor).[^12_1][^12_3]
- **Third-Party Tools**: Comprehensive platforms like Datadog, SolarWinds, and Middleware offer advanced monitoring across different database types.[^12_9][^12_1]


### Performance Tuning

Performance tuning is the process of optimizing database performance by identifying and resolving bottlenecks found during monitoring.

- **Query Tuning**: Rewriting inefficient queries, adding appropriate indexes, or using query hints. Using tools like `EXPLAIN PLAN` to analyze the query execution path is a key step.
- **Index Tuning**: Adding necessary indexes, removing unused ones, and ensuring composite indexes are ordered correctly.
- **Configuration Tuning**: Adjusting database server parameters (e.g., memory allocation for the buffer pool, parallelism settings).
- **Schema Optimization**: Denormalizing tables, partitioning large tables, or using materialized views for frequently accessed, complex aggregations.


### Database Caching (IMP)

Caching involves storing frequently accessed data in a faster storage layer (like RAM) to reduce the need to access the slower primary data store (like a disk).

- **Internal Caching (Buffer Pool)**: The database's own internal memory cache where it stores recently used data pages. Performance tuning often involves properly sizing this buffer pool.
- **External Caching**: Using a separate, dedicated in-memory data store (like Redis or Memcached) to cache query results or application objects.


### Database Caching Strategies (IMP)

This describes how data is populated into and managed within an external cache.


| Strategy | How it Works | Pros | Cons |
| :-- | :-- | :-- | :-- |
| **Cache-Aside** | The application is responsible for managing the cache. **Flow**: 1. App requests data from the cache. 2. If **cache miss**, app reads data from the DB. 3. App stores data in the cache. 4. App returns data. | Resilient to cache failures (app can still talk to the DB). The data model in the cache can be different from the DB. | Inconsistent data if the DB is updated but the cache is not (cache invalidation is complex). Every cache miss results in three trips (cache, DB, cache). |
| **Read-Through** | The application treats the cache as the main data store. The cache itself is responsible for fetching data from the DB on a cache miss. **Flow**: 1. App requests data from cache. 2. If **cache miss**, the *cache* reads data from the DB, stores it, and returns it to the app. | Application code is simpler as the caching logic is abstracted away. | Less flexible data model (usually mirrors the DB). |
| **Write-Through** | Data is written to the cache and the database simultaneously. **Flow**: App writes data to the cache, and the cache immediately writes it to the DB. | High data consistency; data in the cache is never stale. | Higher write latency because every write goes to both the cache and the DB. |
| **Write-Back** | Data is written only to the cache. The cache asynchronously writes the data to the database after a delay. | Very low write latency and high write throughput. | Risk of data loss if the cache fails before the data is written to the DB. |
| **Write-Around** | Data is written directly to the database, bypassing the cache. Only data that is read is populated into the cache. | Good for workloads with few re-reads of recently written data. Avoids "cache pollution." | A read request for recently written data will result in a cache miss and higher latency. |

**Best Practice**: The **Cache-Aside** pattern is the most common caching strategy due to its flexibility and resilience.

</details>

---

<details>
  <summary>12: Security \& Access Control</summary>

### Database Security

Database security refers to the collective measures—policies, procedures, and technologies—used to protect a database from unauthorized access, malicious attacks, and data breaches. It encompasses protecting the data itself, the database management system, and the applications that access it.[^13_2][^13_5]

#### Best Practices for Database Security (IMP)

- **Principle of Least Privilege**: Grant users only the minimum permissions necessary to perform their jobs. Avoid giving broad permissions like `DBA` or `admin` to application service accounts.[^13_5]
- **Separate Servers**: Isolate the database server from the web/application server. This prevents an attacker who compromises the web server from directly accessing the database.[^13_2][^13_5]
- **Regular Patching and Updates**: Keep the DBMS and operating system updated with the latest security patches to protect against known vulnerabilities.[^13_1][^13_5]
- **Use Firewalls**: Implement both network firewalls to restrict traffic to the database server and Web Application Firewalls (WAF) to protect against attacks like SQL injection.[^13_5]
- **Disable Default Accounts**: Remove or rename default administrative accounts and change their passwords immediately after installation.[^13_3]
- **Audit and Monitor**: Regularly audit database activity, log all login attempts, and monitor for suspicious behavior.[^13_5]
- **Separate Environments**: Strictly separate production and testing environments. Never use real production data in test environments.[^13_2][^13_5]


### Data Encryption in DBMS (IMP)

Encryption scrambles data into an unreadable format (ciphertext) that can only be read by someone with the correct decryption key. It is a critical defense against data breaches.[^13_5]

- **Encryption in Transit**: Protects data as it moves over the network (e.g., between the application server and the database server). This is typically achieved using protocols like **TLS (Transport Layer Security)**.[^13_3][^13_2]
- **Encryption at Rest**: Protects data where it is stored on disk (e.g., in database files, backups, or logs). This prevents data from being read if the physical storage media is stolen.[^13_2]
- **Analogy**: Encryption in transit is like sending a letter in a sealed, tamper-proof envelope. Encryption at rest is like keeping the letter in a locked safe.


#### Encryption Techniques in DBMS

- **Transparent Data Encryption (TDE)**: A feature in many DBMSs (like SQL Server and Oracle) that automatically encrypts the entire database file at rest. It's "transparent" because the application does not need to be aware that the data is encrypted.
- **Column-Level Encryption**: Encrypts specific sensitive columns within a table (e.g., social security numbers, credit card numbers). This provides more granular control than TDE but requires application-level changes to manage encryption/decryption.[^13_2]
- **Application-Level Encryption**: The application encrypts the data *before* it is sent to the database. This provides the highest level of security, as the DBAs cannot see the unencrypted data, but it adds complexity to the application code.


### Data Masking Techniques

Data masking (or data obfuscation) is the process of creating a structurally similar but inauthentic version of an organization's data. It's used to protect sensitive data while providing a functional substitute for non-production environments (e.g., testing, development).

- **Substitution**: Replacing sensitive data with random but realistic-looking values from a pre-defined list (e.g., replacing real names with fake names).
- **Shuffling**: Randomly reordering values within a column (e.g., shuffling the `salary` column so that the salary values remain, but they are no longer associated with the correct employee).
- **Redaction/Nulling Out**: Replacing sensitive characters with a fixed character (e.g., `XXX-XX-1234`) or simply `NULL`.


### RBAC (Role-Based Access Control) (IMP)

RBAC is a security model that controls access to resources based on the roles of individual users within an enterprise. Instead of assigning permissions to users directly, permissions are assigned to roles, and users are then assigned to roles.

- **How it Works**:

1. **Permissions** are defined (e.g., `SELECT`, `INSERT` on the `employees` table).
2. **Roles** are created (e.g., `HR_Manager`, `Analyst`, `Clerk`).
3. Permissions are granted to roles (e.g., the `HR_Manager` role gets `SELECT`, `UPDATE` on `employees`; the `Analyst` role gets only `SELECT`).
4. **Users** are assigned to roles (e.g., Alice is assigned the `HR_Manager` role).
- **Advantages**:
  - **Simplified Administration**: Managing roles is easier than managing permissions for hundreds of individual users. When a user changes jobs, you just change their role assignment.
  - **Improved Security**: Enforces the principle of least privilege in a scalable way.


</details>

---

<details>
  <summary>13: Scalability & Big Data</summary>

### Database Scaling (IMP)

Database scaling is the process of increasing a database's capacity to handle growing amounts of data and traffic. There are two primary methods:


| Scaling Method | Description | Pros | Cons |
| :-- | :-- | :-- | :-- |
| **Vertical Scaling (Scaling Up)** | Increasing the resources of a single server, such as adding more CPU, RAM, or faster storage (SSDs). | Simple to implement; no changes needed in the application code. | Has a hard physical limit; becomes prohibitively expensive at the high end. Creates a single point of failure. |
| **Horizontal Scaling (Scaling Out)** | Adding more servers (nodes) to a cluster and distributing the load among them. This is the foundation of most distributed systems. | Virtually limitless scalability; provides high availability and fault tolerance. | More complex to manage; requires changes in application design and database architecture (e.g., sharding). |

**Analogy**:

- **Vertical Scaling**: Replacing your car's four-cylinder engine with a powerful V8.
- **Horizontal Scaling**: Keeping your car but buying several more identical cars to handle more passengers.


### Big Data and DBMS

Big Data refers to datasets that are too large or complex for traditional data-processing application software to adequately deal with. It is characterized by the "3 Vs" (which have expanded over time):

- **Volume**: The sheer amount of data (terabytes, petabytes).
- **Velocity**: The speed at which data is generated and needs to be processed (e.g., real-time streaming data from sensors).
- **Variety**: The different forms of data (structured, semi-structured, and unstructured data like text, images, videos).


#### How DBMS Technologies Handle Big Data:

- **Relational Databases (RDBMS)**: Generally not suitable for the unstructured nature and sheer volume of big data. While they can store large amounts of structured data, they are difficult to scale horizontally.
- **NoSQL Databases**: Designed specifically for big data challenges.
  - **Document \& Key-Value Stores (MongoDB, DynamoDB)** handle variety and volume with flexible schemas.
  - **Column-Family Stores (Cassandra, HBase)** are optimized for high-velocity write operations and large-scale analytics.
- **Distributed Processing Frameworks**: Systems like **Apache Hadoop** (with its Hadoop Distributed File System - HDFS) and **Apache Spark** are not databases themselves but are ecosystems designed to store and process big data across clusters of computers. They often work in conjunction with NoSQL databases.
  - **Hadoop MapReduce**: A programming model for processing large datasets in parallel across a distributed cluster. A "map" job filters and sorts the data, and a "reduce" job performs a summary operation.
  - **Apache Spark**: A faster and more flexible successor to MapReduce. It performs processing in-memory, making it significantly faster for many workloads, especially iterative machine learning tasks.


### DBaaS (Database as a Service)

DBaaS is a cloud computing service that lets users access and use a database system without having to purchase and manage the underlying hardware, software, or infrastructure themselves. The cloud provider is responsible for installation, maintenance, backups, and scaling.

**Advantages of DBaaS**:

- **Reduced Administrative Overhead**: The provider handles patching, backups, and replication, freeing up developers and DBAs to focus on application development.
- **Scalability and Elasticity**: Easily scale resources up or down (both vertically and horizontally) on demand, paying only for what you use.
- **High Availability and Durability**: Most DBaaS offerings include built-in fault tolerance and automated failover mechanisms.
- **Cost-Effectiveness**: Converts large capital expenditures (buying servers) into predictable operational expenses.

**Popular DBaaS Providers and Offerings**:

- **Amazon Web Services (AWS)**:
  - **Amazon RDS (Relational Database Service)**: Managed service for RDBMS like PostgreSQL, MySQL, Oracle.
  - **Amazon DynamoDB**: Fully managed, serverless NoSQL key-value and document database.
  - **Amazon Aurora**: A proprietary, high-performance relational database compatible with MySQL and PostgreSQL.
- **Google Cloud Platform (GCP)**:
  - **Cloud SQL**: Managed RDBMS.
  - **Cloud Spanner**: A globally distributed, strongly consistent relational database service.
- **Microsoft Azure**:
  - **Azure SQL Database**: Managed RDBMS.
  - **Azure Cosmos DB**: A globally distributed, multi-model NoSQL database.


</details>

---

<details>
  <summary>14: Data Warehousing & Migration</summary>

### Database Migration

Database migration is the process of moving data from one or more source databases to a target database. This can involve moving to a new hardware platform, a new version of the DBMS, or a completely different database system (e.g., from an on-premises Oracle database to a cloud-based PostgreSQL database).

#### Phases of Database Migration

1. **Pre-Migration (Planning)**:
  - **Assessment**: Analyze the source schema, data volume, and application dependencies.
  - **Strategy Selection**: Choose the migration approach (e.g., Big Bang vs. Trickle).
  - **Tool Selection**: Select appropriate migration tools.
2. **Migration (Execution)**:
  - **Schema Migration**: Convert the source schema to be compatible with the target database.
  - **Data Migration**: The actual transfer of data.
  - **Testing**: Rigorously test the migrated database for data integrity, performance, and functionality.
3. **Post-Migration**:
  - **Cutover**: Switch the application from the source database to the target database.
  - **Validation**: Perform final checks in the production environment.
  - **Decommission**: Retire the old source database.

#### Migration Strategies (IMP)

- **Big Bang Migration**: The entire database is moved in a single, scheduled event. This requires significant downtime but is simpler to manage.
- **Trickle Migration (Phased Migration)**: The migration occurs in phases. Data is moved incrementally, and the old and new systems run in parallel. An event-driven architecture or triggers can be used to keep both systems in sync. This approach minimizes downtime but is much more complex to execute.


### Data Warehousing (IMP)

A data warehouse is a large, centralized repository of integrated data from one or more disparate sources. It is designed to support business intelligence (BI) activities, especially analytics. Data warehouses store historical data and are optimized for fast query performance (OLAP) rather than transactional processing (OLTP).[^15_7]

#### Characteristics of a Data Warehouse

- **Subject-Oriented**: Data is organized around major subjects of the enterprise (e.g., `Customer`, `Product`, `Sales`) rather than the ongoing operations of applications.
- **Integrated**: Data is collected from multiple, heterogeneous sources and is cleaned and transformed to have a consistent format.
- **Time-Variant**: Data in the warehouse represents a long-range history (e.g., 5-10 years), allowing for analysis of trends over time.
- **Non-Volatile**: Data in the warehouse is read-only. Once loaded, it is not updated or changed, only added to.


#### Data Warehouse vs. OLTP Database

| Feature | Data Warehouse (OLAP) | OLTP Database |
| :-- | :-- | :-- |
| **Purpose** | Analytical Processing, Business Intelligence | Transactional Processing, Day-to-day Operations |
| **Design** | Denormalized, Star/Snowflake schemas | Normalized (3NF), ER Model |
| **Data** | Historical, aggregated data | Current, detailed data |
| **Operations** | Mostly complex `SELECT` queries (reads) | Frequent simple `INSERT`, `UPDATE`, `DELETE` (writes) |
| **Users** | Business analysts, data scientists | End-users, application servers |
| **Metric** | Query throughput, data load speed | Transaction throughput |

#### Data Warehouse Architecture Components

1. **Data Sources**: The operational systems (OLTP databases, CRMs, flat files) that provide the raw data.[^15_1]
2. **ETL/ELT Layer**: The process that moves data from sources to the warehouse.
  - **ETL (Extract, Transform, Load)**: Data is extracted, transformed into a standard format in a staging area, and then loaded into the warehouse.[^15_2][^15_4]
  - **ELT (Extract, Load, Transform)**: Raw data is loaded directly into the data warehouse, and transformations are performed inside the warehouse using its processing power. This is a more modern approach favored by cloud data warehouses.[^15_4]
3. **Central Data Repository**: The core of the warehouse, usually a relational database optimized for analytics.
4. **Data Marts**: Subsets of a data warehouse that are focused on a specific business line or department (e.g., a `Sales` data mart). They provide specific user groups with faster access to the data they need.[^15_1]
5. **BI and Analytics Tools**: The front-end tools that users interact with to run queries, create reports, and build dashboards (e.g., Tableau, Power BI).[^15_2]

### Event-Driven Architecture (EDA)

An event-driven architecture is a software design pattern where components communicate by producing and consuming events. An "event" is a significant change in state (e.g., `OrderPlaced`, `InventoryUpdated`).

- **How it relates to Databases**:
  - **Change Data Capture (CDC)**: A key technique in EDA where changes in a source database (inserts, updates, deletes) are captured as events and streamed to other systems in real-time. This is often used for:
    - Replicating data to a data warehouse without batch ETL jobs.
    - Keeping caches in sync with the database.
    - Powering trickle database migrations.
  - **Tools**: Platforms like **Apache Kafka** and **Debezium** are commonly used to build CDC pipelines.


</details>

