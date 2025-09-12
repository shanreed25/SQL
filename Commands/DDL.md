- **[Data Definition Language(DDL)]():** for defining and modifying the database structure
    - **CREATE:** To create database objects like tables, views, indexes.
    - **ALTER:** To modify the structure of existing database objects.
    - **DROP:** To delete database objects.
    - **TRUNCATE:** To remove all records from a table, including space allocated for the records, but not the table structure itself.
    - **RENAME:** To rename a database object.


_______________________________________________________

# CREATE
- define and create new database objects
1. Creating a Database
    - `CREATE DATABASE db_name;`

2. Creating a Table
    - define and create a new table within a database 
    - specify the table name, column names, their data types, and any constraints
    ```
    CREATE TABLE table_name (
        column1 datatype [constraints],
        column2 datatype [constraints],
        ...
        columnN datatype [constraints]
    );
    ```

3. Creating an Index
    - used to create indexes on tables to improve the performance of data retrieval
    - indexes speed up data retrieval, they can add overhead to data modification operations (inserts, updates, deletes) as the index also needs to be updated
    - indexes should be created strategically on columns frequently used in WHERE clauses or JOIN conditions
        ```
        CREATE INDEX index_name
        ON table_name (column1, column2, ...);
        ```
