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
| Column            | Description                             |
|:------------------|----------------------------------------:|
| `'name'`          | Recipe name                             |
| `'id'`            | Recipe ID                               |
| `'rating'`        | Average Rating of the recipe as floats  |
| `'minutes'`       | Minutes to prepare recipe as integers   |


| Syntax | Description |
| ----------- | ----------- |
| `'name'` | Recipe name |
---

## Cleaning and EDA
### Data Cleaning
#### Data Cleaning Steps: 
1.  In the getting the data part, we have two dataframes, `'recipes'` and `'interactions'`. Left merge them.
2.  In the merged dataset, fill all ratings of 0 with np.nan. This is **neccessary** because if a recipe is rated 0, a review that rates the recipe may entered the rating or may not. So it can be seen as a column containing missing values.
3.  Find the average rating of invidividual recipes and add this Series as `'rating'` column to recipes dataframe. We will use the average rating `'rating'` in the analysis part.
4.  Originally, `'nutrition'` contains nutritions as a list of values. We create individual columns for every unique nutritions.
5.  We create the column `'rating > 3'`, which stores boolean values to indicate whether the rating is greater than 3. If rating is greater than 3, we define it as a high-rating recipe, otherwise a low-rating recipe. This information will be used in our analysis. 
6. For our Bivariate Analysis, we want to know whether a recipe's calories is high or low. We define a recipe that has at least 400 calores to be a high-calorie recipe. Therefore, we create a column high_calories, which stores boolean values to indicate whether the recipe is a high-calorie recipe or not.

#### Cleaned Dataframe

|    | name                                 |     id |   minutes |   rating | rating > 3   |   calories (#) | high_calories   |
|---:|:-------------------------------------|-------:|----------:|---------:|:-------------|---------------:|:----------------|
|  0 | 1 brownies in the world    best ever | 333281 |        40 |        4 | True         |          138.4 | False           |
|  1 | 1 in canada chocolate chip cookies   | 453467 |        45 |        5 | True         |          595.1 | True            |
|  2 | 412 broccoli casserole               | 306168 |        40 |        5 | True         |          194.8 | False           |
|  3 | millionaire pound cake               | 286009 |       120 |        5 | True         |          878.3 | True            |
|  4 | 2000 meatloaf                        | 475785 |        90 |        5 | True         |          267   | False           |

### Univariate Analysis
plot
1-2 sentence explanation about your plot
### Bivariate Analysis
plot
<iframe src="assets/bivariate_plot.html" width=600 height=400 frameBorder=0></iframe>

**explanation**
The distributions of minutes between high_rating recipes and low_rating recipes are similar. In other words, no matter the recipe is rated high or low, they have similar trend that most recipes take under 60 minutes, and there are fewer recipes that take longer time. There is no obvious differences between high and low ratings of a recipe by looking at how long it takes.

(1-2 sentence explanation about your plot(making sure to describe and interpret any trends present)

### Interesting Aggregates


## Assessment of Missingness
### NMAR Analysis
`'rating'` column is NMAR
Explain your reasoning and any additional data you might want to obtain that could explain the missingness (thereby making it MAR).

### Missingness Dependency
K-S statistic
<iframe src="assets/ms_depend_plot.html" width=600 height=400 frameBorder=0></iframe>
### 
---
## Hypothesis Testing
#### **Null Hypothesis**: 
#### **Alternative Hypothesis**: 
#### **Test Statistic**:
#### **Significance level**: 
0.01(1%)
#### **the resulting p-value**:
#### Conclusion: 

**Justify** why these choices are good choices for answering the question you are trying to answer.

---
