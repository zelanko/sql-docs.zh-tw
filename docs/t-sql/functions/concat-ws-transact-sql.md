---
title: CONCAT_WS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- CONCAT_WS
- CONCAT_WS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_WS function
ms.assetid: f1375fd7-a2fd-48bf-922a-4f778f0deb1f
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 7d7932c1887c82b2a10702f9054706e4cf9bce71
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="concatws-transact-sql"></a>CONCAT_WS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

將可變數量的引數與第 1 個引數中指定的分隔符號串連。 (`CONCAT_WS` 指出 *與分隔符號的串連*。)

##  <a name="syntax"></a>語法   
```sql
CONCAT_WS ( separator, argument1, argument1 [, argumentN]… ) 
```

## <a name="arguments"></a>引數   
separator  
這是屬於任何類型的運算式 (`nvarchar``varchar``nchar`或 `char`)。

引數1、引數2、引數*N*  
這是任何類型的運算式。

## <a name="return-types"></a>傳回類型
字串。 長度及類型取決於輸入。

## <a name="remarks"></a>Remarks   
`CONCAT_WS` 會採用可變數量的引數，並用第一個引數當作分隔符號，將它們串連成單一字串。 其必須有分隔符號且至少有兩個引數，否則會引發錯誤。 所有引數皆會以隱含方式轉換為字串類型，然後再行串連。 

隱含轉換成字串會遵循現有的資料類型轉換規則。 如需行為和資料類型轉換的詳細資訊，請參閱 [CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md)。

### <a name="treatment-of-null-values"></a>NULL 值的處理方式

`CONCAT_WS` 會忽略 `SET CONCAT_NULL_YIELDS_NULL {ON|OFF}` 字串。

如果所有引數都是 Null，會傳回類型為 `varchar(1)` 的空白字串。 

Null 值在串連期間會被忽略，而且不添加分隔符號。 這有助於串連通常有空白值之字串的常見案例，例如第二個位址欄位。 請參閱範例 B。

如果您的案例需要包含 Null 值和分隔符號，請參閱使用 `ISNULL` 函數的範例 C。

## <a name="examples"></a>範例   

### <a name="a--concatenating-values-with-separator"></a>A.  使用分隔符號串連值
下列範例會從 sys.databases 資料表中串連三個資料行，並用 `- `分隔值。   

```sql
SELECT CONCAT_WS( ' - ', database_id, recovery_model_desc, containment_desc) AS DatabaseInfo
FROM sys.databases;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

|DatabaseInfo |  
|---------|
|1 - SIMPLE - NONE |
|2 - SIMPLE - NONE |
|3 - FULL - NONE |
|4 - SIMPLE - NONE |


### <a name="b--skipping-null-values"></a>B.  跳過 NULL 值
下列範例會忽略引數清單中的 `NULL` 值。

```sql
SELECT CONCAT_WS(',','1 Microsoft Way', NULL, NULL, 'Redmond', 'WA', 98052) AS Address;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
Address
------------   
1 Microsoft Way,Redmond,WA,98052
```

### <a name="c--generating-csv-file-from-table"></a>C.  從資料表產生 CSV 檔案
下列範例使用逗號作為分隔符號，並新增歸位字元以便造成資料行分隔的值格式。

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, recovery_model_desc, containment_desc), char(13)) AS DatabaseInfo
FROM sys.databases
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
DatabaseInfo
------------   
1,SIMPLE,NONE
2,SIMPLE,NONE
3,FULL,NONE 
4,SIMPLE,NONE 
```

CONCAT_WS 將忽略資料行中的 NULL 值。 如果某些資料行可為 Null，將它與 `ISNULL` 函數包裝在一起，並提供類似下列範例中的預設值：

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, ISNULL(recovery_model_desc,''), ISNULL(containment_desc,'N/A')), char(13)) AS DatabaseInfo
FROM sys.databases;
```

## <a name="see-also"></a>另請參閱
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [TRANSLATE &#40;Transact-SQL&#41;](../../t-sql/functions/translate-transact-sql.md)  
 [字串函數 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)  

