---
title: AllowDrillThrough 元素 (ASSL) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 25bad363975494fc8bd6c8cb343a165d8bb85f85
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34036009"
---
# <a name="allowdrillthrough-element-assl"></a>AllowDrillThrough 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  決定是否允許針對父元素進行鑽研。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningModel> <!-- or MiningModelPermission -->  
<!-- or MiningStructurePermission -->   ...  
   <AllowDrillThrough>...</AllowDrillThrough>  
   ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|**False**|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningModel 元素](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)， [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)， [MiningStructurePermission](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應至父系的項目**AllowDrillThrough**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.MiningModel>， <xref:Microsoft.AnalysisServices.MiningModelPermission>，和<xref:Microsoft.AnalysisServices.MiningStructurePermission>。  
  
## <a name="drillthrough-on-mining-structures"></a>採礦結構的鑽研  
 在[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，您可以定義**AllowDrillthrough**採礦結構與採礦模型的權限。 當您指派這個權限給某個角色時，該角色的任何成員都可以查詢資料採礦模型，而且會傳回此模型不包含的結構資料行。 例如，您建立了只使用下列資料行的模型：客戶索引鍵、客戶收入和客戶購買。 如果您針對此模型啟用鑽研，使用者就可以傳回採礦結構之其他資料行中的資訊，例如客戶電子郵件或名稱。  
  
 因此，為了保護機密資料，在您將資料行加入至採礦結構時，請務必小心。 此外，只有在必要時，才應該授與結構的 **AllowDrillthrough** 權限。  
  
 若要鑽研結構資料行，請使用查詢搭配下列其中一種格式：  
  
 `SELECT * FROM <structure>.CASES`  
  
 或  
  
 `SELECT StructureColumn('<structure-column-name>') FROM <model>.CASES`  
  
## <a name="see-also"></a>另請參閱  
 [Role 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
