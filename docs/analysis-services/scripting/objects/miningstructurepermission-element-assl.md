---
title: "MiningStructurePermission 元素 (ASSL) |Microsoft 文件"
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
apiname: MiningStructurePermission Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: MiningStructurePermission
helpviewer_keywords: MiningStructurePermission element
ms.assetid: 4ba2bfd2-9003-4eed-8049-a74d452894ea
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f0e1ece5a8a03ccd66d2fa93f925d52f3a946b2c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="miningstructurepermission-element-assl"></a>MiningStructurePermission 元素 (ASSL)
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
  
## <a name="see-also"></a>請參閱＜  
 <xref:Microsoft.AnalysisServices.MiningModel.AllowDrillThrough%2A>   
 <xref:Microsoft.AnalysisServices.AdomdClient.MiningModel.AllowDrillThrough%2A>   
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
