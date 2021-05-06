# Shopify_fall_2021_data_science_challenge

## Question1: 
 Given some sample data, write a program to answer the following: click here to access the required data set

On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 

1) Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. 


2) What metric would you report for this dataset?



3) What is its value?


## Question2:
 For this question you’ll need to use SQL. Follow this link to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

1) How many orders were shipped by Speedy Express in total?

```
SELECT COUNT(DISTINCT OrderID) 
FROM Orders LEFT JOIN Shippers
on Orders.ShipperID = Shippers.ShipperID
where ShipperName = 'Speedy Express';
```
- the numerical answer is: 54

2. What is the last name of the employee with the most orders?
```
SELECT Employees.LastName
FROM Orders LEFT JOIN Employees
ON Orders.EmployeeID = Employees.EmployeeID
GROUP BY Orders.EmployeeID
ORDER BY COUNT(DISTINCT OrderID) DESC
LIMIT 1;

```
- Last name: Peacock

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
Group by OrderDetails.ProductID
ORDER BY sum(OrderDetails.Quantity) DESC
LIMIT 1

```
- Answer: Boston Crab Meat
