---
title: "GETUTCDATE （SSIS 運算式） |Microsoft 文件"
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
- dates [Integration Services], GETUTCDATE
- current date
- UTC time
- GETUTCDATE function
ms.assetid: 2282339c-c24f-493e-8e66-181ea8af5ad0
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fd7919482026f85d9261c2a36d16defdf6b59cd9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/28/2017

---
# <a name="getutcdate-ssis-expression"></a>GETUTCDATE (SSIS 運算式)
  使用 DT_DBTIMESTAMP 格式，傳回 UTC 時間格式 (世界標準時間或格林威治標準時間) 的系統目前日期。 GETUTCDATE 函數不接受引數。  
  
## <a name="syntax"></a>語法  
  
```  
  
GETUTCDATE()  
```  
  
## <a name="arguments"></a>引數  
 無  
  
## <a name="result-types"></a>結果類型  
 DT_DBTIMESTAMP  
  
## <a name="expression-examples"></a>運算式範例  
 此範例會傳回 UTC 時間格式的目前日期之年份。  
  
```  
DATEPART("year",GETUTCDATE())  
```  
  
 此範例會傳回 **ModifiedDate** 資料行中的日期與目前 UTC 日期之間的天數。  
  
```  
DATEDIFF("dd",ModifiedDate,GETUTCDATE())  
```  
  
 此範例會將目前的 UTC 日期加上三個月。  
  
```  
DATEADD("Month",3,GETUTCDATE())  
```  
  
## <a name="see-also"></a>另請參閱  
 [GETDATE &#40;SSIS 運算式&#41;](../../integration-services/expressions/getdate-ssis-expression.md)   
 [函數 &#40;SSIS 運算式&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
