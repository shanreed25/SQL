# SQL (Structured Query Language)
- the standard programming language used to interact with and manage relational databases
    - published standard (ANSI/ISO), providing a consistent way to interact with databases
    - database is a systematically organized collection of data
    - relational databases stores data into tables with rows and columns
- powerful language used by database administrators, developers, and data analysts
- allows users to perform a wide range of operations on data, including creating databases and tables, retrieving data using queries, and modifying existing data by adding, updating, or deleting it
- once you learn SQL, you can use it with many different database systems like MySQL, PostgreSQL, and Microsoft SQL Server

## Relational Databases
- store and organize data in structured tables with pre-defined relationships, using a tabular format of rows and columns to represent records and attributes
- managed by a Relational Database Management System (RDBMS), which allows users to define, query, and manipulate data using structured query language (SQL)
- maintains data integrity through transactions and ensures relationships between different tables are robust and accessible
    - robust: strong, reliable, and performs well under various conditions, including errors, invalid inputs, and environmental changes, minimizing failures and ensuring consistent functionality and security for users
- normalization, which involves organizing data in a way that reduces redundancy and improves data integrity within the database

### Where are they located?
**Relational Databses can be located in various places, including on local servers, in desktop applications, or within cloud-based systems offered by providers like Amazon Web Services, Google Cloud, and Microsoft Azure**
- **On-Premises/Local Systems:** can be hosted on dedicated hardware within an organization's own data centers or on individual personal computers for smaller applications. 
- **Desktop Applications:** some desktop applications, such as Microsoft Access, use relational database models to store and manage data locally. 
- **Cloud-Based Services:** major cloud providers offer managed relational database services, making them accessible and scalable for applications hosted in the cloud. 
- **Web Applications and Websites:** many websites and online applications rely on relational databases to store user data, product catalogs, and order information. 

### How Relational Databases Work
- **Tables (or Relations):** data is stored in tables, each designed around a single entity (like a customer or a product). 
- **Columns (Attributes):** each table has columns that define specific data attributes, such as a customer's "name" or "address". 
- **Rows (Tuples):** each row in a table represents a single instance of that data, like a specific customer's information. 
- **Relationships:** tables are connected through defined relationships, often by using unique identifiers (like a customer ID) in multiple tables. This allows users to link and combine data from different tables to gain insights. 

# Why use SQL
- manage large datasets effciently
    - easy to summarize data, by writing queries to get what you need
- analyze and extract insights from data
    - easy to discover patterns, trends, and correlations, and then interpret these findings into meaningful, actionable knowledge that can inform and drive better decision-making, problem-solving, and strategic planning
    - involves transforming complex datasets into a story that provides a deeper understanding of customers, operations, market opportunities, and future outcomes
- ensures data security and integrity
- supports multi-user access and scalability
- enable data-driven decision-making

### What you can do with SQL
- **Create and define:** databases, tables, and other structures within a database. 
- **Insert, update, and delete:** data within tables. 
- **Retrieve data:** from databases by writing structured queries to select specific information. 
- **Join data:** from multiple tables based on common columns to create more comprehensive reports. 
- **Manage permissions:** to control access to the database and its data. 

### How SQL works
- **User Input:** You write a SQL statement (a command) that specifies the data operation you want to perform.
- **Database Interaction:** A SQL engine within the database management system processes your query.
    - query is a request for data or information from a database
    - queries can perform CRUD operations
    - queries are ran from editors, some database provide editors but you can also connect your databse to a third party editor such as VS Code, MySQL or Azure
- **Execution:** The query engine retrieves, modifies, or creates data according to your command.
- **Results:** The database then returns the requested data or a success message to you.

### SQL Commands
- commands are instructions used to interact with a relational database management system (RDBMS) to perform various operations
- commands are fundamental for managing, retrieving, and manipulating data stored in structured formats
- categorized into several types based on their function

#### Command Categories
- **[Data Definition Language(DDL)](./Commands/DDL.md):** for defining and modifying the database structure
- **[Data Manipulation Language(DML)](./Commands/DML.md):** for manipulating data within database tables
- **[Data Control Language(DCL)](./Commands/DCL.md):**  for managing access rights and permissions within the database
- **[Transaction Control(TCL)](./Commands/TCL.md):** for managing transactions within the database to ensure data integrity
- **[Data Query Language(DQL)](./Commands/DQL.md):** for retrieving data from the database


- [SQL Components](./Components/)
- [SQL Tools](./Tools/README.md)
- [SQL Operations and Functions](./Operations-Functions/README.md)

_____________________________________________________


# NULL
- a special marker that signifies that the value is either unknown, not applicable, or will be added later
- is distinct from zero, an empty string, or a blank space, as it represents the absence of any value
- comparisons involving NULL (e.g., NULL = NULL, NULL > 5) do not evaluate to TRUE or FALSE but rather to UNKNOWN due to the indeterminate nature of NULL
- to check for NULL values in a WHERE clause, the IS NULL or IS NOT NULL operators must be used instead of standard comparison operators

## Impact on Aggregate Functions:
- Aggregate functions like AVG(), SUM(), and COUNT() typically ignore NULL values in their calculations unless explicitly handled (e.g., using COALESCE to replace NULL with a default value).
## Sorting:
- when sorting in ascending order, NULL values usually appear first, while in descending order, they typically appear last.
## Constraints:
- columns can be defined as NOT NULL to prevent NULL values from being inserted, ensuring data integrity for mandatory fields like primary keys.
## Functions:
- SQL provides functions like COALESCE (returns the first non-NULL expression in a list) and NULLIF (returns NULL if two expressions are equal, otherwise returns the first expression) to handle NULL values in various scenarios

