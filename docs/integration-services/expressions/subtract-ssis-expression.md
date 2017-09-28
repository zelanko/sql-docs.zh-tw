---
title: "- （減）（SSIS 運算式） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- '- (subtract)'
- subtract operator (-)
ms.assetid: b48da086-37dd-460a-8a4b-912f52c9b158
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d185d99f8ebd22d05446eadb556bd7ebcb95cb2f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="--subtract-ssis-expression"></a>- (減) (SSIS 運算式)
  將第一個數值運算式減第二個數值運算式。  
  
## <a name="syntax"></a>語法  
  
```  
  
numeric_expression1 – numeric_expression2  
  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression1、numeric_expression2*  
 任何有效的數值資料類型運算式。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
## <a name="result-types"></a>結果類型  
 由兩個引數的資料類型決定。 如需相關資訊，請參閱 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)。  
  
## <a name="remarks"></a>備註  
 用括號括住一元減號運算式，以確保運算式以正確的順序接受評估。  
  
## <a name="remarks"></a>備註  
 如果任一個運算元為 Null，則結果為 Null。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會減去數值常值。  
  
```  
5 - 6.09  
```  
  
 此範例會將 **ListPrice** 資料行中的值減去 **StandardCost** 資料行中的值。  
  
```  
ListPrice - StandardCost  
```  
  
 此範例會從 **ListPrice** 資料行減去導出值。 變數 **Discount%** 必須以方括號括住，因為名稱包含 % 字元。 如需詳細資訊，請參閱[識別碼 &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md)。  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算子優先順序與關聯性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
