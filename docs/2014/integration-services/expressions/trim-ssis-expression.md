---
title: TRIM (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- leading blanks
- TRIM function
- trailing blanks
ms.assetid: 7dd9081d-a3d4-483a-bf7e-bf2bd7692d39
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 59d7eb92d79aa77da3faded36036de4b14142c93
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62896513"
---
# <a name="trim-ssis-expression"></a>TRIM (SSIS 運算式)
  傳回移除開頭和尾端空白之後的字元運算式。  
  
> [!NOTE]  
>  TRIM 不會移除空白字元，例如 Tab 鍵或換行字元。 Unicode 會為許多不同類型的空格提供字碼指標，但此功能只會辨識 Unicode 字碼指標 0x0020。 當將雙位元組字集 (DBCS) 字串轉換為 Unicode 時，它們可以包括 0x0020 以外的空格字元，但此功能無法移除這些空格。 若要移除所有種類的空格，您可以在從「指令碼」元件執行的指令碼中使用 Microsoft Visual Basic .NET Trim 方法。  
  
## <a name="syntax"></a>語法  
  
```  
  
TRIM(character_expression)  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 要移除空白的字元運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_WSTR  
  
## <a name="remarks"></a>備註  
 如果引數為 Null，則 TRIM 會傳回 Null 結果。  
  
 TRIM 只適用於 DT_WSTR 資料類型。 如果 *character_expression* 引數是字串常值或具有 DT_STR 資料類型的資料行，則該引數會在 TRIM 執行其作業前隱含轉換成 DT_WSTR 資料類型。 其他資料類型必須明確地轉換為 DT_WSTR 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)和[轉換 &#40;SSIS 運算式&#41;](cast-ssis-expression.md)。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會移除字串常值開頭和尾端的空白。 傳回結果為「New York」。  
  
```  
TRIM("   New York   ")  
```  
  
 此範例會從串連 **FirstName** 和 **LastName** 資料行的結果中移除開頭和尾端的空白。 **FirstName** 和 **LastName** 之間的空白字串則不會移除。  
  
```  
TRIM(FirstName + " "+ LastName)  
```  
  
## <a name="see-also"></a>另請參閱  
 [LTRIM &#40;SSIS 運算式&#41;](trim-ssis-expression.md)   
 [RTRIM &#40;SSIS 運算式&#41;](rtrim-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](functions-ssis-expression.md)  
  
  
