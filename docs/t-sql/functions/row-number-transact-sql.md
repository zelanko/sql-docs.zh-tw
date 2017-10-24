---
title: "ROW_NUMBER (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ROW_NUMBER
- ROW_NUMBER_TSQL
- ROW_NUMBER()_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ROW_NUMBER function
- row numbers [SQL Server]
- sequential row numbers [SQL Server]
ms.assetid: 82fa9016-77db-4b42-b4c8-df6095b81906
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 820acddf7de1282501caf2fcaa43dbc757b98b7a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="rownumber-transact-sql"></a>ROW_NUMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  設定數字的結果輸出。 更具體來說，傳回的資料分割內的資料列，結果集，每個資料分割中的第一個資料列的 1 開始的序號。 
  
`ROW_NUMBER`和`RANK`類似。 `ROW_NUMBER`數字的所有資料列依序 （例如 1、 2、 3、 4、 5）。 `RANK`繫結 （例如 1、 2、 2、 4、 5） 提供相同的數值。   
  
> [!NOTE]
> `ROW_NUMBER`計算查詢執行時暫存值。 若要保存在資料表中的數字，請參閱[IDENTITY 屬性](../../t-sql/statements/create-table-transact-sql-identity-property.md)和[順序](../../t-sql/statements/create-sequence-transact-sql.md)。 
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
 
  
## <a name="syntax"></a>語法  
  
```  
ROW_NUMBER ( )   
    OVER ( [ PARTITION BY value_expression , ... [ n ] ] order_by_clause )  
```  
  
## <a name="arguments"></a>引數  
 PARTITION BY *value_expression*  
 所產生的結果集分成[FROM](../../t-sql/queries/from-transact-sql.md)子句套用 ROW_NUMBER 函數的分割區。 *value_expression*指定結果集之資料分割的資料行。 如果`PARTITION BY`未指定，則函數會將查詢結果集為單一群組的所有資料列。 如需詳細資訊，請參閱[OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 *order_by_clause*  
 `ORDER BY`子句決定了資料列會指派其唯一`ROW_NUMBER`內指定的資料分割。 此為必要。 如需詳細資訊，請參閱[OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## <a name="return-types"></a>傳回類型  
 **bigint**  
  
## <a name="general-remarks"></a>一般備註  
 傳回的資料列不保證查詢使用`ROW_NUMBER()`的排序是每次執行完全相同除非下列條件成立。  
  
1.  分割區資料行的值是唯一的。  
  
2.  值的`ORDER BY`是唯一的資料行。  
  
3.  資料分割資料行的值組合和`ORDER BY`是唯一的資料行。  
  
 `ROW_NUMBER()`不具決定性。 如需詳細資訊，請參閱 [決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-examples"></a>A. 簡單範例 

下列查詢會按字母順序傳回的四個系統資料表。

```t-sql
SELECT 
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5
ORDER BY name ASC;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|name    |recovery_model_desc |  
|-----------  |------------ |  
|master |SIMPLE |
|model |FULL |
|msdb |SIMPLE |
|tempdb |SIMPLE |

若要加入資料列號碼資料行在每個資料列前面，新增的資料行`ROW_NUMBER`函式，在此情況下名為`Row#`。 您必須移動`ORDER BY`達子句`OVER`子句。

```t-sql
SELECT 
  ROW_NUMBER() OVER(ORDER BY name ASC) AS Row#,
  name, recovery_model_desc
FROM sys.databases 
WHERE database_id < 5;
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|資料列號碼 |name    |recovery_model_desc |  
|------- |-----------  |------------ |  
|1 |master |SIMPLE |
|2 |model |FULL |
|3 |msdb |SIMPLE |
|4 |tempdb |SIMPLE |

加入`PARTITION BY`子句`recovery_model_desc`資料行，將會重新啟動時的編號`recovery_model_desc`值變更。 
 
```t-sql
SELECT 
  ROW_NUMBER() OVER(PARTITION BY recovery_model_desc ORDER BY name ASC) 
    AS Row#,
  name, recovery_model_desc
FROM sys.databases WHERE database_id < 5;
```  

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
   
|資料列號碼 |name    |recovery_model_desc |  
|------- |-----------  |------------ |  
|1 |model |FULL |
|1 |master |SIMPLE |
|2 |msdb |SIMPLE |
|3 |tempdb |SIMPLE |


### <a name="b-returning-the-row-number-for-salespeople"></a>B. 傳回銷售人員的資料列編號  
 下列範例根據年初至今的銷售業績排名計算 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] 中銷售人員的資料列編號。  
  
```t-sql  
USE AdventureWorks2012;   
GO  
SELECT ROW_NUMBER() OVER(ORDER BY SalesYTD DESC) AS Row,   
    FirstName, LastName, ROUND(SalesYTD,2,1) AS "Sales YTD"   
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL AND SalesYTD <> 0;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Row FirstName    LastName               SalesYTD  
--- -----------  ---------------------- -----------------  
1   Linda        Mitchell               4251368.54  
2   Jae          Pak                    4116871.22  
3   Michael      Blythe                 3763178.17  
4   Jillian      Carson                 3189418.36  
5   Ranjit       Varkey Chudukatil      3121616.32  
6   José         Saraiva                2604540.71  
7   Shu          Ito                    2458535.61  
8   Tsvi         Reiter                 2315185.61  
9   Rachel       Valdez                 1827066.71  
10  Tete         Mensa-Annan            1576562.19  
11  David        Campbell               1573012.93  
12  Garrett      Vargas                 1453719.46  
13  Lynn         Tsoflias               1421810.92  
14  Pamela       Ansman-Wolfe           1352577.13  
```  
  
### <a name="c-returning-a-subset-of-rows"></a>C. 傳回資料列的子集  
 下列範例會計算 `SalesOrderHeader` 資料表中所有資料列的編號，並以 `OrderDate` 順序排列，然後只傳回包含 `50` 至 `60` 的資料列。  
  
```t-sql  
USE AdventureWorks2012;  
GO  
WITH OrderedOrders AS  
(  
    SELECT SalesOrderID, OrderDate,  
    ROW_NUMBER() OVER (ORDER BY OrderDate) AS RowNumber  
    FROM Sales.SalesOrderHeader   
)   
SELECT SalesOrderID, OrderDate, RowNumber    
FROM OrderedOrders   
WHERE RowNumber BETWEEN 50 AND 60;  
```  
  
### <a name="d-using-rownumber-with-partition"></a>D. 並用 PARTITION 與 ROW_NUMBER()  
 下列範例使用 `PARTITION BY` 引數依據資料行 `TerritoryName` 分割查詢結果集。 `ORDER BY` 子句中指定的 `OVER` 子句會依資料行 `SalesYTD` 排列每個分割區的資料列。 `ORDER BY` 陳述式中的 `SELECT` 子句會依照 `TerritoryName` 排列整個查詢結果集。  
  
```t-sql  
USE AdventureWorks2012;  
GO  
SELECT FirstName, LastName, TerritoryName, ROUND(SalesYTD,2,1) AS SalesYTD,  
ROW_NUMBER() OVER(PARTITION BY TerritoryName ORDER BY SalesYTD DESC) 
  AS Row  
FROM Sales.vSalesPerson  
WHERE TerritoryName IS NOT NULL AND SalesYTD <> 0  
ORDER BY TerritoryName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
FirstName  LastName             TerritoryName        SalesYTD      Row  
---------  -------------------- ------------------   ------------  ---  
Lynn       Tsoflias             Australia            1421810.92    1  
José       Saraiva              Canada               2604540.71    1  
Garrett    Vargas               Canada               1453719.46    2  
Jillian    Carson               Central              3189418.36    1  
Ranjit     Varkey Chudukatil    France               3121616.32    1  
Rachel     Valdez               Germany              1827066.71    1  
Michael    Blythe               Northeast            3763178.17    1  
Tete       Mensa-Annan          Northwest            1576562.19    1  
David      Campbell             Northwest            1573012.93    2  
Pamela     Ansman-Wolfe         Northwest            1352577.13    3  
Tsvi       Reiter               Southeast            2315185.61    1  
Linda      Mitchell             Southwest            4251368.54    1  
Shu        Ito                  Southwest            2458535.61    2  
Jae        Pak                  United Kingdom       4116871.22    1  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-returning-the-row-number-for-salespeople"></a>E. 傳回銷售人員的資料列編號  
 下列範例會傳回`ROW_NUMBER`根據其指派的銷售配額的銷售代表。  
  
```t-sql  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(ORDER BY SUM(SalesAmountQuota) DESC) 
    AS RowNumber,  
    FirstName, LastName,   
    CONVERT(varchar(13), SUM(SalesAmountQuota),1) AS SalesQuota   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq  
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE e.SalesPersonFlag = 1  
GROUP BY LastName, FirstName;  
```  
  
 以下為部分結果集。  

```  

RowNumber  FirstName  LastName            SalesQuota  
---------  ---------  ------------------  -------------  
1          Jillian    Carson              12,198,000.00  
2          Linda      Mitchell            11,786,000.00  
3          Michael    Blythe              11,162,000.00  
4          Jae        Pak                 10,514,000.00  
```

### <a name="f-using-rownumber-with-partition"></a>F. 並用 PARTITION 與 ROW_NUMBER()  
 下列範例顯示如何搭配 `ROW_NUMBER` 引數使用 `PARTITION BY` 函數。 這會導致`ROW_NUMBER`函式中每個資料分割編號的資料列。  
  
```t-sql  
-- Uses AdventureWorks  
  
SELECT ROW_NUMBER() OVER(PARTITION BY SalesTerritoryKey 
        ORDER BY SUM(SalesAmountQuota) DESC) AS RowNumber,  
    LastName, SalesTerritoryKey AS Territory,  
    CONVERT(varchar(13), SUM(SalesAmountQuota),1) AS SalesQuota   
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq  
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE e.SalesPersonFlag = 1  
GROUP BY LastName, FirstName, SalesTerritoryKey;  
```  
  
 以下為部分結果集。  
 
```  
 
RowNumber  LastName            Territory  SalesQuota  
---------  ------------------  ---------  -------------  
1          Campbell            1           4,025,000.00  
2          Ansman-Wolfe        1           3,551,000.00  
3          Mensa-Annan         1           2,275,000.00  
1          Blythe              2          11,162,000.00  
1          Carson              3          12,198,000.00  
1          Mitchell            4          11,786,000.00  
2          Ito                 4           7,804,000.00  
```
  
## <a name="see-also"></a>另請參閱  
 [順位 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/rank-transact-sql.md)   
 [DENSE_RANK &#40;TRANSACT-SQL &#41;](../../t-sql/functions/dense-rank-transact-sql.md)   
 [NTILE &#40;TRANSACT-SQL &#41;](../../t-sql/functions/ntile-transact-sql.md)  
  
  



