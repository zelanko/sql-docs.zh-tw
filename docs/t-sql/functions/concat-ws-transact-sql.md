---
title: CONCAT_WS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- CONCAT_WS
- CONCAT_WS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CONCAT_WS function
ms.assetid: f1375fd7-a2fd-48bf-922a-4f778f0deb1f
caps.latest.revision: 5
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: e1a3d184ccdd0a1716fdace286b2bb8ed6a6cae6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33055185"
---
# <a name="concatws-transact-sql"></a>CONCAT_WS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

此函式會傳回透過以端對端方式串連 (或聯結) 兩個以上字串值所產生的字串。 它使用第一個函數引數中指定的分隔符號來分隔這些串連的字串值。 (`CONCAT_WS` 指出 *與分隔符號的串連*。)

##  <a name="syntax"></a>語法   
```sql
CONCAT_WS ( separator, argument1, argument1 [, argumentN]… ) 
```

## <a name="arguments"></a>引數   
separator  
屬於任何類型的運算式 (`char`'、`nchar`'、`nvarchar` 或 `varchar`)。

引數1、引數2、引數*N*  
任意類型的運算式。

## <a name="return-types"></a>傳回類型
長度和類型取決於輸入的字串值。

## <a name="remarks"></a>Remarks   
`CONCAT_WS` 會採用可變數量的字串引數，並將其串連 (聯結) 成單一字串。 它使用第一個函數引數中指定的分隔符號來分隔這些串連的字串值。 `CONCAT_WS` 需要分隔引數和至少兩個其他字串值引數。否則，`CONCAT_WS` 會引發錯誤。 `CONCAT_WS` 會在串連之前將所有引數隱含地轉換成字串類型。 

隱含轉換成字串會遵循現有的資料類型轉換規則。 如需行為和資料類型轉換的詳細資訊，請參閱 [CONCAT (Transact-SQL)](../../t-sql/functions/concat-transact-sql.md)。

### <a name="treatment-of-null-values"></a>NULL 值的處理方式

`CONCAT_WS` 會忽略 `SET CONCAT_NULL_YIELDS_NULL {ON|OFF}` 字串。

如果 `CONCAT_WS` 收到全部都是 NULL 值的引數，則會傳回 varchar(1) 類型的空字串。

Null 值在串連期間會被 `CONCAT_WS` 忽略，而且不添加分隔符號。 因此，`CONCAT_WS` 可以乾淨地處理可能有「空白」值 - 例如，第二個地址欄位的字串串連。 如需詳細資訊，請參閱範例 B。

如果案例牽涉到被分隔符號隔開的 Null 值，請考慮使用 `ISNULL` 函數。 如需詳細資訊，請參閱範例 C。

## <a name="examples"></a>範例   

### <a name="a--concatenating-values-with-separator"></a>A.  使用分隔符號串連值
此範例會從 sys.databases 資料表中串連三個資料行，並用 `- ` 隔開每個值。   

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
此範例會忽略引數清單中的 `NULL` 值。

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
此範例使用逗號 `,` 作為分隔符號值，並在結果集的資料行分隔值格式中新增歸位字元 `char(13)`。

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

CONCAT_WS 會忽略資料行中的 NULL 值。 使用 `ISNULL` 函數來包裝可為 Null 的資料行，並提供預設值。 如需詳細資訊，請參閱此範例：

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

