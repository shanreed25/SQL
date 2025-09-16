# Recipes DB Design
**There is no single right answer to database design, but there are a lot of wrong answers. Database design is equal parts art and science. It requires having a deep understanding of the relationships between all the data you are trying to connect.**


# 1. Look at a recipe and pull out the relevant information and create tables based on the information
    ```
    Recipe Name: Vegan Pizza
    Recipe Description: The BEST vegan pizza made with a garlic-herb crust, simple tomato sauce, TONS of sauteed veggies, and vegan parmesan cheese. Thin crust, tons of flavor, and ridiculously satisfying
    Author: Lisa Brown
    Recipe Type: Entree
    Prep Time: 40 mins
    Cook Time: 20 mins
    Total Time: 1 hr
    Ingredients:
    Pizza:
    1/2 of one Trader Joe’s garlic-herb pizza crust
    1/2 cup each red, green, and orange bell pepper (loosely chopped)
    1/3 cup red onion (chopped)
    1 cup button mushrooms (chopped)
    1/2 tsp each dried or fresh basil, oregano, and garlic powder
    1/4 tsp sea salt

    SAUCE:
    1 15-ounce can tomato sauce* (organic when possible)
    1/2 tsp each dried or fresh basil, oregano, garlic powder, granulated sugar
    ~1/4 tsp sea salt (to taste)

    TOPPINGS:
    1/2 cup vegan parmesan cheese
    Red pepper flake + dried oregano
    ```
- Recipe Name
- Recipe Description
- Author
- Recipe Type
- Prep Time
- Cook Time
- Total Time
- Ingredients

## 2. Figure out what data can be used in multiple recipes and put them into different tables and which data is unique to each recipe
- Author
- Recipe Type
- Prep Time
- Cook Time
- Total Time
- Ingredients

### Author
- an author can have many recipies, so we do not need to duplicate the authors
- a recipe can have only one author
    - one-to-many relationship with the recipes table
- could create an authors table then include a foreign key, author_id, column in the recipes table, which links each recipe back to a specific author    
    #### author
    | Column Name             | Data Type     | Constraint  |
    | :---------------------- | :-----------: | ----------: |
    | author_id               | int           | PK          |
    | author_name             | string        | NOT NULL    |
    | author_email            | string        | NOT NULL    |

### Recipe Type
- a recipe type can belong to many recipes, so we do not need to duplicate the recipe types
- a recipe can have only one recipe type
    - one-to-many relationship with the recipes table
- could create a recipe_types table then include a foreign key, recipe_type_id, column in the recipes table, which links each recipe back to a specific recipe_type  
    #### recipe_types
    | Column Name             | Data Type     | Constraint  |
    | :---------------------- | :-----------: | ----------: |
    | recipe_type_id          | int           | PK          |
    | recipe_type_name        | string        | NOT NULL    |

### Cook, Prep and total Time
- store prep and cook times in the recipes table with dedicated columns for each time measurement
- total time will be calculated dynamically from the prep and cook times
    - when a user requests a recipe, your application can compute the total time and display it as needed
    - use an SQL query to compute the total time, saving storage space and ensuring the value is always up to date
    - the recommended approach for most applications

### Ingredients
- ingredients can be used in multiple recipes, so we do not need to duplicate all those values
- a recipe has many ingredients, an ingredient has many recipes
    - many-to-many relationship
- **Example:** 1/4 tsp sea salt
    - **ingredient:** sea salt: could have sea salt in another recipe in our database
    
    - **measurement unit:** tsp: could have different tsp amounts
    - could create three different tables then use and join table to connect it with the recipes

        #### ingredients
        | Column Name             | Data Type     | Constraint  |
        | :---------------------- | :-----------: | ----------: |
        | ingredient_id          | int           | PK          |
        | ingredient_name        | string        | NOT NULL    |

        #### measurement_units
        | Column Name             | Data Type     | Constraint  |
        | :---------------------- | :-----------: | ----------: |
        | measurement_unit_id     | int           | PK          |
        | measurement_unit_name   | string        | NOT NULL    |


- **measurement quantity:** 1/4: can be added to the join table


### Recipe Table
- recipe name and description will be different for each recipe, so we need to store both those values
- separate columns for prep and cook times, stored as integers representing minutes
- includes a foreign key column, author_id, which links each recipe back to a specific author
    - ensures that each recipe record in the Recipes table is tied to one and only one record in the authors table
- includes a foreign key column, recipe_type_id, which links each recipe back to a specific recipe type
    - ensures that each recipe record in the Recipes table is tied to one and only one record in the recipe_types table

        #### recipes
        | Column Name            | Data Type     |       Constraint        |
        | :--------------------- | :-----------: | ----------------------: |
        | recipe_id              | int           | PK                      |
        | recipe_name            | string        | NOT NULL                |
        | description            | string        | NOT NULL                |
        | prep_time_minutes      | int           | NOT NULL                |
        | cook_time_minutes      | int           | NOT NULL                |
        | author_id              | int           | FK ref authors table    |
        | recipe_type_id         | int           | FK ref recipe_type table|



## 3. Connect the joining tables
- The recipe table needs to be connected to the ingredients, measurement_units tables using a join table/associative table

### Recipe Ingredients Joining table
- this breaks the many-to-many relationship into two separate one-to-many relationships and also stores extra information, such as the quantity of each ingredient needed for a specific recipe

    #### recipe_ingredients
    | Column Name             | Data Type     | Constraint  |
    | :---------------------- | :-----------: | ----------: |
    | recipe_id               | int           | FK          |
    | ingredient_id           | int           | FK          |
    | quantity                | string        | NOT NULL    |
    | measurement_unit_id     | int           | FK          |

____________________________________________________
```
Instructions
Preheat oven to 425 degrees F (218 C) and position a rack in the middle of the oven.
Bring large skillet to medium heat. Once hot, add 1 Tbsp olive oil (amount as original recipe is written // adjust if altering batch size), onion and peppers. Season with salt, herbs and stir. Cook until soft and slightly charred – 10-15 minutes, adding the mushrooms in the last few minutes. Set aside.
Prepare sauce by adding tomato sauce to a mixing bowl and adding seasonings and salt to taste. Adjust seasonings as needed. Set aside. Note: If using tomato paste, add water to thin until desired consistency is reached.
Prepare vegan parmesan if you haven’t already by blitzing raw cashews, sea salt, nutritional yeast and garlic powder in a food processor until a fine meal is reached. Transfer to jar and refrigerate to keep fresh.

Roll out dough onto a floured surface and transfer to a parchment-lined round baking sheet. You’re going to add the pizza WITH the parchment directly to the oven to properly crisp the crust, so any round object will do as it’s not actually going into the oven (I use a wood board).
Top with desired amount of tomato sauce (you’ll have leftovers, which you can store in a jar for later use), a sprinkle of parmesan cheese and the sautéed veggies.
Use the baking sheet to gently slide the pizza (WITH the parchment underneath) directly onto the oven rack. The parchment will help prevent it from falling through.
Bake for 17-20 minutes or until crisp and golden brown.
Serve with remaining parmesan cheese, dried oregano and red pepper flake. Leftovers keep well – no need to reheat! Cold pizza is yum.
```