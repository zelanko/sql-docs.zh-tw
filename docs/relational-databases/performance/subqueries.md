---
title: 子查詢 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/18/2018
ms.prod: sql
ms.technology: performance
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Subquery
- Subqueries
- subqueries [SQL Server], fundamentals
- subqueries [SQL Server], correlated
- subqueries [SQL Server], types
ms.assetid: bfc97432-c14c-4768-9dc5-a9c512f6b2bd
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 07d8b7936051b202c73b7457c87e7533e1d46192
ms.sourcegitcommit: 0b0f5aba602732834c8439c192d95921149ab4c3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2019
ms.locfileid: "67500225"
---
# <a name="subqueries-sql-server"></a>子查詢 (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 
子查詢是指巢狀於 `SELECT`、`INSERT`、`UPDATE` 或 `DELETE` 陳述式中，或巢狀於另一個子查詢中的查詢。 子查詢允許在運算式的任何位置使用。 在此範例中，子查詢將在 SELECT 陳述式中，作為名為 MaxUnitPrice 的資料行運算式使用。

```sql
USE AdventureWorks2016;
GO
SELECT Ord.SalesOrderID, Ord.OrderDate,
    (SELECT MAX(OrdDet.UnitPrice)
     FROM Sales.SalesOrderDetail AS OrdDet
     WHERE Ord.SalesOrderID = OrdDet.SalesOrderID) AS MaxUnitPrice
FROM Sales.SalesOrderHeader AS Ord;
GO
```

## <a name="fundamentals"></a> 子查詢基本概念
子查詢也稱為內部查詢或內部選取，而包含子查詢的陳述式又稱為外部查詢或外部選取。   

許多包含子查詢的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式也可以構成聯結。 其他的問題也只能以子查詢提出。 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中，包含子查詢的陳述式與語意上相等版本之間的效能，通常沒有差異。 然而，在某些必須檢查存在性的情況下，聯結將可產生更好的效能。 否則，必須針對外部查詢的每個結果來處理巢狀查詢，以確保能消除重複性。 在這樣的情況下，聯結方法將會產生更好的結果。 下列範例顯示可傳回相同結果集的子查詢 `SELECT` 及聯結 `SELECT`：

```sql
USE AdventureWorks2016;
GO

/* SELECT statement built using a subquery. */
SELECT Name
FROM Production.Product
WHERE ListPrice =
    (SELECT ListPrice
     FROM Production.Product
     WHERE Name = 'Chainring Bolts' );
GO

/* SELECT statement built using a join that returns
   the same result set. */
SELECT Prd1. Name
FROM Production.Product AS Prd1
     JOIN Production.Product AS Prd2
       ON (Prd1.ListPrice = Prd2.ListPrice)
WHERE Prd2. Name = 'Chainring Bolts';
GO
```

外部 SELECT 陳述式中的巢狀子查詢擁有下列元件：    
-   包含一般選取清單元件的一般 `SELECT` 查詢。   
-   包含一或多個資料表或檢視名稱的一般 `FROM` 子句。   
-   選擇性的 `WHERE` 子句。   
-   選擇性的 `GROUP BY` 子句。   
-   選擇性的 `HAVING` 子句。   

子查詢的 SELECT 查詢永遠都會以括號括住。 它無法包含 `COMPUTE` 或 `FOR BROWSE` 子句，而且在未指定 TOP 子句時，只能包含 `ORDER BY` 子句。   

子查詢能巢狀於外部 `SELECT`、`INSERT`、`UPDATE` 或 `DELETE` 陳述式的 `WHERE` 或 `HAVING` 子句中，或是巢狀於另一個子查詢中。 巢狀層級最多可達 32 層，不過此限制仍將取決於可用的記憶體，以及查詢中其他運算式的複雜性。 個別的查詢可能無法支援 32 層的巢狀。 若子查詢傳回單一數值的話，它將可出現在能夠使用運算式的任何位置。   

如果資料表只出現在子查詢中，而沒有出現在外部查詢裡面，那麼該資料表的資料行並不能包含於輸出之中 (外部查詢的選取清單)。   

包含子查詢的陳述式通常會採用下列格式之一：   
-   WHERE 運算式 \[NOT] IN (子查詢)
-   WHERE 運算式 comparison_operator \[ANY | ALL] (子查詢)
-   WHERE \[NOT] EXISTS (子查詢)   

在某些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中，可以像獨立查詢一樣評估子查詢。 在概念上，子查詢的結果會替代至外部查詢中 (雖然這不一定是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 實際上處理具子查詢之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的方法)。    

子查詢有三種基本類型。 分別為： 
-   運作於以 `IN` 導入的清單，或是以 `ANY` 或 `ALL` 所修改之比較運算子的子查詢。
-   以未修改的比較運算子提出，並且必須傳回單一數值。
-   為 `EXISTS` 所提出之存在測試的子查詢。

## <a name="rules"></a> 子查詢規則
子查詢具有下列限制： 
-   以比較運算子所提出之子查詢選取清單，只能包含一個運算式或資料行名稱 (除了分別運作於 `SELECT *` 或清單上的 `EXISTS` 與 `IN`)。   
-   若外部查詢的 `WHERE` 子句包含資料行名稱，它必須與子查詢選取清單中的資料行具有聯結相容性。   
-   **ntext**、**text** 及 **image** 資料類型無法在子查詢的選取清單中使用。   
-   因為它們必須傳回單一數值，因此由未修改的比較運算子 (也就是後面沒有跟著關鍵字 ANY 或 ALL) 所提出的子查詢不能包含 `GROUP BY` 與 `HAVING` 子句。   
-   在包含 GROUP BY 的子查詢內，不能使用 `DISTINCT` 關鍵字。
-   不能指定 `COMPUTE` 和 `INTO` 子句。   
-   只有在同時指定 `TOP` 的情況下，才能指定 `ORDER BY`。   
-   不能更新以子查詢建立的檢視。   
-   `EXISTS` 所導入之子查詢的選取清單，依慣例會有星號 (\*)，而非單一資料行名稱。 `EXISTS` 所導入之子查詢的規則和適用於標準選取清單的規則一樣，因為由 `EXISTS` 所導入的子查詢會建立存在測試並傳回 TRUE 或 FALSE，而不是傳回資料。   

## <a name="qualifying"></a> 在子查詢中識別資料行名稱
在以下的範例中，外部查詢之 `WHERE` 子句的 *BusinessEntityID* 資料行會由外部查詢 `FROM` 子句中的資料表名稱 (*Sales.Store*) 進行隱含限定。 在子查詢的選取清單中針對 *CustomerID* 的參考會被子查詢 `FROM` 子句限定，也就是被 *Sales.Customer* 資料表所限定。

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Sales.Store
WHERE BusinessEntityID NOT IN
    (SELECT CustomerID
     FROM Sales.Customer
     WHERE TerritoryID = 5);
GO
```

一般規則為陳述式的資料行名稱會由相同層級之 `FROM` 子句所參考的資料表進行隱含限定。 如果資料行沒有存在於由子查詢之 `FROM` 子句所參考的資料表中，則它會由外部查詢之 `FROM` 子句所所參考的資料表進行隱含限定。   

以下為這些隱含假設下的查詢樣本：

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Sales.Store
WHERE Sales.Store.BusinessEntityID NOT IN
    (SELECT Sales.Customer.CustomerID
     FROM Sales.Customer
     WHERE TerritoryID = 5);
GO
```

以外顯方式來敘述資料表名稱絕對不會錯，而且一定可以使用外顯的限定來覆寫隱含假設的資料表名稱。   

> [!IMPORTANT]
> 如果資料行被不存在於由子查詢的 `FROM` 子句所參考之資料表中的子查詢所參考，但存在於由外部查詢之 `FROM` 子句所參考的資料表中，則查詢會在沒有錯誤之下執行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會以外部查詢中的資料表名稱，對子查詢中的資料行進行隱含限定。   

## <a name="nesting"></a> 多重巢狀層級
子查詢本身可包含一或多個子查詢。 可以將任意個數的子查詢套疊 (Nested) 於陳述式中。   

下列查詢會找出兼具銷售人員身分的員工名稱。   

```sql
USE AdventureWorks2016;
GO
SELECT LastName, FirstName
FROM Person.Person
WHERE BusinessEntityID IN
    (SELECT BusinessEntityID
     FROM HumanResources.Employee
     WHERE BusinessEntityID IN
        (SELECT BusinessEntityID
         FROM Sales.SalesPerson)
    );
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
LastName                                           FirstName
-------------------------------------------------- -----------------------
Jiang                                              Stephen
Abbas                                              Syed
Alberts                                            Amy
Ansman-Wolfe                                       Pamela
Campbell                                           David
Carson                                             Jillian
Ito                                                Shu
Mitchell                                           Linda
Reiter                                             Tsvi
Saraiva                                            Jos
Vargas                                             Garrett
Varkey Chudukatil                                  Ranjit
Valdez                                             Rachel
Tsoflias                                           Lynn
Pak                                                Jae
Blythe                                             Michael
Mensa-Annan                                        Tete

(17 row(s) affected)
```

最內層的查詢將傳回銷售人員識別碼。 緊接的上一層查詢將以這些銷售人員識別碼來運算，並傳回這些員工的連絡識別碼。 最後，外層的查詢將使用連絡識別碼來找出員工名稱。   

您也可以將此查詢表現成聯結 (Join)：

```sql
USE AdventureWorks2016;
GO
SELECT LastName, FirstName
FROM Person.Person c
INNER JOIN HumanResources.Employee e
ON c.BusinessEntityID = e.BusinessEntityID
JOIN Sales.SalesPerson s 
ON e.BusinessEntityID = s.BusinessEntityID;
GO
```

## <a name="correlated"></a> 相互關聯的子查詢
許多查詢都可藉由單次執行子查詢，並將所產生的值替換至外部查詢的 `WHERE` 子句來進行評估。 在包含相互關聯子查詢的查詢中 (也就是重複的子查詢)，子查詢值將取決於外部查詢。 這代表子查詢將重複執行，每個可能會被外部查詢所選取的資料列都執行一次。
這個查詢會針對在 *SalesPerson* 資料表中獎金為 5000，且員工識別碼在 *Employee* 和 *SalesPerson* 資料表中都相符的每個員工，擷取一份他們的名字和姓氏。

```sql
USE AdventureWorks2016;
GO
SELECT DISTINCT c.LastName, c.FirstName, e.BusinessEntityID 
FROM Person.Person AS c JOIN HumanResources.Employee AS e
ON e.BusinessEntityID = c.BusinessEntityID 
WHERE 5000.00 IN
    (SELECT Bonus
    FROM Sales.SalesPerson sp
    WHERE e.BusinessEntityID = sp.BusinessEntityID) ;
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
LastName FirstName BusinessEntityID
-------------------------- ---------- ------------
Ansman-Wolfe Pamela 280
Saraiva José 282

(2 row(s) affected)
```

這個陳述式中先前的子查詢無法在外部查詢之外獨立評估。 它需要 *Employee.BusinessEntityID* 的值，但此值會隨著 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 檢查 *Employee* 中不同的資料列時變更。   
而那就是評估此查詢的確切方式：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會藉由將每個資料列的數值替代至內部查詢中，來考慮是否要將 Employee 資料表的個別資料列包含在結果之中。
例如，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 先檢查 `Syed Abbas` 的資料列，則變數 *Employee.BusinessEntityID* 會採用值 285，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會將它替代至內部查詢中。

```sql
USE AdventureWorks2016;
GO
SELECT Bonus
FROM Sales.SalesPerson
WHERE BusinessEntityID = 285;
GO
```

結果為 0 (因為 `Syed Abbas` 不是業務人員，所以未收到任何獎金)，因此外部查詢會評估為：

```sql
USE AdventureWorks2016;
GO
SELECT LastName, FirstName
FROM Person.Person AS c JOIN HumanResources.Employee AS e
ON e.BusinessEntityID = c.BusinessEntityID 
WHERE 5000 IN (0.00);
GO
```

因為此結果為 false，`Syed Abbas` 的資料列將不會包含於結果之中。 針對 `Pamela Ansman-Wolfe` 的資料列進行相同的程序。 您將會在結果中看到包含這個資料列。     

藉由將外部查詢中之資料表的資料行參考為資料表值函式的引數，相互關聯的子查詢也可以將資料表值函式包含在 `FROM` 子句中。 在上述情形中，針對外部查詢的每個資料列，會根據子查詢估算資料表值函式。    
  
## <a name="types"></a> 子查詢類型
您可以在許多地方使用子查詢： 
-   搭配別名使用。 如需詳細資訊，請參閱[使用別名的子查詢](#aliases)。
-   搭配 `IN` 或 `NOT IN`。 如需詳細資訊，請參閱[使用 IN 的子查詢](#in)和[使用 NOT IN 的子查詢](#notin)。
-   在 `UPDATE`、`DELETE` 和 `INSERT` 陳述式中。 如需詳細資訊，請參閱 [UPDATE、DELETE 與 INSERT 陳述式中的子查詢](#upsert)。
-   搭配比較運算子使用。 如需詳細資訊，請參閱[使用比較運算子的子查詢](#comparison)。
-   搭配 `ANY`、`SOME` 或 `ALL`。 如需詳細資訊，請參閱 [ANY、SOME 或 ALL 修改的比較運算子](#comparison_modified)。
-   搭配 `EXISTS` 或 `NOT EXISTS`。 如需詳細資訊，請參閱[使用 EXISTS 的子查詢](#exists)和[使用 NOT EXISTS 的子查詢](#notexists)。
-   取代運算式。 如需詳細資訊，請參閱[用來取代運算式的子查詢](#expression)。

### <a name="aliases"></a> 使用別名的子查詢
若陳述式中的子查詢與外部查詢都參考到相同的資料表，這些陳述式將可敘述成自我聯結 (將資料表聯結至本身)。 例如，您可以使用子查詢從特定狀態尋找員工的地址。   

```sql
USE AdventureWorks2016;
GO
SELECT StateProvinceID, AddressID
FROM Person.Address
WHERE AddressID IN
    (SELECT AddressID
     FROM Person.Address
     WHERE StateProvinceID = 39);
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  

```
StateProvinceID AddressID
----------- -----------
39 942
39 955
39 972
39 22660

(4 row(s) affected)
```   

您也可以使用自我聯結：   

```sql
USE AdventureWorks2016;
GO
SELECT e1.StateProvinceID, e1.AddressID
FROM Person.Address AS e1
INNER JOIN Person.Address AS e2
ON e1.AddressID = e2.AddressID
AND e2.StateProvinceID = 39;
GO
```

資料表別名是必要的，因為聯結至本身的資料表將出現在兩個不同的角色上。 別名也可用於參考到內部與外部查詢中的同一個資料表的巢狀查詢之中。    

```sql
USE AdventureWorks2016;
GO
SELECT e1.StateProvinceID, e1.AddressID
FROM Person.Address AS e1
WHERE e1.AddressID IN
    (SELECT e2.AddressID
     FROM Person.Address AS e2
     WHERE e2.StateProvinceID = 39);
GO
```

明確別名可清楚表示參考到子查詢中的 *Person.Address* 與外部查詢中參考的意義並不相同。   

### <a name="in"></a> 使用 IN 的子查詢
以 `IN` (或 `NOT IN`) 導入的子查詢結果，為零個或多個值的清單。 當子查詢傳回結果之後，外部查詢將會使用這些傳回結果。    
下列查詢會找到 Adventure Works Cycles 所製造之所有滾輪產品的名稱。     

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID IN
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Wheels');
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]     

```
Name
----------------------------
LL Mountain Front Wheel
ML Mountain Front Wheel
HL Mountain Front Wheel
LL Road Front Wheel
ML Road Front Wheel
HL Road Front Wheel
Touring Front Wheel
LL Mountain Rear Wheel
ML Mountain Rear Wheel
HL Mountain Rear Wheel
LL Road Rear Wheel
ML Road Rear Wheel
HL Road Rear Wheel
Touring Rear Wheel

(14 row(s) affected)
```

此陳述式將以兩個步驟來進行運算。 首先，內部查詢傳回與 'Wheel' (17) 名稱相符的子類別目錄識別碼。 接著，此數值將替代至外部查詢中，該查詢會在 Product 中找出具有子類別目錄識別碼的產品名稱。     

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID IN ('17');
GO
```

在這個相似的問題中，使用聯結 (Join) 而非子查詢的差別在於，聯結可讓您在結果中顯示多個資料表的資料行。 例如，若您想要在結果中包含產品子類別目錄的名稱，必須使用聯結的版本。    

```sql
USE AdventureWorks2016;
GO
SELECT p.Name, s.Name
FROM Production.Product p
INNER JOIN Production.ProductSubcategory s
ON p.ProductSubcategoryID = s.ProductSubcategoryID
AND s.Name = 'Wheels';
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]    

```
Name
LL Mountain Front Wheel Wheels
ML Mountain Front Wheel Wheels
HL Mountain Front Wheel Wheels
LL Road Front Wheel Wheels
ML Road Front Wheel Wheels
HL Road Front Wheel Wheels
Touring Front Wheel Wheels
LL Mountain Rear Wheel Wheels
ML Mountain Rear Wheel Wheels
HL Mountain Rear Wheel Wheels
LL Road Rear Wheel Wheels
ML Road Rear Wheel Wheels
HL Road Rear Wheel Wheels
Touring Rear Wheel Wheels

(14 row(s) affected)
```    

下列查詢會尋找信用評比為優良、Adventure Works Cycles 向其訂購至少 20 項物件，且其訂貨到交貨時間少於 16 天的所有廠商名稱。    

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Purchasing.Vendor
WHERE CreditRating = 1
AND BusinessEntityID IN
    (SELECT BusinessEntityID
     FROM Purchasing.ProductVendor
     WHERE MinOrderQty >= 20
     AND AverageLeadTime < 16);
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
Name
--------------------------------------------------
Compete Enterprises, Inc
International Trek Center
First National Sport Co.
Comfort Road Bicycles
Circuit Cycles
First Rate Bicycles
Jeff's Sporting Goods
Competition Bike Training Systems
Electronic Bike Repair & Supplies
Crowley Sport
Expert Bike Co
Team Athletic Co.
Compete, Inc.   

(13 row(s) affected)
```   

內部查詢進行運算後，會產生符合子查詢資格的廠商識別碼。 外部查詢然後再進行運算。 請注意，您可在內部與外部查詢的 WHERE 子句中包含多個條件。   

透過聯結的使用，上面的查詢可以下列形式來表示：

```sql
USE AdventureWorks2016;
GO
SELECT DISTINCT Name
FROM Purchasing.Vendor v
INNER JOIN Purchasing.ProductVendor p
ON v.BusinessEntityID = p.BusinessEntityID
WHERE CreditRating = 1
  AND MinOrderQty >= 20
  AND AverageLeadTime < 16;
GO
```

聯結總是表示為子查詢。 子查詢通常 (但並非一定) 表示為聯結。 這是因為聯結是對稱的：您可以用任一種順序來聯結 A 與 B，最後答案都是一樣的。 若是包含子查詢，則得到的答案不一定相同。    

### <a name="notin"></a> 使用 NOT IN 的子查詢
NOT IN 關鍵字所提出的子查詢也會傳回零或多個數值的清單。   
下列查詢會尋找不是已完工自行車的產品名稱。   

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID NOT IN
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Mountain Bikes' 
        OR Name = 'Road Bikes'
        OR Name = 'Touring Bikes');
GO
```

此陳述式不能轉換成聯結。 類似的不相等聯結則具有不同意義：它會在其他不屬於已完工自行車的部分子類別中，尋找產品名稱。      

### <a name="upsert"></a> UPDATE、DELETE 與 INSERT 陳述式中的子查詢
子查詢可以巢狀於 `UPDATE`、`DELETE`、`INSERT` 和 `SELECT` 資料操作 (DML) 陳述式中。    

下列範例將 *Production.Product*資料表中 *ListPrice* 資料行的值加倍。 `WHERE` 子句中的子查詢會參考 *Purchasing.ProductVendor* 資料表，以將在 *Product* 資料表中更新的資料列限制為由 *BusinessEntity* 1540 所供應的資料列。

```sql
USE AdventureWorks2016;
GO 
UPDATE Production.Product
SET ListPrice = ListPrice * 2
WHERE ProductID IN
    (SELECT ProductID 
     FROM Purchasing.ProductVendor
     WHERE BusinessEntityID = 1540);
GO
```

下列為使用聯結的相等 `UPDATE` 陳述式：

```sql
USE AdventureWorks2016;
GO 
UPDATE Production.Product
SET ListPrice = ListPrice * 2
FROM Production.Product AS p
INNER JOIN Purchasing.ProductVendor AS pv
    ON p.ProductID = pv.ProductID AND BusinessEntityID = 1540;
GO   
```

### <a name="comparison"></a> 使用比較運算子的子查詢
可以使用其中一個比較運算子 (=、< >、>、> =、<、! >、! < 或 < =)。   

以未修改的比較運算子 (後面未跟著 `ANY` 或 `ALL` 的比較運算子) 導入的子查詢必須傳回單一值，而不是值清單，就像 `IN` 導入的子查詢一樣。 若這類的子查詢傳回一個以上的值，SQL Server 將會顯示錯誤訊息。    

若要使用未修改的比較運算子提出的子查詢，您必須非常熟悉您的資料和問題的本質，才能了解子查詢是否只會傳回一個數值。     

例如，如果您假設每個銷售人員只負責一個銷售區域，而您要尋找 `Linda Mitchell` 所負責之區域的客戶，您可以撰寫一個陳述式加上以簡單 = 比較運算子導入的子查詢。    

```sql
USE AdventureWorks2016;
GO
SELECT CustomerID
FROM Sales.Customer
WHERE TerritoryID =
    (SELECT TerritoryID
     FROM Sales.SalesPerson
     WHERE BusinessEntityID = 276);
GO
```

不過，如果 `Linda Mitchell` 負責一個以上的銷售區域時，就會產生錯誤訊息。 您可以使用 `IN` 形式來取代 = 比較運算子 (= ANY 也可行)。    

以未修改的比較運算子提出的子查詢通常會包含彙總函式，因為它們將傳回單一數值。 例如，下列陳述式尋找定價大於平均定價的所有產品名稱。     

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ListPrice >
    (SELECT AVG (ListPrice)
     FROM Production.Product);
GO
```     

因為由未修改的比較運算子導入的子查詢必須傳回單一值，除非您知道 GROUP BY 或 HAVING 子句本身會傳回單一值，否則這些子查詢不能包含 `GROUP BY` 或 `HAVING` 子句。 例如，下列查詢會尋找子類別 14 中價格高於最低價產品的產品。     

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ListPrice >
    (SELECT MIN (ListPrice)
     FROM Production.Product
     GROUP BY ProductSubcategoryID
     HAVING ProductSubcategoryID = 14);
GO
```

### <a name="comparison_modified"></a> ANY、SOME 或 ALL 修改的比較運算子
提出子查詢的比較運算子可由關鍵字 ALL 或 ANY 來修改。 SOME 為 `ANY` 的 ISO 標準對等項目。     

由已修改的比較運算子導入的子查詢會傳回零個或多個值的清單，並可包含 `GROUP BY` 或 `HAVING` 子句。 這些子查詢可使用 `EXISTS` 來重新敘述。     

使用 > 比較運算子作為範例，`>ALL` 表示大於每一個值。 換言之，它表示大於最大值。 例如，`>ALL (1, 2, 3)` 代表大於 3。 `>ANY` 表示大於至少一個值，也就是大於最小值。 因此 `>ANY (1, 2, 3)` 代表大於 1。
具有 `>ALL` 之子查詢中的資料列，若要滿足外部查詢中所指定的條件，導入子查詢之資料行中的數值必須大於由子查詢所傳回之數值清單中的每個數值。    

同樣地，`>ANY` 代表若要某個資料列滿足外部查詢中所指定的條件，導入子查詢之資料行中的值，至少需要大於由子查詢所傳回之數值清單中的某個數值。    

下列查詢提供了一個以 ANY 修改的比較運算子提出的子查詢範例。 它會尋找清單價格大於或等於任何產品子類別之最大清單價格的產品。    

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ListPrice >= ANY
    (SELECT MAX (ListPrice)
     FROM Production.Product
     GROUP BY ProductSubcategoryID);
GO
```    

對於每一個產品子類別，內部查詢會尋找最大清單價格。 外部查詢則會查看所有這些值，來判斷哪一項個別產品的清單價格大於或等於任何產品子類別的最大清單價格。 如果將 `ANY` 變更為 `ALL`，則查詢只會傳回其清單價格大於或等於由內部查詢所傳回之所有清單價格的產品。    

若子查詢並未傳回任何數值，整個查詢將無法傳回任何數值。    

`=ANY` 運算子等同於 `IN`。 例如，若要找出由 Adventure Works Cycles 所製作之所有輪類產品的名稱，您可以使用 `IN` 或 `=ANY`。

```sql
--Using =ANY
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID =ANY
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Wheels');
GO

--Using IN
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID IN
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Wheels');
GO
```

下列為任一種查詢的結果集：

```
Name
--------------------------------------------------
LL Mountain Front Wheel
ML Mountain Front Wheel
HL Mountain Front Wheel
LL Road Front Wheel
ML Road Front Wheel
HL Road Front Wheel
Touring Front Wheel
LL Mountain Rear Wheel
ML Mountain Rear Wheel
HL Mountain Rear Wheel
LL Road Rear Wheel
ML Road Rear Wheel
HL Road Rear Wheel
Touring Rear Wheel

(14 row(s) affected)
```    

不過，`<>ANY` 運算子與 `NOT IN` 並不相同：`<>ANY` 表示不 = a，或不 = b，或不 = c。 `NOT IN` 則表示不 = a，且不 = b，且不 = c。 `<>ALL` 的意思與 `NOT IN` 相同。     

例如，下列查詢會找出位於任何銷售員都未涵蓋之地區的客戶。     

```sql
USE AdventureWorks2016;
GO
SELECT CustomerID
FROM Sales.Customer
WHERE TerritoryID <> ANY
    (SELECT TerritoryID
     FROM Sales.SalesPerson);
GO
```    

除了銷售區域為 NULL 的客戶以外，其結果將包含其他所有的客戶，因為指派給客戶的每一個區域都有一位銷售人員負責。 內部查詢會先尋找有銷售人員負責的所有銷售區域，然後，外部查詢再尋找不在其中一個區域內的客戶。    

基於相同理由，當您在這個查詢中使用 `NOT IN` 時，其結果將不包括任何客戶。      

您可以使用 `<>ALL` 運算子來取得相同的結果，因為它相當於 `NOT IN`。   

### <a name="exists"></a> 使用 EXISTS 的子查詢
當子查詢是以關鍵字 `EXISTS` 導入時，它可作為存在測試的子查詢函式。 外部查詢的 `WHERE` 子句會測試子查詢所傳回的資料列是否存在。 子查詢並未實際地產生任何資料；而是傳回 TRUE 或 FALSE 值。   

以 EXISTS 所導入的子查詢具有下列語法：   

`WHERE [NOT] EXISTS (subquery)`    

下列查詢會尋找在 Wheels 子類別目錄之所有產品的名稱：    

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE EXISTS
    (SELECT * 
     FROM Production.ProductSubcategory
     WHERE ProductSubcategoryID = 
            Production.Product.ProductSubcategoryID
        AND Name = 'Wheels');
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]    

```
Name
--------------------------------------------------
LL Mountain Front Wheel
ML Mountain Front Wheel
HL Mountain Front Wheel
LL Road Front Wheel
ML Road Front Wheel
HL Road Front Wheel
Touring Front Wheel
LL Mountain Rear Wheel
ML Mountain Rear Wheel
HL Mountain Rear Wheel
LL Road Rear Wheel
ML Road Rear Wheel
HL Road Rear Wheel
Touring Rear Wheel

(14 row(s) affected)
```    

若要了解此查詢的結果，請依次考慮每個產品的名稱。 此值是否可使子查詢至少傳回一個資料列？ 換句話說，查詢是否可使存在測試評估為 TRUE？   

請注意 EXISTS 導入的子查詢和下列方式的其他子查詢有點不同： 
-   關鍵字 `EXISTS` 前面並沒有資料行名稱、常數或其他運算式。     
-   `EXISTS` 所導入之子查詢的選取清單一定會包含星號 (*)。 您並不需要列出資料行名稱，因為您只是在測試是否存在符合於子查詢中所指定之條件的資料行。    

`EXISTS` 關鍵字非常重要，因為沒有子查詢通常就沒有替代的形式。 雖然有些以 EXISTS 建立的查詢並不能以任何其他方式來表示，但是許多查詢都可以使用 IN 或是由 `ANY` 或 `ALL` 所修改的比較運算子來達成類似的結果。     

例如，前面的查詢也可以使用 IN 來表示：   

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE ProductSubcategoryID IN
    (SELECT ProductSubcategoryID
     FROM Production.ProductSubcategory
     WHERE Name = 'Wheels');
GO
```   

### <a name="notexists"></a> 使用 NOT EXISTS 的子查詢
`NOT EXISTS` 的運作方式和 `EXISTS` 類似，不同的是使用它的 `WHERE` 子句會在子查詢沒有傳回資料列的情況下成立。    

例如，若要尋找不在 Wheels 子類別目錄中的產品名稱：   

```sql
USE AdventureWorks2016;
GO
SELECT Name
FROM Production.Product
WHERE NOT EXISTS
    (SELECT * 
     FROM Production.ProductSubcategory
     WHERE ProductSubcategoryID = 
            Production.Product.ProductSubcategoryID
        AND Name = 'Wheels');
GO
```   

### <a name="expression"></a> 用來取代運算式的子查詢
在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中，於 `SELECT`、`UPDATE`、`INSERT` 與 `DELETE` 陳述式中任何可以使用運算式的位置，均可替換成子查詢 (`ORDER BY` 清單除外)。    

以下範例說明了您如何使用此增強功能。 此查詢會尋找所有的登山腳踏車的產品、其平均價格，以及每個登山腳踏車與平均價格之間的價差。    

```sql
USE AdventureWorks2016;
GO
SELECT Name, ListPrice, 
(SELECT AVG(ListPrice) FROM Production.Product) AS Average, 
    ListPrice - (SELECT AVG(ListPrice) FROM Production.Product)
    AS Difference
FROM Production.Product
WHERE ProductSubcategoryID = 1;
GO
```   

## <a name="see-also"></a>另請參閱  
[IN &#40;Transact-SQL&#41;](../../t-sql/language-elements/in-transact-sql.md)       
[EXISTS &#40;Transact-SQL&#41;](../../t-sql/language-elements/exists-transact-sql.md)     
[ALL &#40;Transact-SQL&#41;](../../t-sql/language-elements/all-transact-sql.md)     
[SOME | ANY &#40;Transact-SQL&#41;](../../t-sql/language-elements/some-any-transact-sql.md)     
[聯結](../../relational-databases/performance/joins.md)    
[比較運算子 &#40;Transact-SQL&#41;](../../t-sql/language-elements/comparison-operators-transact-sql.md)       
  
