---
title: LN (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- LN function
- natural logarithm of expression [Integration Services]
ms.assetid: 55d7b657-b5fd-4753-9c81-54ed7575e720
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 45d91013c8da7f68c17af5d19e89a6f968cb0dbe
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969278"
---
# <a name="ln-ssis-expression"></a>LN (SSIS 運算式)
  傳回數值運算式的自然對數。  
  
## <a name="syntax"></a>語法  
  
```  
  
LN(numeric_expression)  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 是有效的非零或非負數值運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_R8  
  
## <a name="remarks"></a>備註  
 numeric expression 會在計算對數之前轉換成 DT_R8 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)。  
  
 如果 *numeric_expression* 評估為零或負值，則傳回結果為 Null。  
  
## <a name="expression-examples"></a>運算式範例  
 這個範例使用數值常值。 此函數傳回值 3.737766961828337。  
  
```  
LN(42)  
```  
  
 這個範例使用資料行 **Length**。 如果資料行的值是 53.99，則函數會傳回 3.9887988442302。  
  
```  
LN(Length)   
```  
  
 這個範例使用變數 **Length**。 變數必須為數值資料類型，或運算式必須包含數值資料類型的明確轉換。 如果 **Length** 為 234.567，則函數會傳回 5.45774126708797。  
  
```  
LN(@Length)   
```  
  
## <a name="see-also"></a>另請參閱  
 [LOG &#40;SSIS 運算式&#41;](log-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](functions-ssis-expression.md)  
  
  
