# Recipe Investigation: What types of recipes tend to have higher average ratings?



## Introduction
<br />
The dataset is merged by two datasets drawn from a real food recipe website Food.com since 2008. One of the datasets record the features of recipes, and another one record the comments by users towards a recipe. We merge the two datasets by recipe id, so each of the row correspond to a recipe's features and a feedback from a user. The question we Investigate in this project is: What types of recipes tend to have higher average ratings?<br />
<br />
This is a real-world dataset about how cooking learners rate the recipe. This question analyze the factors associated with rating, which can help contributors/posters of recipe understand how to write or design the recipe.It has 234429 rows and
###note: change the columns


---

## Cleaning and EDA
### Data cleaning
To explore the question using different analysis tool, data cleaning is needed on the raw data, <br /><br />
•First step: we discard part of features in the dataframe and only preserve columns with features related to the question, namely columns 'name', 'id', "minutes', 'nutrition', 'n_steps', 'n_ingredients' and 'Average_rating'. By doing this, we eliminated irrelevant data which make our data analyzing process more efficient. <br /><br />
•Second step: we prep our data for further analysis by looking at the types of each columns and identifying which column is need to be typecasted. We found that type casting is needed to be applied on column 'nutrition' since they are string representation of a list with nutrition info like calories, sugar etc as elements. We then extrated these elements from 'nutrition' column, split them and make a new column for each nutrition info in our dataframe. For each new column, we typecasted them into 'float' for further analysis. After getting all info out of the 'nutrition' column, we dropped the column to make the dataframe less redundant.<br />
<br />•Third step: by merging two dataframe(information about each recipes and users reviews on the recipes), one recipe can appear in many rows if more than one users leave review for it(each reviews for the same recipe would take one line). Also, to explore the question we have, we just need infomation about the recipe and also average rating. Since we already calculated the average rating and assign to each rows(rows of identical recipe would have the same average rating), we decided to drop duplicates based on the "id" column which stores the unique number for individual recipe. By doing this, we can use count to perform data analysis without being influence by having one recipe appear more than others in the dataframe and eliminate potential bias.<br /><br />
The first five rows of the cleaned dataframe are as below: 
<br />

|    | name                                 |     id |   minutes |   n_steps |   n_ingredients |   rating |   Average_rating |   calories (#) |   total fat (PDV) |   sugar (PDV) |   sodium (PDV) |   protein (PDV) |   saturated fat (PDV) |   carbohydrates (PDV) |
|---:|:-------------------------------------|-------:|----------:|----------:|----------------:|---------:|-----------------:|---------------:|------------------:|--------------:|---------------:|----------------:|----------------------:|----------------------:|
|  0 | 1 brownies in the world    best ever | 333281 |        40 |        10 |               9 |        4 |                4 |          138.4 |                10 |            50 |              3 |               3 |                    19 |                     6 |
|  1 | 1 in canada chocolate chip cookies   | 453467 |        45 |        12 |              11 |        5 |                5 |          595.1 |                46 |           211 |             22 |              13 |                    51 |                    26 |
|  2 | 412 broccoli casserole               | 306168 |        40 |         6 |               9 |        5 |                5 |          194.8 |                20 |             6 |             32 |              22 |                    36 |                     3 |
|  6 | millionaire pound cake               | 286009 |       120 |         7 |               7 |        5 |                5 |          878.3 |                63 |           326 |             13 |              20 |                   123 |                    39 |
|  7 | 2000 meatloaf                        | 475785 |        90 |        17 |              13 |        5 |                5 |          267   |                30 |            12 |             12 |              29 |                    48 |   

### Univariate Analysis
In this section, we choose to visualize the distributions of two variables: number of steps and number of ingredients.<br />
<br />
1.Distribution of Steps Number(n_steps)
According to the diagram, the number of recipes increases in each category as n_steps increases from 1 to 7 and decreases from 7 to 40. Most of the recipes falls in the n_steps range from 1 to 20, and n_steps 7 has the highest count, about 7000. Only very few recipes have n_steps from 40 to 100.
<iframe src="assets/n_steps_distribution.html" width=800 height=600 frameBorder=0></iframe>
<br />
<br />
<br />
2.Distribution of Ingredients Number(n_ingredients)
According to the diagram, the number of recipes in each category increases as n_ingredients increases from 1 to 8 and decreases from 8 to 20. Most of the recipes falls in the n_ingredients range from 1 to 20, and n_ingredients 8 has the highest count, about 9000. Only very few recipes have n_ingredients from 20 to 35.
<iframe src="assets/n_ingredients_distribution.html" width=800 height=600 frameBorder=0></iframe>
<br />

### Interesting Aggregates
To explore the relationship between number of steps it take to make the food('n_steps') and the average rating, I have grouped and labeled recipe with average rating that fall in range [0,1] (including on both side as [0,1]), recipe with average rating that fall in (1,2] (including 2 but excluding 1) as (1,2] and  same for (2,3], (3,4], (4,5]. <br /><br />
Also for step range, I label each n_step as [0,20], (20,40], [40,60), [60,80), (80,100]. Then we created the pivot table as shown below with average rating range as columns and step range as index for rows. Each values indicate the percentage of data in each step range fall into each average rating range individually. <br /><br />
Each row sum up to 100% and to avoid biases that may be introduced by the missingness, we also drop the nan values in the average rating column, leaving all valid average rating. 
<br />

| step range   |      (1,2] |     (2,3] |    (3,4] |    (4,5] |      [0,1] |
|:-------------|-----------:|----------:|---------:|---------:|-----------:|
| (20,40]      | 0.0111622  | 0.0308601 | 0.159991 | 0.790107 | 0.00787919 |
| (40,60]      | 0.00490196 | 0.0245098 | 0.102941 | 0.857843 | 0.00980392 |
| (60,80]      | 0          | 0.04      | 0.04     | 0.92     | 0          |
| (80,100]     | 0          | 0.1       | 0.1      | 0.8      | 0          |
| [0,20]       | 0.00753534 | 0.0331022 | 0.169045 | 0.783396 | 0.00692185 |

<br />
This pivot table give a good representation of the average rating distribution for each step range interval becasue instead of looking at the number of recipe fall in these ranges, we use the percentage which eliminate the potential biases caused by population differences(the total recipes number in certain step range is more than others).<br /><br />
By looking at the table, we can see that recipe with step between 60-80 tended to have higher rating since more than 92 percent of these recipe have average rating between 4 and 5 with 0% percent that fall in average rating between 0-2. 

---
## Assessment of Missingness
<iframe src="assets/rating-n_steps.html" width=800 height=600 frameBorder=0></iframe>

---

## Hypothesis Testing


---
