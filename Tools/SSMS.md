# SQL Server Management Studio (SSMS)



### Errors
- red squiggly lines under table names and columns typically indicate that IntelliSense is not recognizing these objects. This often occurs even when the objects genuinely exist and your SQL code is correct.
    - IntelliSense local cache is not up to date
    - can happen after: Creating new tables or views, Adding new columns to existing tables, and Modifying database objects
    - refreshing the cache forces IntelliSense to re-scan the database metadata and update its understanding of the available objects, which should eliminate the red squiggly lines if the objects are valid
        - Refresh the IntelliSense Local Cache
            - Keyboard Shortcut: `CTRL + SHIFT + R`
            - Menu Option: `Navigate to Edit > IntelliSense > Refresh Local Cache`
