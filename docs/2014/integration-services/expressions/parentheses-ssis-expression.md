---
title: () (括號) (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- () (parentheses operator)
- evaluation order [Integration Services]
- parentheses operator ()
ms.assetid: 931e10eb-1707-4121-b2f1-43565561119f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 50d18745a064ed8d9550017ce1fcfef8c2c0805d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969138"
---
# <a name="-parentheses-ssis-expression"></a>() (括號) (SSIS 運算式)
  識別運算式的評估順序。 加上括號的運算式擁有最高的評估優先順序。 加上括號的巢狀運算式會以由內向外的順序評估。  
  
 括號還可用來讓複雜的運算式更易於了解。  
  
## <a name="syntax"></a>語法  
  
```  
  
(expression)  
  
```  
  
## <a name="arguments"></a>引數  
 *expression*  
 為任何有效運算式。  
  
## <a name="result-types"></a>結果類型  
 *expression*的資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例示範使用括號修改運算子之優先順序的方式。 第一個運算式評估為 100，而第二個運算式則評估為 31。  
  
```  
(5 + 5) * (4 + 6)  
5 + 5 * 4 + 6  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算子優先順序與關聯性](operator-precedence-and-associativity.md)   
 [運算子 &#40;SSIS 運算式&#41;](operators-ssis-expression.md)  
  
  
