---
title: EXP (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- exponential functions
- EXP function
ms.assetid: 4cd96d3c-58c9-4a67-a6f6-b72758232912
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8ffe52a392dfec79afa301df7650cf73f2ad35ac
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65725444"
---
# <a name="exp-ssis-expression"></a>EXP (SSIS 運算式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
 numeric expression 會在計算指數之前轉換成 DT_R8 資料類型。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
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
  
  
