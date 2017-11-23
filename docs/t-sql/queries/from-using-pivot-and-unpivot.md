---
title: "使用 PIVOT 和 UNPIVOT |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: PIVOT_TSQL
helpviewer_keywords:
- FROM clause, UNPIVOT operator
- unpivoting tables
- table pivoting [SQL Server]
- UNPIVOT operator
- crosstab query
- PIVOT operator
- rotating table-valued expressions
- pivoting tables
- FROM clause, PIVOT operator
- rotating columns
ms.assetid: 24ba54fc-98f7-4d35-8881-b5158aac1d66
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 4555a892c55ae8ef40e8fd0c3658412e3641d973
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="from---using-pivot-and-unpivot"></a>從-使用 PIVOT 和 UNPIVOT
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  您可以使用`PIVOT`和`UNPIVOT`關聯式運算子，以變更到另一個資料表的資料表值運算式。 `PIVOT`旋轉資料表值的運算式從一個資料行的唯一值轉成在輸出中，多個資料行運算式中，執行必要的任何最後輸出的其餘資料行值上的彙總。 `UNPIVOT`旋轉成資料行值的資料表值運算式的資料行來執行相反的樞紐作業。  
  
 語法`PIVOT`提供更簡單且更容易閱讀，另外指定一連串複雜的語法比`SELECT...CASE`陳述式。 如需完整的語法說明`PIVOT`，請參閱[(TRANSACT-SQL) 從](../../t-sql/queries/from-transact-sql.md)。  
  
## <a name="syntax"></a>語法  
 下列語法摘要說明如何使用`PIVOT`運算子。  
  
```  
SELECT <non-pivoted column>,  
    [first pivoted column] AS <column name>,  
    [second pivoted column] AS <column name>,  
    ...  
    [last pivoted column] AS <column name>  
FROM  
    (<SELECT query that produces the data>)   
    AS <alias for the source query>  
PIVOT  
(  
    <aggregation function>(<column being aggregated>)  
FOR   
[<column that contains the values that will become column headers>]   
    IN ( [first pivoted column], [second pivoted column],  
    ... [last pivoted column])  
) AS <alias for the pivot table>  
<optional ORDER BY clause>;  
```  

## <a name="remarks"></a>備註  
中的資料行識別碼`UNPIVOT`子句依照目錄定序。 如[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，定序一律為`SQL_Latin1_General_CP1_CI_AS`。 如[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]部分自主的資料庫，定序一律為`Latin1_General_100_CI_AS_KS_WS_SC`。 如果資料行就會結合其他資料行，然後 collate 子句 (`COLLATE DATABASE_DEFAULT`) 才能避免衝突。  

  
## <a name="basic-pivot-example"></a>基本 PIVOT 範例  
 下列程式碼範例會產生包含兩個資料行的資料表，其中有四個資料列。  
  
```  
USE AdventureWorks2014 ;  
GO  
SELECT DaysToManufacture, AVG(StandardCost) AS AverageCost   
FROM Production.Product  
GROUP BY DaysToManufacture;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 DaysToManufacture AverageCost
 ----------------- -----------
 0                 5.0885
 1                 223.88
 2                 359.1082
 4                 949.4105
 ```
  
 沒有任何產品是定義為三天內完工 (`DaysToManufacture`)。  
  
 下列程式碼會顯示同樣的結果，但是經過樞紐處理後，讓 `DaysToManufacture` 值變成了資料行的標題。 即使結果為 `[3]`，還是為這三 `NULL` 天產生了一個資料行。  
  
```  
-- Pivot table with one row and five columns  
SELECT 'AverageCost' AS Cost_Sorted_By_Production_Days,   
[0], [1], [2], [3], [4]  
FROM  
(SELECT DaysToManufacture, StandardCost   
    FROM Production.Product) AS SourceTable  
PIVOT  
(  
AVG(StandardCost)  
FOR DaysToManufacture IN ([0], [1], [2], [3], [4])  
) AS PivotTable;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
Cost_Sorted_By_Production_Days 0           1           2           3           4         
------------------------------ ----------- ----------- ----------- ----------- -----------
AverageCost                    5.0885      223.88      359.1082    NULL        949.4105
```
  
## <a name="complex-pivot-example"></a>複雜 PIVOT 範例  
 當您想要產生跨表格式報表來建立資料摘要時，這個常見的狀況可以顯出 `PIVOT` 的用處。 例如，假設您想要查詢 `PurchaseOrderHeader` 範例資料庫中的 `AdventureWorks2014` 資料表，以判斷某些員工所下的訂單數目。 下列查詢會提供這個報表，並依供應商排序：  
  
```  
USE AdventureWorks2014;  
GO  
SELECT VendorID, [250] AS Emp1, [251] AS Emp2, [256] AS Emp3, [257] AS Emp4, [260] AS Emp5  
FROM   
(SELECT PurchaseOrderID, EmployeeID, VendorID  
FROM Purchasing.PurchaseOrderHeader) p  
PIVOT  
(  
COUNT (PurchaseOrderID)  
FOR EmployeeID IN  
( [250], [251], [256], [257], [260] )  
) AS pvt  
ORDER BY pvt.VendorID;  
```  
  
 以下為部分結果集。  
  
```
VendorID    Emp1        Emp2        Emp3        Emp4        Emp5  
----------- ----------- ----------- ----------- ----------- -----------
1492        2           5           4           4           4
1494        2           5           4           5           4
1496        2           4           4           5           5
1498        2           5           4           4           4
1500        3           4           4           5           4
```
  
 這個子選擇陳述式所傳回的結果，是根據 `EmployeeID` 資料行進行樞紐處理而來。  
  
```  
SELECT PurchaseOrderID, EmployeeID, VendorID  
FROM PurchaseOrderHeader;  
```  
  
 這表示由 `EmployeeID` 資料行所傳回的唯一值本身會變成最終結果集中的欄位。 因此，樞紐子句指定的每個 `EmployeeID` 編號都會有一個資料行：在此情況下，是以下員工 `164`、`198`、`223`、`231` 和 `233`。 `PurchaseOrderID` 資料行會當作數值資料行，這是在最終輸出中傳回的資料行 (稱為群組資料行) 所根據以進行分組的資料行。 在此情況下，`COUNT` 函數會對群組資料行進行彙總。 請注意，此時會顯示警告訊息，指出計算每個員工的 `PurchaseOrderID` 時，並未考慮 `COUNT` 資料行中出現的任何 NULL 值。  
  
> [!IMPORTANT]  
>  與使用彙總函式時`PIVOT`，計算一個彙總時，不會考慮值資料行中的任何 null 值是否存在。  
  
 `UNPIVOT`執行幾乎的反向作業`PIVOT`，資料行旋轉成資料列。 假設上述範例中所產生的資料表在資料庫中是儲存為 `pvt`，而現在您想要將資料行識別碼 `Emp1`、`Emp2`、`Emp3`、`Emp4` 和 `Emp5` 旋轉成對應到特定供應商的資料列值。 這表示您必須識別兩個額外的資料行。 包含所要旋轉的資料行值 (`Emp1`、`Emp2`、...) 的資料行將命名為 `Employee`，而保留目前位在所要旋轉資料行之下的值的資料行則命名為 `Orders`。 這些資料行對應至*pivot_column*和*value_column*，分別在[!INCLUDE[tsql](../../includes/tsql-md.md)]定義。 查詢內容如下。  
  
```  
-- Create the table and insert values as portrayed in the previous example.  
CREATE TABLE pvt (VendorID int, Emp1 int, Emp2 int,  
    Emp3 int, Emp4 int, Emp5 int);  
GO  
INSERT INTO pvt VALUES (1,4,3,5,4,4);  
INSERT INTO pvt VALUES (2,4,1,5,5,5);  
INSERT INTO pvt VALUES (3,4,3,5,4,4);  
INSERT INTO pvt VALUES (4,4,2,5,5,4);  
INSERT INTO pvt VALUES (5,5,1,5,5,5);  
GO  
-- Unpivot the table.  
SELECT VendorID, Employee, Orders  
FROM   
   (SELECT VendorID, Emp1, Emp2, Emp3, Emp4, Emp5  
   FROM pvt) p  
UNPIVOT  
   (Orders FOR Employee IN   
      (Emp1, Emp2, Emp3, Emp4, Emp5)  
)AS unpvt;  
GO  
```  
  
 以下為部分結果集。  
  
```
VendorID    Employee    Orders
----------- ----------- ------
1            Emp1       4
1            Emp2       3 
1            Emp3       5
1            Emp4       4
1            Emp5       4
2            Emp1       4
2            Emp2       1
2            Emp3       5
2            Emp4       5
2            Emp5       5
...
```
  
 請注意，`UNPIVOT`不是完全相反`PIVOT`。 `PIVOT`執行彙總，因此，合併多個資料列可能在輸出中的單一資料列。 `UNPIVOT`不會再出現原始的資料表值運算式結果因為合併的資料列。 此外，null 值的輸入`UNPIVOT`消失在輸出中，而可能有原始的 null 值之前，輸入中`PIVOT`作業。  
  
 `Sales.vSalesPersonSalesByFiscalYears`檢視中[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]範例資料庫會使用`PIVOT`傳回每個會計年度的每位銷售員的銷售總額。 若要編寫指令碼中的檢視[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，請在**物件總管 中**，找出下的檢視**檢視**資料夾[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]資料庫。 檢視名稱，以滑鼠右鍵按一下，然後選取**做為指令碼檢視**。  
  
## <a name="see-also"></a>請參閱＜  
 [從 (TRANSACT-SQL)](../../t-sql/queries/from-transact-sql.md)   
 [案例 (TRANSACT-SQL)](../../t-sql/language-elements/case-transact-sql.md)  
  
  
