---
title: "SQUARE (SSIS 運算式) | Microsoft Docs"
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
- SQUARE
- square values
ms.assetid: cecf1bb2-3d55-40a6-9688-ed67bcc150b4
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2b7181bce75dfe667a643b5ef149c7b9d61f16a6
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="square-ssis-expression"></a>SQUARE (SSIS 運算式)
  傳回數值運算式的平方。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQUARE(numeric_expression)  
```  
  
## <a name="arguments"></a>引數  
 *numeric_expression*  
 任何數值資料類型的數值運算式。 如需相關資訊，請參閱 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
## <a name="result-types"></a>結果類型  
 DT_R8  
  
## <a name="remarks"></a>Remarks  
 如果引數為 Null，則 SQUARE 會傳回 Null 結果。  
  
 引數會在進行平方運算之前，轉換成 DT_R8 資料類型。  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會傳回 12 的平方。 傳回結果為 144。  
  
```  
SQUARE(12)  
```  
  
 此範例會傳回在兩個資料行中減去值之結果的平方。 如果 **Value1** 為 12，而 **Value2** 為 4，則 SQUARE 函數會傳回 64。  
  
```  
SQUARE(Value1 - Value2)  
```  
  
 此範例會將 SQUARE 函數套用至兩個變數，然後計算其總和的平方根，藉此傳回直角三角形第三邊的長度。 如果 **Side1** 包含 3，而 **Side2** 包含 4，SQRT 函數就會傳回 5。  
  
```  
SQRT(SQUARE(@Side1) + SQUARE(@Side2))  
```  
  
> [!NOTE]  
>  在運算式中，變數名稱會固定包含 @ 前置字元。  
  
## <a name="see-also"></a>另請參閱  
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
