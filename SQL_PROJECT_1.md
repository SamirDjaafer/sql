# SQL Mini Project by Samir Djaafer

- Question 1.1

```SQL
SELECT c.CustomerID, c.CompanyName, c.Address, c.City
FROM Customers c
WHERE c.City = 'Paris' OR c.City = 'London'
```

- Question 1.2

```SQL
SELECT p.ProductName, p.QuantityPerUnit FROM Products p
WHERE p.QuantityPerUnit LIKE '%bottles%'
```

- Question 1.3

```SQL
SELECT p.ProductName, p.QuantityPerUnit, s.CompanyName AS "SupplierName", s.Country
FROM Products p
LEFT JOIN Suppliers s ON p.SupplierID = s.SupplierID
WHERE p.QuantityPerUnit LIKE '%bottle%'

```

- Question 1.4

```SQL
SELECT p.CategoryID, c.CategoryName ,COUNT(p.CategoryID) AS "AmountOfProducts"
FROM Products p
LEFT JOIN Categories c ON p.CategoryID = c.CategoryID
GROUP BY p.CategoryID, c.CategoryName
ORDER BY AmountOfProducts DESC
```

- Question 1.5

```SQL
SELECT e.TitleOfCourtesy + ' ' + e.FirstName + ' ' + e.LastName AS "FullName", e.City, e.Country
FROM Employees e
WHERE e.Country = 'UK'
```

- Question 1.6

```SQL
SELECT r.RegionID, FORMAT(SUM(od.UnitPrice * od.Quantity * (1 - od.Discount)), 'C') AS "TotalSales"
FROM [Order Details] od
INNER JOIN Orders o ON od.OrderID = o.OrderID
INNER JOIN EmployeeTerritories et ON o.EmployeeID = et.EmployeeID
INNER JOIN Territories t ON et.TerritoryID = t.TerritoryID
INNER JOIN Region r ON t.RegionID = r.RegionID
GROUP BY r.RegionID
HAVING (SUM(od.UnitPrice * od.Quantity * (1 - od.Discount))) > 1000000
```

- Question 1.7

```SQL
SELECT COUNT(o.OrderID) AS "Orders with Freight over 100"
FROM Orders o
WHERE o.Freight > 100 AND (o.ShipCountry IN ('UK','USA'))
```

- To break it down further we could do

```SQL
SELECT COUNT(o.OrderID) AS "Orders with Freight over 100", o.ShipCountry
FROM Orders o
WHERE o.Freight > 100 AND (o.ShipCountry IN ('UK','USA'))
GROUP BY o.ShipCountry
```

- Question 1.8

```SQL
SELECT TOP 1 od.OrderID, o.CustomerID, od.Discount
FROM Orders o
JOIN [Order Details] od ON o.OrderID = od.OrderID
ORDER BY od.Discount DESC
```

- Question 2.1

```SQL
CREATE TABLE spartans (
    SpartanID INT IDENTITY (1,1),
    Title VARCHAR(5),
    FirstName VARCHAR(20),
    LastName VARCHAR(20),
    Gender VARCHAR(6),
    UniversityAttended VARCHAR(25)
);
```

- Question 2.2

```SQL
INSERT INTO spartans (
    Title, FirstName, LastName, Gender, UniversityAttended
) VALUES (
    'Mr.', 'Samir', 'Djaafer', 'Male', 'a'
), (
    'Mr.', 'Mergim', 'Berisha', 'Male', 'b'
), (
    'Mr.', 'Jonathan', 'Holder', 'Male', 'c'
), (
    'Mr.', 'Marcus', 'Westhuizen', 'Male', 'd'
), (
    'Mr.', 'Avraj', 'Singh', 'Male', 'e'
), (
    'Mr.', 'Ryan', 'Smith', 'Male', 'f'
), (
    'Mr', 'Nathan', 'Forester', 'Male', 'g'
), (
    'Mrs.', 'Saskia', 'Van Barthold', 'Female', 'h'
), (
    'Mr.', 'Fahad', 'Khisaf', 'Male', 'i'
), (
    'Mr.', 'Delvin', 'Roy', 'Male', 'j'
), (
    'Mr.', 'Ashraf', 'Mohamud', 'Male', 'k'
), (
    'Mr.', 'Patrick', 'Clancy', 'Male', 'l'
), (
    'Mr.', 'Hussain', 'Khan', 'Male', 'm'
), (
    'Mr.', 'Stefan', 'Okolo', 'Male', 'n'
);
```

- Question 3.1

```SQL
SELECT e.EmployeeID, e.FirstName + ' ' + e.LastName AS "FullName", s.FirstName + ' ' + s.LastName AS "ReportsTo", s.EmployeeID AS "ReportsToID"
FROM Employees e
INNER JOIN Employees s ON e.ReportsTo = s.EmployeeID
```

- Question 3.2

```SQL
SELECT s.SupplierID, s.CompanyName, FORMAT(SUM(od.UnitPrice * od.Quantity * (1 - od.Discount)), 'C') AS "TotalSales"
FROM [Order Details] od
INNER JOIN Products p ON od.ProductID = p.ProductID
INNER JOIN Suppliers s ON p.SupplierID = s.SupplierID
GROUP BY s.SupplierID, s.CompanyName
HAVING (SUM(od.UnitPrice * od.Quantity * (1 - od.Discount))) > 10000
```

- Question 3.3

```SQL
SELECT TOP 10 c.CustomerID, FORMAT(SUM((od.UnitPrice * od.Quantity) * (1 - od.Discount)), 'c') AS "Total Sales" FROM Orders o
INNER JOIN [order details] od ON od.orderID = o.orderID
INNER JOIN Customers c ON c.customerID = o.CustomerID
WHERE YEAR(o.OrderDate) = (SELECT MAX(YEAR(OrderDate)) FROM Orders) AND o.ShippedDate is not null
GROUP BY c.customerID
```

- Question 3.4

```SQL
SELECT FORMAT(o.ShippedDate, 'MMM-yy') AS "Shipping Month",
AVG(DATEDIFF(dd, o.OrderDate, o.ShippedDate)) AS "Average Ship Time"
FROM Orders o
WHERE o.ShippedDate IS NOT NULL
GROUP BY YEAR(o.ShippedDate), MONTH(o.ShippedDate),FORMAT(o.ShippedDate, 'MMM-yy')
ORDER BY YEAR(o.ShippedDate), MONTH(o.ShippedDate)
```
