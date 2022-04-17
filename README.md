# THELOOK ECOMMERCE CASE STUDY
## INTRODUCTION
## ASK
Three questions will guide improving future sales programs:
1. What is our biggest customer segment? (Overall, by country, gender, age)
2. What traffic source is the most effective for us to acquire users?
3. How is the monthly trend of sales? How Much is the cancellation and refund rate vs the total number of orders?

Business Problem : "How to increase sales in the future by increasing the complete status of the order?"
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
- Combine two tables, there are the orders table and the users table into one table
- Select multiple columns as needed to answer questions from the two columns to be combined
```
Create table `shining-haiku-345911.thelook_ecommerce.project` AS
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
![Preview Data 1](https://user-images.githubusercontent.com/103189217/163342106-c95ce682-b27e-42dd-8a7b-caaa09385eb2.PNG)
After combined data was created, we check for null on this data
```
SELECT
    SUM(CASE WHEN order_id IS NULL THEN 1 ELSE 0 END) AS order_id_null,
    SUM(CASE WHEN user_id IS NULL THEN 1 ELSE 0 END) AS user_id_null,
    SUM(CASE WHEN status IS NULL THEN 1 ELSE 0 END) AS status_null,
    SUM(CASE WHEN created_at IS NULL THEN 1 ELSE 0 END) AS created_at_null,
    SUM(CASE WHEN num_of_item IS NULL THEN 1 ELSE 0 END) AS num_of_item_null,
    SUM(CASE WHEN age IS NULL THEN 1 ELSE 0 END) AS age_null,
    SUM(CASE WHEN gender IS NULL THEN 1 ELSE 0 END) AS gender_null,
    SUM(CASE WHEN country IS NULL THEN 1 ELSE 0 END) AS country_null,
    SUM(CASE WHEN traffic_source IS NULL THEN 1 ELSE 0 END) AS traffic_source_null
FROM `shining-haiku-345911.thelook_ecommerce.project
```
![Preview Data 2](https://user-images.githubusercontent.com/103189217/163342517-e911964f-0532-4f30-af10-ca6a988ddcc3.PNG)
From this query, we can know that there is no null value.

Next we check for duplicated data by using order_id as an unique constraint
```
SELECT  order_id,
        COUNT(order_id)
FROM `shining-haiku-345911.thelook_ecommerce.project` 
GROUP BY order_id
HAVING COUNT(order_id) > 1
```
![Preview Data 3](https://user-images.githubusercontent.com/103189217/163344912-d2c119d4-6957-4440-aa9a-010fb735fbbb.PNG)
From this query, we can know that there is no duplicate data

After checking the data, which consists of checking for null values and duplicate data, neither of them was found in the data to be processed so that the data can be said to be clean. Clean data can facilitate the analysis process
## ANALYZE
![Capture1](https://user-images.githubusercontent.com/103189217/163671542-669c5784-b1b1-4d0f-b53e-cf18f1286c8b.PNG)

![Capture 2](https://user-images.githubusercontent.com/103189217/163701407-6a650add-7d4e-4056-985f-a08903dd3070.PNG)

![Capture 4](https://user-images.githubusercontent.com/103189217/163701618-76fa3098-67a6-4843-bd92-f2576fdf9f3c.PNG)

![Capture3](https://user-images.githubusercontent.com/103189217/163701442-ee57853d-0b0a-41a9-a067-1682d8deb5e5.PNG)

![Capture](https://user-images.githubusercontent.com/103189217/163671525-6490f75f-94cc-42e5-8fa5-9ee2af6737cb.PNG)

## SUMMARY
## RECOMMENDATIONS
