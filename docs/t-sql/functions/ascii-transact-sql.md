---
title: "ASCII (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ASCII_TSQL
- ASCII
dev_langs:
- TSQL
helpviewer_keywords:
- ASCII function
- characters [SQL Server], ASCII
- code [SQL Server], ASCII
- leftmost character of expression
ms.assetid: 45c2044a-0593-4805-8bae-0fad4bde2e6b
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d2c65df1f005b3d624f6a56f689f4125ec8175a7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="ascii-transact-sql"></a>ASCII (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
  
  



