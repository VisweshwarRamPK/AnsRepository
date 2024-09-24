**9) JPA:**

**I) DEFINITION:**

Java Persistence API (JPA) supports object-relational mapping (ORM) that allows developers to map Java objects (entities) to relational database tables and manage interactions between the Java application and a relational database.It allows developers to work with Java objects instead of writing SQL queries directly.

**Purpose: **JPA acts like a translator between your Java code and the database. It takes Java objects (like classes and variables) and stores them as rows and columns in a database (like MySQL or PostgreSQL). When you need the data back, JPA converts the database rows into Java objects again. This makes it much easier to work with databases because you don't have to write complicated SQL queries. You can focus on your Java code, and JPA handles the database for you.

**II) PROBLEMS SOLVED BY JPA:**

**Eliminates Boilerplate Code**: Without JPA, developers would need to write complex and repetitive SQL queries to perform CRUD (Create, Read, Update, Delete) operations. JPA automatically generates the SQL based on the Java entity, reducing boilerplate code.

**Object-Relational Mapping (ORM)**: JPA solves the problem of mapping Java objects to database tables, making it easier to persist Java objects in a database and retrieve them as objects

**III) RELATIONSHIPS IN JPA:**

**One-to-One:** Maps a one-to-one relationship between two entities. Example: A user has exactly one profile.

**One-to-Many: **Maps a one-to-many relationship. Example: A department has many employees.

**Many-to-One:** Maps a many-to-one relationship. Example: Many employees work in one department.

**Many-to-Many: **Maps a many-to-many relationship. Example: Many students can enroll in many courses.

**IV) ADVANTAGES OF JPA:**

**Simplifies Database Operations: J**PA removes the complexities of working directly with the database, reducing the amount of SQL you need to write.

**Platform Independence:** JPA makes your application independent of the underlying database. Switching databases (e.g., from MySQL to PostgreSQL) requires minimal changes.

**V) COMMON JPA PROVIDERS:**

**Hibernate,Eclipse.**

**VI) CRUD OPERATIONS IN JPA:**

**Create (Add data):**



* To add new data to the database, you create a new Java object and use `EntityManager.persist()` to save it as a row in the database.

**Read (Get data):**



* To get data from the database, you can use methods like `EntityManager.find()` or write queries using JPQL (Java Persistence Query Language). This pulls the data from the database and converts it into Java objects.

**Update (Change data):**



* JPA automatically tracks changes you make to objects. When you use `EntityManager.merge()`, it updates the corresponding row in the database with the new values from the object.

**Delete (Remove data):**



* To delete data from the database, you use `EntityManager.remove()` to delete a Java object, which will remove the corresponding row from the database.

**VII) CONCEPTS IN JPA:**

**Entity:**



* An Entity is a Java class that represents a table in the database.
* Each object of that class is like a row in the table.
* You mark it with `@Entity` to tell JPA it should be stored in the database, and the class fields (variables) are mapped to columns in the table.

**EntityManager:**



* This is the main tool in JPA to manage database operations.
* It helps you create, read, update, and delete data, as well as run queries.

**Persistence Context:**



* It’s like a workspace where JPA keeps track of the entities.
* It ensures that when you make changes to entities, they stay in sync with the database.

**JPQL (Java Persistence Query Language):**



* JPQL is similar to SQL, but it works with Java objects instead of directly interacting with tables and rows.
* You use it to run queries (like fetching or updating data) based on objects.

**Annotations:**



* JPA uses annotations to connect Java classes and fields to database tables and columns.

**Important ones include:**



* **<code>@Entity</code>: Maps the class to the database table.</strong>
* <strong><code>@Id</code>: Marks the primary key (unique identifier) for each row.</strong>
* <strong><code>@GeneratedValue</code>: Automatically generates the primary key.</strong>
* <strong><code>@Column</code>: Maps a field to a column in the table.</strong>
* <strong>Relationship annotations like <code>@OneToMany</code>, <code>@ManyToOne</code>, <code>@OneToOne</code>, <code>@ManyToMany</code> show how classes are connected, similar to how tables relate in a database.</strong>

<strong>VIII) FEATURES IN JPA: </strong>

**Lazy vs. Eager Loading:**



* **Lazy Loading:** Loads data only when you actually need it. This helps keep things fast because it doesn’t fetch everything at once.
* **Eager Loading:** Loads all the data immediately. This can be slower because it fetches everything.

**Object-Relational Mapping (ORM):**



* **Definition: **JPA provides a way to map Java objects (entities) to database tables and vice versa. This allows developers to interact with the database using Java objects rather than raw SQL queries.

**Persistence Context:**



* **Definition: **A persistence context is a set of entity instances where JPA manages and tracks their states. It ensures that changes to entities are synchronized with the database.

**Transaction Management:**



* **Definition: **JPA simplifies transaction handling through annotations like `@Transactional`. This ensures that database operations are committed or rolled back consistently.
