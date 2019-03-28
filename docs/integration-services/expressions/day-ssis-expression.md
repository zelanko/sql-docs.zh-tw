---
title: DAY (SSIS 運算式) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- DAY function
- dates [Integration Services], DAY
ms.assetid: d8447187-49df-45b7-a98e-142ad44fd3e2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4f85a19231a7d3e3adaf514ef304f459357c5ec0
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58271948"
---
# <a name="day-ssis-expression"></a>DAY (SSIS 運算式)
  傳回代表日期之日部分的整數。  
  
## <a name="syntax"></a>語法  
  
```  
  
DAY(date)  
```  
  
## <a name="arguments"></a>引數  
 *date*  
 傳回有效日期或日期格式字串的運算式。  
  
## <a name="result-types"></a>結果類型  
 DT_I4  
  
## <a name="remarks"></a>Remarks  
 如果引數為 Null，則 DAY 會傳回 Null 結果。  
  
 日期常值必須明確轉換為日期資料類型之一。 如需詳細資訊，請參閱 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
> [!NOTE]  
>  當日期常值明確轉換成以下其中一個日期資料類型時，此運算式將會驗證失敗：DT_DBTIMESTAMPOFFSET 和 DT_DBTIMESTAMP2。  
  
 使用 DAY 函數較為簡潔，但相當於使用 DATEPART("Day", date)。  
  
## <a name="expression-examples"></a>運算式範例  
 這個範例會傳回日期常值的日數。 如果日期格式為「mm/dd/yyyy」，則這個範例會傳回 23。  
  
```  
DAY((DT_DBTIMESTAMP)"11/23/2002")  
```  
  
 這個範例會傳回 **ModifiedDate** 資料行中，代表天的整數。  
  
```  
DAY(ModifiedDate)  
```  
  
 這個範例會傳回代表目前日期之日子的整數。  
  
```  
DAY(GETDATE())  
```  
  
## <a name="see-also"></a>另請參閱  
 [DATEADD &#40;SSIS 運算式&#41;](../../integration-services/expressions/dateadd-ssis-expression.md)   
 [DATEDIFF &#40;SSIS 運算式&#41;](../../integration-services/expressions/datediff-ssis-expression.md)   
 [DATEPART &#40;SSIS 運算式&#41;](../../integration-services/expressions/datepart-ssis-expression.md)   
 [MONTH &#40;SSIS 運算式&#41;](../../integration-services/expressions/month-ssis-expression.md)   
 [YEAR &#40;SSIS 運算式&#41;](../../integration-services/expressions/year-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
