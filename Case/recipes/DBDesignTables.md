# Vegan Recipes tables

### recipe_types
| Column Name             | Data Type     | Constraint  |
| :---------------------- | :-----------: | ----------: |
| recipe_type_id          | int           | PK          |
| recipe_type_name        | string        | NOT NULL    |

```
CREATE TABLE recipe_types(
recipe_type_id INT IDENTITY(1,1) PRIMARY KEY,
recipe_type_name VARCHAR(255) NOT NULL,
)
```

### author
| Column Name             | Data Type     | Constraint  |
| :---------------------- | :-----------: | ----------: |
| author_id               | int           | PK          |
| author_name             | string        | NOT NULL    |
| author_email            | string        | NOT NULL    |

```
CREATE TABLE authors(
author_id INT IDENTITY(1,1) PRIMARY KEY,
author_name VARCHAR(255) NOT NULL,
author_email VARCHAR(255) NOT NULL,
)
```


### recipes
| Column Name            | Data Type     |       Constraint        |
| :--------------------- | :-----------: | ----------------------: |
| recipe_id              | int           | PK                      |
| recipe_name            | string        | NOT NULL                |
| description            | string        | NOT NULL                |
| prep_time_minutes      | int           | NOT NULL                |
| cook_time_minutes      | int           | NOT NULL                |
| author_id              | int           | FK ref authors table    |
| recipe_type_id         | int           | FK ref recipe_type table|

```
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
```


### ingredients
| Column Name             | Data Type     | Constraint  |
| :---------------------- | :-----------: | ----------: |
| ingredient_id           | int           | PK          |
| ingredient_name         | string        | NOT NULL    |

```
CREATE TABLE ingredients(
ingredient_id INT IDENTITY(1,1) PRIMARY KEY,
ingredient_name VARCHAR(255) NOT NULL,
)
```


### measurement_units
| Column Name             | Data Type     | Constraint  |
| :---------------------- | :-----------: | ----------: |
| measurement_unit_id     | int           | PK          |
| measurement_unit_name   | string        | NOT NULL    |

```
CREATE TABLE measurement_qty(
qty_id INT IDENTITY(1,1) PRIMARY KEY,
qty_amount VARCHAR(255) NOT NULL,
)
```

## Join Table

### recipe_ingredients
| Column Name               | Data Type     | Constraint  |
| :------------------------ | :-----------: | ----------: |
| recipe_id, ingredient_id  | int           | CPK         |
| recipe_id                 | int           | FK          |
| ingredient_id             | int           | FK          |
| quantity                  | string        | NOT NULL    |
| measurement_unit_id       | int           | FK          |

```
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
```

