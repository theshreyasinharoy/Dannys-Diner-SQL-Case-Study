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


