---
title: YEAR (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], YEAR
- YEAR function
ms.assetid: 9d88dead-ace8-44b9-b8e2-916c1842e155
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0781278539a1c01be5aec69dd86e4d0f93e65dde
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58271824"
---
# <a name="year-ssis-expression"></a>YEAR (SSIS 運算式)
  傳回代表日期之年份部分的整數。  
  
## <a name="syntax"></a>語法  
  
```  
  
YEAR(date)  
```  
  
## <a name="arguments"></a>引數  
 *date*  
 使用任何日期格式的日期。  
  
## <a name="result-types"></a>結果類型  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 如果引數為 Null，則 YEAR 會傳回 Null 結果。  
  
 日期常值必須明確轉換為日期資料類型之一。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
> [!NOTE]  
>  當日期常值明確轉換成以下其中一個日期資料類型時，此運算式將會驗證失敗：DT_DBTIMESTAMPOFFSET 和 DT_DBTIMESTAMP2。  
  
 使用 YEAR 函數較為簡潔，但相當於使用 DATEPART("Year", date) 函數。  
  
## <a name="expression-examples"></a>運算式範例  
 這個範例會傳回日期常值的年數。 如果日期格式為 mm/dd/yyyy，則這個範例會傳回「2002」。  
  
```  
YEAR((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 這個範例會傳回代表 **ModifiedDate** 資料行中年份的整數。  
  
```  
YEAR(ModifiedDate)  
```  
  
 這個範例會傳回代表目前日期之年份的整數。  
  
```  
YEAR(GETDATE())  
```  
  
## <a name="see-also"></a>另請參閱  
 [DATEADD &#40;SSIS 運算式&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;SSIS 運算式&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40;SSIS 運算式&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY &#40;SSIS 運算式&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH &#40;SSIS 運算式&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
