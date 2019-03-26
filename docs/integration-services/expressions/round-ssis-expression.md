---
title: ROUND (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- rounding expressions
- ROUND function [SSIS]
ms.assetid: 376f1947-4fc5-4611-ad86-823e4db1b468
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3bb02a98330a7ad93e7784ae9ce6d08284585ff9
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58275945"
---
# <a name="round-ssis-expression"></a>ROUND (SSIS 運算式)
  傳回已經進位到指定長度或有效位數的數值運算式。 length 參數必須評估為整數。  
  
## <a name="syntax"></a>語法  
  
```  
  
ROUND(numeric_expression,length)  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 是有效數值類型的運算式。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 *長度*  
 是整數運算式。 它是 *numeric_expression* 進位到的有效位數。  
  
## <a name="result-types"></a>結果類型  
 與 *numeric*_*expression*相同的類型。  
  
## <a name="remarks"></a>Remarks  
 *length* 引數必須評估為正整數或零。  
  
 如果引數為 Null，則 ROUND 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 這些範例會將數值常值進位到長度 3。 第一個傳回結果為 137.1570，第二個為 137.1580。  
  
```  
ROUND(137.1574,3)  
ROUND(137.1575,3)  
```  
  
## <a name="see-also"></a>另請參閱  
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
