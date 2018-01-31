---
title: "ROUND (SSIS 運算式) | Microsoft Docs"
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
- rounding expressions
- ROUND function [SSIS]
ms.assetid: 376f1947-4fc5-4611-ad86-823e4db1b468
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bc531db140527e9ec2bfd73adffb2a81f2bcfcf4
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="round-ssis-expression"></a>ROUND (SSIS 運算式)
  傳回已經進位到指定長度或有效位數的數值運算式。 length 參數必須評估為整數。  
  
## <a name="syntax"></a>語法  
  
```  
  
ROUND(numeric_expression,length)  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 是有效數值類型的運算式。 如需相關資訊，請參閱 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
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
  
  
