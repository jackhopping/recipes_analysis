# Recipe Reviews: Data Analysis Project

## Introduction

The dataset for this projest is sourced from food.com, and consists of two files. One file contains recipe information, and the other contains ratings submitted by food.com users who cooked the recipes.

The recipes dataframe contains data including recipe names, IDs, preparation time, the submission data of the recipe, food.com tags, nutritional value. The dataframe has a shape of (83782, 12), meaning that there are 83,782 recipes and each recipe has 12 data categories.

The reviews dataframe contains data including user IDs, recipe IDs, the rating given by the user, and text included as part of the review. The dataframe has a shape of (731927, 5), meaning that there are 731927 reviews and each review has 5 data categories.

My analysis aims to answer the question: What is the relationship between the number of steps in a recipe and the average rating? Throughout this analysis I will clean the data and perform exploratory data analysis, assess the missingness of data in the food.com datasets, and perform a hypothesis to determine the relationship between the number of steps in a recipe and the average rating.
