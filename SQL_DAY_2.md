# SQL - Day 2 With Astha & Shahrukh

1. FILTERING Data Using the WHERE Clause.

``` SQL
SELECT * FROM Customers
WHERE City='Paris'
```

2. COUNT (Column_name) = Counts the amounts of Rows for the specific Column.
- AS "new column name" will return the count in a new column with the name specified.

```SQL
SELECT COUNT (EmployeesID) AS "Number of Employees" FROM Employees
SELECT * FROM Employees
WHERE City='London'
```

3. We can SELECT Multiple COLUMNS to be shown.

```SQL
SELECT CustomerID, City FROM Customers
WHERE Country = 'France'
```

4. SELECTing the COUNT of all Columns FROM Products TABLE.

```SQL
SELECT COUNT(*) FROM Products
```

5. The AND Clause is used to FILTER 2 Conditions. Both must equal to TRUE in order for the data row to be displayed.

```SQL
SELECT p.productName, p.UnitPrice
FROM Products p
WHERE  p.CategoryID=1  AND p.Discountinued=0
```

6. Here we are checking for data that is > (greater than) on both sides of the AND Clause.

```SQL
SELECT ProductName, UnitPrice FROM Products
WHERE UnitsInStock > 0 AND UnitPrice> 29.99
```

7. The OR Clause requires only 1 of the statements either side of the clause to be TRUE.

```SQL
SELECT ProductName, UnitPrice FROM Products
WHERE UnitsInStock > 0 OR UnitPrice> 29.99
```

8. The DISTINCT clause here Ensures that no duplicates are shown for c.Country.

- Hence the name DISTINCT meaning different.

```SQL
SELECT DISTINCT c.Country
FROM Customers c
WHERE c.ContactTitle='Owner' AND c.Country LIKE '[^MSD]%'
```

9. The BETWEEN clause will filter data that is BETWEEN the 2 values given.

```SQL
SELECT *
FROM EmployeeTerritories
WHERE TerritoryID BETWEEN 06800 AND 09999
```

# Wildcards

1. The first wildcard is %
- It resembles a filler for zero or more characters.
- In this example we are filtering for data that STARTS with 'S' and is followed by either no characters or unlimited characters.

```SQL
SELECT * FROM Categories
WHERE Categories LIKE 'S%'
```

2. The second wildcard is _
- It resembles a filler for a single character ONLY.
- We can chain _ to represent more than 1 characters.
- In this example we are FILTERING for data that has 'W' as the THIRD letter.

```SQL
SELECT * FROM Categories
WHERE Categories LIKE '__W%'
```

3. The third wildcard is [charlist]
- It can take any number of values and will bring back values starting with the values given.
- In this examples we are FILTERING for data that starts with either B, C or D.

```SQL
SELECT * FROM Categories c
WHERE c.CategoryName LIKE '[BCD]%'
```

4. The fourth wildcard is [^charlist]
- It is the same a charlist however using the ^ at the start will show all the values that DO NOT start with the given values.
- In this example we are FILTERING for data that DOES NOT start with either G, B or P.

```SQL
SELECT * FROM Categories c
WHERE c.CategoryName LIKE '[^GBP]%'
```
