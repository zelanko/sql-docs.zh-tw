---
title: ReadDefinition 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 566190775f9247f253ae614876d3b011dea604b7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34041184"
---
# <a name="readdefinition-element-assl"></a>ReadDefinition 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  決定成員是否可以讀取資料庫的定義或資料庫中物件的定義。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Permission> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <ReadDefinition>...</ReadDefinition>  
   ...  
</Permission>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*無*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md)， [DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md)， [DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md)， [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)， [MiningStructurePermission](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)，[權限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|說明|  
|-----------|-----------------|  
|*無*|不允許對物件定義進行存取。|  
|*Basic*|允許對物件定義進行基本存取。<br /><br /> 附註： 此權限，才能建立本機 cube、 連結量值群組和連結維度。|  
|*允許*|允許對物件定義進行完整存取。<br /><br /> 請注意： 此權限就必須執行[探索](../../../analysis-services/xmla/xml-elements-methods-discover.md)XML for Analysis (XMLA) 呼叫使用 DISCOVER_XML_METADATA 參數。|  
  
 對應至父系的項目**ReadDefinition**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.CubePermission>， <xref:Microsoft.AnalysisServices.DatabasePermission>， <xref:Microsoft.AnalysisServices.DimensionPermission>， <xref:Microsoft.AnalysisServices.MiningModelPermission>， <xref:Microsoft.AnalysisServices.MiningStructurePermission>，和<xref:Microsoft.AnalysisServices.Permission>.  
  
## <a name="see-also"></a>另請參閱  
 [Role 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
