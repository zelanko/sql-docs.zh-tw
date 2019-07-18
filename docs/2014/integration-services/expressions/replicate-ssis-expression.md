---
title: REPLICATE (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- REPLICATE function
ms.assetid: e7a37b93-6d1d-42d5-9a65-de1790abf6a5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 349a100a295ef00b19b2de69214fdd7af8bd2d32
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62897347"
---
# <a name="replicate-ssis-expression"></a>REPLICATE (SSIS 運算式)
  傳回複寫許多次的字元運算式。 *times* 引數必須評估為整數。  
  
> [!NOTE]  
>  REPLICATE 函數經常使用長字串，因此很可能產生運算式長度為 4000 個字元的限制。 如果運算式的評估結果具有 Integration Services 資料類型 DT_WSTR 或 DT_STR，則會將運算式在 4000 個字元處截斷。 如果子運算式的結果類型為 DT_STR 或 DT_WSTR，則同樣會將子運算式截斷到 4000 個字元，不論整體運算式的結果類型為何。 截斷的結果可正常地處理，或造成警告或錯誤。 如需詳細資訊，請參閱[語法 &#40;SSIS&#41;](syntax-ssis.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
REPLICATE(character_expression,times)  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 是要複寫的字元運算式。  
  
 *times*  
 是整數運算式，指定複寫 *character_expression* 的次數。  
  
## <a name="result-types"></a>結果類型  
 DT_WSTR  
  
## <a name="remarks"></a>備註  
 如果 *times* 為零，則函數會傳回長度為 0 的字串。  
  
 如果 *times* 為負數，則函數會傳回錯誤。  
  
 *times* 引數亦使用變數和資料行。  
  
 REPLICATE 只適用於 DT_WSTR 資料類型。 如果 *character_expression* 引數是字串常值或具有 DT_STR 資料類型的資料行，則該引數會在 REPLICATE 執行其作業前隱含轉換成 DT_WSTR 資料類型。 其他資料類型必須明確地轉換為 DT_WSTR 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)和[轉換 &#40;SSIS 運算式&#41;](cast-ssis-expression.md)。  
  
 如果其中一個引數為 Null，則 REPLICATE 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會複寫字串常值三次。 傳回結果為「Mountain BikeMountain BikeMountain Bike」。  
  
```  
REPLICATE("Mountain Bike", 3)  
```  
  
 此範例會以 **Times** 變數中的值複寫 **Name** 資料行中的值。 如果 **Times** 是 3，且 **Name** 是 Touring Front Wheel，則傳回結果為 Touring Front WheelTouring Front WheelTouring Front Wheel。  
  
```  
REPLICATE(Name, @Times)  
```  
  
 此範例會以 **Times** 資料行中的值複寫 **Name** 變數中的值。 **Times** 的資料類型為非整數，且運算式包括明確轉換成整數的資料類型。 如果 **Name** 包含 Helmet，且 **Times** 為 2，則傳回結果為 "HelmetHelmet"。  
  
```  
REPLICATE(@Name, (DT_I4(Times))  
```  
  
## <a name="see-also"></a>另請參閱  
 [函數 &#40;SSIS 運算式&#41;](functions-ssis-expression.md)  
  
  
