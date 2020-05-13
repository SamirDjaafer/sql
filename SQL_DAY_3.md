# SQL - Day 3 With Astha & Shahrukh

```SQL
SELECT COUNT (EmployeesID) AS "Number of Employees" FROM Employees
WHERE City='London'
```

```SQL
SELECT p.productName, p.UnitPrice
FROM Products p
WHERE  p.CategoryID=1  AND p.Discountinued=0
```

```SQL
SELECT DISTINCT c.Country
FROM Customers c
WHERE c.ContactTitle='Owner' AND c.Country LIKE '[^MSD]%'
```

```SQL
SELECT count(*) as "NumberOfOrders"
FROM Orders o
WHERE o.EmployeeID IN (5,7)
```

```SQL
SELECT o.UnitPrice, o.Quantity, o.Discount, o.UnitPrice * o.Quantity AS "Gross Total", o.UnitPrice * o.Quantity * (1 - o.Discount) AS "Net Total"
FROM [Order Details] o
ORDER BY "Net Total" DESC
```

```SQL
SELECT o.OrderID, o.UnitPrice, o.Quantity, o.Discount, SUM(o.UnitPrice * o.Quantity) AS "Gross Total"
FROM [Order Details] o
GROUP BY o.OrderID, o.UnitPrice, o.Quantity, o.Discount
ORDER BY "Gross Total" DESC
```


```SQL
SELECT c.PostalCode AS "Post Code",
LEFT(c.PostalCode, CHARINDEX(' ',c.PostalCode)-1) AS "Postal Code Region",
CHARINDEX(' ', c.PostalCode) AS "Space Found", c.Country
FROM Customers c
WHERE Country = 'UK'
```

```SQL
SELECT p.ProductName
FROM Products p
WHERE p.ProductName LIKE '%''%'
```

```SQL
SELECT p.ProductName
FROM Products p
WHERE CHARINDEX('''',p.ProductName)>0
```

```SQL
SELECT DATEADD(d,5,OrderDate) AS "Due Date",
DATEDIFF(d,OrderDate,ShippedDate) AS "Ship Days"
FROM Orders
```

```SQL
SELECT FirstName + ' ' + LastName AS "Name",
DATEDIFF(YY, BirthDate, GetDate()) AS "Age"
FROM Employees
```

```SQL
SELECT FirstName + '' + LastName AS "Name",
DATEDIFF(DD, BirthDate, GetDate())/365.25 AS "Age"
FROM Employees
```

```SQL
SELECT CASE
WHEN DATEDIFF(d,OrderDate,ShippedDate) < 10 THEN 'On Time'
ELSE 'Overdue'
END AS "Status"
FROM Orders
```

```SQL
SELECT DATEDIFF(d,OrderDate,ShippedDate) AS "Days For Delivery",
CASE
WHEN DATEDIFF(d,OrderDate,ShippedDate) < 10
THEN 'On Time'
ELSE 'Overdue'
END AS "Status"
FROM Orders
```

```SQL
SELECT SUM(p.UnitsOnOrder) AS "Total On Order",
AVG(p.UnitsOnOrder) AS "Avg On Order",
MIN(p.UnitsOnOrder) AS "Min On Order",
MAX(p.UnitsOnOrder) AS "Max On Order"
FROM Products p
```

```SQL
SELECT p.supplierID,
SUM(p.UnitsOnOrder) AS "Total On Order",
AVG(p.UnitsOnOrder) AS "Avg On Order",
MAX(p.UnitsOnOrder) AS "Max On Order"
FROM Products p
GROUP BY p.SupplierID
```

```SQL
SELECT TOP 1 CategoryID,
AVG(ReorderLevel) AS "avg on reorder level"
FROM Products
GROUP BY CategoryID
ORDER BY "Avg on reorder level" DESC
```

```SQL
SELECT p.supplierID,
SUM(p.UnitsOnOrder) AS "Total On Order",
AVG(p.UnitsOnOrder) AS "Avg On Order"
FROM Products p
GROUP BY p.SupplierID
HAVING AVG(UnitsOnOrder) > 5
ORDER BY "Total On Order"
```

```SQL
SELECT p.SupplierID,s.CompanyName AS "Supplier Name", AVG(p.UnitsOnOrder) AS "Average Units On Order"
FROM Products p INNER JOIN Suppliers s
ON p.SupplierID=s.SupplierID
GROUP BY p.SupplierID, s.CompanyName
```

```SQL
SELECT p.ProductName, p.UnitPrice, s.CompanyName AS "Supplier", CategoryName AS "Category"
FROM Products p
INNER JOIN Suppliers s ON p.SupplierID = s.SupplierID
INNER JOIN Categories c ON p.CategoryID = c.CategoryID
```

```SQL
SELECT o.OrderID, o.OrderDate, o.Freight,
e.FirstName+' '+e.LastName AS "Employee Name",
c.CompanyName
FROM Orders o
INNER JOIN Customers c ON o.CustomersID = c.CustomerID
INNER JOIN Employees e ON o.EmployeeID = e.EmployeeID
```
 
