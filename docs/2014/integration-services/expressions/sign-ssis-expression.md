---
title: SIGN (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- positive values [Integration Services]
- SIGN function
- negative values
ms.assetid: 1547db08-4329-4781-91c2-36898ed71b15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1ff2f3cdf2bd44aa617dc378c32ad99cf1aa2042
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48150788"
---
# <a name="sign-ssis-expression"></a>SIGN (SSIS 運算式)
  傳回數值運算式的正 (+1)、負 (-1) 或零 (0) 符號。  
  
## <a name="syntax"></a>語法  
  
```  
  
SIGN(numeric_expression)  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 是帶正負號的有效數值運算式。 如需詳細資訊，請參閱 [Integration Services 資料類型](../data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>結果類型  
 DT_I4  
  
## <a name="remarks"></a>備註  
 如果引數為 Null，則 SIGN 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會傳回數值常值的正負號。 傳回結果為 -1。  
  
```  
SIGN(-123.45)  
```  
  
 此範例會傳回從 **DealerPrice** 資料行減去 **StandardCost** 資料行之結果的正負號。  
  
```  
SIGN(DealerPrice - StandardCost)  
```  
  
## <a name="see-also"></a>另請參閱  
 [函式&#40;SSIS 運算式&#41;](functions-ssis-expression.md)  
  
  
