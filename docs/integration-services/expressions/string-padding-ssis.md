---
title: "字串填補 (SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- padding strings [Integration Services]
- expressions [Integration Services], string padding
- string padding
ms.assetid: d3fed73d-e0d4-4c67-9355-fb7083a72dd6
caps.latest.revision: "33"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 017d4fd1f967cbbb54abebc63add0ecf6b6d1c62
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="string-padding-ssis"></a>字串填補 (SSIS)
  運算式評估工具不會檢查字串是否包含開頭和尾端空白，也不會在比較之前填補字串，使其長度相等。 如果運算式需要字串填補，您可使用 + 運算子串連資料行的值和空白字串。 如需詳細資訊，請參閱 [+ &#40;串連&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/concatenate-ssis-expression.md)。  
  
 換句話說，如果您要移除空白，運算式評估工具提供 LTRIM、RTRIM 和 TRIM 函數，可用來移除開頭和 (或)尾端空白。 如需詳細資訊，請參閱 [LTRIM &#40;SSIS 運算式&#41;](../../integration-services/expressions/ltrim-ssis-expression.md)[RTRIM &#40;SSIS 運算式&#41;](../../integration-services/expressions/rtrim-ssis-expression.md)，和 [TRIM &#40;SSIS 運算式&#41;](../../integration-services/expressions/trim-ssis-expression.md)。  
  
> [!NOTE]  
>  LEN 函數的計數中包含開頭和尾端空白。  
  
## <a name="related-content"></a>相關內容  
 pragmaticworks.com 上的技術文件： [SSIS 運算式小抄](http://go.microsoft.com/fwlink/?LinkId=746575)  
  
  
