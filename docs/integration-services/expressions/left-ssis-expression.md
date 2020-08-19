---
description: LEFT (SSIS 運算式)
title: LEFT (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5634dbfb-740d-4c93-8fd5-2854cc741327
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 619fea9cdf5f9445d9da3146f98453e0d5d60550
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425460"
---
# <a name="left-ssis-expression"></a>LEFT (SSIS 運算式)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


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
  
 LEFT 只適用於 DT_WSTR 資料類型。 如果 *character_expression* 引數是字串常值或具有 DT_STR 資料類型的資料行，則該引數會在 LEFT 執行其作業前隱含轉換成 DT_WSTR 資料類型。 其他資料類型必須明確地轉換為 DT_WSTR 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)和[轉換 &#40;SSIS 運算式&#41;](../../integration-services/expressions/cast-ssis-expression.md)。  
  
 如果其中一個引數為 Null，則 LEFT 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 下列範例會使用字串常值。 傳回結果為 `"Mountain"`。  
  
```  
LEFT("Mountain Bike", 8)  
```  
  
## <a name="see-also"></a>另請參閱  
 [RIGHT &#40;SSIS 運算式&#41;](../../integration-services/expressions/right-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
