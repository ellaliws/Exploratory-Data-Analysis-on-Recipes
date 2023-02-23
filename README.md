# Exploratory-Data-Analysis-on-Recipes
a project for DSC 80 at UCSD
---
## Introduction
introduction to your dataset
Analysis Question: What is the relationship between the cooking time and average rating of recipes? Do recipes have higher ratings tend to take shorter time than the recipes of lower ratings? (Do recipes that take shorter time have higher ratings?)


Why should readers of your website care about the dataset and your question specifically?
Report the number of rows in the dataset, the names of the columns that are relevant to your question, and 

### descriptions of relevant columns:
`'name'` : Recipe name
`'id'`
`'rating'` 
`'minutes'`
| **Column**        | **Description**                         |
|:------------------|----------------------------------------:|
| `'name'`          | Recipe name                             |
| `'id'`            | Recipe ID                               |
| `'rating'`        | Average Rating of the recipe as floats  |
| `'minutes'`       | Minutes to prepare recipe as integers   |

---

## Cleaning and EDA
### Data Cleaning
#### Data Cleaning Steps: 
1.  In the getting the data part, we have two dataframes, `'recipes'` and `'interactions'`. Left merge them.
2.  In the merged dataset, fill all ratings of 0 with np.nan. This is **neccessary** because if a recipe is rated 0, a review that rates the recipe may entered the rating or may not. So it can be seen as a column containing missing values.
3.  Find the average rating of invidividual recipes and add this Series as `'rating'` column to recipes dataframe. We will use the average rating `'rating'` in the analysis part.
4. Originally, `'nutrition'` contains nutritions as a list of values. We create individual columns for every unique nutritions.

#### Cleaned Dataframe

|    | name                                 |     id |   minutes |   rating | rating > 3   |
|---:|:-------------------------------------|-------:|----------:|---------:|:-------------|
|  0 | 1 brownies in the world    best ever | 333281 |        40 |        4 | True         |
|  1 | 1 in canada chocolate chip cookies   | 453467 |        45 |        5 | True         |
|  2 | 412 broccoli casserole               | 306168 |        40 |        5 | True         |
|  3 | millionaire pound cake               | 286009 |       120 |        5 | True         |
|  4 | 2000 meatloaf                        | 475785 |        90 |        5 | True         |


### Univariate Analysis
plot
1-2 sentence explanation about your plot
### Bivariate Analysis
plot
<iframe src="assets/bivariate_plot.html" width=800 height=600 frameBorder=0></iframe>
</iframe>

1-2 sentence explanation about your plot(making sure to describe and interpret any trends present)


### Interesting Aggregates

## Assessment of Missingness
---
## Hypothesis Testing
null hypothesis:
alternative hypothesis: 
test statistic:
significance level
the resulting p-value:
your conclusion. 

**Justify** why these choices are good choices for answering the question you are trying to answer.

---
