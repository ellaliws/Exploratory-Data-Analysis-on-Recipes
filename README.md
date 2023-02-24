# Exploratory-Data-Analysis-on-Recipes
a project for DSC 80 at UCSD
---
## Introduction
introduction to your dataset
Analysis Question: Is there a relationship between the preparing time and average rating of recipes?

Why should readers of your website care about the dataset and your question specifically?

### Dataset Information
We have 83782 **rows** in the dataset, and the relevant columns are 
`'name'` : Recipe name
`'id'`: Recipe ID
`'rating'` : Average Rating of the recipe as floats
`'minutes'` : Minutes to prepare recipe as integers

---

## Cleaning and EDA
### Data Cleaning
#### Data Cleaning Steps: 
1.  In the getting the data part, we have two dataframes, `'recipes'` and `'interactions'`. Left merge them.
2.  In the merged dataset, fill all ratings of 0 with np.nan. This is **neccessary** because if a recipe is rated 0, it means a reviewer did not enter the rating. So it can be seen as a column containing missing values.
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
#### Plots of Distributions: 
we care about the distribution of rating and minutes to answer our analysis question. So we plot these two distributions.
<iframe src="assets/rating_plot.html" width=700 height=400 frameBorder=0></iframe>
**Explanation:** The average of mean rating for all recipes is 4.63, the distribution is left skewed, majority of the ratings are positive. 

<iframe src="assets/plot_min.html" width=700 height=400 frameBorder=0></iframe>
**Explanation:** mean after removing outlier is 38.68, the distribution is right skewed, majority of recipes take less than one hour to prepare

### Bivariate Analysis
plot
<iframe src="assets/bivariate_plot.html" width=700 height=400 frameBorder=0></iframe>

**explanation**
The distributions of minutes between high_rating recipes and low_rating recipes are similar. In other words, no matter the recipe is rated high or low, they have similar trend that most recipes take under 60 minutes, and there are fewer recipes that take longer time. There is no obvious differences between high and low ratings of a recipe by looking at how long it takes.


### Interesting Aggregates
#### Pivot Table
|   rating |   ('mean', 'minutes') |   ('count', 'minutes') |
|---------:|----------------------:|-----------------------:|
|        1 |               95.7864 |                    590 |
|        2 |               98.6    |                    775 |
|        3 |               96.3054 |                   2760 |
|        4 |              106.359  |                  20924 |
|        5 |              114.329  |                  56124 |

**Explanation:**
The pivot table shows that it does seem like there is a trend where the higher ratings (4 and 5) takes longer time to prepare.

## Assessment of Missingness
### NMAR Analysis
We believe the `'rating'` column is not missing at random(NMAR), the chance that a value is missing depends on the actual missing value. For example, the user is less likely to fill in a 3 when they feel neutral towards the recipe, compared to 5 and 1 when they are extremely satified or dissatisfied.

any additional data you might want to obtain that could explain the missingness (thereby making it MAR).

### Missingness Dependency
#### Comparing null and non-null `'description'` distributions for `'n_ingredients'`
We use **K-S statistic** to identify missingness of `'description'` 
#### Results of Missingness Permutation Tests
```py
ks_2samp(recipes_df.loc[recipes_df['description missing'] == True, 'n_steps'], recipes_df.loc[recipes_df['description missing'] == False, 'n_ingredients'])
```
#### Plot: 
<iframe src="assets/ks_fig.html" width=700 height=400 frameBorder=0></iframe>
<iframe src="assets/ms_depend_plot.html" width=700 height=400 frameBorder=0></iframe>
 
---
## Hypothesis Testing
#### **Null Hypothesis**: 
The distribution for high rating recipes's minutes to prepare and low rating recipes's minutes are the same.

#### **Alternative Hypothesis**: 
The distribution for high rating recipes's minutes to prepare and low rating recipes's minutes are not the same.

#### **Test Statistic**:
#### **Significance level**: 
0.01(1%)
#### **the resulting p-value**: 
6.5 * 10^-27
#### Conclusion: 
p value is less than the threshold of 0.05 therefore we reject the null. There is likely a relationship between recipes's rating and recipes.

**Justify** why these choices are good choices for answering the question you are trying to answer.


---
