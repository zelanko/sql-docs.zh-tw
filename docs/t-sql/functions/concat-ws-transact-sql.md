---
title: "CONCAT_WS (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 5
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 377db445118e55f1bdeec220f1e6701e9f89706c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="concatws-transact-sql"></a>CONCAT_WS (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ssvNxt-asdb-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-asdb-xxxx-xxx.md)]

第 1 個引數中指定的分隔符號與串連可變數目的引數。 (`CONCAT_WS`指出*串連的分隔符號*。)

##  <a name="syntax"></a>語法   
```sql
CONCAT_WS ( separator, argument1, argument1 [, argumentN]… ) 
```

## <a name="arguments"></a>引數   
separator  
這是任何字元類型的運算式 (`nvarchar`， `varchar`， `nchar`，或`char`)。

引數 1，引數 2，引數*N*  
是任何類型的運算式。

## <a name="return-types"></a>傳回型別
字串。 長度及類型取決於輸入。

## <a name="remarks"></a>備註   
`CONCAT_WS`會接受可變數目的引數，並將它們串連成單一字串做為分隔符號使用的第一個引數。 它需要分隔符號，以及至少兩個引數。否則，就會引發錯誤。 所有引數會隱含轉換成字串類型，然後再行串連。 

隱含轉換成字串會遵循現有的資料類型轉換規則。 如需行為和資料類型轉換的詳細資訊，請參閱[CONCAT (TRANSACT-SQL)](../../t-sql/functions/concat-transact-sql.md)。

### <a name="treatment-of-null-values"></a>NULL 值的處理方式

`CONCAT_WS`會忽略`SET CONCAT_NULL_YIELDS_NULL {ON|OFF}`設定。

如果所有引數為 null、 空字串型別的`varchar(1)`傳回。 

Null 值串連期間會被忽略，而且不加入分隔符號。 這有助於串連字串通常有空白值，例如第二個 [位址] 欄位的常見的案例。 請參閱範例 B。

如果您的案例需要以分隔符號包含 null 值，請參閱 < 範例 C 使用`ISNULL`函式。

## <a name="examples"></a>範例   

### <a name="a--concatenating-values-with-separator"></a>A.  具有分隔符號串連值
下列範例會串連三個資料行從 sys.databases 資料表中，分隔的值與`- `。   

```sql
SELECT CONCAT_WS( ' - ', database_id, recovery_model_desc, containment_desc) AS DatabaseInfo
FROM sys.databases;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

|DatabaseInfo |  
|---------|
|1-簡單-無 |
|2-簡單-無 |
|3-完整-無 |
|4-簡單-無 |


### <a name="b--skipping-null-values"></a>B.  正在略過的 NULL 值
下列範例會忽略`NULL`引數清單中的值。

```sql
SELECT CONCAT_WS(',','1 Microsoft Way', NULL, NULL, 'Redmond', 'WA', 98052) AS Address;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   

```sql
Address
------------   
1 Microsoft Way,Redmond,WA,98052
```

### <a name="c--generating-csv-file-from-table"></a>C.  從資料表產生的 CSV 檔案
下列範例會使用逗號做為分隔符號，並將歸位字元所造成的資料行分隔的值格式。

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

CONCAT_WS 將會忽略資料行中的 NULL 值。 如果某些資料行可為 null，包裝它與`ISNULL`函式，並提供類似下列範例中的預設值：

```sql
SELECT 
STRING_AGG(CONCAT_WS( ',', database_id, ISNULL(recovery_model_desc,''), ISNULL(containment_desc,'N/A')), char(13)) AS DatabaseInfo
FROM sys.databases;
```

## <a name="see-also"></a>另請參閱
[字串函數 (TRANSACT-SQL)](../../t-sql/functions/string-functions-transact-sql.md)  
[CONCAT (TRANSACT-SQL)](../../t-sql/functions/concat-transact-sql.md)      


