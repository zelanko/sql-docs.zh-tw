---
title: REPLACE (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- replacing string expression
- REPLACE function
ms.assetid: a6837043-ea70-4c6a-9c7a-6868b02b2adc
caps.latest.revision: 41
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7888b72ed7193a1c2910db06a70496ee30761903
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031467"
---
# <a name="replace-ssis-expression"></a>REPLACE (SSIS 運算式)
  以不同的字元字串或空白字串取代運算式中的字元字串後，傳回字元運算式。  
  
> [!NOTE]  
>  REPLACE 函數經常會使用長的字串。 截斷的結果可正常地處理，或造成警告或錯誤。 如需詳細資訊，請參閱[語法 &#40;SSIS&#41;](syntax-ssis.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
REPLACE(character_expression,searchstring,replacementstring)  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 為函數搜尋的有效字元運算式。  
  
 *searchstring*  
 為函數嘗試尋找的有效字元運算式。  
  
 *replacementstring*  
 為取代運算式的有效字元運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_WSTR  
  
## <a name="remarks"></a>備註  
 *searchstring* 的長度不得為零。  
  
 *replacementstring* 的長度可以為零。  
  
 *searchstring* 和 *replacementstring* 引數可使用變數和資料行。  
  
 REPLACE 只適用於 DT_WSTR 資料類型。 為字串常值或具有 DT_STR 資料類型之資料行的*character_expression1、character_expression2* 和 *character_expression3* 引數，會在 REPLACE 執行其作業之前隱含轉換為 DT_WSTR 資料類型。 其他資料類型必須明確地轉換為 DT_WSTR 資料類型。 如需詳細資訊，請參閱 [Cast &#40;SSIS 運算式&#41;](cast-ssis-expression.md)。  
  
 如果任何引數為 Null，則 REPLACE 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 這個範例使用字串常值。 傳回結果為「All Terrain Bike」。  
  
```  
REPLACE("Mountain Bike", "Mountain","All Terrain")  
```  
  
 此範例會從 **Product** 資料行移除「Bike」字串。  
  
```  
REPLACE(Product, "Bike","")  
```  
  
 此範例會取代 **DaysToManufacture** 資料行中的值。 資料行的資料類型為整數，且運算式包含將 **DaysToManufacture** 轉換為 DT_WSTR 資料類型。  
  
```  
REPLACE((DT_WSTR,8)DaysToManufacture,"6","5")  
```  
  
## <a name="see-also"></a>另請參閱  
 [子字串&#40;SSIS 運算式&#41;](substring-ssis-expression.md)   
 [函式&#40;SSIS 運算式&#41;](functions-ssis-expression.md)  
  
  