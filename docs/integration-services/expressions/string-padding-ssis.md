---
description: 字串填補 (SSIS)
title: 字串填補 (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- padding strings [Integration Services]
- expressions [Integration Services], string padding
- string padding
ms.assetid: d3fed73d-e0d4-4c67-9355-fb7083a72dd6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e5b72ff09988b609a82f4a5c2f57c6825ad5f0cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495619"
---
# <a name="string-padding-ssis"></a>字串填補 (SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  運算式評估工具不會檢查字串是否包含開頭和尾端空白，也不會在比較之前填補字串，使其長度相等。 如果運算式需要字串填補，您可使用 + 運算子串連資料行的值和空白字串。 如需詳細資訊，請參閱 [+ &#40;串連&#41; &#40;SSIS 運算式&#41;](../../integration-services/expressions/concatenate-ssis-expression.md)。  
  
 換句話說，如果您要移除空白，運算式評估工具提供 LTRIM、RTRIM 和 TRIM 函數，可用來移除開頭和 (或)尾端空白。 如需詳細資訊，請參閱 [LTRIM &#40;SSIS 運算式&#41;](../../integration-services/expressions/ltrim-ssis-expression.md)[RTRIM &#40;SSIS 運算式&#41;](../../integration-services/expressions/rtrim-ssis-expression.md)，和 [TRIM &#40;SSIS 運算式&#41;](../../integration-services/expressions/trim-ssis-expression.md)。  
  
> [!NOTE]  
>  LEN 函數的計數中包含開頭和尾端空白。  
  
## <a name="related-content"></a>相關內容  
 pragmaticworks.com 上的技術文件： [SSIS 運算式小抄](https://go.microsoft.com/fwlink/?LinkId=746575)  
  
  
