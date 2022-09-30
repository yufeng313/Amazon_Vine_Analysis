# Amazon_Vine_Analysis
## Overview
In this project, we are going to analyze Amazon reviews written by members of the paid Amazon Vine program and determine if there is any bias toward favorable reviews from Vine members.

## Resources
Data Source: [Amazon Review datasets](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt)<br/>
Software: Google Colab Notebook, PostgreSQL 11.16, pgAdmin4 6.11

## Results
### Perform ETL on Amazon product reviews
In this project, I’ll pick the kitchen dataset from [Amazon Review datasets](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt) to do the analysis with following steps: <br/>
1. Create an AWS RDS database with tables in pgAdmin<br/>
2. Use PySpark to perform the ETL process to extract the dataset, transform the DataFrame into four separate DataFrames that match the table schema in pgAdmin<br/>
3. Upload the transformed data into pgAdmin<br/>

Here are the four tables in pgAdmin below:<br/>
#### 1) customers_table
![customers_table](https://user-images.githubusercontent.com/107179765/192223563-7bac627e-f393-4394-978f-6976654b1c54.png)<br/>
#### 2) products_table
![products_table](https://user-images.githubusercontent.com/107179765/192223611-942578ae-9b59-4349-b3fe-749e7bfcebbb.png)<br/>
#### 3) review_id_table
![review_id_table](https://user-images.githubusercontent.com/107179765/192223635-bd94d619-0ab0-471c-819b-af138660e65d.png)<br/>
#### 4) vine_table
![vine_table](https://user-images.githubusercontent.com/107179765/192223687-5719fbfb-eb40-4692-9def-d388db3b710d.png)

### Determine bias of vine reviews
In order to determine if having a paid Vine review makes a difference in the percentage of 5-star reviews, we’ll analyze the dataset with following steps: <br/>
1. Filtered the data to retrieve all the rows which meet these prerequisites: ‘total_votes’>=20, helpful_votes/total_votes>=50%, vine =='Y' or 'N'.<br/>
2. Determine the total number of reviews, the number of 5-star reviews, and the percentage of 5-star reviews for the two types of review (paid vs unpaid). <br/>

Here are the results below: <br/>

![output for vine bias analysis](https://user-images.githubusercontent.com/107179765/192223829-89dea553-da9e-4706-95df-9e3860478f97.png)<br/>
- How many Vine reviews and non-Vine reviews were there? <br/>
  There were 1,207 Vine reviews and 97,839 non-Vine reviews. <br/>
- How many Vine reviews were 5 stars? How many non-Vine reviews were 5 stars? <br/>
  509 Vine reviews were 5 stars, and 45,858 non-Vine reviews were 5 stars. <br/>
- What percentage of Vine reviews were 5 stars? What percentage of non-Vine reviews were 5 stars? <br/>
  42.17% of Vine reviews were 5 stars, and 46.87% of non-Vine reviews were 5 stars.

## Summary
The results show that 42.17% of Vine reviews were 5 stars, while 46.87% of non-Vine reviews were 5 stars, with almost the same percentage, we can say that there isn’t too much bias for reviews in the Vine program of kitchen category. <br/>
In order to make a further detailed analysis to support the statement, I think we could perform the similar analysis on 1-4 star_rating reviews to see if there is any bias in the Vine program.
