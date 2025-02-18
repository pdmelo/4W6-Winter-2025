# NoSQL vs SQL

## Databases

- A structured way to store and manage data.

- Two major types: SQL (Relational) & NoSQL (Non-relational).

- Choosing the right database depends on your project needs.

## SQL

- A SQL database, is a relational database. This means that data is stored in a structured format, usually called tables, rows columns, containing specific pieces and types of data.

- Relationships are explicitly made between these tables. That is why you have foreign keys, joins, etc. along with the idea of one-to-one, one-to-many, many-to-one and many-to-many relationships.

- A SQL database works best when the data they contain doesn't change very often, and when accuracy is crucial.
  **Examples:** MySQL, PostgreSQL, Microsoft SQL Server, Oracle.

## NoSQL

- A NoSQL database is non-relational. Data is stored in "unstructured", non-tabular form. For instance, they might be stored in data structures called documents. A document can be highly detailed while containing a range of different types of information in different formats. This lets various types of information be organized side-by-side

- A NoSQL database is often used when large quantities of complex and diverse data need to be organized, and/or when data changes frequently.
- They are also useful for developing applications where the data needs change quickly.
  Unstructured data = not arranged according to a pre-set model or schema.

In many cases, a NoSQL document is specified in terms of name-value pairs and can be represented using **JSON format**

**Examples:** MongoDB, Cassandra, Redis, Neo4j.

## Key Differences Between SQL and NoSQL

| Feature         | SQL Databases                   | NoSQL Databases                      |
| --------------- | ------------------------------- | ------------------------------------ |
| **Schema**      | Fixed schema                    | Flexible schema                      |
| **Structure**   | Tables & Rows                   | JSON, Key-Value, Graph, Column-based |
| **Scalability** | Vertical Scaling                | Horizontal Scaling                   |
| **Use Cases**   | Structured data, financial apps | Big data, real-time analytics        |

## SQL vs NoSQL – Real-World Scenarios

- E-commerce: SQL for inventory management, NoSQL for product recommendations.

- Social Media: SQL for user profiles, NoSQL for real-time feeds.

- Healthcare: SQL for patient records, NoSQL for large-scale medical data.
