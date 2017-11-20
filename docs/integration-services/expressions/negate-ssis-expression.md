---
title: "- （負）（SSIS 運算式） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- '- (negative)'
- negative operator (-)
ms.assetid: f0118dfc-aced-4de2-953e-5ebf9c962b8d
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bf561a2e4533f47e7bf6219e141c995ad4c2e60e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="--negate-ssis-expression"></a>- (負) (SSIS 運算式)
  執行數值運算式的否定運算。  
  
## <a name="syntax"></a>語法  
  
```  
  
-numeric_expression  
  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 是任何數值資料類型的任何有效運算式。 只支援帶正負號的數值資料類型。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
## <a name="result-types"></a>結果類型  
 傳回 *numeric_expression*的資料類型。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會執行 **Counter** 變數值的否定運算並與數值常值 50 相加。  
  
```  
-@Counter + 50  
```  
  
## <a name="see-also"></a>請參閱＜  
 [運算子優先順序和關聯性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式 &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  

