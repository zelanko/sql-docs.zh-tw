---
title: "翻譯 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 12/16/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- TRANSLATE
- TRANSLATE_TSQL
helpviewer_keywords: TRANSLATE function
ms.assetid: 0426fa90-ef6d-4d19-8207-02ee59f74aec
caps.latest.revision: "5"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fda4f4793f0692b77ba8a606c904612674e29721
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="translate-transact-sql"></a>翻譯 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

傳回提供做為第一個引數之後的第二個引數中指定某些字元轉譯為目的地的一組字元的字串。

## <a name="syntax"></a>語法   
```
TRANSLATE ( inputString, characters, translations) 
```

## <a name="arguments"></a>引數   

inputString   
是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)nvarchar、 varchar、 nchar （char） 的任何字元類型。

字元   
是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)包含字元應該用來取代任何字元類型。

翻譯   
是字元[運算式](../../t-sql/language-elements/expressions-transact-sql.md)符合第二個引數類型和長度。

## <a name="return-types"></a>傳回類型   
傳回字元運算式做為相同型別的`inputString`其中字元的第二個引數會取代從第三個引數比對的字元。

## <a name="remarks"></a>備註   

`TRANSLATE`如果字元和翻譯有不同的長度，則函數會傳回錯誤。 `TRANSLATE`如果做為字元或取代引數提供 null 值，函式應傳回未變更的輸入。 行為`TRANSLATE`函式應該與相同[取代](../../t-sql/functions/replace-transact-sql.md)函式。   

行為`TRANSLATE`函數即相當於使用多個`REPLACE`函式。

`TRANSLATE`一定是搭配 SC 定序感知。

## <a name="examples"></a>範例   

### <a name="a-replace-square-and-curly-braces-with-regular-braces"></a>A. 取代規則的大括號的正方形和大括號    
下列查詢會加上括弧取代輸入字串中的方形和大括號：
```
SELECT TRANSLATE('2*[3+4]/{7-2}', '[]{}', '()()');
```
[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]
```
2*(3+4)/(7-2)
```

>  [!NOTE]
>  `TRANSLATE`函式，在此範例中是相當於但遠比下列陳述式使用 simplier `REPLACE`:`SELECT REPLACE(REPLACE(REPLACE(REPLACE('2*[3+4]/{7-2}','[','('), ']', ')'), '{', '('), '}', ')');` 


###  <a name="b-convert-geojson-points-into-wkt"></a>B. 將 GeoJSON 點轉換成 well-known text，WKT    
GeoJSON 是一種格式的編碼方式各種不同的地理資料結構。 與`TRANSLATE`函式，開發人員可以輕鬆轉換 GeoJSON 點 well-known text，WKT 格式，反之亦然。 下列查詢會將輸入中的方形和大括號取代規則的大括號：   
```tsql
SELECT TRANSLATE('[137.4, 72.3]' , '[,]', '( )') AS Point,
    TRANSLATE('(137.4 72.3)' , '( )', '[,]') AS Coordinates;
```

[!INCLUDE[ssResult_md](../../includes/ssresult-md.md)]   


|點  |座標 |  
---------|--------- |
(137.4  72.3) |[137.4,72.3] |


## <a name="see-also"></a>請參閱＜

[字串函數 (TRANSACT-SQL)](../../t-sql/functions/string-functions-transact-sql.md)   
[取代 (TRANSACT-SQL)](../../t-sql/functions/replace-transact-sql.md)   

