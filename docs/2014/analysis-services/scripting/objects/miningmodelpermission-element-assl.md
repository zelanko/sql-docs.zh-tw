---
title: MiningModelPermission 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c6bad2b1bda46fcc1437a5f4c967ced8a6c726f0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48113468"
---
# <a name="miningmodelpermission-element-assl"></a>MiningModelPermission 元素 (ASSL)
  定義的權限成員[角色](role-element-assl.md)項目有針對個別[MiningModel](miningmodel-element-assl.md)項目。  
  
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
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningModelPermissions](../collections/miningmodelpermissions-element-assl.md)|  
|子元素|[AllowBrowsing](../properties/allowbrowsing-element-assl.md)， [AllowDrillThrough](../properties/allowdrillthrough-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 在  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，您可以藉由新增來讓採礦結構的鑽研`AllowDrillthrough`權限[MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md)集合。 如果`AllowDrillthrough`採礦結構和採礦模型，具有角色的任何成員上啟用[AllowDrillThrough 元素&#40;ASSL&#41; ](../properties/allowdrillthrough-element-assl.md)模型的權限可以查詢資料採礦模型，並傳回未包含在模型中，使用下列語法的結構資料行：  
  
```  
SELECT StructureColumn('<column name>') FROM <model>.CASES  
```  
  
 因此，若要保護敏感性資料或個人資訊，您應該只在必要時，授與採礦模型的 `AllowDrillthrough` 權限。 如需詳細資訊，請參閱 < [AllowDrillThrough 元素&#40;ASSL&#41;](../properties/allowdrillthrough-element-assl.md)。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.MiningModelPermission>。  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
