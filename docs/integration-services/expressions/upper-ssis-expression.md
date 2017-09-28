---
title: "UPPER （SSIS 運算式） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- UPPER function
- converting lowercase to uppercase
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: d33985f7-1048-4023-83e4-274090acda78
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1764b39b0242ce7e23d56c9c74f7b953f45009b2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="upper-ssis-expression"></a>UPPER (SSIS 運算式)
  傳回小寫字元轉換為大寫字元之後的字元運算式。  
  
## <a name="syntax"></a>語法  
  
```  
  
UPPER(character_expression)  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 是轉換成大寫字元的字元運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_WSTR  
  
## <a name="remarks"></a>備註  
 UPPER 只適用於 DT_WSTR 資料類型。 如果 *character_expression* 引數是字串常值或具有 DT_STR 資料類型的資料行，則該引數會在 LOWER 執行其作業前隱含轉換成 DT_WSTR 資料類型。 其他資料類型必須明確地轉換為 DT_WSTR 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)和 [Cast &#40;SSIS 運算式&#41;](../../integration-services/expressions/cast-ssis-expression.md)。  
  
 如果引數為 Null，則 UPPER 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會將字串常值轉換成大寫字元。 傳回結果為「HELLO」。  
  
```  
UPPER("hello")  
```  
  
 此範例會將 **FirstName** 資料行中的第一個字元轉換成大寫字元。 如果 **FirstName** 為 anna，則傳回結果為「A」。 如需詳細資訊，請參閱 [SUBSTRING &#40;SSIS 運算式&#41;](../../integration-services/expressions/substring-ssis-expression.md)。  
  
```  
UPPER(SUBSTRING(FirstName, 1, 1))  
```  
  
 此範例會將 **PostalCode** 變數中的值轉換成大寫字元。 如果 **PostalCode** 為 k4b1s2，則傳回結果為「K4B1S2」。  
  
```  
UPPER(@PostalCode)  
```  
  
## <a name="see-also"></a>另請參閱  
 [LOWER &#40;SSIS 運算式&#41;](../../integration-services/expressions/lower-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
