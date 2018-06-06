---
title: '- (負) (SSIS 運算式) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
ms.assetid: f0118dfc-aced-4de2-953e-5ebf9c962b8d
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 579b2c8471b02db4786c540b978f8a23c71527a0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="--negate-ssis-expression"></a>- (負) (SSIS 運算式)
  執行數值運算式的否定運算。  
  
## <a name="syntax"></a>語法  
  
```  
  
-numeric_expression  
  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 是任何數值資料類型的任何有效運算式。 只支援帶正負號的數值資料類型。 如需相關資訊，請參閱 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>結果類型  
 傳回 *numeric_expression*的資料類型。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會執行 **Counter** 變數值的否定運算並與數值常值 50 相加。  
  
```  
-@Counter + 50  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算子優先順序與關聯性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
