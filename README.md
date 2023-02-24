# Data Analysis on Recipes Rating and Preparation Time
A project for DSC 80 at UCSD. Some good advice to pick a good recipe💓

---
## Introduction
**Analysis Question:** Is there a relationship between the preparing time and average rating of recipes?
**Why is this important:** By analyzing this dataset, we will identify whether the preparing time and average rating of recipes are related. If there is a relationship, we can help readers filter out the recipes that are more likely to be bad by looking at its preperation time.


### Dataset Information
We have 83782 **rows** in the dataset, and the relevant columns are 
- `'name'` : Recipe name
- `'id'`: Recipe ID
- `'minutes'` : Minutes to prepare recipe as integers
- `'nutrition'` : Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value”
- `'description'` : User-provided description
- `'n_ingredients'` : number of ingredients in the recipe
- `'rating'` : Average Rating of the recipe as floats

---

## Cleaning and EDA
### Data Cleaning
#### Data Cleaning Steps: 
1.  In the getting the data part, we have two dataframes, `'recipes'` and `'interactions'`. Left merge them.
2.  In the merged dataset, fill all ratings of 0 with np.nan. This is **neccessary** because if a recipe is rated 0, it means a reviewer did not enter the rating. So it can be seen as a column containing missing values.
3.  Find the average rating of invidividual recipes and add this Series as `'rating'` column to recipes dataframe. We will use the average rating `'rating'` in the analysis part.
4.  Originally, `'nutrition'` contains nutritions as a list of values. We create individual columns for every unique nutritions.
5.  We create the column `'rating > 3'`, which stores boolean values to indicate whether the rating is greater than 3. If rating is greater than 3, we define it as a high-rating recipe, otherwise a low-rating recipe. This information will be used in our analysis. 
6.  We create the column `'description missing'`, which stores boolean values to indicate whether the description is missing. This information will be used in our missingness analysis.
7. For our Bivariate Analysis, we want to know whether a recipe's calories is high or low. We define a recipe that has at least 400 calores to be a high-calorie recipe. Therefore, we create a column high_calories, which stores boolean values to indicate whether the recipe is a high-calorie recipe or not.

#### Cleaned Dataframe
**Note**: this dataframe shows only relevant columns in the cleaned dataframe instead of the whole dataframe

---

|    | name                                 |     id |   minutes | nutrition                                                   | description                                                                                                                                                                                                                                                                                                                                                                       |   n_ingredients |   rating |
|---:|:-------------------------------------|-------:|----------:|:------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|---------:|
|  0 | 1 brownies in the world    best ever | 333281 |        40 | ['138.4', '10.0', '50.0', '3.0', '3.0', '19.0', '6.0']      | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              |               9 |        4 |
|  1 | 1 in canada chocolate chip cookies   | 453467 |        45 | ['595.1', '46.0', '211.0', '22.0', '13.0', '51.0', '26.0']  | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            |              11 |        5 |
|  2 | 412 broccoli casserole               | 306168 |        40 | ['194.8', '20.0', '6.0', '32.0', '22.0', '36.0', '3.0']     | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 |               9 |        5 |
|  3 | millionaire pound cake               | 286009 |       120 | ['878.3', '63.0', '326.0', '13.0', '20.0', '123.0', '39.0'] | why a millionaire pound cake?  because it's super rich!  this scrumptious cake is the pride of an elderly belle from jackson, mississippi.  the recipe comes from "the glory of southern cooking" by james villas.                                                                                                                                                                |               7 |        5 |
|  4 | 2000 meatloaf                        | 475785 |        90 | ['267.0', '30.0', '12.0', '12.0', '29.0', '48.0', '2.0']    | ready, set, cook! special edition contest entry: a mediterranean flavor inspired meatloaf dish. featuring: simply potatoes - shredded hash browns, egg, bacon, spinach, red bell pepper, and goat cheese.                                                                                                                                                                         |              13 |        5 |

---
### Univariate Analysis
#### Plots of Distributions: 
we care about the distribution of rating and minutes to answer our analysis question. So we plot these two distributions.
<iframe src="assets/rating_plot.html" width=700 height=400 frameBorder=0></iframe>
**Explanation:** The average of mean rating for all recipes is 4.63, the distribution is left skewed, majority of the ratings are positive. 

<iframe src="assets/plot_min.html" width=700 height=400 frameBorder=0></iframe>
**Explanation:** mean after removing outlier is 38.68, the distribution is right skewed, majority of recipes take less than one hour to prepare

### Bivariate Analysis
Plot the distributions of minutes of high_rating and low_rating recipes
<iframe src="assets/bivariate_plot.html" width=700 height=400 frameBorder=0></iframe>

**explanation**
The distributions of minutes between high_rating recipes and low_rating recipes are similar. In other words, no matter the recipe is rated high or low, they have similar trend that most recipes take under 60 minutes, and there are fewer recipes that take longer time. There is no obvious differences between high and low ratings of a recipe by looking at how long it takes.

Plot the distributions of recipes' preparation time of high calories and high calories
<iframe src="assets/bivariate_plot2.html" width=700 height=400 frameBorder=0></iframe>

**explanation**
There appears to be a difference between how many ingredients are in high-calories recipes and non-high-calories recipes
high_caloreies food tend to have more ingredients.

### Interesting Aggregates
#### Pivot Table
---

|   rating |   ('mean', 'minutes') |   ('count', 'minutes') |
|---------:|----------------------:|-----------------------:|
|        1 |               95.7864 |                    590 |
|        2 |               98.6    |                    775 |
|        3 |               96.3054 |                   2760 |
|        4 |              106.359  |                  20924 |
|        5 |              114.329  |                  56124 |

---

**Explanation:**
The pivot table shows that it does seem like there is a trend where the higher ratings (4 and 5) takes longer time to prepare.

## Assessment of Missingness
### NMAR Analysis
We believe the `'rating'` column is not missing at random(NMAR), the chance that a value is missing depends on the actual missing value. In our Data Generating Process, we first filled all 0 ratings with np.nan and then get the average rating in `'rating'` column. Thus, `'rating'` of a recipe is missing if a recipe has no reviews with any rating. The probability that a users leave no rating for a recipe is likely to depends on the intended rating itself.
For example, the user is less likely to fill in a 3 when they feel neutral towards the recipe, compared to 5 and 1 when they are extremely satified or dissatisfied. 

**additional data you to obtain that could explain the missingness:** If the reviews came with tags the reviewer can select, it will likely turn rating into an MAR column. For example, a review with **"delicious"** tag is less likely to be missing its rating. 

### Missingness Dependency

**Comparing null and non-null `'description'` distributions for `'n_ingredients'`**.
We use **K-S statistic** to identify missingness of `'description'` 
In our permutation test of testing `'description'`'s missingness dependency on `'n_ingredients'`
Our null hypothesis is: `'description'` missingness does not depend on `'n_ingredients'`


#### Results of Missingness Permutation Tests

Plot of K-S Distribution: 
<iframe src="assets/ks_fig.html" width=700 height=400 frameBorder=0></iframe>

We get p-value about 0.01, we reject null hypothesis, we can conclude that description missingness likely depends on n_ingredients.

---
## Permutation Testing
#### **Null Hypothesis**: 
The distribution for high rating recipes's minutes to prepare and low rating recipes's minutes are the same.

#### **Alternative Hypothesis**: 
The distribution for high rating recipes's minutes to prepare and low rating recipes's minutes are not the same.

#### **Test Statistic**: K-S Statistic
The Kolmogorov-Smirnov test statistic measures the similarity between two distributions. We have two distributions of minutes, which are labeled high-rating and low rating(two dimensions). We selected K-S Statistic to compare our two distributions and see if they differ. 

#### **Significance level**: 
0.05(or 5%)
#### **the resulting p-value**: 
0.0
#### **Conclusion**: 
p value is close to 0.00, less than the threshold of 0.05, therefore we reject the null. There is likely a relationship between recipes's rating and recipes's cooking time.
Since we reject null, the difference in distribution of minutes for rating > 3 and rating <= 3 is not due to random chance. There is probably a relationship between a recipe's rating and its cooking time.


---
