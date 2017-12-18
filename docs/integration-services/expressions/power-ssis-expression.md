---
title: "POWER (SSIS 運算式) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: POWER function
ms.assetid: db48ae65-bfa6-4db1-8d3c-d0d4f8a399bc
caps.latest.revision: "30"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f505360aa71886a98f0a56f8402507ecef8f4903
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="power-ssis-expression"></a>POWER (SSIS 運算式)
  傳回數值運算式的乘冪結果。 power 參數必須評估為整數。  
  
## <a name="syntax"></a>語法  
  
```  
  
POWER(numeric_expression,power)  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 有效的數值運算式。  
  
 *power*  
 有效的數值運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_R8  
  
## <a name="remarks"></a>備註  
 *numeric_expression* 和 *power* 引數會在計算 power 之前，轉換成 DT_R8 資料類型。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
 如果 *numeric_expression* 評估為零，且 *power* 為負數，則運算式評估工具會傳回錯誤並將傳回結果設為 Null。  
  
 如果 *numeric_expression* 或 *power* 評估為未定的結果，則傳回結果為 Null。  
  
 *power* 引數可以是分數。 例如，您可以使用數值 0.5 做為 power。  
  
## <a name="expression-examples"></a>運算式範例  
 這個範例使用數值常值。 函數會將 4 自乘至 3 的乘冪，並傳回 64。  
  
```  
POWER(4,3)  
```  
  
 此範例使用 **Length** 資料行和 **DimensionCount** 變數。 如果 **Length** 是 8 且 **DimensionCount** 是 2，則傳回結果為 64。  
  
```  
POWER(Length, @DimensionCount)   
```  
  
## <a name="see-also"></a>另請參閱  
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
