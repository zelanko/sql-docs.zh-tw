---
title: "CubeHierarchy 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: CubeHierarchy Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CubeHierarchy
helpviewer_keywords: CubeHierarchy data type
ms.assetid: cd633409-0c14-4dd9-97cc-3d30e25df24f
caps.latest.revision: "44"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6ed9177da67bf17a4be9cabf49404bd1b51a31de
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="cubehierarchy-data-type-assl"></a>CubeHierarchy 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定義代表的相關資訊的基本資料類型[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)中的項目[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)項目。  
  
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
|子元素|[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[啟用](../../../analysis-services/scripting/properties/enabled-element-assl.md)， [HierarchyID](../../../analysis-services/scripting/properties/hierarchyid-element-assl.md)，[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)， [OptimizedState](../../../analysis-services/scripting/properties/optimizedstate-element-assl.md)，[可見](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
|衍生的元素|[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)([階層](../../../analysis-services/scripting/collections/hierarchies-element-assl.md)集合[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md))|  
  
## <a name="remarks"></a>備註  
 此資料類型沒有任何限制，而且可在任何部署模式下使用：0-多維度和資料採礦、1-SharePoint 及 2-表格式。  
  
 在 SQL Server 2016 Analysis Services 和更新版本，*啟用*屬性不能設定為**False**如*CubeHierarchy*。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.CubeHierarchy>。  
  
## <a name="see-also"></a>請參閱  
 [探索方法 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-methods-discover.md)   
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
