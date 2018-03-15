---
title: TRANSLATE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- TRANSLATE
- TRANSLATE_TSQL
helpviewer_keywords:
- TRANSLATE function
ms.assetid: 0426fa90-ef6d-4d19-8207-02ee59f74aec
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e7ea679043b83d8cee26f431602450d023516647
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="translate-transact-sql"></a>TRANSLATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

將第二個引數中指定的部分字元轉譯為一組目的地字元之後，傳回提供作為第一個引數的字串。

## <a name="syntax"></a>語法   
```
TRANSLATE ( inputString, characters, translations) 
```

## <a name="arguments"></a>引數   

inputString   
這是任何字元類型的[運算式](../../t-sql/language-elements/expressions-transact-sql.md) (nvarchar、varchar、nchar、char)。

字元   
這是任何字元類型的[運算式](../../t-sql/language-elements/expressions-transact-sql.md)，其中包含應該遭到取代的字元。

翻譯   
這是類型和長度符合第二個引數的字元[運算式](../../t-sql/language-elements/expressions-transact-sql.md)。

## <a name="return-types"></a>傳回類型   
將相同類型的字元運算式當作 `inputString` 傳回，其中第二個引數中的字元會取代為第三個引數中相符的字元。

## <a name="remarks"></a>Remarks   

如果字元和轉譯的長度不同，則 `TRANSLATE` 函數會傳回錯誤。 如果 Null 值是當作字元或取代引數提供，則 `TRANSLATE` 函數應該會傳回未變更的輸入。 `TRANSLATE` 函數的行為應該與 [REPLACE](../../t-sql/functions/replace-transact-sql.md) 函數相同。   

`TRANSLATE` 函數的行為相當於使用多個 `REPLACE` 函數。

`TRANSLATE` 永遠是 SC 定序感知。

## <a name="examples"></a>範例   

### <a name="a-replace-square-and-curly-braces-with-regular-braces"></a>A. 將方括號和大括號取代為一般括號    
下列查詢會將輸入字串中的方括號和大括號取代為括號：
```
SELECT TRANSLATE('2*[3+4]/{7-2}', '[]{}', '()()');
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
```
2*(3+4)/(7-2)
```

>  [!NOTE]
>  此範例中的 `TRANSLATE` 函數相當於使用 `REPLACE` 的陳述式但更為簡單：`SELECT REPLACE(REPLACE(REPLACE(REPLACE('2*[3+4]/{7-2}','[','('), ']', ')'), '{', '('), '}', ')');` 


###  <a name="b-convert-geojson-points-into-wkt"></a>B. 將 GeoJSON 點轉換成 WKT    
GeoJSON 是一種格式，可針對各種不同的地理資料結構編碼。 開發人員可以利用 `TRANSLATE` 函數，輕鬆地將 GeoJSON 點轉換為 WKT 格式，反之亦然。 下列查詢會將輸入中的方括號和大括號取代為一般括號：   
```sql
SELECT TRANSLATE('[137.4, 72.3]' , '[,]', '( )') AS Point,
    TRANSLATE('(137.4 72.3)' , '( )', '[,]') AS Coordinates;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   


|點  |座標 |  
---------|--------- |
(137.4  72.3) |[137.4,72.3] |


## <a name="see-also"></a>另請參閱
 [CONCAT &#40;Transact-SQL&#41;](../../t-sql/functions/concat-transact-sql.md)  
 [CONCAT_WS &#40;Transact-SQL&#41;](../../t-sql/functions/concat-ws-transact-sql.md)  
 [FORMATMESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/formatmessage-transact-sql.md)  
 [QUOTENAME &#40;Transact-SQL&#41;](../../t-sql/functions/quotename-transact-sql.md)  
 [REPLACE &#40;Transact-SQL&#41;](../../t-sql/functions/replace-transact-sql.md)  
 [REVERSE &#40;Transact-SQL&#41;](../../t-sql/functions/reverse-transact-sql.md)  
 [STRING_AGG &#40;Transact-SQL&#41;](../../t-sql/functions/string-agg-transact-sql.md)  
 [STRING_ESCAPE &#40;Transact-SQL&#41;](../../t-sql/functions/string-escape-transact-sql.md)  
 [STUFF &#40;Transact-SQL&#41;](../../t-sql/functions/stuff-transact-sql.md)  
 [字串函數 (Transact-SQL)](../../t-sql/functions/string-functions-transact-sql.md)   

