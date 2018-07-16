---
title: ReportServer 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ReportServer Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReportServer
helpviewer_keywords:
- ReportServer element
ms.assetid: 677437aa-9d15-4dcc-a9bc-34f851d9640d
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 68d80b432482d5b84db38d43291459c6aff8c758
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208198"
---
# <a name="reportserver-element-assl"></a>ReportServer 元素 (ASSL)
  包含名稱的[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]執行個體，以供[ReportAction](../data-type/action-data-type-assl.md)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ReportAction>  
  ...  
   <ReportServer>...</ReportServer>  
   ...  
</ReportAction>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ReportAction](../data-type/action-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素`ReportServer`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.ReportAction>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
