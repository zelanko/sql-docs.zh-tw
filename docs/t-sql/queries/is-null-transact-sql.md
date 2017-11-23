---
title: "為 NULL (TRANSACT-SQL) |Microsoft 文件"
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
f1_keywords:
- NULL_TSQL
- IS_[NOT]_NULL_TSQL
- IS_NULL_TSQL
- NULL
- '[NOT]_TSQL'
- IS
- IS_TSQL
- IS NULL
- IS [NOT] NULL
- '[NOT]'
dev_langs: TSQL
helpviewer_keywords:
- verifying nullability
- IS NOT NULL clause
- null values [SQL Server], verifying
- null values [SQL Server], IS [NOT] NULL
- IS [NOT] NULL clause
- testing nullability
- checking nullability
ms.assetid: cdc45cd8-e9b6-4648-8417-892fbeab15af
caps.latest.revision: "37"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 4b978c9c51acde0cacca4b65103681009f1975b7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="is-null-transact-sql"></a>為 NULL (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  判斷指定的運算式是否為 NULL。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
expression IS [ NOT ] NULL  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 任何有效[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。  
  
 NOT  
 指定執行布林結果的否定運算。 這個述詞會反轉它的傳回值，如果值不是 NULL，就傳回 TRUE，如果值是 NULL，就傳回 FALSE。  
  
## <a name="result-types"></a>結果類型  
 **布林**  
  
## <a name="return-code-values"></a>傳回碼值  
 如果值*運算式*是 NULL，IS NULL 會傳回 TRUE; 否則它會傳回 FALSE。  
  
 如果值*運算式*是 NULL，IS NOT NULL 會傳回 FALSE; 否則它會傳回 TRUE。  
  
## <a name="remarks"></a>備註  
 若要判斷運算式是否為 NULL，請利用 IS NULL 或 IS NOT NULL 來取代比較運算子 (如 = 或 !=)。 當兩個引數或其中一個引數是 NULL 時，比較運算子會傳回 UNKNOWN。  
  
## <a name="examples"></a>範例  
 下列範例會傳回重量少於 `10` 磅，或顏色未知之所有產品的名稱和重量，或傳回 `NULL`。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name, Weight, Color  
FROM Production.Product  
WHERE Weight < 10.00 OR Color IS NULL  
ORDER BY Name;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會傳回所有中間的縮寫與員工的完整名稱。  
  
```  
-- Uses AdventureWorks  
  
SELECT FirstName, LastName, MiddleName  
FROM DIMEmployee  
WHERE MiddleName IS NOT NULL  
ORDER BY LastName DESC;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [案例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/case-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [像 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [邏輯運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/logical-operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [其中 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

