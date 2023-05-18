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
•Second step: we prep our data for further analysis by looking at the types of each columns and identifying which column is need to be typecasted. We found that type casting is needed to be applied on column 'nutrition' since they are string representation of a list with nutrition info like calories, sugar etc as elements. We then extrated these elements from 'nutrition' column, split them and make a new column for each nutrition info in our dataframe. For each new column, we typecasted them into 'float' for further analysis. After getting all info out of the 'nutrition' column, we dropped the column to make the dataframe less redundant.<br /><br />
The first five rows of the cleaned dataframe are as below:
| name                                 |     id |   minutes |   n_steps |   n_ingredients |   Average_rating |   calories (#) |   total fat (PDV) |   sugar (PDV) |   sodium (PDV) |   protein (PDV) |   saturated fat (PDV) |   carbohydrates (PDV) |
|:-------------------------------------|-------:|----------:|----------:|----------------:|-----------------:|---------------:|------------------:|--------------:|---------------:|----------------:|----------------------:|----------------------:|
| 1 brownies in the world    best ever | 333281 |        40 |        10 |               9 |                4 |          138.4 |                10 |            50 |              3 |               3 |                    19 |                     6 |
| 1 in canada chocolate chip cookies   | 453467 |        45 |        12 |              11 |                5 |          595.1 |                46 |           211 |             22 |              13 |                    51 |                    26 |
| 412 broccoli casserole               | 306168 |        40 |         6 |               9 |                5 |          194.8 |                20 |             6 |             32 |              22 |                    36 |                     3 |
| 412 broccoli casserole               | 306168 |        40 |         6 |               9 |                5 |          194.8 |                20 |             6 |             32 |              22 |                    36 |                     3 |
| 412 broccoli casserole               | 306168 |        40 |         6 |               9 |                5 |          194.8 |                20 |             6 |             32 |              22 |                    36 |                     3 |

### Interesting Aggregates
Pivot table
| step range  rating range  |   (1,2] |   (2,3] |   (3,4] |   (4,5] |   [0,1] |   nan |
|:-------------|--------:|--------:|--------:|--------:|--------:|------:|
| (20,40]      |      68 |     245 |    1245 |   10968 |      50 |   251 |
| (40,60]      |       1 |       8 |      52 |     914 |       2 |    24 |
| (60,80]      |     nan |       1 |       1 |      85 |     nan |     3 |
| (80,100]     |     nan |       1 |       1 |      31 |     nan |     2 |
| [20,0]       |     720 |    3714 |   22108 |  190792 |     645 |  2497 |
---
## Assessment of Missingness


---

## Hypothesis Testing


---
