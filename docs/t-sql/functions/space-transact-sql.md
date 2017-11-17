---
title: "空間 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SPACE_TSQL
- SPACE
dev_langs:
- TSQL
helpviewer_keywords:
- strings [SQL Server], repeated spaces
- repeated spaces
- SPACE function
ms.assetid: b4fac3b8-2d47-4c11-a6a6-009e5a538f40
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f5de41d3d7619af5f83fa2bee8cd30f980f291b7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="space-transact-sql"></a>SPACE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回重複空格的字串。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SPACE ( integer_expression )  
```  
  
## <a name="arguments"></a>引數  
 *integer_expression*  
 這是代表空格數的正整數。 如果*clause><*是負數，會傳回 null 字串。  
  
 如需詳細資訊，請參閱[運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
## <a name="return-types"></a>傳回類型  
 **varchar**  
  
## <a name="remarks"></a>備註  
 若要在 Unicode 資料中加入空格，或者傳回超過 8000 個字元空格，請使用 REPLICATE 而非 SPACE。  
  
## <a name="examples"></a>範例  
 下列範例會修剪姓氏，並且將逗號、兩個空格以及 `Person` 之 `AdventureWorks2012` 資料表所列人員的名字串連起來。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT RTRIM(LastName) + ',' + SPACE(2) +  LTRIM(FirstName)  
FROM Person.Person  
ORDER BY LastName, FirstName;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會修剪姓氏，並且將逗號、兩個空格以及 `DimCustomer` 之 `AdventureWorksPDW2012` 資料表所列人員的名字串連起來。  
  
```  
-- Uses AdventureWorks  
  
SELECT RTRIM(LastName) + ',' + SPACE(2) +  LTRIM(FirstName)  
FROM dbo.DimCustomer  
ORDER BY LastName, FirstName;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [複寫 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/replicate-transact-sql.md)   
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
 [內建函數 &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)  
  
  



