---
title: EXP (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 4cd96d3c-58c9-4a67-a6f6-b72758232912
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6c8327f2f39e5c90d6bbf4d990430ccecfc50273
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077118"
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
  
## <a name="remarks"></a>備註  
 numeric expression 會在計算指數之前轉換成 DT_R8 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)。  
  
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
 [記錄&#40;SSIS 運算式&#41;](log-ssis-expression.md)   
 [函式&#40;SSIS 運算式&#41;](functions-ssis-expression.md)  
  
  
