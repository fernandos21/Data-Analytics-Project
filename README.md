# THELOOK ECOMMERCE CASE STUDY
## INTRODUCTION
## ASK
Three questions will guide the future marketing program:
1. What is our biggest customer segment? (Overall, by country, gender, age)
2. What traffic source is the most effective for us to acquire users?
3. How is the monthly trend of sales? How Much is the cancellation and refund rate vs the total number of orders?
## PREPARE
''' SELECT
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
ON o.user_id = u.id '''
## PROCESS
### Tools
### Data Cleaning Process
## ANALYZE
## SUMMARY
## RECOMMENDATIONS
