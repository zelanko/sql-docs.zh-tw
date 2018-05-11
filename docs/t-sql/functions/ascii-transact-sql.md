---
title: ASCII (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7ead380efbe45e5a04fd530afc42fce0b844773f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
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
**char** 或 **varchar** 類型的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。
  
## <a name="return-types"></a>傳回類型
 **int**  
  
## <a name="remarks"></a>Remarks
ASCII 代表「美國訊息交換標準代碼」(**A**merican **S**tandard **C**ode for **I**nformation **I**nterchange)。 它是現代電腦的字元編碼標準。 如需 ASCII 字元清單，請參閱 [ASCII](https://www.wikipedia.org/wiki/ASCII) 的＜可列印字元＞(Printable characters) 一節。

## <a name="examples"></a>範例  
這個範例假設使用 ASCII 字元集，並傳回 6 個字元的 `ASCII` 值。
  
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
 [CHAR &#40;Transact-SQL&#41;](../../t-sql/functions/char-transact-sql.md)  
 [NCHAR &#40;Transact-SQL&#41;](../../t-sql/functions/nchar-transact-sql.md)  
 [UNICODE &#40;Transact-SQL&#41;](../../t-sql/functions/unicode-transact-sql.md)  
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
  
  


