---
title: LEN (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- LEN function
- number of characters
ms.assetid: d961398b-e4d0-4936-be17-8f4c5882a640
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4f84bb32435afe7cbe52cea6ed25f59940dbd42c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297531"
---
# <a name="len-ssis-expression"></a>LEN (SSIS 運算式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  傳回字元運算式中的字元數。 如果字串包含開頭和尾端空白，則函數會將它們加入計數中。 LEN 會針對單位元組和雙位元組字元的相同字串傳回完全相同的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
LEN(character_expression)  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 是要評估的運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_I4  
  
## <a name="remarks"></a>備註  
 *character_expression* 引數可以是 DT_WSTR、DT_TEXT、DT_NTEXT 或 DT_IMAGE 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 如果 *character_expression* 是字串常值或具有 DT_STR 資料類型的資料行，則它會在 LEN 執行其作業前隱含轉換成 DT_WSTR 資料類型。 其他資料類型必須明確地轉換為 DT_WSTR 資料類型。 如需詳細資訊，請參閱 [Cast &#40;SSIS 運算式&#41;](../../integration-services/expressions/cast-ssis-expression.md)。  
  
 如果傳遞至 LEN 函數的引數資料類型為「二進位大型物件區塊」(Binary Large Object Block，BLOB)，例如 DT_TEXT、DT_NTEXT 或 DT_IMAGE，則函數會傳回位元組計數。  
  
 如果引數為 Null，則 LEN 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會傳回字串常值的長度。 傳回結果為 12。  
  
```  
LEN("Ball Bearing")  
```  
  
 此範例會傳回 **FirstName** 和 **LastName** 資料行中各值長度之間的差異。  
  
```  
LEN(FirstName) - LEN(LastName)  
```  
  
 使用「系統」變數 **MachineName**傳回電腦名稱的長度。  
  
```  
LEN(@MachineName)  
```  
  
## <a name="see-also"></a>另請參閱  
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
