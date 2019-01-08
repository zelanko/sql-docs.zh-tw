---
title: RIGHT (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- RIGHT function
ms.assetid: 83e70e75-4be5-4783-a8cf-032f82afe16e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0e8d1cfdda299c786aa926aad26f724009a683ec
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52796105"
---
# <a name="right-ssis-expression"></a>RIGHT (SSIS 運算式)
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
  
## <a name="remarks"></a>備註  
 如果 *integer_expression* 大於 *character_expression*的長度，函數會傳回 *character_expression*。  
  
 如果 *integer_expression* 為零，則函數會傳回長度為 0 的字串。  
  
 如果 *integer_expression* 為負數，則函數會傳回錯誤。  
  
 *integer_expression* 引數可採用變數和資料行。  
  
 RIGHT 只適用於 DT_WSTR 資料類型。 如果 *character_expression* 引數是字串常值或具有 DT_STR 資料類型的資料行，則該引數會在 RIGHT 執行其作業前隱含轉換成 DT_WSTR 資料類型。 其他資料類型必須明確地轉換為 DT_WSTR 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)和[轉換 &#40;SSIS 運算式&#41;](cast-ssis-expression.md)。  
  
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
 [LEFT &#40;SSIS 運算式&#41;](left-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](functions-ssis-expression.md)  
  
  
