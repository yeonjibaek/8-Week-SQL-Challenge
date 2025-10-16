## Case Study #1 - Danny's Diner
_Note: This [website](https://www.db-fiddle.com/f/2rM8RAnq7h5LLDTzZiRWcd/138) contains the schema SQL where I wrote my SQL queries!_

### 💬 Problem Statement
Danny has just opened up a new restaurant and does not know how to fully utilize his data to improve his business. He thinks having a deeper connection to the customers will help them have more personalized experience when visting his restaurant.
Can we use the data to help Danny keep his business alive?

### 📊 Tables/Datasets
- sales: customer_id, order_date, product_id
- menu: product_id, product_name, price
- members: customer_id, join_date

<img width="604" height="355" alt="Screenshot 2025-10-16 at 12 00 53 AM" src="https://github.com/user-attachments/assets/95f7da08-8125-4028-a3f7-aa6dc9d6d6f6" />

---

### ❔ Case Study Questions

**1. What is the total amount each customer spent at the restaurant?**

**Query SQL:**
```sql
SELECT
  	customer_id,
	  SUM(price) AS total_sales
FROM sales
LEFT JOIN menu
ON sales.product_id = menu.product_id
GROUP BY customer_id
ORDER BY customer_id ASC;
```

**Thought Process:**
1. First, I see that we have to group by _customer_id_ because we need to sum the amount spent from each customer.
2. I decided to _LEFT JOIN_ _sales_ table with _menu_ table on _product_id_ because I saw that it was the key that can connect the two tables.
3. Once the tables are joined and grouped by _customer_id_, I aggregate the price and named it as _total_sales_.

**Answer:**
| customer_id | total_sales |
|---|---|
| A | 76 |
| B | 74 |
| C | 36 |

- Customer A spent $76 in total.
- Customer B spent $74 in total.
- Customer C spent $36 in total.


**2. How many days has each customer visited the restaurant?**

**Query SQL:**
```sql
SELECT
  	customer_id,
	  COUNT(DISTINCT order_date) AS total_visits
FROM sales
GROUP BY customer_id
ORDER BY customer_id ASC;
```

**Thought Process:**
1. First, I see that we don't have to join any tables because _customer_id_ and _order_dates_ are both in _sales_ table.
2. I use _COUNT_ function to count _DISTINCT_ _order_dates_ from each customers and named it _total_visits_. I made sure to use the _DISTINCT_ keyword because there might be a case where a customer orders twice in one day.
3. I also grouped by _customer_id_ so that we get summary of each customers.

**Answer:**
| customer_id | total_sales |
|---|---|
| A | 4 |
| B | 6 |
| C | 2 |

- Customer A visited the restaurant 4 times.
- Customer B visited the restaurant 6 times.
- Customer C visited the restaurant 2 times.

**3. What was the first item from the menu purchased by each customer?**

**4. What is the most purchased item on the menu and how many times was it purchased by all customers?**

**5. Which item was the most popular for each customer?**

**6.Which item was purchased first by the customer after they became a member?**

**7.Which item was purchased just before the customer became a member?**

**8. What is the total items and amount spent for each member before they became a member?**

**9. If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?**

**10. In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B have at the end of January?**
