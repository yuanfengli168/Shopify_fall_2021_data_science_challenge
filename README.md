# Shopify_fall_2021_data_science_challenge

## Question1:

Given some sample data, write a program to answer the following: click here to access the required data set

On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis.

1. Think about what could be going wrong with our calculation. Think about a better way to evaluate this data.

- Answer:

  - My first guess is that there are some outliers that makes the mean a biased value. One better way to evaluate is to move the outliers if there is any.

  - I used Jupyter notebook to analyse the dataset, and I have found two outliers.(My codes are in shopify_YuanfengLi.ipynb)

  1. The first outlier is a user:
     There is a user (user_id:607) who should be one of the outliers that we can remove. Because all the purchases of user_id:607 are 2000 items. And all of its order amount are $704000 which is way much higher than the rest of orders.

  2. The second outlier is a shop (shop_id:78), its shoe's price ($25725) is too expensive than the rest of 99 shops.

  - After we get rid of this two outliers, our AOV turns to $302.58 which is more appropriate than $3145.13.

  - The reason why we can get rid of these two outliers is because they can not show the AOV of most orders. Because these two outliers include only 63 rows of orders, and only take 1.26% of all 5000 rows of data, but it can increase the AOV from $302.58 to $3145.13. So it is reasonable to remove this two outliers when we are calculating AOV.

2. What metric would you report for this dataset?

- Answer:
  - **I would use more metrics for the report, such as Mean, Median, Mode, and top 5 most frequent order amount to report, because it can help us to make better strategies.**,
  - My metrics include:
  1. Mean for the dataset without data from shop(shop_id:78) and user(user_id:607), which is $302.58.
  2. The median of the dataset without data from shop(shop_id:78) and user(user_id:607), which is $284.00.
  3. The mode of the dataset without data from shop(shop_id:78) and user(user_id:607), which is $153.00.
  4. Top 5 most frequent order_amount for the dataset without data from shop(shop_id:78) and user(user_id:607), which are:
     [(153, 87), (306, 85), (354, 82), (156, 75), (160, 75)].
  - let me show you how to interpret this list of ordered data. For example, (153, 87) means the $153 is the 1st most frequent order amount that has occured 87 times in the whole datasets. (306, 85) means $306 is the second most frequent order amount that 85 orders have. So on so fourth. This list of top highest order amount could give us a better focus on the groups of target customers, so we can develope better marketing strategies on each group of customers.

3. What is its value?

- Answer:
  I have put some values in the answer for 2nd question, but in summarise. The values for my metric are:

  | Measure                        | Value               |
  | ------------------------------ | ------------------- |
  | AOV                            | $302.58             |
  | Median                         | $284.00             |
  | Mode                           | $153.00             |
  | 1st most frequent order amount | $153.00 (87 orders) |
  | 2nd most frequent order amount | $306.00 (85 orders) |
  | 3rd most frequent order amount | $354.00 (82 orders) |
  | 4th most frequent order amount | $156.00 (75 orders) |
  | 5th most frequent order amount | $160.00 (75 orders) |

## Question2:

For this question you’ll need to use SQL. Follow this link to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

1. How many orders were shipped by Speedy Express in total?

```
SELECT COUNT(DISTINCT OrderID)
FROM Orders LEFT JOIN Shippers
ON Orders.ShipperID = Shippers.ShipperID
WHERE ShipperName = 'Speedy Express';
```

- Answer: 54

2. What is the last name of the employee with the most orders?

```
SELECT Employees.LastName
FROM Orders LEFT JOIN Employees
ON Orders.EmployeeID = Employees.EmployeeID
GROUP BY Orders.EmployeeID
ORDER BY COUNT(DISTINCT OrderID) DESC
LIMIT 1;

```

- Answer: Peacock

3. What product was ordered the most by customers in Germany?

```
SELECT Products.ProductName
FROM Customers JOIN Orders
ON Customers.CustomerID = Orders.CustomerID
JOIN OrderDetails ON
Orders.OrderID = OrderDetails.OrderID
JOIN Products ON
OrderDetails.ProductID = Products.ProductID
WHERE Customers.Country = 'Germany'
GROUP BY OrderDetails.ProductID
ORDER BY sum(OrderDetails.Quantity) DESC
LIMIT 1;

```

- Answer: Boston Crab Meat
