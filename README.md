# THELOOK ECOMMERCE CASE STUDY
## INTRODUCTION
TheLook Ecommerce is an ecommerce business that has started to actively conduct online buying and selling transactions starting in January 2019. Starting from its establishment until now, Thelook Ecommerce business growth has begun to develop. The development of Thelook Ecommerce can be seen from the level of monthly sales trends that have occurred to date. This project is carried out to evaluate the level of sales for the period 2019 to 2022. The evaluation of the level of sales carried out can be seen from the level of orders in the category of complete status orders. Complete order status indicates the success of a sales transaction so that it will be counted as sales data. Sales level evaluation is carried out to provide new information that can be useful for developing more sales levels in the future.
## ASK
Three questions will guide improving future sales programs:
1. What is our biggest customer segment? (Overall, by country, gender, age)
2. What traffic source is the most effective for us to acquire users?
3. How is the monthly trend of sales? How Much is the cancellation and return rate vs the total number of orders?

Business Problem : "How to increase sales in the future by increasing the complete status of the order?"
## PREPARE
- Data is located in this [link](https://drive.google.com/drive/folders/10X9zeO-JUt40rIsY0y_tQwi6AYvqvMLG?usp=sharing)
- Overall there are 33,639 rows and 24 columns in this data
### Data Preview
![Preview Data](https://user-images.githubusercontent.com/103189217/163332934-8548a783-5379-41aa-8aef-e9136c47c8ca.PNG)
## PROCESS
### Tools
- SQL (BigQuery) for cleaning and format data.
- Google Data Studio to analyze and make data visualization.
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

And then, we double check to ensure is our data really clean or not with previous query.
```
-- Check for Null --
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

-- Check for Duplicates --
SELECT  order_id,
        COUNT(order_id)
FROM `shining-haiku-345911.thelook_ecommerce.project` 
GROUP BY order_id
HAVING COUNT(order_id) > 1
```
After checking the data, which consists of checking for null values and duplicate data, neither of them was found in the data to be processed so that the data can be said to be clean. Clean data can facilitate the analysis process
## ANALYZE
- Number of a customer segment by gender
![Capture1](https://user-images.githubusercontent.com/103189217/163671542-669c5784-b1b1-4d0f-b53e-cf18f1286c8b.PNG)

- Number of a customer segment by age range

![Capture 2](https://user-images.githubusercontent.com/103189217/163701407-6a650add-7d4e-4056-985f-a08903dd3070.PNG)

- Number of traffic source

![Capture 4](https://user-images.githubusercontent.com/103189217/163701618-76fa3098-67a6-4843-bd92-f2576fdf9f3c.PNG)

- Number of the monthly trend of sales

![Capture3](https://user-images.githubusercontent.com/103189217/163701442-ee57853d-0b0a-41a9-a067-1682d8deb5e5.PNG)

- Number of the complete orders, return rates, and cancellation

![Capture](https://user-images.githubusercontent.com/103189217/163671525-6490f75f-94cc-42e5-8fa5-9ee2af6737cb.PNG)

## SUMMARY
- According to the largest consumers of Thailook E-Commerce by country, 3 countries are the largest consumers consisting of China, the United States, and Brazil.
- According to Thailook E-Commerce's smallest consumers by country, 3 countries are the smallest consumers consisting Spain, Japan, and Australia.
- Observed from the largest Thailook Ecommerce consumer by gender, it can be seen that both males and females have almost the same purchase value in every country.
- Based on the traffic source used by users to find out Thelook Ecommerce, there are 5 categories of traffic sources consisting of Search, Organic, Facebook, Email, and Display. Traffic source Search is the most widely used traffic source compared to other traffic sources.
- In reviewing the monthly trend of sales in the period 2019 to 2022, it is known that the level of sales tends to increase every month. Especially for the month of April 2022, the level of sales has decreased, apparently, this is because the month of April has not ended.
- The monthly sales trend generated describes orders with complete categories. Order types are grouped into three categories consisting of complete, return rate, and cancellation. It can be seen that the complete category is the largest group compared to the others. However, it can be seen that the return rate category is in the second-highest position, which when viewed in more detail, the return rate category has quite a lot of nominal as well.
## RECOMMENDATIONS
- In the evaluation of the level of sales, it was found that based on the order status, the return category still has a high enough value that affects the level of sales.
- In increasing sales, the return rate and cancellation categories should be minimized. The number of these two categories can be minimized by increasing Thelook Ecommerce services such as on-time delivery of goods and improving product quality. In this case, further analysis is needed.
- In reviewing the level of sales by country segmentation, it can be seen that there are three countries with the lowest sales levels, such as Spain, Japan, and Australia. In overcoming this, there is a need for further evaluation of customer culture and sales methods in these countries.
- The level of sales based on several segmentation categories such as gender and age range has an almost balanced value result so that it has little effect on increasing sales
- In evaluating the level of sales, it is also necessary to study based on the traffic source used by the user to place an order on Thelook Ecommerce. It can be seen that the most used traffic source is the Search category compared to other categories. In this case, it is necessary to increase the appearance that is more attractive from various other traffic sources which can ultimately affect the level of sales in the future.
