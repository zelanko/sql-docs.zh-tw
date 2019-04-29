---
title: 運算子 (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS, operators
- SQL Server Integration Services, operators
- operators [Integration Services]
- expressions [Integration Services], operators
ms.assetid: 33df3a3d-1f5c-429b-a3b9-52b7d8689089
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7689110600b7c4cded50572828ab469dd51c1432
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62897357"
---
# <a name="operators-ssis-expression"></a>運算子 (SSIS 運算式)
  本節描述運算式語言提供的運算子，以及運算式評估工具使用的運算子優先順序和關聯性。  
  
 下表列出本節中運算子的相關主題。  
  
|運算子|描述|  
|--------------|-----------------|  
|[轉換 &#40;SSIS 運算式&#41;](cast-ssis-expression.md)|將運算式從一種資料類型轉換成不同資料類型。|  
|[&#40;&#41; &#40;括孤&#41; &#40;SSIS 運算式&#41;](parentheses-ssis-expression.md)|識別運算式的評估順序。|  
|[+ &#40;加&#41; &#40;SSIS&#41;](add-ssis.md)|加入兩個數值運算式。|  
|[+ &#40;串連&#41; &#40;SSIS 運算式&#41;](concatenate-ssis-expression.md)|串連兩個運算式。|  
|[- &#40;減&#41; &#40;SSIS 運算式&#41;](subtract-ssis-expression.md)|將第一個數值運算式減第二個數值運算式。|  
|[- &#40;負&#41; &#40;SSIS 運算式&#41;](negate-ssis-expression.md)|執行數值運算式的否定運算。|  
|[&#42; &#40;乘&#41; &#40;SSIS 運算式&#41;](multiply-ssis-expression.md)|將兩個數值運算式相乘。|  
|[除 &#40;SSIS 運算式&#41;](divide-ssis-expression.md)|將第一個數值運算式除以第二個數值運算式。|  
|[&#40;模數&#41; &#40;SSIS 運算式&#41;](modulo-ssis-expression.md)|提供第一個數值運算式除以第二個數值運算式之後的整數餘數。|  
|[&#124;&#124;&#40;邏輯 OR&#41; &#40;SSIS 運算式&#41;](logical-or-ssis-expression.md)|執行邏輯 OR 運算。|  
|[&& &#40;邏輯 AND&#41; &#40;SSIS 運算式&#41;](logical-and-ssis-expression.md)|執行邏輯 AND 運算。|  
|[\! &#40;邏輯 NOT&#41; &#40;SSIS 運算式&#41;](logical-not-ssis-expression.md)|執行布林運算元的否定運算。|  
|[&#124; &#40;位元包含 OR&#41; &#40;SSIS 運算式&#41;](bitwise-inclusive-or-ssis-expression.md)|執行兩個整數值的位元 OR 運算。|  
|[^ &#40;位元排除 OR&#41; &#40;SSIS 運算式&#41;](bitwise-exclusive-or-ssis-expression.md)|執行兩個整數值的位元排除 OR 運算。|  
|[& &#40;位元 AND&#41; &#40;SSIS 運算式&#41;](bitwise-and-ssis-expression.md)|執行兩個整數值的位元 AND 運算。|  
|[~ &#40;位元 Not&#41; &#40;SSIS 運算式&#41;](bitwise-not-ssis-expression.md)|執行整數的位元否定運算。|  
|[== &#40;等於&#41; &#40;SSIS 運算式&#41;](equal-ssis-expression.md)|執行比較來決定兩個運算式是否相等。|  
|[\!= &#40;不等於&#41; &#40;SSIS 運算式&#41;](unequal-ssis-expression.md)|執行比較來決定兩個運算式是否不相等。|  
|[&#62; &#40;大於&#41; &#40;SSIS 運算式&#41;](greater-than-ssis-expression.md)|執行比較來決定第一個運算式是否大於第二個運算式。|  
|[&#60; &#40;小於&#41; &#40;SSIS 運算式&#41;](less-than-ssis-expression.md)|執行比較來決定第一個運算式是否小於第二個運算式。|  
|[&#62;= &#40;大於或等於&#41; &#40;SSIS 運算式&#41;](greater-than-or-equal-to-ssis-expression.md)|執行比較來決定第一個運算式是否大於或等於第二個運算式。|  
|[&#60;= &#40;小於或等於&#41; &#40;SSIS 運算式&#41;](less-than-or-equal-to-ssis-expression.md)|執行比較來決定第一個運算式是否小於或等於第二個運算式。|  
|[? : &#40;條件式&#41; &#40;SSIS 運算式&#41;](conditional-ssis-expression.md)|依據布林運算式的評估傳回兩個運算式的其中一個。|  
  
 如需每個運算子在優先順序階層中的位置之詳細資訊，請參閱＜ [Operator Precedence and Associativity](operator-precedence-and-associativity.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [函數 &#40;SSIS 運算式&#41;](functions-ssis-expression.md)   
 [進階 Integration Services 運算式範例](examples-of-advanced-integration-services-expressions.md)   
 [Integration Services &#40;SSIS&#41; 運算式](integration-services-ssis-expressions.md)  
  
  
