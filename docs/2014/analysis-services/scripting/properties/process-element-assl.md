---
title: 處理元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Process Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Process
helpviewer_keywords:
- Process element
ms.assetid: 4aa08718-be44-4781-92cf-7b32b20f862c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: af200735a07812720110df6665cffcfbdf34db10
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48216600"
---
# <a name="process-element-assl"></a>Process 元素 (ASSL)
  決定使用者是否可以處理父元素的擁有者。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Permission> <-- or one of the other elements contained in the Element Relationships table -->  
   ...  
   <Process>...</Process>  
   ...  
</Permission>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|False|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CubePermission](../objects/cubepermission-element-assl.md)， [DatabasePermission](../objects/databasepermission-element-assl.md)， [DimensionPermission](../objects/dimensionpermission-element-assl.md)， [MiningModelPermission](../objects/miningmodelpermission-element-assl.md)， [MiningStructurePermission](../objects/miningstructurepermission-element-assl.md)，[權限](../data-type/permission-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中對應至 `Process` 父系的元素是 <xref:Microsoft.AnalysisServices.CubePermission>、<xref:Microsoft.AnalysisServices.DatabasePermission>、<xref:Microsoft.AnalysisServices.DimensionPermission>、<xref:Microsoft.AnalysisServices.MiningModelPermission>、<xref:Microsoft.AnalysisServices.MiningStructurePermission> 和 <xref:Microsoft.AnalysisServices.Permission>。  
  
## <a name="see-also"></a>另請參閱  
 [Role 元素&#40;ASSL&#41;](../objects/role-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
