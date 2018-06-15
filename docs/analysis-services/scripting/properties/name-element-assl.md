---
title: Name 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: aa5073bd0728035ff4940b66fd2593eaf13cfd44
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34044042"
---
# <a name="name-element-assl"></a>Name 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (最多 100 個字元)|  
|預設值|非固定|  
|基數|1-1：只出現一次的必要元素|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../../../analysis-services/scripting/objects/action-element-assl.md)，[彙總](../../../analysis-services/scripting/objects/aggregation-element-assl.md)， [AggregationDesign](../../../analysis-services/scripting/objects/aggregationdesign-element-assl.md)， [AlgorithmParameter](../../../analysis-services/scripting/objects/algorithmparameter-element-assl.md)，[註解](../../../analysis-services/scripting/objects/annotation-element-assl.md)， [組件](../../../analysis-services/scripting/objects/assembly-element-assl.md)， [ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)， [Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)， [CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)， [CubeHierarchy](../../../analysis-services/scripting/data-type/cubehierarchy-data-type-assl.md)， [資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)， [DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md)， [DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)，[維度](../../../analysis-services/scripting/objects/dimension-element-assl.md)， [DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)，[群組](../../../analysis-services/scripting/objects/group-element-assl.md)，[階層](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)， [Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)，[層級](../../../analysis-services/scripting/objects/level-element-assl.md)， [MdxScript](../../../analysis-services/scripting/objects/mdxscript-element-assl.md)， [量值](../../../analysis-services/scripting/objects/measure-element-assl.md)， [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md)， [MemberProperty](../../../analysis-services/scripting/objects/attributerelationship-element-assl.md)， [MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)， [MiningModelColumn](../../../analysis-services/scripting/data-type/miningmodelcolumn-data-type-assl.md)， [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)， [MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)，[分割](../../../analysis-services/scripting/objects/partition-element-assl.md)，[權限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)， [檢視方塊](../../../analysis-services/scripting/objects/perspective-element-assl.md)， [PerspectiveCalculation](../../../analysis-services/scripting/data-type/perspectivecalculation-data-type-assl.md)， [ReportFormatParameter](../../../analysis-services/scripting/objects/reportformatparameter-element-asl.md)， [ReportParameter](../../../analysis-services/scripting/objects/reportparameter-element-assl.md)， [角色](../../../analysis-services/scripting/objects/role-element-assl.md)，[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)， [ServerProperty](../../../analysis-services/scripting/objects/serverproperty-element-assl.md)，[追蹤](../../../analysis-services/scripting/objects/trace-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 用來定義物件的每個項目 (執行個體[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]、 階層、 屬性及等等) 已**名稱**元素當做屬性。 值**名稱**項目具有下列限制：  
  
-   此值不得包含開頭或尾端空格。 如果值包含開頭或尾端空格**名稱**項目，這些空格會隱含地移除[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
-   此值不應該包含控制字元。 強烈建議名稱中不要出現控制字元，這有時可能會導致 XML 驗證錯誤。  
  
     建立使用物件的**GetNewName**方法中的[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，AMO 會檢查並隨後會予以移除任何控制字元、 開頭空白，或名稱中的尾端空白。 這個原因，使用**GetNewName**是設定物件名稱的建議的方法。  
  
     不過，如果您設定**名稱**屬性直接，相同的驗證不會執行檢查，但可能會造成 XML 驗證錯誤。 實際上是否發生錯誤取決於名稱中出現的控制字元。  
  
     雖然控制字元永遠不應使用於物件名稱，Analysis Services 不會明確地防止它們。 舊版 Analysis Services 有時會接受物件名稱中的控制字元。 這個原因，SQL Server 2016 Analysis Services 和更新版本會忽略物件名稱以避免破壞舊的方案中的控制字元。  
  
-   下列保留的值不可使用：  
  
    -   AUX  
  
    -   CLOCK$  
  
    -   COM1 到 COM9 (COM1、COM2、COM3 等等)  
  
    -   CON  
  
    -   LPT1 到 LPT9 (LPT1、LPT2、LPT3 等等)  
  
    -   NUL  
  
    -   PRN  
  
 下表列出的值之中不能使用的其他字元**名稱**項目，並根據父項目。  
  
|父元素|無效字元|  
|--------------------|------------------------|  
|[Server](../../../analysis-services/scripting/objects/server-element-assl.md)|此名稱必須依照 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 電腦名稱的規則。 IP 位址無效。|  
|[DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md)|:/\\*&#124;?"（) []{}<>|  
|[層級](../../../analysis-services/scripting/objects/level-element-assl.md)，[屬性項目](../../../analysis-services/scripting/objects/attribute-element-assl.md)|.,;'`:/\\*&#124;?"& %$！ + = []{}<>|  
|所有其他的父元素。|.,;'`:/\\*&#124;?"& %$！ + = （) []{}<>|  
  
## <a name="see-also"></a>另請參閱  
 [ID 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/id-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
