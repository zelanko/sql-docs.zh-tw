---
title: Cast (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- CAST function
- cast operator
- converting data types [Integration Services]
- data types [Integration Services], expressions
- data types [Integration Services], converting
ms.assetid: d4e915cc-1c7b-4b2e-93b0-13a8b0cb9242
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b19b2e960aa2383568d3977d19368576f4178949
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176438"
---
# <a name="cast-ssis-expression"></a>Cast (SSIS 運算式)
  將運算式從一種資料類型明確轉換成另一種資料類型。 轉換運算子也可以當作截斷運算子使用。

## <a name="syntax"></a>語法

```

(type_spec) expression

```

## <a name="arguments"></a>引數
 *type_spec*是有效[!INCLUDE[ssIS](../../includes/ssis-md.md)]的資料類型。

 *運算式*這是有效的運算式。

## <a name="result-types"></a>結果類型
 
  *type_spec*的資料類型。 如需詳細資訊，請參閱[Integration Services 資料類型](../data-flow/integration-services-data-types.md)。

## <a name="remarks"></a>備註
 下列圖表顯示合法的轉換運算。

 ![資料類型之間的合法和不合法轉換](../media/data-conversion.gif "資料類型之間的合法和不合法轉換")

 轉換成某些資料類型需要參數。 下表列出這些資料類型及其參數。

|資料類型|參數|範例|
|---------------|---------------|-------------|
|DT_STR|*charcount*<br /><br /> *頁*|(DT_STR,30,1252) 會使用 1252 字碼頁將 30 個位元組 (或 30 個單一字元) 轉換成 DT_STR 資料類型。|
|DT_WSTR|*Charcount*|(DT_WSTR,20) 會將成對的 20 個位元組 (或 20 個 Unicode 字元) 轉換成 DT_WSTR 資料類型。|
|DT_BYTES|*Bytecount*|(DT_BYTES,50) 將 50 個位元組轉換為 DT_BYTES 資料類型。|
|DT_DECIMAL|*調整*|(DT_DECIMAL,2) 將數值轉換為 DT_DECIMAL 資料類型，使用 2 位小數位數。|
|DT_NUMERIC|*Precision*<br /><br /> *調整*|(DT_NUMERIC,10,3) 將數值轉換為 DT_NUMERIC 資料類型，使用 10 位有效位數與 3 位小數位數。|
|DT_TEXT|*頁*|(DT_TEXT,1252) 將值轉換為 DT_TEXT 資料類型，使用 1252 字碼頁。|

 當字串轉換成 DT_DATE 或 DT_DATE 轉換成字串時，會使用轉換的地區設定。 不過，日期是使用 ISO 格式 YYYY-MM-DD，而不論地區設定的偏好設定是否使用 ISO 格式。

> [!NOTE]
>  若要將字串轉換成 DT_DATE 以外的日期資料類型，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)。

 如果字碼頁為多位元組字元字碼頁，則位元組和字元的數目可能會不一樣。 使用相同的 *charcount* 值從 DT_WSTR 轉換成 DT_STR，可能會截斷轉換完成字串中的最後幾個字元。 如果目的地資料表的資料行中有足夠的儲存體，請將 *charcount* 參數的值設定為反映多位元組字碼頁所需的位元組數目。 例如，如果您使用 936 字碼頁將字元資料轉換成 DT_STR 資料類型，則應將 *charcount* 設定成最多為您希望資料包含的字元數之兩倍的值；如果使用 UTF-8 字碼頁轉換字元資料，則應將 *charcount* 設定為四倍。

 如需日期資料類型結構的詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)。

## <a name="ssis-expression-examples"></a>SSIS 運算式範例
 此範例會將數值轉換成整數。

```
(DT_I4) 3.57
```

 此範例會使用 1252 字碼頁將整數轉換成字元字串。

```
(DT_STR,1,1252)5
```

 此範例會將 3 個字元的字串轉換成雙位元組字元。

```
(DT_WSTR,3)"Cat"
```

 此範例會將整數轉換成擁有 2 位小數位數的小數。

```
(DT_DECIMAl,2)500
```

 此範例會將整數轉換成擁有 7 位有效位數和 3 位小數位數的數值。

```
(DT_NUMERIC,7,3)4000
```

 此範例會使用 1252 字碼頁將 **FirstName** 資料行中，以 **nvarchar** 資料類型定義且長度為 50 的值轉換成字元字串。

```
(DT_STR,50,1252)FirstName
```

 此範例會將 **DateFirstPurchase** 資料行中 DT_DBDATE 類型的值轉換成長度為 20 的 Unicode 字元字串。

```
(DT_WSTR,20)DateFirstPurchase
```

 此範例會將字串常值「True」轉換成布林。

```
(DT_BOOL)"True"
```

 此範例會將字串常值轉換為 DT_DBDATE。

```
(DT_DBDATE) "1999-10-11"
```

 此範例會將字串常值轉換為使用 5 位數毫秒的 DT_DBTIME2 資料類型 (DT_DBTIME2 資料類型可以指定 0 到 7 位數之間的毫秒)。

```
(DT_DBTIME2, 5) "16:34:52.12345"
```

 此範例會將字串常值轉換為使用 4 位數毫秒的 DT_DBTIMESTAMP2 資料類型 (DT_DBTIMESTAMP2 資料類型可以指定 0 到 7 位數之間的毫秒)。

```
(DT_DBTIMESTAMP2, 4) "1999-10-11 16:34:52.1234"
```

 此範例會將字串常值轉換為使用 7 位數毫秒的 DT_DBTIMESTAMPOFFSET 資料類型 (DT_DBTIMESTAMPOFFSET 資料類型可以指定 0 到 7 位數之間的毫秒)。

```
(DT_DBTIMESTAMPOFFSET, 7) "1999-10-11 16:34:52.1234567 + 5:35"
```

## <a name="see-also"></a>另請參閱
 [運算子優先順序和關聯](operator-precedence-and-associativity.md)性[運算子 &#40;ssis 運算式&#41;](operators-ssis-expression.md) [Integration Services &#40;Ssis&#41;](integration-services-ssis-expressions.md)運算式[中 Integration Services 資料類型](integration-services-data-types-in-expressions.md)


