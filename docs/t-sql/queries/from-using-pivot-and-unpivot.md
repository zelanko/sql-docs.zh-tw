---
title: 使用 PIVOT 和 UNPIVOT | Microsoft Docs
ms.custom: ''
ms.date: 10/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PIVOT_TSQL
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
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d776fbae94ae69af10595d7c0d50b84449dd9875
ms.sourcegitcommit: 49082f9b6b3bc8aaf9ea3f8557f40c9f1b6f3b0b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2020
ms.locfileid: "77255990"
---
# <a name="from---using-pivot-and-unpivot"></a>FROM - 使用 PIVOT 和 UNPIVOT

[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

您可以使用 `PIVOT` 和 `UNPIVOT` 關係運算子，將資料表值運算式變更為另一個資料表。 `PIVOT` 會透過將唯一值從運算式中的某一資料行轉換為輸出中的多個資料行，來旋轉表格值運算式。 而 `PIVOT` 會在最終輸出中需要它們的任何其餘資料行上執行彙總。 `UNPIVOT` 執行的作業與 PIVOT 相反，它會將資料表值運算式的資料行旋轉成資料行值。  
  
`PIVOT` 提供的語法比您另外指定一連串複雜的 `SELECT...CASE` 陳述式，還要簡單易讀。 如需 `PIVOT` 語法的完整描述，請參閱 [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)。  
  
## <a name="syntax"></a>語法  
下列語法摘要說明如何使用 `PIVOT` 運算子。  
  
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
`UNPIVOT` 子句中的資料行識別碼會依照目錄定序。 就 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 而言，定序一律為 `SQL_Latin1_General_CP1_CI_AS`。 就 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 部分自主資料庫而言，定序一律為 `Latin1_General_100_CI_AS_KS_WS_SC`。 如果資料行與其他資料行結合，就必須使用定序子句 (`COLLATE DATABASE_DEFAULT`) 來避免衝突。  

  
## <a name="basic-pivot-example"></a>基本 PIVOT 範例  
下列程式碼範例會產生包含兩個資料行的資料表，其中有四個資料列。  
  
```sql
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
  
```sql
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
當您想要產生跨表格式報表來提供資料摘要時，這個常見的狀況可以顯示出 `PIVOT` 的用處。 例如，假設您想要查詢 `PurchaseOrderHeader` 範例資料庫中的 `AdventureWorks2014` 資料表，以判斷某些員工所下的訂單數目。 下列查詢會提供這個報表，並依供應商排序：  
  
```sql
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
  
```sql
SELECT PurchaseOrderID, EmployeeID, VendorID  
FROM PurchaseOrderHeader;  
```  
  
由 `EmployeeID` 資料行所傳回的唯一值會變成最終結果集中的欄位。 因此，樞紐子句指定的每個 `EmployeeID` 編號都會有一個資料行：在此情況下是員工 `250`、`251`、`256`、`257` 和 `260`。 `PurchaseOrderID` 資料行會當作數值資料行，這是在最終輸出中傳回的資料行 (稱為群組資料行) 所根據以進行分組的資料行。 在此情況下，`COUNT` 函數會對群組資料行進行彙總。 請注意，此時會顯示警告訊息，指出計算每個員工的 `PurchaseOrderID` 時，並未考慮 `COUNT` 資料行中出現的任何 Null 值。  
  
> [!IMPORTANT]  
>  搭配 `PIVOT` 使用彙總函數時，在計算彙總期間不會考慮值資料行中出現的任何 Null 值。  

## <a name="unpivot-example"></a>UNPIVOT 範例
  
`UNPIVOT` 執行的作業則幾乎與 `PIVOT` 相反，它會將資料行旋轉成資料列。 假設上述範例中所產生的資料表在資料庫中是儲存為 `pvt`，而現在您想要將資料行識別碼 `Emp1`、`Emp2`、`Emp3`、`Emp4` 和 `Emp5` 旋轉成對應到特定供應商的資料列值。 因此，您必須識別兩個額外的資料行。 包含所要旋轉資料行值 (`Emp1`、`Emp2`、...) 的資料行將命名為 `Employee`，而保留目前所要旋轉資料行下存在值的資料行則命名為 `Orders`。 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 定義中，這些資料行會分別與 *pivot_column* 和 *value_column* 對應。 查詢內容如下。  
  
```sql
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
  
請注意，`UNPIVOT` 並非與 `PIVOT` 完全相反。 `PIVOT` 會執行彙總，並將多個可能資料列合併成輸出中的單一資料列。 由於資料列已經合併，因此 `UNPIVOT` 並不會重新產生原始資料表值運算式結果。 此外，`UNPIVOT` 輸入的 Null 值會在輸出中消失。 如果這些值會消失，這表示在 `PIVOT` 作業之前，輸入中可能已經有原始 Null 值。  
  
[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫中的 `Sales.vSalesPersonSalesByFiscalYears` 檢視表會使用 `PIVOT` 來傳回每位銷售人員在每個會計年度的總銷售額。 若要在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中編寫該檢視表的指令碼，請在 [物件總管]  中，於 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫的 [檢視表]  資料夾底下找出該檢視表。 在檢視表名稱上按一下滑鼠右鍵，然後選取 [編寫檢視表的指令碼為]  。  
  
## <a name="see-also"></a>另請參閱  
[FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)   
[CASE (Transact-SQL)](../../t-sql/language-elements/case-transact-sql.md)  
  
