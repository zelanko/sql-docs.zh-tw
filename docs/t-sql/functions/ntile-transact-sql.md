---
title: "NTILE (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NTILE_TSQL
- NTILE
dev_langs:
- TSQL
helpviewer_keywords:
- distributing rows
- groups [SQL Server], row distribution
- row distribution [SQL Server]
- NTILE function
ms.assetid: 1c364511-d72a-4789-8efa-3cf2a1f6b791
caps.latest.revision: 63
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7cb3ab21f1707c1af1c689e438e9d6ead291dcc4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="ntile-transact-sql"></a>NTILE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  將排序分割區中的資料列散發到指定數目的群組中。 這些群組從 1 開始編號。 對於每個資料列，NTILE 都會傳回資料列所屬群組的號碼。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
NTILE (integer_expression) OVER ( [ <partition_by_clause> ] < order_by_clause > )  
```  
  
## <a name="arguments"></a>引數  
 *integer_expression*  
 用於指定每個分割區必須劃分之群組數的正整數常數運算式。 *clause><*可以屬於型別**int**，或**bigint**。  
  
 \<partition_by_clause >  
 所產生的結果集分成[FROM](../../t-sql/queries/from-transact-sql.md)子句套用函數的分割區。 如需 PARTITION BY 語法，請參閱[OVER 子句 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
 \<order_by_clause >  
 指定 NTILE 值指派給分割區中之資料列的順序。 整數無法表示資料行時\<order_by_clause > 排名函數中使用。  
  
## <a name="return-types"></a>傳回類型  
 **bigint**  
  
## <a name="remarks"></a>備註  
 資料分割中的資料列數目是否未整除*clause><*，這會導致兩個大小不同的一個成員群組。 在 OVER 子句所指定的順序中，較大群組會在較小群組的前面。 例如，如果資料列總數是 53，群組數目是 5，前三個群組會有 11 個資料列，後兩個群組會有 10 個資料列。 如果群組數目可以整除資料列的總數，資料列就會平均分散在各個群組中。 例如，如果資料列總數是 50，有 5 個群組，每個貯體都會包含 10 個資料列。  
  
 NTILE 不具決定性。 如需詳細資訊，請參閱 [決定性與非決定性函數](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-dividing-rows-into-groups"></a>A. 將資料列分割成數個群組  
 在下列範例中，根據員工年初至今的銷售收益，將資料列歸類為四組員工。 由於群組數目無法整除資料列的總數，前兩組有四個資料列，其他組各有三個資料列。  
  
```  
USE AdventureWorks2012;   
GO  
SELECT p.FirstName, p.LastName  
    ,NTILE(4) OVER(ORDER BY SalesYTD DESC) AS Quartile  
    ,CONVERT(nvarchar(20),s.SalesYTD,1) AS SalesYTD  
    , a.PostalCode  
FROM Sales.SalesPerson AS s   
INNER JOIN Person.Person AS p   
    ON s.BusinessEntityID = p.BusinessEntityID  
INNER JOIN Person.Address AS a   
    ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
FirstName      LastName              Quartile  SalesYTD       PostalCode  
-------------  --------------------- --------- -------------- ----------  
Linda          Mitchell              1         4,251,368.55   98027  
Jae            Pak                   1         4,116,871.23   98055  
Michael        Blythe                1         3,763,178.18   98027  
Jillian        Carson                1         3,189,418.37   98027  
Ranjit         Varkey Chudukatil     2         3,121,616.32   98055  
José           Saraiva               2         2,604,540.72   98055  
Shu            Ito                   2         2,458,535.62   98055  
Tsvi           Reiter                2         2,315,185.61   98027  
Rachel         Valdez                3         1,827,066.71   98055  
Tete           Mensa-Annan           3         1,576,562.20   98055  
David          Campbell              3         1,573,012.94   98055  
Garrett        Vargas                4         1,453,719.47   98027  
Lynn           Tsoflias              4         1,421,810.92   98055  
Pamela         Ansman-Wolfe          4         1,352,577.13   98027  
 (14 row(s) affected)  
```  
  
### <a name="b-dividing-the-result-set-by-using-partition-by"></a>B. 使用 PARTITION BY 分割結果集  
 下列範例會在範例 A 的程式碼中加入 `PARTITION BY` 引數。資料列會先由 `PostalCode` 進行資料分割，接著再依據每個 `PostalCode` 分成四個群組。 此範例也會宣告一個變數`@NTILE_Var`和使用該變數來指定的值*clause><*參數。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @NTILE_Var int = 4;  
  
SELECT p.FirstName, p.LastName  
    ,NTILE(@NTILE_Var) OVER(PARTITION BY PostalCode ORDER BY SalesYTD DESC) AS Quartile  
    ,CONVERT(nvarchar(20),s.SalesYTD,1) AS SalesYTD  
    ,a.PostalCode  
FROM Sales.SalesPerson AS s   
INNER JOIN Person.Person AS p   
    ON s.BusinessEntityID = p.BusinessEntityID  
INNER JOIN Person.Address AS a   
    ON a.AddressID = p.BusinessEntityID  
WHERE TerritoryID IS NOT NULL   
    AND SalesYTD <> 0;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
FirstName    LastName             Quartile SalesYTD      PostalCode  
------------ -------------------- -------- ------------  ----------  
Linda        Mitchell             1        4,251,368.55  98027  
Michael      Blythe               1        3,763,178.18  98027  
Jillian      Carson               2        3,189,418.37  98027  
Tsvi         Reiter               2        2,315,185.61  98027  
Garrett      Vargas               3        1,453,719.47  98027  
Pamela       Ansman-Wolfe         4        1,352,577.13  98027  
Jae          Pak                  1        4,116,871.23  98055  
Ranjit       Varkey Chudukatil    1        3,121,616.32  98055  
José         Saraiva              2        2,604,540.72  98055  
Shu          Ito                  2        2,458,535.62  98055  
Rachel       Valdez               3        1,827,066.71  98055  
Tete         Mensa-Annan          3        1,576,562.20  98055  
David        Campbell             4        1,573,012.94  98055  
Lynn         Tsoflias             4        1,421,810.92  98055  
  
(14 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-dividing-rows-into-groups"></a>C. 將資料列分割成數個群組  
 下列範例會將分成四個群組，根據其指派的銷售配額，2003 年的銷售人員的一組使用 NTILE 函式。 因為無法整除的群組數目的資料列總數，第一個群組具有五個資料列，其餘群組會有四個資料列。  
  
```  
-- Uses AdventureWorks  
  
SELECT e.LastName, NTILE(4) OVER(ORDER BY SUM(SalesAmountQuota) DESC) AS Quartile,  
       CONVERT (varchar(13), SUM(SalesAmountQuota), 1) AS SalesQuota  
FROM dbo.DimEmployee AS e   
INNER JOIN dbo.FactSalesQuota AS sq   
    ON e.EmployeeKey = sq.EmployeeKey  
WHERE sq.CalendarYear = 2003  
    AND SalesTerritoryKey IS NOT NULL AND SalesAmountQuota <> 0  
GROUP BY e.LastName  
ORDER BY Quartile, e.LastName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `LastName          Quartile SalesYTD`  
  
 `----------------- -------- ------------`  
  
 `Blythe            1        4,716,000.00`  
  
 `Carson            1        4,350,000.00`  
  
 `Mitchell          1        4,682,000.00`  
  
 `Pak               1        5,142,000.00`  
  
 `Varkey Chudukatil 1        2,940,000.00`  
  
 `Ito               2        2,644,000.00`  
  
 `Reiter            2        2,768,000.00`  
  
 `Saraiva           2        2,293,000.00`  
  
 `Vargas            2        1,617,000.00`  
  
 `Ansman-Wolfe      3        1,183,000.00`  
  
 `Campbell          3        1,438,000.00`  
  
 `Mensa-Annan       3        1,481,000.00`  
  
 `Valdez            3        1,294,000.00`  
  
 `Abbas             4          172,000.00`  
  
 `Albert            4          651,000.00`  
  
 `Jiang             4          544,000.00`  
  
 `Tsoflias          4          867,000.00`  
  
### <a name="d-dividing-the-result-set-by-using-partition-by"></a>D. 使用 PARTITION BY 分割結果集  
 下列範例會將 PARTITION BY 引數加入範例 a 中的程式碼資料列會先依分割`SalesTerritoryCountry`而再分成兩個群組內每個`SalesTerritoryCountry`。 請注意，OVER 子句中的 ORDER BY 排序 NTILE ORDER BY 的 SELECT 陳述式排序結果集。  
  
```  
-- Uses AdventureWorks  
  
SELECT e.LastName, NTILE(2) OVER(PARTITION BY e.SalesTerritoryKey ORDER BY SUM(SalesAmountQuota) DESC) AS Quartile,  
       CONVERT (varchar(13), SUM(SalesAmountQuota), 1) AS SalesQuota  
   ,st.SalesTerritoryCountry  
FROM dbo.DimEmployee AS e   
INNER JOIN dbo.FactSalesQuota AS sq   
    ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory AS st  
    ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE sq.CalendarYear = 2003  
GROUP BY e.LastName,e.SalesTerritoryKey,st.SalesTerritoryCountry  
ORDER BY st.SalesTerritoryCountry, Quartile;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `LastName          Quartile SalesYTD       SalesTerritoryCountry`  
  
 `----------------- -------- -------------- ------------------`  
  
 `Tsoflias          1         867,000.00     Australia`  
  
 `Saraiva           1        2,293,000.00    Canada`  
  
 `Varkey Chudukatil 1        2,940,000.00    France`  
  
 `Valdez            1        1,294,000.00    Germany`  
  
 `Alberts           1          651,000.00    NA`  
  
 `Jiang             1          544,000.00    NA`  
  
 `Pak               1        5,142,000.00    United Kingdom`  
  
 `Mensa-Annan       1        1,481,000.00    United States`  
  
 `Campbell          1        1,438,000.00    United States`  
  
 `Reiter            1        2,768,000.00    United States`  
  
 `Blythe            1        4,716,000.00    United States`  
  
 `Carson            1        4,350,000.00     United States`  
  
 `Mitchell          1        4,682,000.00     United States`  
  
 `Vargas            2        1,617,000.00     Canada`  
  
 `Abbas             2          172,000.00     NA`  
  
 `Ito               2        2,644,000.00     United States`  
  
 `Ansman-Wolfe      2        1,183,000.00     United States`  
  
## <a name="see-also"></a>另請參閱  
 [順位 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/rank-transact-sql.md)   
 [DENSE_RANK &#40;TRANSACT-SQL &#41;](../../t-sql/functions/dense-rank-transact-sql.md)   
 [ROW_NUMBER &#40;TRANSACT-SQL &#41;](../../t-sql/functions/row-number-transact-sql.md)   
 [排名函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/ranking-functions-transact-sql.md)   
 [內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  



