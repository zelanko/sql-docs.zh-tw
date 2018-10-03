---
title: LEFT (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 5634dbfb-740d-4c93-8fd5-2854cc741327
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 41aef87375e50d40ccdec3b6d80782ab028bbf1f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103678"
---
# <a name="left-ssis-expression"></a>LEFT (SSIS 運算式)
  傳回來自給定字元運算式最左邊部分的指定字元數。  
  
## <a name="syntax"></a>語法  
  
```  
  
LEFT(character_expression,number)  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 要擷取字元的字元運算式。  
  
 *number*  
 為表示要傳回字元數的整數運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_WSTR  
  
## <a name="remarks"></a>備註  
 如果 *number* 大於 *character_expression*的長度，函數會傳回 *character_expression*。  
  
 如果 *number* 為零，則函數會傳回長度為 0 的字串。  
  
 如果 *number* 為負數，則函數會傳回錯誤。  
  
 *number* 引數可採用變數和資料行。  
  
 LEFT 只適用於 DT_WSTR 資料類型。 如果 *character_expression* 引數是字串常值或具有 DT_STR 資料類型的資料行，則該引數會在 LEFT 執行其作業前隱含轉換成 DT_WSTR 資料類型。 其他資料類型必須明確地轉換為 DT_WSTR 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)和[轉換 &#40;SSIS 運算式&#41;](cast-ssis-expression.md)。  
  
 如果其中一個引數為 Null，則 LEFT 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 下列範例會使用字串常值。 傳回結果為 `"Mountain"`。  
  
```  
LEFT("Mountain Bike", 8)  
```  
  
## <a name="see-also"></a>另請參閱  
 [權限&#40;SSIS 運算式&#41;](right-ssis-expression.md)   
 [函式&#40;SSIS 運算式&#41;](functions-ssis-expression.md)  
  
  
