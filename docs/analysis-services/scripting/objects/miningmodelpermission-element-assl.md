---
title: MiningModelPermission 元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 98045d14e06c73ee0a68082395e95625afb550d0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="miningmodelpermission-element-assl"></a>MiningModelPermission 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義的權限成員[角色](../../../analysis-services/scripting/objects/role-element-assl.md)針對個別的項目有[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningModelPermissions>  
   <MiningModelPermission xsi:type="Permission">  
      <!-- The following elements extend Permission -->  
      <AllowDrillThrough>...</AllowDrillThrough>  
      <AllowBrowsing>...</AllowBrowsing>  
   </MiningModelPermission>  
</MiningModelPermissions>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|[權限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningModelPermissions](../../../analysis-services/scripting/collections/miningmodelpermissions-element-assl.md)|  
|子元素|[AllowBrowsing](../../../analysis-services/scripting/properties/allowbrowsing-element-assl.md)， [AllowDrillThrough](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 在[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，您可以啟用採礦結構的鑽研藉由新增**AllowDrillthrough**權限[MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)集合。 如果**AllowDrillthrough**採礦結構和採礦模型具有的角色的任何成員上啟用[AllowDrillThrough 元素&#40;ASSL&#41; ](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md)可以查詢模型的權限資料採礦模型，然後傳回結構資料行未包含在模型中，使用下列語法：  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 因此，若要保護敏感性資料或個人資訊，您應該只在必要時，授與採礦模型的 **AllowDrillthrough** 權限。 如需詳細資訊，請參閱[AllowDrillThrough 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md)。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.MiningModelPermission>。  
  
## <a name="see-also"></a>另請參閱  
 [物件 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
