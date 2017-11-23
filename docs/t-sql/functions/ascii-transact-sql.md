---
title: "ASCII (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ASCII_TSQL
- ASCII
dev_langs: TSQL
helpviewer_keywords:
- ASCII function
- characters [SQL Server], ASCII
- code [SQL Server], ASCII
- leftmost character of expression
ms.assetid: 45c2044a-0593-4805-8bae-0fad4bde2e6b
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 02267e12891bf1ab237cd7bffb2fa89f4be32363
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="ascii-transact-sql"></a>ASCII (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回字元運算式最左側字元的 ASCII 字碼值。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
ASCII ( character_expression )  
```  
  
## <a name="arguments"></a>引數  
*character_expression*  
是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)型別的**char**或**varchar**。
  
## <a name="return-types"></a>傳回型別
 **int**  
  
## <a name="remarks"></a>備註
ASCII 是美國資訊交換的標準代碼的縮寫。 它是一種字元編碼的電腦所使用的標準。 如需 ASCII 字元的清單，請參閱**可列印字元**區段[ASCII](https://www.wikipedia.org/wiki/ASCII)。

## <a name="examples"></a>範例  
下列範例假設 ASCII 字元集，並傳回`ASCII`6 個字元的值。
  
```sql
SELECT ASCII('A') AS A, ASCII('B') AS B,   
ASCII('a') AS a, ASCII('b') AS b,  
ASCII(1) AS [1], ASCII(2) AS [2];  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
A           B           a           b           1           2  
----------- ----------- ----------- ----------- ----------- -----------  
65          66          97          98          49          50  
```  
  
## <a name="see-also"></a>另請參閱
[字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)
  
  


