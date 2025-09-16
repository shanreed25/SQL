--1. Create Database
Create Database VeganRecipes

USE VeganRecipes
--2. Define the primary tables
--authors
CREATE TABLE authors(
author_id INT IDENTITY(1,1) PRIMARY KEY,
author_name VARCHAR(255) NOT NULL,
author_email VARCHAR(255) NOT NULL,
)

INSERT INTO authors
VALUES
    ('Lea Blackburn', 'leab@email.com'),
    ('Tori Arche', 'toria@email.com'),
    ('Eddie Grimes', 'eddieg@email.com'),
    ('Ian Ingram', 'iani@email.com'),
    ('Clay Macias', 'claym@email.com'),
    ('Isabella Ward', 'isabellaw@email.com'),
    ('Anne Hayden', 'anneh@email.com'),
    ('Claire Tanner', 'clairet@email.com'),
    ('Eleanor Lynn', 'eleanorl@email.com'),
    ('Julie McGee', 'juliem@email.com');

--recipe_types
CREATE TABLE recipe_types(
recipe_type_id INT IDENTITY(1,1) PRIMARY KEY,
recipe_type_name VARCHAR(255) NOT NULL,
)

INSERT INTO recipe_types
VALUES
    ('Appetizers'),
    ('Breakfast'),
    ('Soup'),
    ('Stew'),
    ('Salad'),
    ('Side Dish'),
    ('Entree'),
    ('Snack'),
    ('Brunch'),
    ('Dessert');


--recipes
--recipe_id:  is an integer, automatically increments starting from 1, and is the primary key
CREATE TABLE recipes(
recipe_id INT IDENTITY(1,1) PRIMARY KEY,
recipe_name VARCHAR(255) NOT NULL,
recipe_description VARCHAR(255) NOT NULL,
prep_time INT NOT NULL,
cook_time INT NOT NULL,
author_id INT,
FOREIGN KEY (author_id) REFERENCES authors(author_id),
recipe_type_id INT,
FOREIGN KEY (recipe_type_id) REFERENCES recipe_types(recipe_type_id)
)



SELECT * FROM recipes
SELECT * FROM recipe_types
SELECT * FROM authors

INSERT INTO recipes
VALUES
    ('Lentil Shepherd''s Pie', 
    'This savory and comforting twist on a classic shepherd''s pie features a rich and hearty lentil and vegetable filling topped with a fluffy potato mash. It''s an excellent, warming meal for a weeknight dinner.',
    30,
    60,
    5,
    7
    ),
    ('Black Bean Burgers',
    'Made with pantry staples like black beans and oats, this recipe produces flavorful and sturdy patties. They can be cooked on a skillet or grilled and served on buns with your favorite toppings.',
    15,
    20,
    8,
    7
    ),
    ('BBQ Jackfruit Pulled "Pork" Sandwiches',
    'Shredded jackfruit simmered in a sweet and smoky barbecue sauce creates a vegan-friendly version of a pulled "pork" sandwich. It''s a quick, easy, and tangy meal to serve on toasted buns',
    10,
    30,
    1,
    7
    ),
    ('Chickpea Curry',
    'A one-pan, 30-minute dish featuring chickpeas and vegetables swimming in a creamy coconut milk sauce. This versatile and nutritious curry is perfect for a quick weekday dinner and pairs well with rice or naan',
    15,
    25,
    4,
    7
    ),
    ('Cauliflower Buffalo Wings',
    'A delicious, plant-based version of buffalo wings. Cauliflower florets are coated in a batter, baked until crispy, and then tossed in a spicy buffalo sauce',
    20,
    40,
    8,
    1
    ),
    ('Mac and Cheese',
    'Enjoy a creamy, cheesy, and quick mac and cheese without any dairy. The sauce is often made from a blend of vegetables like potatoes and carrots or with a mix of vegan cheeses and spices. This recipe can be made entirely on the stovetop or baked for a crispy finish.',
    25,
    30,
    4,
    6
    ),
    ('Chocolate Avocado Mousse',
    'For a rich, decadent, and healthy dessert, this mousse uses ripe avocados for a creamy texture combined with cocoa powder and a natural sweetener like maple syrup. The best part? No baking required.',
    10,
    0,
    8,
    10
    ),
    ('Roasted Butternut Squash Soup',
    'Made with roasted butternut squash, this soup has a deep, rich flavor from the roasting process. The creamy texture is achieved by blending the roasted squash with aromatic seasonings like sage and rosemary. ',
    10,
    45,
    3,
    3
    ),
    ('Minestrone Soup',
    'This hearty Italian-style vegetable soup is packed with a mix of vegetables, beans, and pasta. It''s a colorful and nutritious meal, perfect for a cozy dinner.',
    15,
    25,
    10,
    3
    ),
    ('Smoothie Bowl',
    'A thick, delicious, and nutrient-dense smoothie served in a bowl and topped with fresh fruit, granola, seeds, or nuts. It''s ready in just five minutes and easily customized.',
    5,
    5,
    2,
    2
    );
--Error: String or binary data would be truncated...
--Cause: attempting to insert or update the recipe_description column with a string that is longer than the column's maximum length
-- change recipe_description VARCHAR(255) NOT NULL, to recipe_description VARCHAR(MAX);

--ALTER TABLE recipes table
ALTER TABLE recipes
ALTER COLUMN recipe_description VARCHAR(MAX);


--DROP TABLE recipes

CREATE TABLE ingredients(
ingredient_id INT IDENTITY(1,1) PRIMARY KEY,
ingredient_name VARCHAR(255) NOT NULL,
)

CREATE TABLE measurement_units(
measurement_unit_id INT IDENTITY(1,1) PRIMARY KEY,
measurement_unit_name VARCHAR(255) NOT NULL,
)

--3. Create the associative tables
CREATE TABLE recipe_ingredient (
    recipe_id INT,
    ingredient_id INT,
    measurement_unit_id INT,
    quantity VARCHAR(255),
    PRIMARY KEY (recipe_id, ingredient_id), -- Composite primary key
    FOREIGN KEY (recipe_id) REFERENCES recipes(recipe_id),
    FOREIGN KEY (ingredient_id) REFERENCES ingredients(ingredient_id),
    FOREIGN KEY (measurement_unit_id) REFERENCES measurement_units(measurement_unit_id)
);

