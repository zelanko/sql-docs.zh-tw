---
description: LOG (SSIS 運算式)
title: LOG (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- base-10 logarithms
- LOG function
ms.assetid: f7fccace-c178-4e13-bde9-7dc4ef1d98fa
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 211797a6291145b7f1499f23c03f255f504eaf9b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425450"
---
# <a name="log-ssis-expression"></a>LOG (SSIS 運算式)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  傳回數值運算式以 10 為底的對數。  
  
## <a name="syntax"></a>語法  
  
```  
  
LOG(numeric_expression)  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 是有效的非零或非負數值運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_R8  
  
## <a name="remarks"></a>備註  
 *numeric expression* 會在計算對數之前轉換成 DT_R8 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 如果 *numeric_expression* 評估為零或負值，則傳回結果為 Null。  
  
## <a name="expression-examples"></a>運算式範例  
 這個範例使用數值常值。 函數傳回值 1.988291341907488。  
  
```  
LOG(97.34)  
```  
  
 這個範例使用資料行 **Length**。 如果資料行是 101.24，則函數會傳回 2.005352136486217。  
  
```  
LOG(Length)   
```  
  
 這個範例使用變數 **Length**。 變數必須為數值資料類型，或運算式必須包含數值 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 資料類型的明確轉換。 如果 **Length** 為 234.567，則函數會傳回 2.370266913465859。  
  
```  
LOG(@Length)   
```  
  
## <a name="see-also"></a>另請參閱  
 [EXP &#40;SSIS 運算式&#41;](../../integration-services/expressions/exp-ssis-expression.md)   
 [LN &#40;SSIS 運算式&#41;](../../integration-services/expressions/ln-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
