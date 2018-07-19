---
title: MiningStructurePermission 元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d933d5051a9280d779c23eeb60832aee286dc131
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032549"
---
# <a name="miningstructurepermission-element-assl"></a>MiningStructurePermission 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義的權限的成員[角色](../../../analysis-services/scripting/objects/role-element-assl.md)針對個別的項目有[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<MiningStructurePermissions>  
   <MiningStructurePermission xsi:type="Permission">  
      <AllowDrillthrough>...</AllowDrillthrough>  
  
      <!-- This element also inherits all the child elements listed in Permission -->  
   </MiningStructurePermission>  
</MiningStructurePermissions>  
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
|父元素|[MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.MiningStructurePermission>。  
  
 在[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，權限**AllowDrillthrough**已經過擴充，可套用至採礦結構。 當您指派這個權限給某個角色時，屬於該角色成員的任何使用者都可以使用下列語法來直接查詢採礦結構：  
  
```  
SELECT <structure column list> FROM <structure>.CASES  
```  
  
 此外，如果**AllowDrillthrough**已啟用在採礦結構和採礦模型中，使用者可以查詢結構資料行不包含在採礦模型中使用下列語法：  
  
```  
SELECT StructureColumn('<structure column name>' FROM <model>.CASES  
```  
  
 例如，您建立了只使用下列資料行的模型：客戶索引鍵、客戶收入和客戶購買。 透過使用鑽研，使用者就可以傳回此採礦模型不包含的其他結構資料行，例如客戶連絡資訊。  
  
 因此，若要保護敏感性資料或個人資訊，您應該建構您的資料來源檢視來遮罩個人資訊，並授與**AllowDrillthrough**只在必要時在結構上的權限。  
  
 如需詳細資訊，請參閱[鑽研查詢 &#40;資料採礦&#41;](../../../analysis-services/data-mining/drillthrough-queries-data-mining.md)。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.MiningModel.AllowDrillThrough%2A>   
 <xref:Microsoft.AnalysisServices.AdomdClient.MiningModel.AllowDrillThrough%2A>   
 [物件 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
