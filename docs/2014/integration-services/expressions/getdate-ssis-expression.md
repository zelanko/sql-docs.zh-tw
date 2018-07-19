---
title: GETDATE (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- current date
- GETDATE function
- dates [Integration Services], GETDATE
ms.assetid: 6d20ec93-3244-4d63-baf6-70eff7bd598c
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ed8a87ea53054aff7db3ed5461c0074244ee97db
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37166859"
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
 無  
  
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
 [GETUTCDATE &#40;SSIS 運算式&#41;](getutcdate-ssis-expression.md)   
 [函式&#40;SSIS 運算式&#41;](functions-ssis-expression.md)  
  
  
