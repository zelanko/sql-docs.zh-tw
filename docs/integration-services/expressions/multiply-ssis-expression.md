---
title: '* (乘) (SSIS 運算式) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- '* (multiply operator)'
- multiply operator (*)
ms.assetid: d457f052-ffbb-4485-833f-f4bed4349b69
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c5d887698263638a96d664edc549545f21a1a7c6
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58279242"
---
# <a name="-multiply-ssis-expression"></a>* (乘) (SSIS 運算式)
  將兩個數值運算式相乘。  
  
## <a name="syntax"></a>語法  
  
```  
  
numeric_expression1 * numeric_expression2  
  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression1、numeric_expression2*  
 任何有效的數值資料類型運算式。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>結果類型  
 由兩個引數的資料類型決定。 如需相關資訊，請參閱 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)。  
  
## <a name="remarks"></a>Remarks  
 如果任一個運算元為 Null，則結果為 Null。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會乘以數值常值。  
  
```  
5 * 6.09  
```  
  
 此範例會將 **ListPrice** 資料行中的值乘以 10%。  
  
```  
ListPrice * .10  
```  
  
 此範例會從 **ListPrice** 資料行減去運算式的結果。 變數 **Discount%** 必須以方括號括住，因為名稱包含 % 字元。 如需詳細資訊，請參閱[識別碼 &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md)。  
  
```  
ListPrice - (ListPrice * @[Discount%])  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算子優先順序與關聯性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
