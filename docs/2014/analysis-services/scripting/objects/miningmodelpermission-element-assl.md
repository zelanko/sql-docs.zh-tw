---
title: MiningModelPermission 元素 (ASSL) |Microsoft 文件
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
- MiningModelPermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelPermission
helpviewer_keywords:
- MiningModelPermission element
ms.assetid: 4bd2f7e7-ff0d-404e-96fb-7e2c4eeb91e9
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 42a02eedcc2c054269872e4c0f9523ab63632eda
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36135700"
---
# <a name="miningmodelpermission-element-assl"></a>MiningModelPermission 元素 (ASSL)
  定義的權限成員[角色](role-element-assl.md)針對個別的項目有[MiningModel](miningmodel-element-assl.md)項目。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[權限](../data-type/permission-data-type-assl.md)|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningModelPermissions](../collections/miningmodelpermissions-element-assl.md)|  
|子元素|[AllowBrowsing](../properties/allowbrowsing-element-assl.md)， [AllowDrillThrough](../properties/allowdrillthrough-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 在[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，您可以啟用採礦結構的鑽研藉由新增`AllowDrillthrough`權限[MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md)集合。 如果`AllowDrillthrough`採礦結構和採礦模型具有的角色的任何成員上啟用[AllowDrillThrough 元素&#40;ASSL&#41; ](../properties/allowdrillthrough-element-assl.md)模型的權限可以查詢資料採礦模型，並傳回結構資料行未包含在模型中，使用下列語法：  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 因此，若要保護敏感性資料或個人資訊，您應該只在必要時，授與採礦模型的 `AllowDrillthrough` 權限。 如需詳細資訊，請參閱[AllowDrillThrough 元素&#40;ASSL&#41;](../properties/allowdrillthrough-element-assl.md)。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.MiningModelPermission>。  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  