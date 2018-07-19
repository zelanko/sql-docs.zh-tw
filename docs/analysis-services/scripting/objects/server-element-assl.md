---
title: Server 元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d9715dd8e6ebd5c080362004850674adc3113c8c
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34030569"
---
# <a name="server-element-assl"></a>Server 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  描述的執行個體[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Server>  
   <!—These elements are common to each major object -->  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreatedTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <Description>...</Description>  
   <Annotations>...</Annotations>  
   <!-- server elements or properties -->  
   <ProductName>...</ProductName>  
   <Edition>...</Edition>  
   <EditionId>...</Edition>  
   <Version>...</Version>  
   <ServerMode>...</ServerMode>  
   <ProductLevel>...</Databases>  
   <Databases>...</Databases>  
   <Assemblies>...</Assemblies>  
   <Traces>...</Traces>  
   <Roles>...</Roles>  
   <ServerProperties>...</ServerProperties>  
</Server>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)，[識別碼](../../../analysis-services/scripting/properties/id-element-assl.md)， [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)， [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)，[描述](../../../analysis-services/scripting/properties/description-element-assl.md)， [註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [ProductName](../../../analysis-services/scripting/properties/productname-element-assl.md)， [Edition](../../../analysis-services/scripting/properties/edition-element-assl.md)， [EditionId](../../../analysis-services/xmla/xml-elements-properties/editionid-element.md)，[版本](../../../analysis-services/scripting/properties/version-element-assl.md)， [ServerMode](../../../analysis-services/xmla/xml-elements-properties/editionid-element.md)， [ProductLevel](../../../analysis-services/xmla/xml-elements-properties/productlabel-element.md)，[資料庫](../../../analysis-services/scripting/collections/databases-element-assl.md)，[組件](../../../analysis-services/scripting/collections/assemblies-element-assl.md)，[追蹤](../../../analysis-services/scripting/collections/traces-element-assl.md)，[角色](../../../analysis-services/scripting/collections/roles-element-assl.md)，[ServerProperties](../../../analysis-services/scripting/collections/serverproperties-element-assl.md)>|  
  
## <a name="remarks"></a>備註  
 **伺服器**項目代表的執行個體[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，並做為 Analysis Services 指令碼語言 (ASSL) 節點階層中的最上層節點。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Server>。  
  
## <a name="see-also"></a>另請參閱  
 [物件 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
