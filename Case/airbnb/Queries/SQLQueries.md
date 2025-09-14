Create Database Airbnbcasestudy

USE Airbnbcasestudy

--Creating a table
CREATE TABLE airbnb_listings (
   id NUMERIC(20, 0),
    name VARCHAR(255),
    host_id INT,
    host_name VARCHAR(255),
    neighbourhood_group VARCHAR(255),
    neighbourhood VARCHAR(255),
    latitude DECIMAL(12, 8),
    longitude DECIMAL(12, 8),
    room_type VARCHAR(255),
    price DECIMAL(8, 2),
    minimum_nights INT,
    number_of_reviews INT,
    last_review DATE,
    reviews_per_month DECIMAL(10, 2),
    calculated_host_listings_count INT,
    availability_365 INT,
    number_of_reviews_ltm INT,
    license VARCHAR(255)
);

--Querying the data 
SELECT *  FROM airbnb_listings
DROP TABLE airbnb_listings


--Importing the Data
BULK INSERT airbnb_listings
FROM 'C:\Getting Started with SQL Course\listings.csv'
WITH (
    FIELDTERMINATOR = ',',  -- Specify the delimiter (comma)
    ROWTERMINATOR = '\n',   -- Specify the row terminator (newline)
    FIRSTROW = 2,           -- Skip the header row (starts importing from row 2)
    FORMAT = 'CSV'          -- Specify that the input file is in CSV format
);

---creating pricing table
CREATE TABLE airbnb_pricing (
    listing_id INT,
    date DATE,
    available VARCHAR(10),
    price DECIMAL(10, 2),
    adjusted_price DECIMAL(10, 2),
    minimum_nights INT,
    maximum_nights INT,
    PRIMARY KEY (listing_id, date)
);

BULK INSERT airbnb_pricing
FROM 'C:\Getting Started with SQL Course\pricing.csv'
WITH (
    FIELDTERMINATOR = ',',  -- Specify the delimiter
    ROWTERMINATOR = '\n',   -- Specify the row terminator
    FIRSTROW = 2,           -- Skip the header row (starts importing from row 2)
    FORMAT = 'CSV'          -- Specify that the input file is in CSV format
);

SELECT * FROM airbnb_pricing


--Creating Reviews table
CREATE TABLE airbnb_reviews (
    listing_id BIGINT,
    id BIGINT,
    date DATE,
    reviewer_id INT,
    reviewer_name VARCHAR(255),
    comments TEXT
);

SELECT * FROM airbnb_reviews

BULK INSERT airbnb_reviews
FROM 'C:\Getting Started with SQL Course\reviews.csv'
WITH (
    FIELDTERMINATOR = ',',  -- Specify the delimiter (comma)
    ROWTERMINATOR = '\n',   -- Specify the row terminator (newline)
    FIRSTROW = 2,           -- Skip the header row (starts importing from row 2)
    FORMAT = 'CSV'          -- Specify that the input file is in CSV format
);


# GREATER THAN
--Find Listing name, neighbourhood, and price with a price greater than $500
SELECT name, neighbourhood, price
FROM airbnb_listings
WHERE price > 500

# NOT EQUAL TO
--Find listings that are not in the Queen Anne neighbourhood
SELECT name, neighbourhood, price
FROM airbnb_listings
WHERE neighbourhood <> 'Queen Anne'

# EQUAL TO
--Find listings that are in the Wallingford neighbourhood
SELECT name, neighbourhood, price
FROM airbnb_listings
WHERE neighbourhood = 'Wallingford'

# GREATER THAN OR EQUAL TO
--Find Listings that have a minimum stay of more than 30 days and were last reviewed after 1/1/2016
SELECT name, minimum_nights, last_review
FROM airbnb_listings
WHERE minimum_nights > 30
AND  last_review >= '2015-1-1'


# CONCAT
--Combine the name and neighbourhood columns into a single string(use dash(-) as the delimiter)
SELECT CONCAT(name, ' - ', neighbourhood) AS address
FROM airbnb_listings


# SUBSTRING
--Extract the first 10 characters from the name
SELECT SUBSTRING(name, 1, 10) As short_name
FROM airbnb_listings

# LENGTH
--Find the length of each reviewer's name in the airbnb_reviews table
SELECT reviewer_name, LEN(reviewer_name) AS name_length
FROM airbnb_reviews

# UPPER
--Convert all reviewers name to uppercase
SELECT UPPER(reviewer_name) AS upper_name
FROM airbnb_reviews

# REPLACE
--Repalce all occurrences of 'APT' with 'Unit' in the room_type_column
SELECT name, REPLACE(room_type, 'apt', 'unit')
FROM airbnb_listings

--AGGREGATIONS----------------------------------------------------------------------------------

# COUNT
--Count how many airbnb listings there are in the table Seattle(counts duplicates)
SELECT COUNT(*) AS listing_count
FROM airbnb_listings

# DISTINCT
--Count how many airbnb listings there are in Seattle(no duplicates)
SELECT COUNT(DISTINCT id) AS listing_count
FROM airbnb_listings

--Return a list of neighborhoods(no duplicates)
SELECT DISTINCT neighbourhood 
FROM airbnb_listings


# AVERAGE
--Get the average price of listings in different neighborhoods
SELECT neighbourhood, AVG(price) AS average_price
FROM airbnb_listings
GROUP BY neighbourhood


# ROUND
--Get the average price of listings in different neighborhoods and round to two decimal places
SELECT neighbourhood, ROUND(AVG(price), 2) AS average_price
FROM airbnb_listings
GROUP BY neighbourhood


# CAST
--Get the average price of listings in different neighborhoods, round to two decimal places and remove trailing zeros
--to remove trailing zeros, cast to a data type that does not preserve them, such as FLOAT or VARCHAR
SELECT neighbourhood, CAST(ROUND(AVG(price), 2) AS FLOAT) AS average_price
FROM airbnb_listings
GROUP BY neighbourhood

--OR----------------------------------
SELECT neighbourhood, CAST(ROUND(AVG(price), 2) AS DECIMAL(10, 2)) AS average_price
FROM airbnb_listings
GROUP BY neighbourhood


# MAX and MIN
--Find the highest and lowest prices among all listings
SELECT MAX(price) AS max_price, MIN(price) AS min_price
FROM airbnb_listings


--Find the highest and lowest prices for each neighbourhood
SELECT neighbourhood, MAX(price) AS max_price, MIN(price) AS min_price
FROM airbnb_listings
GROUP BY neighbourhood


--Find the highest and lowest prices for each neighbourhood, and order by min_price
SELECT neighbourhood, MAX(price) AS max_price, MIN(price) AS min_price
FROM airbnb_listings
GROUP BY neighbourhood
ORDER BY min_price

# SUM
--Find the total revenue generated by all listings
SELECT SUM(price) AS total_revenue
FROM airbnb_listings

# WILDCARDS

## PERCENT(%)
--Find all listings where name has the word 'private' in it
SELECT * 
FROM airbnb_listings
WHERE name LIKE '%private%'


--Find all listings where name ends with 'private' 
SELECT * 
FROM airbnb_listings
WHERE name LIKE '%private'

--Find all listings where name starts with 'quiet'
SELECT * 
FROM airbnb_listings
WHERE name LIKE 'quiet%'

--Find all reviews where the reviewer_name starts with 'Chris' in it
SELECT listing_id, reviewer_name
FROM airbnb_reviews
WHERE reviewer_name LIKE '%Chris%'

--Find reviewers who used the word recommend in their comments
SELECT reviewer_id, reviewer_name, comments
FROM airbnb_reviews
WHERE comments LIKE '%recommend%'


--Find listings with a room_type that starts with 'entire' or neighborhood that contains 'hill'
SELECT name, room_type, neighbourhood
FROM airbnb_listings
WHERE room_type LIKE '%entire%'
OR neighbourhood LIKE '%hill%'

## UNDERSCORE(_)
--Find all reviews where comment only like 'Amazing' 'Bmazing' 'Cmazing' etc
SELECT * 
FROM airbnb_reviews
WHERE comments LIKE '_mazing'


--Find all listings where date is the month of November
SELECT * 
FROM airbnb_reviews
WHERE date LIKE '____-11-__'

--Select All

SELECT *  FROM airbnb_listings

SELECT * FROM airbnb_pricing

SELECT * FROM airbnb_reviews
