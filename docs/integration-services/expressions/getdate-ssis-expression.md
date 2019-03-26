---
title: GETDATE (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- current date
- GETDATE function
- dates [Integration Services], GETDATE
ms.assetid: 6d20ec93-3244-4d63-baf6-70eff7bd598c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 283f668b1c751a1808c8254eaaceb523de757081
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58275254"
---
# <a name="getdate-ssis-expression"></a>GETDATE (SSIS 運算式)
  以 DT_DBTIMESTAMP 格式傳回目前的系統日期。 GETDATE 函數不採用引數。  
  
> [!NOTE]  
>  從 GETDATE 函數傳回結果的長度為 29 個字元。  
  
## <a name="syntax"></a>語法  
  
```  
  
GETDATE()  
```  
  
## <a name="arguments"></a>引數  
 None  
  
## <a name="result-types"></a>結果類型  
 DT_DBTIMESTAMP  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會傳回目前日期的年。  
  
```  
DATEPART("year",GETDATE())  
```  
  
 此範例會傳回 **ModifiedDate** 資料行中日期與目前日期之間的天數。  
  
```  
DATEDIFF("dd",ModifiedDate,GETDATE())  
```  
  
 此範例會對目前日期加上三個月。  
  
```  
DATEADD("Month",3,GETDATE())  
```  
  
## <a name="see-also"></a>另請參閱  
 [GETUTCDATE &#40;SSIS 運算式&#41;](../../integration-services/expressions/getutcdate-ssis-expression.md)   
 [函式 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
