---
title: DATEPART (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- dates [Integration Services], DATEPART
- DATEPART function
ms.assetid: 3e590094-fc49-4144-805f-fdc1bf2fe509
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e85eb7e41a3211f132ea32858bf859c153f15de7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71290287"
---
# <a name="datepart-ssis-expression"></a>DATEPART (SSIS 運算式)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  傳回代表日期之日期部分的整數。  
  
## <a name="syntax"></a>語法  
  
```  
  
DATEPART(datepart, date)  
```  
  
## <a name="arguments"></a>引數  
 *日期部份*  
 這是指定日期中哪一個部分要傳回新值的參數。  
  
 *date*  
 傳回有效日期或日期格式字串的運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 如果引數為 Null，則 DATEPART 會傳回 Null 結果。  
  
 日期常值必須明確轉換為日期資料類型之一。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
 下表列出運算式評估工具所辨識的日期部份與縮寫。 日期部份的名稱不區分大小寫。  
  
|日期部份|縮寫|  
|--------------|-------------------|  
|Year|yy, yyyy|  
|Quarter|qq, q|  
|Month|mm, m|  
|Dayofyear|dy, y|  
|Day|dd, d|  
|週|wk, ww|  
|Weekday|dw|  
|Hour|Hh|  
|Minute|mi, n|  
|第二個|ss, s|  
|Millisecond|Ms|  
  
## <a name="ssis-expression-examples"></a>SSIS 運算式範例  
 這個範例會傳回在日期常值中代表月份的整數。 如果日期格式為 mm/dd/yyyy"，則這個範例會傳回 11。  
  
```  
DATEPART("month", (DT_DBTIMESTAMP)"11/04/2002")  
```  
  
 這個範例會傳回 **ModifiedDate** 資料行中，代表天的整數。  
  
```  
DATEPART("dd", ModifiedDate)  
```  
  
 這個範例會傳回代表目前日期之年份的整數。  
  
```  
DATEPART("yy",GETDATE())  
```  
  
## <a name="see-also"></a>另請參閱  
 [DATEADD &#40;SSIS 運算式&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;SSIS 運算式&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DAY &#40;SSIS 運算式&#41;](../../integration-services/expressions/day-ssis-expression.md)   
 [MONTH &#40;SSIS 運算式&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR &#40;SSIS 運算式&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
