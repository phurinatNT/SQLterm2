-- *********แบบฝึกหัด Basic Query #2 ***************
 
 --1. จงแสดงรหัสสินค้า ชื่อสินค้า ราคาต่อหน่วย เฉพาะสินค้าประเภท Seafood
 --แบบ Product
SELECT ProductID, ProductName, UnitPrice FROM Products P, Categories C WHERE P.CategoryID = C.CategoryID AND C.CategoryName = 'Seafood'
--แบบ Join
SELECT ProductID, ProductName, UnitPrice FROM Products P
JOIN Categories CR ON P.CategoryID = CR.CategoryID
WHERE CategoryName = 'Seafood'
---------------------------------------------------------------------
--2.จงแสดงชื่อบริษัทลูกค้า ประเทศที่ลูกค้าอยู่ และจำนวนใบสั่งซื้อที่ลูกค้านั้น ๆ ที่รายการสั่งซื้อในปี 1997
--แบบ Product
SELECT CompanyName, Country, COUNT(OrderID) AS OrderCount FROM Customers C, Orders O 
WHERE C.CustomerID = O.CustomerID AND YEAR(O.OrderDate) = '1997' GROUP BY CompanyName, Country 
--แบบ Join
SELECT C.CompanyName, C.Country, COUNT(O.OrderID) AS OrderCount FROM Customers C
JOIN Orders O ON C.CustomerID = O.CustomerID
WHERE YEAR(OrderDate) = '1997'
GROUP BY C.CompanyName, C.Country

---------------------------------------------------------------------
--3. จงแสดงรหัสสินค้า ชื่อสินค้า ราคาต่อหน่วย ชื่อบริษัทและประเทศที่จัดจำหน่ายสินค้านั้น ๆ
--แบบ Product
SELECT P.ProductID, P.ProductName, P.UnitPrice, S.CompanyName, S.Country FROM Products P, Suppliers S WHERE P.SupplierID = S.SupplierID
--แบบ Join
SELECT P.ProductID, P.ProductName, P.UnitPrice, S.CompanyName, S.Country FROM Products P JOIN Suppliers S ON P.SupplierID = S.SupplierID

---------------------------------------------------------------------
--4. ชื่อ-นามสกุลของพนักงานขาย ตำแหน่งงาน และจำนวนใบสั่งซื้อที่แต่ละคนเป็นผู้ทำรายการขาย 
--เฉพาะที่ทำรายการขายช่วงเดือนมกราคม-เมษายน ปี 1997 และแสดงเฉพาะพนักงานที่ทำรายการขายมากกว่า 10 ใบสั่งซื้อ 
--แบบ Product
SELECT FirstName+SPACE(3)+LastName AS EmployeeName, Title, COUNT(OrderID) NumberOrders FROM Employees E, Orders O WHERE E.EmployeeID = O.EmployeeID AND OrderDate BETWEEN '1997-01-01' AND '1997-04-30' 
GROUP BY FirstName,LastName, Title
Having COUNT(OrderID) > 10
--แบบ Join
SELECT FirstName+SPACE(3)+LastName AS EmployeeName, Title, COUNT(OrderID) NumberOrders FROM Employees E JOIN Orders O ON E.EmployeeID = O.EmployeeID AND OrderDate BETWEEN '1997-01-01' AND '1997-04-30' 
GROUP BY FirstName,LastName, Title
Having COUNT(OrderID) > 10
---------------------------------------------------------------------
--5.จงแสดงรหัสสินค้า ชื่อสินค้า ยอดขายรวม(ไม่คิดส่วนลด) ของสินค้าแต่ละชนิด
--แบบ Product
SELECT P.ProductID, P.ProductName, SUM(OD.Quantity * OD.UnitPrice) Total FROM Products P, [Order Details] OD 
WHERE P.ProductID = OD.ProductID
GROUP BY P.ProductID, P.ProductName ORDER BY ProductID ASC
--แบบ Join
SELECT P.ProductID, P.ProductName, SUM(OD.Quantity * OD.UnitPrice) Total FROM Products P 
JOIN [Order Details] OD ON P.ProductID = OD.ProductID
GROUP BY P.ProductID, P.ProductName ORDER BY ProductID ASC
---------------------------------------------------------------------
/*6.จงแสดงรหัสบริษัทจัดส่ง ชื่อบริษัทจัดส่ง จำนวนใบสั่งซื้อที่จัดส่งไปยังประเทศสหรัฐอเมริกา, 
อิตาลี, สหราชอาณาจักร, แคนาดา ในเดือนมกราคม-สิงหาคม ปี 1997 */
--แบบ Product
SELECT ShipperID, CompanyName, COUNT(OrderID) OrderCount FROM Orders O, Shippers S
WHERE O.ShipVia = S.ShipperID AND ShipCountry IN ('USA', 'Italy','UK','Canada')
AND ShippedDate BETWEEN '1997-01-01' AND '1997-08-31'
GROUP BY ShipperID, CompanyName
--แบบ Join
SELECT ShipperID, CompanyName, COUNT(OrderID) OrderCount FROM Orders O JOIN Shippers S
ON O.ShipVia = S.ShipperID AND ShipCountry IN ('USA', 'Italy','UK','Canada')
AND ShippedDate BETWEEN '1997-01-01' AND '1997-08-31'
GROUP BY ShipperID, CompanyName

---------------------------------------------------------------------
-- *** 3 ตาราง ****
/*7 : จงแสดงเลขเดือน ยอดสั่งซื้อรวม(ไม่คิดส่วนลด) เฉพาะรายการสั่งซื้อที่ทำรายการขายในปี 1996 
และจัดส่งไปยังประเทศสหราชอาณาจักร,เบลเยี่ยม, โปรตุเกส ของพนักงานขายชื่อ nancy, Davolio*/
--แบบ Product
SELECT MONTH(O.OrderDate) Month_no, SUM(OD.Quantity*OD.UnitPrice) Total FROM Orders O, [Order Details] OD, Employees E 
WHERE O.OrderID = OD.OrderID AND O.EmployeeID = E.EmployeeID AND YEAR(O.OrderDate) = '1996'
AND E.FirstName = 'Nancy' AND E.LastName = 'Davolio' AND O.ShipCountry IN ('UK', 'Belgium', 'Portugal')
GROUP BY MONTH(O.OrderDate)
--แบบ Join
SELECT MONTH(O.OrderDate) Month_no, SUM(OD.Quantity*OD.UnitPrice) Total 
FROM Orders O INNER JOIN [Order Details] OD
ON O.OrderID = OD.OrderID INNER JOIN Employees E ON O.EmployeeID = E.EmployeeID
WHERE YEAR(O.OrderDate) = '1996'
AND E.FirstName = 'Nancy' AND E.LastName = 'Davolio' AND O.ShipCountry IN ('UK', 'Belgium', 'Portugal')
GROUP BY MONTH(O.OrderDate)
--------------------------------------------------------------------------------

/*8 : จงแสดงข้อมูลรหัสลูกค้า ชื่อบริษัทลูกค้า และยอดรวม(ไม่คิดส่วนลด) เฉพาะใบสั่งซื้อที่ทำรายการสั่งซื้อในเดือน มค. ปี 1997 
จัดเรียงข้อมูลตามยอดสั่งซื้อมากไปหาน้อย*/
--แบบ Product
SELECT C.CustomerID, C.CompanyName, SUM(OD.Quantity * OD.UnitPrice) Total FROM [Order Details] OD, Orders O, Customers C
WHERE OD.OrderID = O.OrderID AND O.CustomerID = C.CustomerID 
AND YEAR(O.ShippedDate) = '1997' AND MONTH(O.ShippedDate) = '1'
GROUP BY C.CustomerID, C.CompanyName
ORDER BY Total DESC;

--แบบ Join
SELECT C.CustomerID, C.CompanyName, SUM(OD.Quantity * OD.UnitPrice) Total FROM [Order Details] OD
INNER JOIN Orders O ON OD.OrderID = O.OrderID
INNER JOIN Customers C ON O.CustomerID = C.CustomerID 
AND YEAR(O.ShippedDate) = '1997' AND MONTH(O.ShippedDate) = '1'
GROUP BY C.CustomerID, C.CompanyName
ORDER BY Total DESC;
---------------------------------------------------------------------------------

/*9 : จงแสดงรหัสผู้จัดส่ง ชื่อบริษัทผู้จัดส่ง ยอดรวมค่าจัดส่ง เฉพาะรายการสั่งซื้อที่ Nancy Davolio เป็นผู้ทำรายการขาย*/
--แบบ Product
SELECT S.ShipperID, S.CompanyName, SUM(O.Freight) AS Freight FROM Employees E, Orders O, Shippers S
WHERE E.EmployeeID = O.EmployeeID AND O.ShipVia = S.ShipperID
AND E.FirstName = 'Nancy' AND E.LastName = 'Davolio'
GROUP BY S.ShipperID, S.CompanyName
--แบบ Join
SELECT S.ShipperID, S.CompanyName, SUM(O.Freight) AS Freight FROM Employees E
INNER JOIN Orders O ON E.EmployeeID = O.EmployeeID
INNER JOIN Shippers S ON S.ShipperID = O.ShipVia
WHERE E.FirstName = 'Nancy' AND E.LastName = 'Davolio'
GROUP BY S.ShipperID, S.CompanyName

---------------------------------------------------------------------------------
/*10 : จงแสดงข้อมูลรหัสใบสั่งซื้อ วันที่สั่งซื้อ รหัสลูกค้าที่สั่งซื้อ ประเทศที่จัดส่ง จำนวนที่สั่งซื้อทั้งหมด ของสินค้าชื่อ Tofu ในช่วงปี 1997*/
--แบบ Product
SELECT O.OrderID, O.OrderDate, O.CustomerID, O.ShipCountry, OD.Quantity AS TotalOrder 
FROM Products P, [Order Details] OD, Orders O
WHERE P.ProductID = OD.ProductID AND OD.OrderID = O.OrderID
AND P.ProductName = 'Tofu' AND YEAR(O.OrderDate) = '1997'
ORDER BY O.OrderID ASC;

--แบบ Join
SELECT O.OrderID, O.OrderDate, C.CompanyName, O.ShipCountry, OD.Quantity AS TotalOrder FROM Products P
INNER JOIN [Order Details] OD ON P.ProductID = OD.ProductID  
INNER JOIN Orders O ON OD.OrderID = O.OrderID
INNER JOIN Customers C ON O.CustomerID = C.CustomerID
AND P.ProductName = 'Tofu' AND YEAR(O.OrderDate) = '1997'
ORDER BY O.OrderID ASC;
-----------------------------------------------------------------------------
/*11 : จงแสดงข้อมูลรหัสสินค้า ชื่อสินค้า ยอดขายรวม(ไม่คิดส่วนลด) ของสินค้าแต่ละรายการเฉพาะที่มีการสั่งซื้อในเดือน มค.-สค. ปี 1997*/
--แบบ Product
SELECT P.ProductID, P.ProductName, SUM(OD.Quantity * OD.UnitPrice) AS TotalPrice 
FROM Products P, [Order Details] OD, Orders O
WHERE P.ProductID = OD.ProductID AND OD.OrderID = O.OrderID
AND O.OrderDate BETWEEN '1997-01-01' AND '1997-08-31'
GROUP BY P.ProductID, P.ProductName

--แบบ Join
SELECT P.ProductID, P.ProductName, SUM(OD.Quantity * OD.UnitPrice) AS TotalPrice FROM Products P
INNER JOIN [Order Details] OD ON P.ProductID = OD.ProductID
INNER JOIN Orders O ON OD.OrderID = O.OrderID
WHERE O.OrderDate BETWEEN '1997-01-01' AND '1997-08-31'
GROUP BY P.ProductID, P.ProductName
-----------------------------------------------------------------------------
-- *** 4 ตาราง ****
/*12 : จงแสดงข้อมูลรหัสประเภทสินค้า ชื่อประเภทสินค้า ยอดสั่งซื้อรวม(ไม่คิดส่วนลด) เฉพาะที่มีการจัดส่งไปประเทศสหรัฐอเมริกา ในปี 1997*/
--แบบ Product
SELECT C.CategoryID, C.CategoryName, SUM(OD.Quantity * OD.UnitPrice) TotalPrice
FROM Categories C, Products P, [Order Details] OD, Orders O
WHERE C.CategoryID = P.CategoryID AND P.ProductID = OD.ProductID AND OD.OrderID = O.OrderID
AND O.ShipCountry = 'USA' AND YEAR(O.ShippedDate) = 1997
GROUP BY C.CategoryID, C.CategoryName
--แบบ Join
SELECT C.CategoryID, C.CategoryName, SUM(OD.Quantity * OD.UnitPrice) TotalPrice FROM Categories C
INNER JOIN Products P ON C.CategoryID = P.CategoryID
INNER JOIN [Order Details] OD ON OD.ProductID = P.ProductID
INNER JOIN Orders O ON O.OrderID = OD.OrderID
WHERE O.ShipCountry = 'USA' AND YEAR(O.ShippedDate) = 1997
GROUP BY C.CategoryID, C.CategoryName
----------------------------------------------------------------------------
/*13 : จงแสดงรหัสพนักงาน ชื่อและนามสกุล(แสดงในคอลัมน์เดียวกัน) ยอดขายรวมของพนักงานแต่ละคน เฉพาะรายการขายที่จัดส่งโดยบริษัท Speedy Express 
ไปยังประเทศสหรัฐอเมริกา และทำการสั่งซื้อในปี 1997 */
--แบบ Product
SELECT E.EmployeeID, E.FirstName+SPACE(1)+E.LastName AS empName, SUM(OD.Quantity * OD.UnitPrice) SumPrice
FROM Employees E, [Order Details] OD, Orders O, Shippers S
WHERE E.EmployeeID = O.EmployeeID AND O.OrderID = OD.OrderID AND O.ShipVia = S.ShipperID
AND S.CompanyName = 'Speedy Express ' AND O.ShipCountry = 'USA' AND YEAR(O.OrderDate) = '1997'
GROUP BY E.EmployeeID, E.FirstName+SPACE(1)+E.LastName
ORDER BY EmployeeID
--แบบ Join
SELECT E.EmployeeID, E.FirstName+SPACE(1)+E.LastName AS empName, SUM(OD.Quantity * OD.UnitPrice) SumPrice 
FROM Employees E INNER JOIN Orders O ON E.EmployeeID = O.EmployeeID
INNER JOIN [Order Details] OD ON OD.OrderID = O.OrderID
INNER JOIN Shippers S ON S.ShipperID = O.ShipVia
WHERE S.CompanyName = 'Speedy Express ' AND O.ShipCountry = 'USA' AND YEAR(O.OrderDate) = '1997'
GROUP BY E.EmployeeID, E.FirstName, E.LastName
ORDER BY EmployeeID
--------------------------------------------------------------------------
/*14 : จงแสดงรหัสสินค้า ชื่อสินค้า ยอดขายรวม เฉพาะสินค้าที่นำมาจัดจำหน่ายจากประเทศญี่ปุ่น และมีการสั่งซื้อในปี 1997 และจัดส่งไปยังประเทศสหรัฐอเมริกา */
--แบบ Product
SELECT P.ProductID, P.ProductName, SUM(OD.Quantity * OD.UnitPrice) AS TotalPrice
FROM Products P, Suppliers S, [Order Details] OD, Orders O
WHERE P.SupplierID = S.SupplierID AND P.ProductID = OD.ProductID AND OD.OrderID = O.OrderID
AND S.Country = 'Japan' AND YEAR(O.OrderDate) = 1997 AND O.ShipCountry = 'USA'
GROUP BY P.ProductID, P.ProductName
--แบบ Join
SELECT P.ProductID, P.ProductName, SUM(OD.Quantity * OD.UnitPrice) AS TotalPrice FROM Products P
JOIN Suppliers S ON P.SupplierID = S.SupplierID
JOIN [Order Details] OD ON P.ProductID = OD.ProductID
JOIN Orders O ON OD.OrderID = O.OrderID
WHERE S.Country = 'Japan' AND YEAR(O.OrderDate) = 1997 AND O.ShipCountry = 'USA'
GROUP BY P.ProductID, P.ProductName
----------------------------------------------------------------------------
-- *** 5 ตาราง ***
/*15 : จงแสดงรหัสลูกค้า ชื่อบริษัทลูกค้า ยอดสั่งซื้อรวมของการสั่งซื้อสินค้าประเภท Beverages ของลูกค้าแต่ละบริษัท  และสั่งซื้อในปี 1997 จัดเรียงตามยอดสั่งซื้อจากมากไปหาน้อย*/
--แบบ Product
SELECT C.CustomerID, C.CompanyName, SUM(OD.Quantity * OD.UnitPrice) AS TotalPrice
FROM Customers C, Orders O, [Order Details] OD, Products P, Categories CA
WHERE C.CustomerID = O.CustomerID AND O.OrderID = OD.OrderID AND OD.ProductID = P.ProductID AND P.CategoryID = CA.CategoryID
AND CA.CategoryName = 'Beverages' AND YEAR(O.OrderDate) = 1997
GROUP BY C.CustomerID, C.CompanyName
ORDER BY TotalPrice DESC
--แบบ Join
SELECT C.CustomerID, C.CompanyName, SUM(OD.Quantity * OD.UnitPrice) AS TotalPrice FROM Customers C
JOIN Orders O ON C.CustomerID = O.CustomerID
JOIN [Order Details] OD ON O.OrderID = OD.OrderID
JOIN Products P ON OD.ProductID = P.ProductID
JOIN Categories CA ON P.CategoryID = CA.CategoryID
WHERE CA.CategoryName = 'Beverages' AND YEAR(O.OrderDate) = 1997
GROUP BY C.CustomerID, C.CompanyName
ORDER BY TotalPrice DESC

---------------------------------------------------------------------------
/*16 : จงแสดงรหัสผู้จัดส่ง ชื่อบริษัทที่จัดส่ง จำนวนใบสั่งซื้อที่จัดส่งสินค้าประเภท Seafood ไปยังประเทศสหรัฐอเมริกา ในปี 1997 */
--แบบ Product
SELECT S.ShipperID, S.CompanyName, COUNT(O.OrderID) AS OrderCount
FROM Shippers S, Orders O, [Order Details] OD, Products P, Categories C
WHERE S.ShipperID = O.ShipVia AND O.OrderID = OD.OrderID AND OD.ProductID = P.ProductID AND P.CategoryID = C.CategoryID
AND C.CategoryName = 'Seafood' AND O.ShipCountry = 'USA' AND YEAR(O.OrderDate) = 1997
GROUP BY S.ShipperID, S.CompanyName

--แบบ Join
SELECT S.ShipperID, S.CompanyName, COUNT(O.OrderID) AS OrderCount FROM Shippers S
JOIN Orders O ON S.ShipperID = O.ShipVia
JOIN [Order Details] OD ON O.OrderID = OD.OrderID
JOIN Products P ON OD.ProductID = P.ProductID
JOIN Categories C ON P.CategoryID = C.CategoryID
WHERE C.CategoryName = 'Seafood' AND O.ShipCountry = 'USA' AND YEAR(O.OrderDate) = 1997
GROUP BY S.ShipperID, S.CompanyName

---------------------------------------------------------------------------
-- *** 6 ตาราง ***
/*17 : จงแสดงรหัสประเภทสินค้า ชื่อประเภท ยอดสั่งซื้อรวม(ไม่คิดส่วนลด) ที่ทำรายการขายโดย Margaret Peacock ในปี 1997 
และสั่งซื้อโดยลูกค้าที่อาศัยอยู่ในประเทศสหรัฐอเมริกา สหราชอาณาจักร แคนาดา */

--แบบ Product
SELECT CA.CategoryID, CA.CategoryName, SUM(OD.Quantity * OD.UnitPrice) AS TotalPrice
FROM Categories CA, Products P, [Order Details] OD, Orders O, Employees E, Customers C
WHERE CA.CategoryID = P.CategoryID AND P.ProductID = OD.ProductID AND OD.OrderID = O.OrderID
AND O.EmployeeID = E.EmployeeID AND O.CustomerID = C.CustomerID
AND E.FirstName = 'Margaret' AND E.LastName = 'Peacock'
AND C.Country IN ('USA', 'UK', 'Canada')
GROUP BY CA.CategoryID, CA.CategoryName

--แบบ Join
SELECT CA.CategoryID, CA.CategoryName, SUM(OD.Quantity * OD.UnitPrice) AS TotalPrice FROM Categories CA
JOIN Products P ON CA.CategoryID = P.CategoryID
JOIN [Order Details] OD ON P.ProductID = OD.ProductID
JOIN Orders O ON OD.OrderID = O.OrderID
JOIN Employees E ON O.EmployeeID = E.EmployeeID
JOIN Customers C ON O.CustomerID = C.CustomerID
WHERE E.FirstName = 'Margaret' AND E.LastName = 'Peacock'
AND C.Country IN ('USA', 'UK', 'Canada')
GROUP BY CA.CategoryID, CA.CategoryName

---------------------------------------------------------------------------
/*18 : จงแสดงรหัสสินค้า ชื่อสินค้า ยอดสั่งซื้อรวม(ไม่คิดส่วนลด) ของสินค้าที่จัดจำหน่ายโดยบริษัทที่อยู่ประเทศสหรัฐอเมริกา ที่มีการสั่งซื้อในปี 1997 
จากลูกค้าที่อาศัยอยู่ในประเทศสหรัฐอเมริกา และทำการขายโดยพนักงานที่อาศัยอยู่ในประเทศสหรัฐอเมริกา */

--แบบ Product
SELECT P.ProductID, P.ProductName, SUM(OD.Quantity * OD.UnitPrice) AS TotalPrice
FROM Products P, Suppliers S, [Order Details] OD, Orders O, Customers C, Employees E
WHERE P.SupplierID = S.SupplierID AND P.ProductID = OD.ProductID AND OD.OrderID = O.OrderID
AND O.CustomerID = C.CustomerID AND O.EmployeeID = E.EmployeeID
AND S.Country = 'USA' AND YEAR(O.OrderDate) = '1997'
AND C.Country = 'USA' AND E.Country = 'USA'
GROUP BY P.ProductID, P.ProductName

--แบบ Join
SELECT P.ProductID, P.ProductName, SUM(OD.Quantity * OD.UnitPrice) AS TotalPrice FROM Products P
JOIN Suppliers S ON P.SupplierID = S.SupplierID
JOIN [Order Details] OD ON P.ProductID = OD.ProductID
JOIN Orders O ON OD.OrderID = O.OrderID
JOIN Customers C ON O.CustomerID = C.CustomerID
JOIN Employees E ON O.EmployeeID = E.EmployeeID
WHERE S.Country = 'USA' AND YEAR(O.OrderDate) = '1997'
AND C.Country = 'USA' AND E.Country = 'USA'
GROUP BY P.ProductID, P.ProductName
