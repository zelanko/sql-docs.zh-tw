---
title: LOWER (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- converting uppercase to lowercase
- LOWER function
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: 109328e1-5604-40ff-895e-f2e7c13fff41
author: janinezhang
ms.author: janinez
ms.openlocfilehash: fc0309a47b19cc4df0ece6c0785ba47644082a89
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941267"
---
# <a name="lower-ssis-expression"></a>LOWER (SSIS 運算式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
## <a name="remarks"></a>Remarks  
 LOWER 只適用於 DT_WSTR 資料類型。 如果 *character_expression* 引數是字串常值或具有 DT_STR 資料類型的資料行，則該引數會在 LOWER 執行其作業前隱含轉換成 DT_WSTR 資料類型。 其他資料類型必須明確地轉換為 DT_WSTR 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)和[轉換 &#40;SSIS 運算式&#41;](../../integration-services/expressions/cast-ssis-expression.md)。  
  
 如果引數為 Null，則 LOWER 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會將字串常值轉換成小寫字元。 傳回結果為 "new york"。  
  
```  
LOWER("New York")  
```  
  
 此範例會將 **Color** 輸入資料行中的所有字元轉換成小寫字元，除了第一個字元以外。 如果 Color 是 YELLOW，則傳回結果為 "Yellow"。 如需詳細資訊，請參閱 [SUBSTRING &#40;SSIS Expression&#41;](../../integration-services/expressions/substring-ssis-expression.md) (SUBSTRING (SSIS 運算式))。  
  
```  
LOWER(SUBSTRING(Color, 2, 15))  
```  
  
 此範例會將 **CityName** 變數中的值轉換成小寫字元。  
  
```  
LOWER(@CityName)  
```  
  
## <a name="see-also"></a>另請參閱  
 [UPPER &#40;SSIS 運算式&#41;](../../integration-services/expressions/upper-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
