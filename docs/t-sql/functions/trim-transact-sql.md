---
title: "TRIM (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- TRIM
- TRIM_TSQL
dev_langs: TSQL
helpviewer_keywords: TRIM function
ms.assetid: a00245aa-32c7-4ad4-a0d1-64f3d6841153
caps.latest.revision: "4"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 88ba00513a8f76ae560ed717801150aa9b80046e
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="trim-transact-sql"></a>TRIM (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

會移除空白字元`char(32)`或其他指定的字元開始或字串的結尾。  
 
## <a name="syntax"></a>語法   
```
TRIM ( [ characters FROM ] string ) 
```
[//]: # "[兩者 |前置 |尾端] 不尚未使用。"

## <a name="arguments"></a>引數   

字元   
是常值、 變數或函式呼叫的任何非 LOB 字元類型 (`nvarchar`， `varchar`， `nchar`，或`char`) 包含應移除的字元。 `nvarchar(max)`和`varchar(max)`不允許類型。

string   
這是任何字元類型的運算式 (`nvarchar`， `varchar`， `nchar`，或`char`) 字元應加以移除。

## <a name="return-types"></a>傳回類型   
傳回字元運算式具有類型的字串引數其中空白字元`char(32)`或其他指定的字元會從兩邊移除。 傳回`NULL`輸入的字串是否`NULL`。

## <a name="remarks"></a>備註   
根據預設`TRIM`函式會移除空白字元`char(32)`兩端。 這相當於 `LTRIM(RTRIM(@string))`。 行為`TRIM `函式具有指定的字元是相同的行為`REPLACE`函式的開頭或結尾的字元位置取代空字串。


## <a name="examples"></a>範例
### <a name="a--removes-the-space-character-from-both-sides-of-string"></a>A.  字串的兩方會移除空白字元   
下列範例會從之前和之後 word 移除空格`test`。   
```sql
SELECT TRIM( '     test    ') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

`test`


### <a name="b--removes-specified-characters-from-both-sides-of-string"></a>B.  移除指定的字元字串的兩面   
下列範例會移除尾端句號和尾端空白。
```sql
SELECT TRIM( '.,! ' FROM  '#     test    .') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
`#     test`


## <a name="see-also"></a>另請參閱
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [權限 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [字串函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/string-functions-transact-sql.md)   
