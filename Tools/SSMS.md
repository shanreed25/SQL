# SQL Server Management Studio (SSMS)
### SSMS(SQL Server Management Studio)
-  editor that will allow you to write queries
- https://learn.microsoft.com/en-us/ssms/install/install



### Bring Data Manually(CSV)
**Instead of using a query to create the table**
1. Right click database
    - Tasks --> Import Flat Data --> Next
    - Click Browse and choose file --> Next --> Next
### Errors
- red squiggly lines under table names and columns typically indicate that IntelliSense is not recognizing these objects. This often occurs even when the objects genuinely exist and your SQL code is correct.
    - IntelliSense local cache is not up to date
    - can happen after: Creating new tables or views, Adding new columns to existing tables, and Modifying database objects
    - refreshing the cache forces IntelliSense to re-scan the database metadata and update its understanding of the available objects, which should eliminate the red squiggly lines if the objects are valid
        - Refresh the IntelliSense Local Cache
            - Keyboard Shortcut: `CTRL + SHIFT + R`
            - Menu Option: `Navigate to Edit > IntelliSense > Refresh Local Cache`
