---
title: (模數) (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '% (modulo operator)'
- remainder of division operation
- modulo operator (%)
ms.assetid: e2920821-2f5b-4c76-8db8-8b9eddf4606f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 163dbfecd4605c6c9624d94c047b1c7e893d8fcd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768874"
---
# <a name="modulo-ssis-expression"></a>(模數) (SSIS 運算式)
  提供第一個數值運算式除以第二個數值運算式之後的整數餘數。  
  
## <a name="syntax"></a>語法  
  
```  
  
dividend % divisor  
  
```  
  
## <a name="arguments"></a>引數  
 *dividend*  
 要執行除法的數值運算式。 *dividend* 可以是任何有效的數值運算式。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)  
  
 *divisor*  
 要除以被除數的數值運算式。 *divisor* 可以是任何有效的數值運算式 (零除外)。  
  
## <a name="result-types"></a>結果類型  
 由兩個引數的資料類型決定。 如需相關資訊，請參閱 [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md)。  
  
## <a name="remarks"></a>備註  
 這兩個運算式都須評估為帶正負號或不帶正負號的整數資料類型。  
  
 如果任一個運算元為 Null，則結果為 Null。  
  
 模數零不合法。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會計算來自兩個數值常值的模數。 結果為 3。  
  
```  
42 % 13  
```  
  
 此範例會計算來自 **SalesQuota** 資料行和數值常數的模數。  
  
```  
SalesQuota % 12  
```  
  
 此範例會計算來自 **Sales$** 和 **Month**這兩個數值變數的模數。 **Sales$** 變數必須加上方括號，因為名稱包含 $ 字元。 如需詳細資訊，請參閱[識別碼 &#40;SSIS&#41;](identifiers-ssis.md)。  
  
```  
@[Sales$] % @Month  
```  
  
 此範例使用模數運算子判斷 **Value** 變數的值為偶數或奇數，並使用條件運算子傳回描述結果的字串。 如需詳細資訊，請參閱 [? : &#40;條件式&#41; &#40;SSIS 運算式&#41;](conditional-ssis-expression.md)。  
  
```  
@Value % 2 == 0? "even":"odd"  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算子優先順序與關聯性](operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式&#41;](operators-ssis-expression.md)  
  
  
