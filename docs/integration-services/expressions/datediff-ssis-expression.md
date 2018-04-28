---
title: DATEDIFF (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- DATEDIFF statement
- dates [Integration Services], DATEDIFF
ms.assetid: 449b327f-47c7-4709-8bc6-4ee9a35cc330
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 4e8cd3e6dea813adf354f2d767efd286161c4f16
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2018
---
# <a name="datediff-ssis-expression"></a>DATEDIFF (SSIS 運算式)
  傳回跨越兩個指定日期的日期和時間界線數目。 *datepart* 參數會識別要比較的日期和時間界線。  
  
## <a name="syntax"></a>語法  
  
```  
  
DATEDIFF(datepart, startdate, endate)  
```  
  
## <a name="arguments"></a>引數  
 *datepart*  
 是指定日期中哪一個部分要進行比較和傳回值的參數。  
  
 *startdate*  
 是間隔的開始日期。  
  
 *endate*  
 是間隔的結束日期。  
  
## <a name="result-types"></a>結果類型  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 下表列出運算式評估工具所辨識的日期部份與縮寫。  
  
|datepart|縮寫|  
|--------------|-------------------|  
|Year|yy, yyyy|  
|Quarter|qq, q|  
|Month|mm, m|  
|Dayofyear|dy, y|  
|Day|dd, d|  
|週|wk, ww|  
|Weekday|dw, w|  
|Hour|Hh|  
|Minute|mi, n|  
|第二個|ss, s|  
|Millisecond|Ms|  
  
 如果任何引數為 Null，則 DATEDIFF 會傳回 Null 結果。  
  
 日期常值必須明確轉換為日期資料類型之一。 如需相關資訊，請參閱 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 如果日期無效、日期或時間單位不是字串、開始日期不是日期，或結束日期不是日期，則會發生錯誤。  
  
 如果結束日期早於開始日期，則函數會傳回負數。 如果開始和結束日期相等或落在相同的間隔內，則函數會傳回零。  
  
## <a name="ssis-expression-examples"></a>SSIS 運算式範例  
 此範例會計算兩個日期常值之間的天數。 如果日期格式為 "mm/dd/yyyy"，則函數會傳回 7。  
  
```  
DATEDIFF("dd", (DT_DBTIMESTAMP)"8/1/2003", (DT_DBTIMESTAMP)"8/8/2003")  
```  
  
 此範例會傳回日期常值和目前日期之間的月數。  
  
```  
DATEDIFF("mm", (DT_DBTIMESTAMP)"8/1/2003",GETDATE())  
```  
  
 此範例會傳回 **ModifiedDate** 資料行中的日期與 **YearEndDate** 變數之間的星期數。 如果 **YearEndDate** 的資料類型為 **date** ，則不需要明確轉換。  
  
```  
DATEDIFF("Week", ModifiedDate,@YearEndDate)  
```  
  
## <a name="see-also"></a>另請參閱  
 [DATEADD &#40;SSIS 運算式&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEPART &#40;SSIS 運算式&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [DAY &#40;SSIS 運算式&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH &#40;SSIS 運算式&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR &#40;SSIS 運算式&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
