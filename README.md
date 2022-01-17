# Shopify Data Science Intern Challenge 2022

## Question 1

### *Part a):*

The following anomalies were detected in the data:


1.   Shop 42:

      *   User 607 consistently purchases 2,000 pairs of sneakers at 4:00 on 17 separate occasions.
      *   The suspiciously consistent pattern of these large transactions warrants further investigation.
      *   Without further context or detail, it is difficult to determine the legitimacy of these orders.
      *   It is recommended to exclude these orders from the analysis.


2.   Shop 78:
      
      *   The unit price of sneakers at this store is $25,725.
      *   Given the unreasonable high cost of sneakers at this store, it is recommended that orders from this store are excluded from the analysis.

### *Part b):*

Average unit retail (AUR) is suggested to be used as the new metric.
AUR can be calculated as:

  AUR = Total revenue [$] / Total items sold

This metric is less sensitive to extremely large statistical outliers in the dataset, because it accounts for the total number of items ordered. Orders with a large number of items will not affect AUR, but will skew the original AOV metric.

### *Part c):*
After removing the anomalies detected in the *Analysis*, the calculated AUR is **$151.69**.

*Re-Calculated AOV:*

AOV can still be used as a metric to evaluate the data set, if the detected anomalies are excluded from the calculation. 
Excluding the anomalies detected in the *Analysis*, the calculated AOV is **$302.58**.

## Question 2

### Part a)
```
SELECT COUNT(OrderID), ShipperName
FROM Orders as o
JOIN Shippers as s
ON s.ShipperID = o.ShipperID
WHERE s.ShipperName == 'Speedy Express'
GROUP BY ShipperName;
```
*Speedy Express shipped 54 orders.*

### Part b)
```
SELECT COUNT(o.OrderID) as TotalOrders, e.LastName
FROM Orders as o
JOIN Employees as e
ON o.EmployeeID == e.EmployeeID
GROUP BY e.EmployeeID
ORDER BY COUNT(o.OrderID) DESC;
```
*The employee with the last name Peacock had the most orders (40 orders).*

## Part c)
```
SELECT COUNT(o.OrderID) as TotalOrders, p.ProductName
FROM Orders as o
JOIN Customers as c
ON o.CustomerID == c.CustomerID
JOIN OrderDetails as d
ON o.OrderID == d.OrderID
JOIN Products as P
ON d.ProductID == p.ProductID
WHERE c.Country == 'Germany'
GROUP BY p.ProductName
ORDER BY COUNT(o.OrderID) DESC;
```
*Gorgonzola Telino was ordered most by German customers (5 orders).*





