- **[Data Manipulation Language(DML)]():** for manipulating data within database tables
    - **INSERT:** To add new rows of data into a table.
    - **UPDATE:** To modify existing data in a table.
    - **DELETE:** To remove rows of data from a table.
    - **MERGE:** To combine

# INSERT(DML)
1. Inserting values into specified columns
    - allows you to insert data into specific columns of a table, leaving other columns to their default values or NULL if permitted
    - order of values must match the order of columns. String values should be enclosed in single quotes
    ```
    INSERT INTO table_name (column1, column2, column3, ...)
    VALUES (value1, value2, value3, ...);
    ```

2. Inserting values into all columns
    - you can omit the column names
    - the order of values in the VALUES clause must match the order of columns in the table's definition
    ```
    INSERT INTO table_name
    VALUES (value1, value2, value3, ...);
    ```

3. Inserting multiple rows
    - insert multiple rows in a single INSERT INTO statement by separating each set of values with a comma
    ```
    INSERT INTO table_name (column1, column2)
    VALUES (value1a, value2a),
        (value1b, value2b),
        (value1c, value2c);
    ```

4. Inserting data from another table (INSERT INTO SELECT)
    - copies data from one table and inserts it into another
    - data types of the source and target columns must be compatible
    ```
    INSERT INTO target_table (column1, column2, ...)
    SELECT source_column1, source_column2, ...
    FROM source_table
    WHERE condition;
    ```