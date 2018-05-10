---
title: SUBSTRING (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SUBSTRING function
- part of expression returned [Integration Services]
ms.assetid: 3a46748a-f5f8-4a6c-9108-673666754068
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 17a66809ba29a56748e4f59aa39905f13f9216d8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="substring-ssis-expression"></a>SUBSTRING (SSIS 運算式)
  傳回從指定位置開始算起指定長度的字元運算式部分。 *position* 參數和 *length* 參數必須評估為整數。  
  
## <a name="syntax"></a>語法  
  
```  
  
SUBSTRING(character_expression, position, length)  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 要擷取字元的字元運算式。  
  
 *position*  
 是指定子字串開始處的整數。  
  
 *length*  
 是指定做為字元數之子字串長度的整數。  
  
## <a name="result-types"></a>結果類型  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 SUBSTRING 使用以 1 為基底的索引。 如果 *position* 是 1，則子字串會以 *character_expression*中的第一個字元開頭。  
  
 SUBSTRING 只適用於 DT_WSTR 資料類型。 如果 *character_expression* 引數是字串常值或具有 DT_STR 資料類型的資料行，則該引數會在 SUBSTRING 執行其作業前隱含轉換成 DT_WSTR 資料類型。 其他資料類型必須明確地轉換為 DT_WSTR 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)和[轉換 &#40;SSIS 運算式&#41;](../../integration-services/expressions/cast-ssis-expression.md)。  
  
 如果引數為 Null，則 SUBSTRING 會傳回 Null 結果。  
  
 運算式中的所有引數都可使用變數和資料行。  
  
 *length* 引數可以超過字串長度。 在此情況下，函數會傳回字串的其餘部份。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會從字串常值傳回以第 4 個字元開頭的兩個字元。 傳回結果為 "ph"。  
  
```  
SUBSTRING("elephant",4,2)  
```  
  
 此範例會傳回從字串常值中第 4 個字元起算的其餘部份。 傳回結果為 "phant"。 *length* 引數超過字串長度並非錯誤。  
  
```  
SUBSTRING ("elephant",4,50)  
```  
  
 此範例會傳回 **MiddleName** 資料行中的第一個字母。  
  
```  
SUBSTRING(MiddleName,1,1)  
```  
  
 此範例會使用 *position* 和 *length* 引數中的變數。 如果 **Start** 是 1 且 **Length** 是 5，則函數會傳回 **Name** 資料行中的前五個字元。  
  
```  
SUBSTRING(Name,@Start,@Length)  
```  
  
 此範例會傳回 **PostalCode** 變數中，從第六個字元起算的後四個字元。  
  
```  
SUBSTRING (@PostalCode,6,4)  
```  
  
 此範例會從字串常值中傳回零長度的字串。  
  
```  
SUBSTRING ("Redmond",4,0)  
```  
  
## <a name="see-also"></a>另請參閱  
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
