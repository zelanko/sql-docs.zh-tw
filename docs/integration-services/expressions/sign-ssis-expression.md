---
title: "SIGN (SSIS 運算式) | Microsoft Docs"
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
- positive values [Integration Services]
- SIGN function
- negative values
ms.assetid: 1547db08-4329-4781-91c2-36898ed71b15
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea4e7e994644975e36d42eb4720184a39e9d44e7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="sign-ssis-expression"></a>SIGN (SSIS 運算式)
  傳回數值運算式的正 (+1)、負 (-1) 或零 (0) 符號。  
  
## <a name="syntax"></a>語法  
  
```  
  
SIGN(numeric_expression)  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 是帶正負號的有效數值運算式。 如需相關資訊，請參閱 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>結果類型  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
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
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
