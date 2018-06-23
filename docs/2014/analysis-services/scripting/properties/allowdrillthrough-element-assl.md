---
title: AllowDrillThrough 元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- AllowDrillThrough Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AllowDrillThrough
helpviewer_keywords:
- AllowDrillThrough element
ms.assetid: 53c9e4a3-a376-447d-a13f-80d845cc9789
caps.latest.revision: 51
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e5ee132903b98c616ce756b423455302ca6e65f4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035315"
---
# <a name="allowdrillthrough-element-assl"></a>AllowDrillThrough 元素 (ASSL)
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|布林|  
|預設值|`False`|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningModel 元素](../objects/miningmodel-element-assl.md)， [MiningModelPermission](../objects/miningmodelpermission-element-assl.md)， [MiningStructurePermission](../objects/miningstructurepermission-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 在「分析管理物件」(AMO) 物件模型中對應至 `AllowDrillThrough` 父系的元素是 <xref:Microsoft.AnalysisServices.MiningModel>、<xref:Microsoft.AnalysisServices.MiningModelPermission> 和 <xref:Microsoft.AnalysisServices.MiningStructurePermission>。  
  
## <a name="drillthrough-on-mining-structures"></a>採礦結構的鑽研  
 在[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，您可以定義`AllowDrillthrough`採礦結構與採礦模型的權限。 當您指派這個權限給某個角色時，該角色的任何成員都可以查詢資料採礦模型，而且會傳回此模型不包含的結構資料行。 例如，您建立了只使用下列資料行的模型：客戶索引鍵、客戶收入和客戶購買。 如果您針對此模型啟用鑽研，使用者就可以傳回採礦結構之其他資料行中的資訊，例如客戶電子郵件或名稱。  
  
 因此，為了保護機密資料，在您將資料行加入至採礦結構時，請務必小心。 此外，只有在必要時，才應該授與結構的 `AllowDrillthrough` 權限。  
  
 若要鑽研結構資料行，請使用查詢搭配下列其中一種格式：  
  
 `SELECT * FROM <structure>.CASES`  
  
 中的多個  
  
 `SELECT StructureColumn('<structure-column-name>') FROM <model>.CASES`  
  
## <a name="see-also"></a>另請參閱  
 [Role 元素&#40;ASSL&#41;](../objects/role-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  