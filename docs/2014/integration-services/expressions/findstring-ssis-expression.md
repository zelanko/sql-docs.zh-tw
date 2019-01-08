---
title: FINDSTRING (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- FINDSTRING function
ms.assetid: c83cb1b1-3c52-4496-b518-4c9253b9336d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dc77f0d87be4595e672cec61b43d041f0b89a22a
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2018
ms.locfileid: "52782530"
---
# <a name="findstring-ssis-expression"></a>FINDSTRING (SSIS 運算式)
  傳回字元運算式中字串的指定出現位置。 傳回結果是以 1 為主的索引出現位置。 string 參數的評估結果必須為字串運算式，且 occurrence 參數的評估結果必須為整數。 如果找不到字串，傳回值將為 0。 如果字串出現的次數少於 occurrence 引數指定的次數，傳回值也是 0。  
  
## <a name="syntax"></a>語法  
  
```  
  
FINDSTRING(character_expression, searchstring, occurrence)  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 是要在其中搜尋的字元字串。  
  
 *searchstring*  
 是要搜尋的字元字串。  
  
 *occurrence*  
 是帶正負號或不帶正負號的整數，指定要報告的 *searchstring* 出現位置。  
  
## <a name="result-types"></a>結果類型  
 DT_I4  
  
## <a name="remarks"></a>備註  
 FINDSTRING 只適用於 DT_WSTR 資料類型。  為字串常值或具有 DT_STR 資料類型之資料行的*character_expression* 和 *searchstring* 引數，會在 FINDSTRING 執行其作業之前隱含轉換為 DT_WSTR 資料類型。 其他資料類型必須明確地轉換為 DT_WSTR 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)和 [Cast &#40;SSIS 運算式&#41;](cast-ssis-expression.md)。  
  
 如果 *character_expression* 或 *searchstring* 都是 null，FINDSTRING 會傳回 null。  
  
 *occurrence* 引數使用數值 1 會取得第一次出現位置的索引，使用數值 2 則取得第二次出現位置，依此類推。  
  
 *occurrence* 必須為大於 0 值的整數。  
  
## <a name="expression-examples"></a>運算式範例  
 這個範例使用字串常值。 它會傳回數值 11。  
  
```  
FINDSTRING("New York, NY, NY", "NY", 1)   
```  
  
 這個範例使用字串常值。 由於字串 "NY" 只出現兩次，因此傳回結果為 0。  
  
```  
FINDSTRING("New York, NY, NY", "NY", 3)   
```  
  
 此範例使用 **Name** 資料行。 它會傳回數值 n 在 **Name** 資料行中的位置。 傳回結果視 **Name**中的值而有所不同。 如果 **Name** 包含 Anderson，則函數會傳回 8。  
  
```  
FINDSTRING(Name,"n", 2)   
```  
  
 此範例使用 **Name** 和 **Size** 資料行。 它會傳回 **Name** 資料行中， **Size** 值最左邊字元的位置。 傳回的結果視資料行的值而有所不同。 如果 **Name** 包含 Mountain,500Red,42，而 **Size** 包含 42，則傳回結果為 17。  
  
```  
FINDSTRING(Name,Size,1)   
```  
  
## <a name="see-also"></a>另請參閱  
 [REPLACE &#40;SSIS 運算式&#41;](replace-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](functions-ssis-expression.md)  
  
  
