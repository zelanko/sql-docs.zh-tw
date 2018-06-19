---
title: CEILING (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- smallest integer great than or equal to expression
- CEILING function [SSIS]
ms.assetid: c35bd4ee-1ab6-46ab-89a7-cf771527faa2
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7317a71579712aa51ef1539a0c671e2a71201c14
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/12/2018
ms.locfileid: "35328552"
---
# <a name="ceiling-ssis-expression"></a>CEILING (SSIS 運算式)
  傳回大於或等於數值運算式的最小整數。  
  
## <a name="syntax"></a>語法  
  
```  
  
CEILING(numeric_expression)  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 有效的數值運算式。  
  
## <a name="result-types"></a>結果類型  
 提交至函數之數值運算式的資料類型。  
  
## <a name="remarks"></a>Remarks  
 如果引數為 Null，則 CEILING 會傳回 Null 結果。  
  
## <a name="expression-examples"></a>運算式範例  
 這些範例會將 CEILING 函數套用至正值、負值和零值。  
  
```  
CEILING(123.74)  
```  
  
 傳回 124.00  
  
```  
CEILING(-124.27)  
```  
  
 傳回 -124.00  
  
```  
CEILING(0.00)  
```  
  
 傳回 0.00  
  
## <a name="see-also"></a>另請參閱  
 [FLOOR &#40;SSIS 運算式&#41;](../../integration-services/expressions/floor-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
