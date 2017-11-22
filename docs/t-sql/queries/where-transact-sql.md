---
title: "位置 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WHERE_TSQL
- WHERE
dev_langs: TSQL
helpviewer_keywords:
- retrieving rows
- clauses [SQL Server], WHERE
- WHERE clause, about WHERE clause
- row retrieval [SQL Server], WHERE clause
- WHERE clause
ms.assetid: a8430421-7bce-4fab-a2d2-56c00a3c6fa4
caps.latest.revision: "37"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 122bf7814a90223319310c49749eb94eea02581a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="where-transact-sql"></a>WHERE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指定查詢所傳回之資料列的搜尋條件。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
[ WHERE <search_condition> ]  
```  
  
## <a name="arguments"></a>引數  
\<*s* > 定義要傳回的資料列，必須滿足的條件。 搜尋條件中所能包括的述詞數目沒有限制。 如需有關搜尋條件和述詞的詳細資訊，請參閱[搜尋條件 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
## <a name="examples"></a>範例  
 下列範例示範如何在 `WHERE` 子句中使用某些常見的搜尋條件。  
  
### <a name="a-finding-a-row-by-using-a-simple-equality"></a>A. 使用簡單的等式尋找資料列  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName = 'Smith' ;  
```  
  
### <a name="b-finding-rows-that-contain-a-value-as-part-of-a-string"></a>B. 尋找包含做為字串一部分之值的資料列  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName LIKE ('%Smi%');  
```  
  
### <a name="c-finding-rows-by-using-a-comparison-operator"></a>C. 使用比較運算子尋找資料列  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey  <= 500;  
```  
  
### <a name="d-finding-rows-that-meet-any-of-three-conditions"></a>D. 尋找符合三個條件中任何一個條件的資料列  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey = 1 OR EmployeeKey = 8 OR EmployeeKey = 12;  
```  
  
### <a name="e-finding-rows-that-must-meet-several-conditions"></a>E. 尋找必須符合數個條件的資料列  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey <= 500 AND LastName LIKE '%Smi%' AND FirstName LIKE '%A%';  
```  
  
### <a name="f-finding-rows-that-are-in-a-list-of-values"></a>F. 尋找位於值清單中的資料列  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE LastName IN ('Smith', 'Godfrey', 'Johnson');  
```  
  
### <a name="g-finding-rows-that-have-a-value-between-two-values"></a>G. 尋找兩個值之間有一個值的資料列  
  
```  
-- Uses AdventureWorks  
  
SELECT EmployeeKey, LastName  
FROM DimEmployee  
WHERE EmployeeKey Between 100 AND 200;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [述詞 &#40;TRANSACT-SQL &#41;](~/t-sql/queries/predicates.md)   
 [搜尋條件 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/search-condition-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  
  
  


