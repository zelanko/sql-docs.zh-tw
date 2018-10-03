---
title: MiningStructurePermission 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MiningStructurePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningStructurePermission
helpviewer_keywords:
- MiningStructurePermission element
ms.assetid: 4ba2bfd2-9003-4eed-8049-a74d452894ea
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 89521b4201e3956ab6d44d95d7234321a0948f56
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197618"
---
# <a name="miningstructurepermission-element-assl"></a>MiningStructurePermission 元素 (ASSL)
  定義的權限的成員[角色](role-element-assl.md)項目有針對個別[MiningStructure](miningstructure-element-assl.md)項目。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[權限](../data-type/permission-data-type-assl.md)|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.MiningStructurePermission>。  
  
 在  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]，權限`AllowDrillthrough`已擴充到套用至採礦結構。 當您指派這個權限給某個角色時，屬於該角色成員的任何使用者都可以使用下列語法來直接查詢採礦結構：  
  
```  
SELECT <structure column list> FROM <structure>.CASES  
```  
  
 此外，如果您同時針對採礦結構和採礦模型啟用了 `AllowDrillthrough`，使用者就可以使用下列語法來查詢此採礦模型不包含的結構資料行：  
  
```  
SELECT StructureColumn('<structure column name>' FROM <model>.CASES  
```  
  
 例如，您建立了只使用下列資料行的模型：客戶索引鍵、客戶收入和客戶購買。 透過使用鑽研，使用者就可以傳回此採礦模型不包含的其他結構資料行，例如客戶連絡資訊。  
  
 因此，若要保護機密資料或個人資訊，您應該建構資料來源檢視來遮罩個人資訊，並只有在必要時，才授與結構的 `AllowDrillthrough` 權限。  
  
 如需詳細資訊，請參閱[鑽研查詢 &#40;資料採礦&#41;](../../data-mining/drillthrough-queries-data-mining.md)。  
  
## <a name="see-also"></a>另請參閱  
 <xref:Microsoft.AnalysisServices.MiningModel.AllowDrillThrough%2A>   
 <xref:Microsoft.AnalysisServices.AdomdClient.MiningModel.AllowDrillThrough%2A>   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
