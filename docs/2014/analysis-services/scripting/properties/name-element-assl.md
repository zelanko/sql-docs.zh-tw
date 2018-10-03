---
title: Name 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Name Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Name
helpviewer_keywords:
- Name element
ms.assetid: caf2af86-5f9c-4e14-8168-f3a79248b4fe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 72a9dc3d252848a987e62c392f91086d0b62cc19
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083388"
---
# <a name="name-element-assl"></a>Name 元素 (ASSL)
  包含父元素的名稱。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Action> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <Name>...</Name>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (最多 100 個字元)|  
|預設值|非固定|  
|基數|1-1：只出現一次的必要元素|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../objects/action-element-assl.md)，[彙總](../objects/aggregation-element-assl.md)， [AggregationDesign](../objects/aggregationdesign-element-assl.md)， [AlgorithmParameter](../objects/algorithmparameter-element-assl.md)，[註釋](../objects/annotation-element-assl.md)， [組件](../objects/assembly-element-assl.md)， [ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)， [Cube](../objects/cube-element-assl.md)， [CubeDimension](../data-type/dimension-data-type-assl.md)， [CubeHierarchy](../data-type/hierarchy-data-type-assl.md)， [資料庫](../objects/database-element-assl.md)， [DataSource](../objects/datasource-element-assl.md)， [DataSourceView](../objects/datasourceview-element-assl.md)，[維度](../objects/dimension-element-assl.md)， [DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)，[群組](../objects/group-element-assl.md)，[階層](../objects/hierarchy-element-assl.md)， [Kpi](../objects/kpi-element-assl.md)，[層級](../objects/level-element-assl.md)， [MdxScript](../objects/mdxscript-element-assl.md)， [量值](../objects/measure-element-assl.md)， [MeasureGroup](../objects/measuregroup-element-assl.md)， [MemberProperty](../objects/attributerelationship-element-assl.md)， [MiningModel](../objects/miningmodel-element-assl.md)， [MiningModelColumn](../data-type/miningmodelcolumn-data-type-assl.md)， [MiningStructure](../objects/miningstructure-element-assl.md)， [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)，[分割](../objects/partition-element-assl.md)，[權限](../data-type/permission-data-type-assl.md)， [檢視方塊](../objects/perspective-element-assl.md)， [PerspectiveCalculation](../data-type/perspectivecalculation-data-type-assl.md)， [ReportFormatParameter](../objects/reportformatparameter-element-asl.md)， [ReportParameter](../objects/reportparameter-element-assl.md)， [角色](../objects/role-element-assl.md)，[伺服器](../objects/server-element-assl.md)， [ServerProperty](../objects/serverproperty-element-assl.md)，[追蹤](../objects/trace-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 每個項目，用來定義物件 (執行個體[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，階層、 屬性和等等) 已`Name`元素當做屬性。 `Name` 元素的值具有下列限制：  
  
-   此值不得包含開頭或尾端空格。 如果 `Name` 元素的值包含開頭或尾端空格，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 就會隱含地移除這些空格。  
  
-   此值不應該包含控制字元。 強烈建議名稱中不要出現控制字元，這有時可能會導致 XML 驗證錯誤。  
  
     對於使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 中的 `GetNewName` 方法所建立的物件，AMO 會檢查名稱中的任何控制字元、開頭空白或尾端空格，隨後會予以移除。 因此，使用 `GetNewName` 是設定物件名稱的建議方法。  
  
     不過，如果您直接設定 `Name` 屬性，則不會執行相同的驗證檢查，但可能會造成 XML 驗證錯誤。 實際上是否發生錯誤取決於名稱中出現的控制字元。  
  
     雖然控制字元永遠不應使用於物件名稱，Analysis Services 不會明確地防止它們。 舊版 Analysis Services 有時會接受物件名稱中的控制字元。 因此，[!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)] 會忽略物件名稱中的控制字元，以避免破壞舊的方案。  
  
-   下列保留的值不可使用：  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 到 COM9 (COM1、COM2、COM3 等等)  
  
    -   CON  
  
    -   LPT1 到 LPT9 (LPT1、LPT2、LPT3 等等)  
  
    -   NUL  
  
    -   PRN  
  
 下表將列出無法在 `Name` 元素值內部使用的其他字元，端視父元素而定。  
  
|父元素|無效字元|  
|--------------------|------------------------|  
|[Server](../objects/server-element-assl.md)|此名稱必須依照 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 電腦名稱的規則。 IP 位址無效。|  
|[DataSource](../objects/datasource-element-assl.md)|:/\\*&#124;?"（) []{}<>|  
|[層級](../objects/level-element-assl.md)，[屬性項目](../objects/attribute-element-assl.md)|.,;'`:/\\*&#124;?"& %$！ + = []{}<>|  
|所有其他的父元素。|.,;'`:/\\*&#124;?"& %$！ + = （) []{}<>|  
  
## <a name="see-also"></a>另請參閱  
 [ID 項目&#40;ASSL&#41;](id-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
