# taller-slq-y-power-bi
--1
create view empleados_mark_1 as
select  FirstName,LastName from [Person].[Person] where FirstName='Mark'

--2
create view numero_empleados_2 as
select count(*) as 'Numero de empleados' from [Person].[Person]
--3
create view primeras_100filas_3 as
select top(100)* from [Production].[Product] where ListPrice <> 0
--4
create view apellidos_letra_inferior_a_D_4 as
select * from [HumanResources].[vEmployee] where LastName like '[a-d]%'
--5
create view promedio_standardcost_5 as
select Name,avg(StandardCost) from Production.Product where StandardCost>0 GROUP BY Name
--6
create view Ejercicio_6 as
select PersonType, count(*) from Person.Person group by PersonType
--7
create view Ejercicio_7 as
select * from Person.StateProvince where CountryRegionCode='CA' 
--8
create view Ejercicio_8 as
select color, count(*) as Productos from [Production].[Product] where Color = 'black' OR Color = 'red' group by Color
--9.	¿Cuál es el valor promedio de Freight por cada venta? 
create view Ejercicio_9_1 as
SELECT TerritoryID,SalesOrderID, AVG(Freight) AS Promedio  FROM [Sales].[SalesOrderHeader] GROUP BY TerritoryID,SalesOrderID
--(Sales.SalesOrderHeader) donde la venta se dio en el TerriotryID 4?
create view Ejercicio_9_2 as
SELECT TerritoryID,SalesOrderID, AVG(Freight) AS Promedio FROM [Sales].[SalesOrderHeader] where TerritoryID=4 GROUP BY TerritoryID,SalesOrderID
--10
create view Ejercicio_10 as
select * from Sales.vIndividualCustomer WHERE (LastName = 'Lopez' OR LastName = 'Martin' OR LastName = 'Wood') AND (FirstName LIKE '[c-l]%')
--11
create view Ejercicio_11 as
SELECT FirstName as PrimerNombre, LastName as Apellido FROM [Sales].[vIndividualCustomer] WHERE LastName = 'Smith'
--12
create view Ejercicio_12 as
SELECT *  FROM [Sales].[vIndividualCustomer] WHERE (CountryRegionName = 'Australia') OR (PhoneNumberType='Cell' AND EmailPromotion = 0)
--13
create view Ejercicio_13 as
select max(ListPrice) as 'precio más caro'from Production.Product
--14
create view Ejercicio_14 as
SELECT [TerritoryID], SUM(TotalDue) AS Ventas FROM [Sales].[SalesOrderHeader] GROUP BY TerritoryID HAVING SUM(TotalDue) >= 10000000
--15
create view Ejercicio_15 as
SELECT S.Name, SUM(O.TotalDue) AS Ventas
  FROM [Sales].[SalesOrderHeader] as O
  JOIN [Sales].[SalesTerritory] as S
  ON S.TerritoryID = O.TerritoryID
  GROUP BY S.Name
  HAVING SUM(TotalDue) >= 10000000
--16
--primera
create view Ejercicio_16_1 as
SELECT *
  FROM [HumanResources].[vEmployeeDepartment]
  WHERE Department = 'Executive' OR Department = 'Tool Design' OR Department = 'Engineering'
--segunda  
create view Ejercicio_16_2 as
SELECT *
  FROM [HumanResources].[vEmployeeDepartment]
  WHERE Department LIKE 'Executive' OR Department LIKE 'Engineering' OR Department LIKE 'Tool Design'
--17
--primera
create view Ejercicio_17_1 as
SELECT *
  FROM [HumanResources].[vEmployeeDepartment]
  WHERE StartDate BETWEEN '2000-07-01' AND '2002-06-30'
--segunda  
create view Ejercicio_17_2 as
SELECT *
  FROM [HumanResources].[vEmployeeDepartment]
  WHERE StartDate >= '2000-07-01' AND StartDate <= '2002-06-30'
--18
create view Ejercicio_18 as
SELECT *
  FROM [Sales].[SalesOrderHeader]
  WHERE SalesPersonID >= 0
--19
create view Ejercicio_19 as
SELECT COUNT(*) AS NotNULL
  FROM [Person].[Person]
  WHERE MiddleName IS NOT NULL
--20
create view Ejercicio_20 as
SELECT SalesPersonID, TotalDue
  FROM [Sales].[SalesOrderHeader]
  WHERE SalesPersonID IS NOT NULL AND TotalDue > 70000
--21
create view Ejercicio_21 as
  SELECT *
  FROM [Sales].[vIndividualCustomer]
  WHERE LastName LIKE '[R]%'
 --22
 create view Ejercicio_22 as
 SELECT *
  FROM [Sales].[vIndividualCustomer]
  WHERE LastName LIKE '%r'
--23
create view Ejercicio_23 as
SELECT Color, COUNT(*) AS Productos
  FROM [Production].[Product]
  WHERE COLOR IS NOT NULL
  GROUP BY color
  HAVING COUNT(Color) >=20
 --24
 create view Ejercicio_24 as
 SELECT SUM(i.Quantity * p.ListPrice) AS Ganancia
  FROM [Production].[Product] as p
  JOIN [Production].[ProductInventory] as i
  ON p.ProductID = i.ProductID
  WHERE p.ListPrice > 0
--25
create view Ejercicio_25 as
SELECT [FirstName], [LastName], EmailPromotion =
	CASE
		WHEN EmailPromotion = 0 then 'Promo 1'
		WHEN EmailPromotion = 1 then 'Promo 2'
		WHEN EmailPromotion = 2 then 'Promo 3'
	END
  FROM [Person].[Person]
--26
create view Ejercicio_26 as
SELECT t.Name, p.[BusinessEntityID], p.[SalesYTD]
  FROM [Sales].[SalesPerson] as p
  LEFT JOIN [Sales].[SalesTerritory] as t
  ON p.TerritoryID = t.TerritoryID
--27
create view Ejercicio_27 as
SELECT pe.FirstName,pe.LastName,t.Name, p.[BusinessEntityID], p.[SalesYTD]
  FROM [Sales].[SalesPerson] as p
  LEFT JOIN [Sales].[SalesTerritory] as t
  ON p.TerritoryID = t.TerritoryID
  JOIN Person.Person as pe
  ON p.BusinessEntityID = pe.BusinessEntityID
  WHERE t.Name = 'Northeast' or t.Name = 'Central'
  --28
  create view Ejercicio_28 as
  SELECT p.FirstName, p.LastName, pa.PasswordHash
  FROM [Person].[Person] as p
  JOIN Person.Password as pa
  ON p.BusinessEntityID = pa.BusinessEntityID
--29
create view Ejercicio_29 as
SELECT FirstName,title =
	CASE
		WHEN Title IS NULL then 'No hay titulo'
		WHEN Title IS NOT NULL then Title
	END
  FROM [Person].[Person]
--30
create view Ejercicio_30 as
SELECT FirstName,MiddleName =
	CASE
		WHEN MiddleName IS NULL then CONCAT(FirstName, ' ', LastName)
		WHEN MiddleName IS NOT NULL then CONCAT(FirstName, ' ', MiddleName, ' ', LastName)
	END
  FROM [Person].[Person]
--31
create view Ejercicio_31 as
SELECT [ProductID], MakeFlag =
	CASE
		WHEN MakeFlag = FinishedGoodsFlag then NULL
		WHEN NOT MakeFlag = FinishedGoodsFlag then 'Iguales'
	END
  FROM [Production].[Product]
--32
create view Ejercicio_32 as
SELECT [ProductID], Color =
	CASE
		WHEN Color IS NOT NULL then Color
		WHEN Color IS NULL then 'Sin color'
	END
  FROM [Production].[Product]
SELECT ProductID, ISNULL(Color, 'Sin color')
  FROM [Production].[Product]
