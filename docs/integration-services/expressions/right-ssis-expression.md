---
title: RIGHT (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- RIGHT function
ms.assetid: 83e70e75-4be5-4783-a8cf-032f82afe16e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1dcd15de93893b34a6842110767b2242fbc3a146
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297403"
---
# <a name="right-ssis-expression"></a>RIGHT (SSIS 運算式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  傳回來自給定字元運算式最右邊部分的指定字元數。  
  
## <a name="syntax"></a>語法  
  
```  
  
RIGHT(character_expression,integer_expression)  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 要擷取字元的字元運算式。  
  
 *integer_expression*  
 為表示要傳回字元數的整數運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_WSTR  
  
## <a name="remarks"></a>Remarks  
 如果 *integer_expression* 大於 *character_expression*的長度，函數會傳回 *character_expression*。  
  
 如果 *integer_expression* 為零，則函數會傳回長度為 0 的字串。  
  
 如果 *integer_expression* 為負數，則函數會傳回錯誤。  
  
 *integer_expression* 引數可採用變數和資料行。  
  
 RIGHT 只適用於 DT_WSTR 資料類型。 如果 *character_expression* 引數是字串常值或具有 DT_STR 資料類型的資料行，則該引數會在 RIGHT 執行其作業前隱含轉換成 DT_WSTR 資料類型。 其他資料類型必須明確地轉換為 DT_WSTR 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)和[轉換 &#40;SSIS 運算式&#41;](../../integration-services/expressions/cast-ssis-expression.md)。  
  
 如果其中一個引數為 Null，則 RIGHT 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 下列範例會使用字串常值。 傳回結果為 `"Bike"`。  
  
```  
RIGHT("Mountain Bike", 4)  
```  
  
 下列範例會從 `Times` 資料行傳回 `Name` 變數中指定的最右邊字元數。 如果 `Name` 為 `Touring Front Wheel` 且 `Times` 為 5，傳回的結果為 `"Wheel"`。  
  
```  
RIGHT(Name, @Times)  
```  
  
 下列範例亦會從 `Times` 資料行傳回 `Name` 變數中指定的最右邊字元數。 `Times` 的資料類型為非整數，且運算式包括明確轉換成 DT_I2 的資料類型。 如果 `Name` 是 `Touring Front Wheel` ，而 `Times` 是 `4.32`，傳回的結果會是 `"heel"` ，因為 RIGHT 函數會將值 4.32 轉換成 4，然後傳回最右邊的四個字元。  
  
```  
RIGHT(Name, (DT_I2)@Times))  
```  
  
## <a name="see-also"></a>另請參閱  
 [LEFT &#40;SSIS 運算式&#41;](../../integration-services/expressions/left-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
