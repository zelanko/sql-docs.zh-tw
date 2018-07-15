---
title: + (加法) (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
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
ms.openlocfilehash: 2b7b971521991be68d69efd2519b423958ef4fbf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37248858"
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
 由兩個引數的資料類型決定。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)。  
  
## <a name="remarks"></a>備註  
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
  
 此範例會將計算出的值加入至 **StandardCost** 資料行。 **Profit%** 變數必須加上方括號，因為名稱包含 % 字元。 如需詳細資訊，請參閱[識別碼 &#40;SSIS&#41;](identifiers-ssis.md)。  
  
```  
StandardCost + (StandardCost * @[Profit%])  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算子優先順序和關聯性](operator-precedence-and-associativity.md)   
 [運算子&#40;SSIS 運算式&#41;](operators-ssis-expression.md)  
  
  
