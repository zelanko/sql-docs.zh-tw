---
title: DrillThroughAction 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DrillThroughAction Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DrillThroughAction
helpviewer_keywords:
- DrillThroughAction data type
ms.assetid: e212d575-a0d7-4548-92b4-33542ef59034
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8142fd9978ae456b03b4a0381e2ab9261cdc8c4d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37241438"
---
# <a name="drillthroughaction-data-type-assl"></a>DrillThroughAction 資料類型 (ASSL)
  定義代表鑽研動作的衍生資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DrillThroughAction>  
   <!-- The following elements extend Action -->  
   <Default>...</Default>  
   <Columns>...</Columns>  
</DrillThroughAction>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[動作](action-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[資料行](../collections/columns-element-assl.md)，[預設](../properties/default-element-assl.md)|  
|衍生的元素|[動作](../objects/action-element-assl.md)([動作](../collections/actions-element-assl.md)，集合[Cube](../objects/cube-element-assl.md)，或[觀點來看](../objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.DrillThroughAction>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
