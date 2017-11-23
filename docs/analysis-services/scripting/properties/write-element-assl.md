---
title: "Write 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Write Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords: Write element
ms.assetid: d8f7a367-d7bf-4b40-acb4-19c8bc8c6c20
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 469471f8c7838d4a17d6516e506e7ab55357fad9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="write-element-assl"></a>Write 元素 (ASSL)
  判斷是否可寫入資料或中繼資料的指定[CubeDimensionPermission](../../../analysis-services/scripting/data-type/cubedimensionpermission-data-type-assl.md)或[權限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CubeDimensionPermission> <!-- or Permission -->  
   ...  
   <Write>...</Write>  
   ...  
</CubeDimensionPermission>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*無*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CubeDimensionPermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)，[權限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|說明|  
|-----------|-----------------|  
|*無*|不允許存取父物件的資料或中繼資料。|  
|*允許*|允許寫入父物件的資料和中繼資料。|  
  
## <a name="remarks"></a>備註  
 對應至父系的項目**寫入**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.CubeDimensionPermission>和<xref:Microsoft.AnalysisServices.Permission>。  
  
## <a name="see-also"></a>請參閱＜  
 [Cube 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/cube-element-assl.md)   
 [Dimension 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/dimension-element-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
