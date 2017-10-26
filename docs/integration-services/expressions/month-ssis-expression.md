---
title: "MONTH （SSIS 運算式） |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dates [Integration Services], MONTH
- MONTH function
ms.assetid: b5a47a11-c2ef-49bd-bd70-235632ff7bf6
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e2e480bc53181fdf01a64716e1fdb94fe4116716
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="month-ssis-expression"></a>MONTH (SSIS 運算式)
  傳回代表日期之月份部分的整數。  
  
## <a name="syntax"></a>語法  
  
```  
  
MONTH(date)  
```  
  
## <a name="arguments"></a>引數  
 *date*  
 使用任何日期格式的日期。  
  
## <a name="result-types"></a>結果類型  
 DT_I4  
  
## <a name="remarks"></a>備註  
 如果引數為 Null，則 MONTH 會傳回 Null 結果。  
  
 日期常值必須明確轉換為日期資料類型之一。 如需詳細資訊，請參閱＜ [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)＞。  
  
> [!NOTE]  
>  當日期常值明確轉換成以下其中一個日期資料類型時，此運算式將會驗證失敗：DT_DBTIMESTAMPOFFSET 和 DT_DBTIMESTAMP2。  
  
 使用 MONTH 函數較為簡潔，但相當於使用 DATEPART("Month", date)。  
  
## <a name="expression-examples"></a>運算式範例  
 這個範例會傳回日期常值的月數。 如果日期格式為「mm/dd/yyyy」，則這個範例會傳回 11。  
  
```  
MONTH((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 這個範例會傳回代表 **ModifiedDate** 資料行中月份的整數。  
  
```  
MONTH(ModifiedDate)  
```  
  
 這個範例會傳回代表目前日期的月份的整數。  
  
```  
MONTH(GETDATE())  
```  
  
## <a name="see-also"></a>請參閱＜  
 [DATEADD &#40;SSIS 運算式 &#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;SSIS 運算式 &#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40;SSIS 運算式 &#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [日 &#40;SSIS 運算式 &#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [年份 &#40;SSIS 運算式 &#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [函式 &#40;SSIS 運算式 &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

