---
title: 路徑元素 (ASSL) |Microsoft 文件
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
- Path Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Path
helpviewer_keywords:
- Path element
ms.assetid: 0edc59ac-1671-4fe1-9b7c-6c1548df5c63
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5ba53c4ee4399a39ebd8e4a1b14c9c062b3abaa7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031985"
---
# <a name="path-element-assl"></a>Path 元素 (ASSL)
  包含所提供的執行個體的路徑， [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]，所使用之報表的[ReportAction](../data-type/action-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ReportAction>  
   ...  
   <Path>...</Path>  
   ...  
</ReportAction>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|無|  
|基數|0-1：只出現一次的選擇性元素|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ReportAction](../data-type/action-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目`Path`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ReportAction>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  