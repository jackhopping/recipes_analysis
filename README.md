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

After finding the average rating per recipe, I wanted to double check the data types of each column to make sure that they were cast as I expected.

'''yml
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
'''

## Assessment of Missingness

## Hypothesis Testing
