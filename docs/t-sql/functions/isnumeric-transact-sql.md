---
title: "ISNUMERIC (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ISNUMERIC
- ISNUMERIC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- expressions [SQL Server], valid numeric type
- numeric data
- ISNUMERIC function
- verifying valid numeric type
- valid numeric type [SQL Server]
- checking valid numeric type
ms.assetid: 7aa816de-529a-4f6c-a99f-4d5a9ef599eb
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a3a993fed6ec04a033586feec02afb1a84b983e6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="isnumeric-transact-sql"></a>ISNUMERIC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  判斷運算式是否為有效的數值類型。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
ISNUMERIC ( expression )  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)進行評估。  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="remarks"></a>備註  
 當輸入運算式評估為有效數值資料類型時，ISNUMERIC 就會傳回 1，否則便傳回 0。 有效數值資料類型包括下列各種類型：  
  
|||  
|-|-|  
|**int**|**numeric**|  
|**bigint**|**money**|  
|**smallint**|**smallmoney**|  
|**tinyint**|**float**|  
|**decimal**|**real**|  
  
> [!NOTE]  
>  ISNUMERIC 會針對某些不是數字的字元傳回 1，例如加號 (+)、減號 (-) 和有效貨幣符號 (如錢幣符號 ($))。 如需貨幣符號的完整清單，請參閱[money 和 smallmoney &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md).  
  
## <a name="examples"></a>範例  
 下列範例會使用 `ISNUMERIC`，傳回所有非數值的郵遞區號。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, PostalCode  
FROM Person.Address   
WHERE ISNUMERIC(PostalCode)<> 1;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會使用 `ISNUMERIC`，傳回所有非數值的郵遞區號。  
  
```  
USE master;  
GO  
SELECT name, isnumeric(name) AS IsNameANumber, database_id, isnumeric(database_id) AS IsIdANumber   
FROM sys.databases;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  


