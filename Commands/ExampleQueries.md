USE testDB2;
--Comment
/*
Mutiline comment
*/

CREATE TABLE Viewers(
Fullname Varchar(60),
Email Varchar(50),
Age Int,
TotalViews decimal Not Null,
)

SELECT * FROM Viewers

--Inserting values into all columns
INSERT INTO Viewers
VALUES('Shakeya', 'keya@gmail.com', 34, 114)

--Inserting multiple rows
INSERT INTO Viewers
VALUES('Tai', 'tia@gmail.com', 21, 14),
	  ('Lisa', 'lisa@gmail.com', 29, 56),
	  ('Reed', 'reed@gmail.com', 32, 98),
	  ('James', 'james@gmail.com', 37, 51),
	  ('Will', 'will@gmail.com', 22, 216)


--Selecting specific columns from a table
SELECT Fullname, Age
FROM Viewers


-- Selecting data with a condition using WHERE clause
SELECT * 
FROM Viewers
WHERE Age > 30

-- Selecting data with a WHERE clause with multiple conditions
SELECT * 
FROM Viewers
WHERE Age > 30
and Email = 'keya@gmail.com'


-- Updating a single column in a specific row
UPDATE Viewers
SET Age = 33
WHERE Fullname = 'Lisa';

--Updating multiple columns in a specific row
UPDATE Viewers
SET Age = 23, Email = 'willy@gmail.com'
WHERE Fullname = 'Will';

--Updating a column for all rows based on a condition
UPDATE Viewers
SET TotalViews = 223
WHERE Age < 30;

--Updating a column for all rows in a table (without a WHERE clause)
UPDATE Viewers
SET TotalViews = 24

--Delete all rows in the table
DELETE Viewers

--Delete all rows in the table
TRUNCATE TABLE Viewers

--Delete table
DROP TABLE Viewers

--Add New Column
ALTER TABLE Viewers
Add Country Varchar(50)

UPDATE Viewers
SET Country = 'Singapore'
WHERE Email = 'james@gmail.com'

SELECT * 
FROM Viewers