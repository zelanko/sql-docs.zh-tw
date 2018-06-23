---
title: CubeHierarchy 資料類型 (ASSL) |Microsoft 文件
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
- CubeHierarchy Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeHierarchy
helpviewer_keywords:
- CubeHierarchy data type
ms.assetid: cd633409-0c14-4dd9-97cc-3d30e25df24f
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 48176b4096b7fa7ba8e1847750410be0f65da552
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36131585"
---
# <a name="cubehierarchy-data-type-assl"></a>CubeHierarchy 資料類型 (ASSL)
  定義代表的相關資訊的基本資料類型[階層](../objects/hierarchy-element-assl.md)中的項目[Cube](../objects/cube-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```  
<CubeHierarchy>   <HierarchyID>...</HierarchyID>   <Name>...</Name>   <OptimizedState>...</OptimizedState>   <Visible>...</Visible>   <Enabled>...</Enabled>   <Annotations>...</Annotations></CubeHierarchy>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[註解](../collections/annotations-element-assl.md)，[啟用](../properties/enabled-element-assl.md)， [HierarchyID](../properties/id-element-assl.md)，[名稱](../properties/name-element-assl.md)， [OptimizedState](../properties/state-element-assl.md)，[可見](../properties/visible-element-assl.md)|  
|衍生的元素|[階層](../objects/hierarchy-element-assl.md)([階層](../collections/hierarchies-element-assl.md)集合[CubeDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>備註  
 此資料類型沒有任何限制，而且可在任何部署模式下使用：0-多維度和資料採礦、1-SharePoint 及 2-表格式。  
  
 在[!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)]、*啟用*屬性不能設定為`False`如*CubeHierarchy*。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.CubeHierarchy>。  
  
## <a name="see-also"></a>另請參閱  
 [Discover 方法&#40;XMLA&#41;](../../xmla/xml-elements-methods-discover.md)   
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  