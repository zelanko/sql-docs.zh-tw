---
title: '| (位元包含 OR) (SSIS 運算式) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- '| (bitwise inclusive OR)'
- bitwise inclusive OR (|)
ms.assetid: 4dce9eb2-3680-4adc-81a3-816ea52cef49
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a8ec37dfaf84ed50c0318060f9822086e301ef70
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35406610"
---
# <a name="-bitwise-inclusive-or-ssis-expression"></a>| (位元包含 OR) (SSIS 運算式)
  執行兩個整數值的位元 OR 運算。 它會比較其第一個運算元的每個位元和其第二個運算元的對應位元。 如果其中一個位元是 1，則對應的結果位元會設為 1。 否則，對應的結果位元會設為零 (0)。  
  
 兩個條件都必須是簽署的整數資料類型，或者都必須是未簽署的整數資料類型。  
  
## <a name="syntax"></a>語法  
  
```  
  
integer_expression1 | integer_expression2  
  
```  
  
## <a name="arguments"></a>引數  
 *integer_expression1、integer_expression2*  
 已簽署或未簽署整數資料類型的任何有效運算式。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>結果類型  
 由兩個引數的資料類型決定。 如需相關資訊，請參閱 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)。  
  
## <a name="remarks"></a>Remarks  
 如果任一個條件為 Null，則運算式結果為 Null。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會在 **NumberA** 和 **NumberB**變數之間執行位元包含 OR 運算。 **NumberA** 包含 3 (00000011) 且 **NumberB** 包含 9 (00001001)。  
  
```  
@NumberA | @NumberB  
```  
  
 運算式評估為 11 (00001011)。  
  
 00000011  
  
 00001001  
  
 ----------\-  
  
 00001011  
  
 此範例會在 **ReorderPoint** 和 **SafetyStockLevel** 資料行之間執行位元包含 OR 運算。  
  
```  
ReorderPoint | SafetyStockLevel  
```  
  
 如果 **ReorderPoint** 為 10，且 **SafetyStockLevel** 為 8，則運算式評估結果為 10 (00001010)。  
  
 00001010  
  
 00001000  
  
 ----------\-  
  
 00001010  
  
 此範例會在兩個整數之間執行位元包含 OR 運算。  
  
```  
3 | 5   
```  
  
 運算式評估為 7 (00000111)。  
  
 00000011  
  
 00000101  
  
 ----------\-  
  
 00000111  
  
## <a name="see-also"></a>另請參閱  
 [&#124;&#124; &#40;邏輯 OR&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/logical-or-ssis-expression.md)   
 [^ &#40;位元排除 OR&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/bitwise-exclusive-or-ssis-expression.md)   
 [運算子優先順序與關聯性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
