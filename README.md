# THELOOK ECOMMERCE CASE STUDY
## INTRODUCTION
## ASK
Three questions will guide the future marketing program:
1. What is our biggest customer segment? (Overall, by country, gender, age)
2. What traffic source is the most effective for us to acquire users?
3. How is the monthly trend of sales? How Much is the cancellation and refund rate vs the total number of orders?
## PREPARE
- Data is located in this [link](https://drive.google.com/drive/folders/10X9zeO-JUt40rIsY0y_tQwi6AYvqvMLG?usp=sharing)
- Overall there are 33,639 rows and 24 columns in this data
### Data Preview
![Preview Data](https://user-images.githubusercontent.com/103189217/163332934-8548a783-5379-41aa-8aef-e9136c47c8ca.PNG)
## PROCESS
### Tools
- SQL (BigQuery) for cleaning and format data.
- R studio to analyze and make data visualization.
- Tableau to make interactive dashboard
### Data Cleaning Process
```
SELECT
    order_id,
    user_id,
    status,
    o.created_at,
    num_of_item,
    u.age,
    u.gender,
    u.country,
    u.traffic_source
FROM
    `bigquery-public-data.thelook_ecommerce.orders` o 
INNER JOIN
    `bigquery-public-data.thelook_ecommerce.users` u
ON o.user_id = u.id
```
## ANALYZE
## SUMMARY
## RECOMMENDATIONS
