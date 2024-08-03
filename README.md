# Case Study #1 - Danny's Diner

#### ![Danny's Diner](https://github.com/user-attachments/assets/4057eff8-3847-435e-9af6-853ead99e840)

## 📚 Table of Contents

- Business Task
- Entity Relationship Diagram
- Questions & Solutions

---
Please note that all the information regarding the case study has been sourced from the following link: [here](https://8weeksqlchallenge.com/case-study-1/)

# Business Task

Danny wants to use the data to answer a few simple questions about his customers, especially about their visiting patterns, how much money they’ve spent and also which menu items are their favourite.

Danny has shared 3 key datasets for this case study:

- sales
- menu
- members

# Entity Relationship Diagram

![Danny](https://github.com/user-attachments/assets/50bbab53-c565-4357-8834-1db749ca7fc4)

# Questions & Solutions

#### 1. What is the total amount each customer spent at the restaurant?

#### Solution:-

```
SELECT
         customer_id,
         SUM(price) AS Total_spent
FROM
         sales JOIN menu
WHERE 
         sales.product_id=menu.product_id
GROUP BY
         customer_id;
```

#### Output:-

![Ans 1](https://github.com/user-attachments/assets/70ff6885-7640-42a8-9da7-c1508e4c7fad)

- Customer A spent $76
- Customer B spent $74
- Customer C spent $36

---

#### 2. How many days has each customer visited the restaurant?

#### Solution:-
```
SELECT
          customer_id,
          COUNT(DISTINCT order_date) AS COUNT_OF_DAYS
FROM
          sales 
GROUP BY
          customer_id;
```

### Output:-

![Ans 2](https://github.com/user-attachments/assets/479128fa-0ff0-45d6-905a-c42638251e60)

- Customer A has visited the restaurant 4 days.
- Customer B has visited the restaurant 6 days.
- Customer C has visited the restaurant 2 days.
---
  
#### 3. What was the first item from the menu purchased by each customer?

#### Solution:-
```
WITH CALCULATE AS (
SELECT
       customer_id,
       product_name,
       order_date,
       DENSE_RANK() over(partition by customer_id order by order_date) AS RANKS
FROM
       sales JOIN menu
WHERE
       sales.product_id=menu.product_id
GROUP BY
        customer_id,
        product_name,
        order_date
)
SELECT
       customer_id,
       product_name
FROM
       CALCULATE
WHERE
       RANKS=1
```
#### Output:-

![Ans 3](https://github.com/user-attachments/assets/89802568-f19e-4046-902c-e9a3af9441c9)

- Customer A placed an order for both curry and sushi simultaneously, making them the first items in the order.
- Customer B's first order is curry.
- Customer C's first order is ramen.
---

#### 4. What is the most purchased item on the menu and how many times was it purchased by all customers?

#### Solution:- 
```
WITH RANKING AS (
SELECT 
          product_name,
          COUNT(sales.PRODUCT_ID) AS TOTAL_COUNT,
          rank() over(order by COUNT(sales.PRODUCT_ID) DESC ) AS RANKS
FROM
          sales JOIN menu
WHERE
	      sales.product_id=menu.product_id
GROUP BY
          product_name
)     
SELECT
       product_name,
       TOTAL_COUNT
FROM
       RANKING
WHERE
       RANKS=1;
```
#### Output:-

![Ans 4](https://github.com/user-attachments/assets/eea13dfc-d857-42a1-b7ed-051b16ead093)

Ramen is the item that was purchased the most by all customers and it was purchased 8 times.




  


