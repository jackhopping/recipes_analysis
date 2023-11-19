# Recipe Reviews: Data Analysis Project

## Introduction

The dataset for this projest is sourced from food.com, and consists of two files. One file contains recipe information, and the other contains ratings submitted by food.com users who cooked the recipes.

The recipes dataframe contains data including recipe names, recipe IDs, preparation time, the submission data of the recipe, food.com tags, and nutritional value. The dataframe has a shape of (83782, 12), meaning that there are 83,782 recipes and each recipe has 12 data categories.

The reviews dataframe contains data including user IDs, recipe IDs, the rating given by the user, and text included as part of the review. The dataframe has a shape of (731927, 5), meaning that there are 731927 reviews and each review has 5 data categories.

My analysis aims to answer the question: What is the relationship between the number of steps in a recipe and the average rating? Throughout this analysis I will clean the data and perform exploratory data analysis, assess the missingness of data in the food.com datasets, and perform a hypothesis to determine the relationship between the number of steps in a recipe and the average rating.

## Cleaning and EDA (Exploratory Data Analysis)

My first step in cleaning the data was to merge the recipe and review datasets on the recipe id column. This merge gave me a dataframe with shape (234429, 17).

Next, I filled all ratings of 0 with np.nan. The reason why I did this is because food.com does not allow reviews of 0 - therefore, if a review has a value of 0 in the dataset, the value must be missing. Replacing values of 0 with np.nan allows me to analyze the missingness of reviews more easily.

My next step was to find the average rating per recipe, stored in a Series, and to merge the Series into the dataframe. Since my main question in this analysis revolves around the average rating for each recipe, I wanted to have this readily available.

After finding the average rating per recipe, I wanted to double check the data types of each column to make sure that they were cast as I expected. These were the inital column data types:

```yml
[('name', str),
 ('id', numpy.int64),
 ('minutes', numpy.int64),
 ('contributor_id', numpy.int64),
 ('submitted', str),
 ('tags', str),
 ('nutrition', str),
 ('n_steps', numpy.int64),
 ('steps', str),
 ('description', str),
 ('ingredients', str),
 ('n_ingredients', numpy.int64),
 ('user_id', numpy.float64),
 ('recipe_id', numpy.float64),
 ('date', str),
 ('rating', numpy.float64),
 ('review', str),
 ('avg recipe rating', numpy.float64)]
```

I notice that the "tags", "nutrition", "steps", and "ingredients" columns are all type str. I wanted them to be in the form of lists, so I cleaned them. The cleaned column data types are below:

```yml
[('name', str),
 ('id', numpy.int64),
 ('minutes', numpy.int64),
 ('contributor_id', numpy.int64),
 ('submitted', str),
 ('tags', list),
 ('nutrition', list),
 ('n_steps', numpy.int64),
 ('steps', list),
 ('description', str),
 ('ingredients', list),
 ('n_ingredients', numpy.int64),
 ('user_id', numpy.float64),
 ('recipe_id', numpy.float64),
 ('date', str),
 ('rating', numpy.float64),
 ('review', str),
 ('avg recipe rating', numpy.float64)]
```

My last step in data cleaning was to get rid of columns that not necessary for my analysis. The columns that I dropped from the dataset were: `"contributor_id"`, `"submitted"`, `"date"`, `"nutrition"`, `"tags"`, `"name"`, `"user_id"`, `"recipe_id"`, `"description"`, and `"steps"`.

Now that my data had been cleaned, this is the dataframe I had:

|     id |   minutes |   n_steps | ingredients                                                                                                                                                                                              |   n_ingredients |   rating | review                                                                                                                                                                                                                                                                                                                                           |   avg recipe rating |
|-------:|----------:|----------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|---------:|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------:|
| 333281 |        40 |        10 | ["'bittersweet chocolate'", " 'unsalted butter'", " 'eggs'", " 'granulated sugar'", " 'unsweetened cocoa powder'", " 'vanilla extract'", " 'brewed espresso'", " 'kosher salt'", " 'all-purpose flour'"] |               9 |        4 | These were pretty good, but took forever to bake.  I would send it ended up being almost an hour!  Even then, the brownies stuck to the foil, and were on the overly moist side and not easy to cut.  They did taste quite rich, though!  Made for My 3 Chefs.                                                                                   |                   4 |
| 453467 |        45 |        12 | ["'white sugar'", " 'brown sugar'", " 'salt'", " 'margarine'", " 'eggs'", " 'vanilla'", " 'water'", " 'all-purpose flour'", " 'whole wheat flour'", " 'baking soda'", " 'chocolate chips'"]              |              11 |        5 | Originally I was gonna cut the recipe in half (just the 2 of us here), but then we had a park-wide yard sale, & I made the whole batch & used them as enticements for potential buyers ~ what the hey, a free cookie as delicious as these are, definitely works its magic! Will be making these again, for sure! Thanks for posting the recipe! |                   5 |
| 306168 |        40 |         6 | ["'frozen broccoli cuts'", " 'cream of chicken soup'", " 'sharp cheddar cheese'", " 'garlic powder'", " 'ground black pepper'", " 'salt'", " 'milk'", " 'soy sauce'", " 'french-fried onions'"]          |               9 |        5 | This was one of the best broccoli casseroles that I have ever made.  I made my own chicken soup for this recipe. I was a bit worried about the tsp of soy sauce but it gave the casserole the best flavor. YUM!                                                                                                                                  |                   5 |
|        |           |           |                                                                                                                                                                                                          |                 |          | The photos you took (shapeweaver) inspired me to make this recipe and it actually does look just like them when it comes out of the oven.                                                                                                                                                                                                        |                     |
|        |           |           |                                                                                                                                                                                                          |                 |          | Thanks so much for sharing your recipe shapeweaver. It was wonderful!  Going into my family's favorite Zaar cookbook :)                                                                                                                                                                                                                          |                     |
| 306168 |        40 |         6 | ["'frozen broccoli cuts'", " 'cream of chicken soup'", " 'sharp cheddar cheese'", " 'garlic powder'", " 'ground black pepper'", " 'salt'", " 'milk'", " 'soy sauce'", " 'french-fried onions'"]          |               9 |        5 | I made this for my son's first birthday party this weekend. Our guests INHALED it! Everyone kept saying how delicious it was. I was I could have gotten to try it.                                                                                                                                                                               |                   5 |
| 306168 |        40 |         6 | ["'frozen broccoli cuts'", " 'cream of chicken soup'", " 'sharp cheddar cheese'", " 'garlic powder'", " 'ground black pepper'", " 'salt'", " 'milk'", " 'soy sauce'", " 'french-fried onions'"]          |               9 |        5 | Loved this.  Be sure to completely thaw the broccoli.  I didn&#039;t and it didn&#039;t get done in time specified.  Just cooked it a little longer though and it was perfect.  Thanks Chef.                                                                                                                                                     |                   5 |

Note that the text in the 3rd row of the `review` column is quite long, and therefore takes up space in 3 rows.

### Univariate Analysis

The plot embedded below shows the distribution of `n_steps`, the number of steps in each recipe that was reviewed.

<iframe src="recipes_analysis/assets/n_steps_dist.html" width=800 height=600 frameBorder=0></iframe>

The plot shows that the distribution of `n_steps` is skewed right. The graph is centered around 7, and most of the values are between 3 and 12.

### Bivariate Analysis

The plot embedded below shows the relationship between `

## Assessment of Missingness

## Hypothesis Testing
