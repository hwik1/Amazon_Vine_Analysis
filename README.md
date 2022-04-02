# Amazon Vine Review Analysis
Module 16 Challenge prepared by Hannah Wikum - April 2022
___
## Resources
Data Source: https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Beauty_v1_00.tsv.gz

Software: AWS, PostgreSQL, Google Colab, PySpark
___
## Overview
This challenge involved completing the ETL (extract, transform, load) process on reviews of beauty products from Amazon. I used PySpark in a Google Colab notebook to extract the review data into a DataFrame, before separating it into four DataFrames for customer data, product data, review information, and Vine (paid review) details. Schema was provided to build matching tables in a PostgreSQL datbase that was connected to my AWS server. Finally, I created a connection to Postgres and loaded the data from my four DataFrames into the tables.

In the second part of the challenge, I used PySpark in another Google Colab notebook to analyze if there was a postivity bias toward higher ratings for reviews collected as part of the Vine program where participants are paid for their reviews. I recreated the Vine DataFrame from the first deliverable in my second notebook and filtered for reviews that had 20 or more total votes **and** where 50% or more of total votes were considered helpful. This step ensured we got the highest quality review data for the analysis. Once that filtering was done, I created two new DataFrames: one for paid reviews from the Vine program and a second for unpaid reviews. I used select() and count() or where() and count() in PySpark to calculate the following three metrics for both paid and unpaid reviews: total reviews, number of 5-star ratings, and percentage of 5-star ratings.
___
## Results
After completing my analysis of paid versus unpaid reviews of beauty products from Amazon, there were a few key findings:

 * For beauty product reviews with 20+ total votes and at least 50% helpful votes, there were far more unpaid reviews than paid reviews from the Vine program. Of the 74,760 reviews that fit the criteria I mentioned, only 647 were paid Vine reviews. That means 99.1% of the quality reviews we analyzed were unpaid.

_PySpark Code for Determining Review Counts_

![image](https://user-images.githubusercontent.com/93058069/161403708-a535bf59-b8fc-4e54-ad63-b6604c25c1b3.png)

 * To determine the number of 5-star ratings for each review type, I filtered the DataFrames by reviewer type using where() to focus on entries in the star_rating column that were equal to 5. For the Vine reviews, 229 had a 5-star rating. For unpaid reviews, 43,217 were for 5-stars.

_PySpark Code for Determining Counts of 5-Star Ratings_
![image](https://user-images.githubusercontent.com/93058069/161403742-ddc2922e-d166-4e7d-a05b-ceea62fbac52.png)

 * Based on the two bullets above, I used division in the Google Colab notebook with the two variables above to determine the percentage of 5-star reviews for paid versus unpaid. The results were that 35.4% of quality Vine reviews were for 5-stars, while a much large 58.3% of unpaid reviews were for a perfect 5-stars. 

_Code to Determine Percentage of 5-Star Reviews_

![image](https://user-images.githubusercontent.com/93058069/161403793-6f4d260c-2e91-4b54-a149-2a660c8e4395.png)
__
## Summary
In summary, my results did **not** show a positivity bias for reviews submitted via the paid Vine program versus unpaid reviews. Only 35.4% of paid reviews were for a perfect 5-stars, while 58.3% of unpaid reviews gave the beauty products they rated 5-stars. An additional anlysis I would do on the data is to calculate the median rating for the paid Vine reviews compared to the median for unpaid. (I recommend median over mean because we already know that the unpaid data is skewed toward higher reviews, so this would give a second method for researching if a positivity bias exists for paid reviews.)
