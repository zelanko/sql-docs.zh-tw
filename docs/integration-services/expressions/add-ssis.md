---
title: + (加法) (SSIS) | Microsoft Docs
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
- + (add)
- add operator (+)
- adding expressions
ms.assetid: 44df4154-fed5-4e7f-9995-e703a0164f6a
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 127f311e284cec40bf1fda3e38398a1959e0226b
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35411770"
---
# <a name="-add-ssis"></a>+ (加) (SSIS)
  加入兩個數值運算式。  
  
## <a name="syntax"></a>語法  
  
```  
  
numeric_expression1 + numeric_expression2  
  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression1、numeric_ expression2*  
 任何有效的數值資料類型運算式。  
  
## <a name="result-types"></a>結果類型  
 由兩個引數的資料類型決定。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="remarks"></a>Remarks  
 如果任一個運算元為 Null，則結果為 Null。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會加上數值常值。  
  
```  
5 + 6.09 + 7.0  
```  
  
 此範例會將 **VacationHours** 和 **SickLeaveHours** 資料行中的值相加。  
  
```  
VacationHours + SickLeaveHours  
```  
  
 此範例會將計算出的值加入至 **StandardCost** 資料行。 **Profit%** 變數必須加上方括號，因為名稱包含 % 字元。 如需詳細資訊，請參閱[識別碼 &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md)。  
  
```  
StandardCost + (StandardCost * @[Profit%])  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算子優先順序與關聯性](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
