---
title: "別名 （Azure SQL 資料倉儲、 Parallel Data Warehouse） |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7b3a5c74-05cf-4385-8ee6-6176d003cb8a
caps.latest.revision: 11
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: edc81ce4377f490b482d920871ad361c98f961c5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="aliasing-azure-sql-data-warehouse-parallel-data-warehouse"></a>別名 （Azure SQL 資料倉儲、 Parallel Data Warehouse）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  別名可讓採取短暫且容易記住的字串來取代資料表或資料行名稱中的暫存替代[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)][!INCLUDE[DWsql](../../includes/dwsql-md.md)]查詢。 資料表別名通常是聯結查詢中使用，因為聯結語法的參考資料行時，需要完整限定的物件名稱。  
  
 別名必須是符合物件命名規則的單字。 如需詳細資訊，請參閱 < 物件命名規則 > 中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。 別名不得包含空格，而且無法以單引號或雙引號括住。  
  
## <a name="syntax"></a>語法  
  
```  
object_source [ AS ] alias  
```  
  
## <a name="arguments"></a>引數  
 *object_source*  
 來源資料表或資料行的名稱。  
  
 AS  
 的選擇性別名的前置詞。 當使用範圍變數的別名，被禁止的 AS 關鍵字。  
  
 *別名*  
 所需的臨時參考的資料表或資料行名稱。 可以使用任何有效的物件名稱。 如需詳細資訊，請參閱 < 物件命名規則 > 中[!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)]。  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例顯示使用多個聯結的查詢。 在此範例中示範資料表和資料行的別名。  
  
-   資料行別名： 兩個資料行和運算式的 select 清單中的資料行是在此範例中的別名。 `SalesTerritoryRegion AS SalesTR`示範簡單的資料行別名。 `Sum(SalesAmountQuota) AS TotalSales`示範  
  
-   資料表別名：`dbo.DimSalesTerritory AS st`顯示的建立`st`別名，以供`dbo.DimSalesTerritory`資料表。  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) AS TotalSales, SalesTerritoryRegion AS SalesTR,  
    RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) AS RankResult  
FROM dbo.DimEmployee AS e  
INNER JOIN dbo.FactSalesQuota AS sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory AS st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
  
```  
  
 AS 關鍵字可以排除，如下所示，但通常是為了可讀性。  
  
```  
-- Uses AdventureWorks  
  
SELECT LastName, SUM(SalesAmountQuota) TotalSales, SalesTerritoryRegion SalesTR,  
RANK() OVER (PARTITION BY SalesTerritoryRegion ORDER BY SUM(SalesAmountQuota) DESC ) RankResult  
FROM dbo.DimEmployee e  
INNER JOIN dbo.FactSalesQuota sq ON e.EmployeeKey = sq.EmployeeKey  
INNER JOIN dbo.DimSalesTerritory st ON e.SalesTerritoryKey = st.SalesTerritoryKey  
WHERE SalesPersonFlag = 1 AND SalesTerritoryRegion != N'NA'  
GROUP BY LastName, SalesTerritoryRegion;  
```  
  
## <a name="see-also"></a>另請參閱  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  
  
  

