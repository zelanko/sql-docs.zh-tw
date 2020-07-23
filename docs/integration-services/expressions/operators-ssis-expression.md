---
title: 運算子 (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS, operators
- SQL Server Integration Services, operators
- operators [Integration Services]
- expressions [Integration Services], operators
ms.assetid: 33df3a3d-1f5c-429b-a3b9-52b7d8689089
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cce2d53a48a55dad2f8d8120e8a7fd091b062ebe
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921109"
---
# <a name="operators-ssis-expression"></a>運算子 (SSIS 運算式)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  本節描述運算式語言提供的運算子，以及運算式評估工具使用的運算子優先順序和關聯性。  
  
 下表列出本節中運算子的相關主題。  
  
|運算子|描述|  
|--------------|-----------------|  
|[轉換 &#40;SSIS 運算式&#41;](../../integration-services/expressions/cast-ssis-expression.md)|將運算式從一種資料類型轉換成不同資料類型。|  
|[&#40;&#41; &#40;括孤&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/parentheses-ssis-expression.md)|識別運算式的評估順序。|  
|[+ &#40;加&#41; &#40;SSIS&#41;](../../integration-services/expressions/add-ssis.md)|加入兩個數值運算式。|  
|[+ &#40;串連&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/concatenate-ssis-expression.md)|串連兩個運算式。|  
|[- &#40;減&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/subtract-ssis-expression.md)|將第一個數值運算式減第二個數值運算式。|  
|[- &#40;負&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/negate-ssis-expression.md)|執行數值運算式的否定運算。|  
|[&#42; &#40;乘&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/multiply-ssis-expression.md)|將兩個數值運算式相乘。|  
|[/ (除法) &#40;SSIS 運算式&#41;](../../integration-services/expressions/divide-ssis-expression.md)|將第一個數值運算式除以第二個數值運算式。|  
|[% &#40;模數&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/modulo-ssis-expression.md)|提供第一個數值運算式除以第二個數值運算式之後的整數餘數。|  
|[&#124;&#124; &#40;邏輯 OR&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/logical-or-ssis-expression.md)|執行邏輯 OR 運算。|  
|[&& &#40;邏輯 AND&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/logical-and-ssis-expression.md)|執行邏輯 AND 運算。|  
|[\! &#40;邏輯 NOT&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/logical-not-ssis-expression.md)|執行布林運算元的否定運算。|  
|[&#124; &#40;位元包含 OR&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)|執行兩個整數值的位元 OR 運算。|  
|[^ &#40;位元排除 OR&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)|執行兩個整數值的位元排除 OR 運算。|  
|[& &#40;位元 AND&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/bitwise-and-ssis-expression.md)|執行兩個整數值的位元 AND 運算。|  
|[~ &#40;位元 NOT&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/bitwise-not-ssis-expression.md)|執行整數的位元否定運算。|  
|[== &#40;等於&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/equal-ssis-expression.md)|執行比較來決定兩個運算式是否相等。|  
|[\!= &#40;不等於&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/unequal-ssis-expression.md)|執行比較來決定兩個運算式是否不相等。|  
|[&#62; &#40;大於&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/greater-than-ssis-expression.md)|執行比較來決定第一個運算式是否大於第二個運算式。|  
|[&#60; &#40;小於&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/less-than-ssis-expression.md)|執行比較來決定第一個運算式是否小於第二個運算式。|  
|[&#62;= &#40;大於或等於&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/greater-than-or-equal-to-ssis-expression.md)|執行比較來決定第一個運算式是否大於或等於第二個運算式。|  
|[&#60;= &#40;小於或等於&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/less-than-or-equal-to-ssis-expression.md)|執行比較來決定第一個運算式是否小於或等於第二個運算式。|  
|[? : &#40;條件式&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/conditional-ssis-expression.md)|依據布林運算式的評估傳回兩個運算式的其中一個。|  
  
 如需每個運算子在優先順序階層中的位置之詳細資訊，請參閱＜ [Operator Precedence and Associativity](../../integration-services/expressions/operator-precedence-and-associativity.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)   
 [進階 Integration Services 運算式範例](../../integration-services/expressions/examples-of-advanced-integration-services-expressions.md)   
 [Integration Services &#40;SSIS&#41; 運算式](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
