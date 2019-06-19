---
title: '|| (邏輯 OR) (SSIS 運算式) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- OR operator
- logical OR (||)
- '|| (logical OR)'
ms.assetid: a3c07c09-f121-4187-9617-b01adcf843c4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4ea60751df8c27ba61c190a3f48d25e4dfce8cb1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725216"
---
# <a name="-logical-or-ssis-expression"></a>|| (邏輯 OR) (SSIS 運算式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  執行邏輯 OR 運算。 如果其中一項或兩項條件均為 TRUE，則運算式的評估結果為 TRUE。  
  
## <a name="syntax"></a>語法  
  
```  
  
boolean_expression1 || boolean_expression2  
```  
  
## <a name="arguments"></a>引數  
 *boolean_expression1、boolean_expression2*  
 評估為 TRUE、FALSE 或 NULL 的任何有效運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_BOOL  
  
## <a name="remarks"></a>Remarks  
 下表顯示 || 運算子的結果。  
  
|結果|運算式|運算式|  
|------------|----------------|----------------|  
|TRUE|TRUE|TRUE|  
|TRUE|TRUE|FALSE|  
|FALSE|FALSE|FALSE|  
|NULL|NULL|NULL|  
|TRUE|NULL|TRUE|  
|NULL|NULL|FALSE|  
  
## <a name="ssis-expression-examples"></a>SSIS 運算式範例  
 此範例使用 **StandardCost** 和 **ListPrice** 資料行。 如果 **StandardCost** 資料行的值小於 300，或 **ListPrice** 資料行的值大於 500，則範例的評估結果為 TRUE。  
  
```  
StandardCost < 300 || ListPrice > 500  
```  
  
 此範例使用 **SPrice** 和 **LPrice** 變數，而非數值常值。  
  
```  
StandardCost < @SPrice || ListPrice > @LPrice  
```  
  
## <a name="see-also"></a>另請參閱  
 [&#124; &#40;位元包含 OR&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/bitwise-inclusive-or-ssis-expression.md)   
 [^ &#40;位元排除 OR&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)   
 [運算子優先順序與關聯性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
