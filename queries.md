# Database Queries

### Display the ProductName and CategoryName for all products in the database. Shows 76 records.

```sql
SELECT productname, categoryname
FROM products p
JOIN categories c ON c.categoryid = p.categoryid
```

### Display the OrderID and ShipperName for all orders placed before January 9, 1997. Shows 161 records.

```sql
SELECT orderid, shippername, orderdate
FROM orders o
JOIN shippers s ON s.shipperid = o.shipperid
WHERE orderdate < '1997-01-09'
```

### Display all ProductNames and Quantities placed on order 10251. Sort by ProductName. Shows 3 records.

```sql
SELECT productname, quantity
FROM orderdetails od
JOIN products p ON od.productid = p.productid
WHERE orderid = 10251
ORDER BY productname
```

### Display the OrderID, CustomerName and the employee's LastName for every order. All columns should be labeled clearly. Displays 196 records.

```sql
SELECT orderid, customername, lastname AS EmployeeLastName
FROM orders o
JOIN customers c ON o.customerid = c.customerid
JOIN employees e ON e.employeeid = o.employeeid
```

### (Stretch) Displays CategoryName and a new column called Count that shows how many products are in each category. Shows 9 records.

```sql
SELECT categoryname, count(productid) as num_products
FROM categories c
LEFT JOIN products p ON p.categoryid = c.categoryid
GROUP BY categoryname
ORDER BY num_products
```

### (Stretch) Display OrderID and a column called ItemCount that shows the total number of products placed on the order. Shows 196 records.

```sql
SELECT orderid, count(productid) AS num_products, sum(quantity) as total_quantity
FROM orderdetails od
GROUP BY orderid
```

### Display all customers who have not made an order

```sql
SELECT c.customerid, customername, count(orderid) AS num_orders
FROM customers c
LEFT JOIN orders o ON o.customerid = c.customerid
WHERE o.customerid IS NULL
GROUP BY 1,2
```
