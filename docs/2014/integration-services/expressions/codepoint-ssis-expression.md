---
title: CODEPOINT (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- CODEPOINT function
- leftmost character of expression
ms.assetid: 0783d05e-7f35-42fb-a2c4-9621c46effd6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 10d2eeb6991c0c75e8dbe8102f94148f60f0a361
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62769372"
---
# <a name="codepoint-ssis-expression"></a>CODEPOINT (SSIS 運算式)
  傳回字元運算式最左邊字元的 Unicode 字碼指標。  
  
## <a name="syntax"></a>語法  
  
```  
  
CODEPOINT(character_expression)  
```  
  
## <a name="arguments"></a>引數  
 *character_expression*  
 是將要評估最左邊字元的字元運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_UI2  
  
## <a name="remarks"></a>備註  
 *character_expression* 引數必須是 DT_WSTR 資料類型。  
  
 如果 *character_expression* 為 Null 或空字串，則 CODEPOINT 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 這個範例使用字串常值。 傳回結果為 77，即 M 的 Unicode 字碼指標。  
  
```  
CODEPOINT("Mountain Bike")  
```  
  
 這個範例使用變數。 如果 **Name** 是 Touring Front Wheel，則傳回結果為 84，即 T 的 Unicode 字碼指標。  
  
```  
CODEPOINT(@Name)  
```  
  
## <a name="see-also"></a>另請參閱  
 [函數 &#40;SSIS 運算式&#41;](functions-ssis-expression.md)  
  
  
