---
title: LOWER (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- converting uppercase to lowercase
- LOWER function
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: 109328e1-5604-40ff-895e-f2e7c13fff41
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ed93892fc9157e51453db9fe2cac4d541444db77
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37277014"
---
# <a name="lower-ssis-expression"></a>LOWER (SSIS 運算式)
  傳回將大寫字元轉換為小寫字元之後的字元運算式。  
  
## <a name="syntax"></a>語法  
  
```  
  
LOWER(character_expression)  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 是轉換成小寫字元的字元運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_WSTR  
  
## <a name="remarks"></a>備註  
 LOWER 只適用於 DT_WSTR 資料類型。 如果 *character_expression* 引數是字串常值或具有 DT_STR 資料類型的資料行，則該引數會在 LOWER 執行其作業前隱含轉換成 DT_WSTR 資料類型。 其他資料類型必須明確地轉換為 DT_WSTR 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)和[轉換 &#40;SSIS 運算式&#41;](cast-ssis-expression.md)。  
  
 如果引數為 Null，則 LOWER 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會將字串常值轉換成小寫字元。 傳回結果為 "new york"。  
  
```  
LOWER("New York")  
```  
  
 此範例會將 **Color** 輸入資料行中的所有字元轉換成小寫字元，除了第一個字元以外。 如果 Color 是 YELLOW，則傳回結果為 "Yellow"。 如需詳細資訊，請參閱 [SUBSTRING &#40;SSIS Expression&#41;](substring-ssis-expression.md) (SUBSTRING (SSIS 運算式))。  
  
```  
LOWER(SUBSTRING(Color, 2, 15))  
```  
  
 此範例會將 **CityName** 變數中的值轉換成小寫字元。  
  
```  
LOWER(@CityName)  
```  
  
## <a name="see-also"></a>另請參閱  
 [上方&#40;SSIS 運算式&#41;](upper-ssis-expression.md)   
 [函式&#40;SSIS 運算式&#41;](functions-ssis-expression.md)  
  
  
