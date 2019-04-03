---
title: TRIM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: conceptual
f1_keywords:
- TRIM
- TRIM_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- TRIM function
ms.assetid: a00245aa-32c7-4ad4-a0d1-64f3d6841153
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||= azure-sqldw-latest ||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ae5abf48d2cdd2325c69df1c1f680594a7d8b3eb
ms.sourcegitcommit: a9a03f9a7ec4dad507d2dfd5ca33571580114826
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2019
ms.locfileid: "58566397"
---
# <a name="trim-transact-sql"></a>TRIM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-asdw-xxx-md.md)]

從字串的開頭或結尾移除空白字元 `char(32)` 或其他指定的字元。  
 
## <a name="syntax"></a>語法   
``` 
-- Syntax for SQL Server and Azure SQL Database
TRIM ( [ characters FROM ] string ) 
```
[//]: # "[ BOTH | LEADING | TRAILING ] 還無法使用。"

```
-- Syntax for Azure SQL Data Warehouse
TRIM ( string )
```
## <a name="arguments"></a>引數

字元是應移除所含字元的任何非 LOB 字元類型 (`nvarchar`、`varchar`、`nchar` 或 `char`) 的常值、變數或函式呼叫。 不允許 `nvarchar(max)` 和 `varchar(max)` 類型。

字串是應移除字元的任何字元類型 (`nvarchar`、`varchar`、`nchar` 或 `char`) 的運算式。

## <a name="return-types"></a>傳回類型
以字串引數的類型傳回字元運算式，其中空白字元 `char(32)` 或其他指定的字元會從兩端移除。 如果輸入字串為 `NULL`，傳回 `NULL`。

## <a name="remarks"></a>Remarks
根據預設，`TRIM` 函數會從兩端移除空白字元 `char(32)`。 此行為相當於 `LTRIM(RTRIM(@string))`。 具有指定字元之 `TRIM` 函數的行為與 `REPLACE` 函數的行為相同，其中會將開頭或結尾的字元取代為空字串。


## <a name="examples"></a>範例
### <a name="a--removes-the-space-character-from-both-sides-of-string"></a>A.  從字串兩端移除空白字元   
下列範例會移除 `test` 這個字前面和後面的空格。   
```sql
SELECT TRIM( '     test    ') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

`test`


### <a name="b--removes-specified-characters-from-both-sides-of-string"></a>B.  從字串的兩端移除指定的字元   
下列範例會移除尾端句號和尾端空格。
```sql
SELECT TRIM( '.,! ' FROM  '#     test    .') AS Result;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   
`#     test`


## <a name="see-also"></a>另請參閱
 [LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)  
 [LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)  
 [RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)  
 [RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)  
 [STRING_SPLIT &#40;Transact-SQL&#41;](../../t-sql/functions/string-split-transact-sql.md)  
 [SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)  
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
