---
title: "EXP (SSIS 運算式) | Microsoft Docs"
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
- exponential functions
- EXP function
ms.assetid: 4cd96d3c-58c9-4a67-a6f6-b72758232912
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7c45673700f84d108b3ed9a6f64f780e007c00d7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="exp-ssis-expression"></a>EXP (SSIS 運算式)
  傳回做為數值運算式中 e 之基底的指數。 EXP 函數會補充 LN 函數的動作，有時亦稱為反對數 (Antilogarithm)。  
  
## <a name="syntax"></a>語法  
  
```  
  
EXP(numeric_expression)  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 有效的數值運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 numeric expression 會在計算指數之前轉換成 DT_R8 資料類型。 如需相關資訊，請參閱 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 傳回結果永遠為正數。  
  
## <a name="expression-examples"></a>運算式範例  
 這些範例會將 EXP 函數套用至正值、負值和零值。  
  
```  
EXP(74)  
```  
  
 傳回 1.373382979540176E+32。  
  
```  
EXP(-27)  
```  
  
 傳回 1.879528816539083E-12。  
  
```  
EXP(0)  
```  
  
 傳回 1。  
  
## <a name="see-also"></a>另請參閱  
 [LOG &#40;SSIS 運算式&#41;](../../integration-services/expressions/log-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
