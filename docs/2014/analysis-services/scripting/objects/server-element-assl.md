---
title: Server 元素 (ASSL) |Microsoft Docs
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
- Server Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- server
helpviewer_keywords:
- Server element
ms.assetid: 92ca67f6-817e-4a75-9244-8f8bcf412190
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d5ae1dc9c10bce01cb9b0f90da2ef25b023392f3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319228"
---
# <a name="server-element-assl"></a>Server 元素 (ASSL)
  Popisuje instanci [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[名稱](../properties/name-element-assl.md)，[識別碼](../properties/id-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)，[描述](../properties/description-element-assl.md)， [的註解](../collections/annotations-element-assl.md)， [ProductName](../properties/productname-element-assl.md)， [Edition](../properties/edition-element-assl.md)， [EditionId](../../xmla/xml-elements-properties/editionid-element.md)，[版本](../properties/version-element-assl.md)， [ServerMode](../../xmla/xml-elements-properties/editionid-element.md)， [ProductLevel](../../xmla/xml-elements-properties/productlabel-element.md)，[資料庫](../collections/databases-element-assl.md)，[組件](../collections/assemblies-element-assl.md)，[追蹤](../collections/traces-element-assl.md)，[角色](../collections/roles-element-assl.md)，[ServerProperties](../collections/serverproperties-element-assl.md)>|  
  
## <a name="remarks"></a>備註  
 `Server` 元素代表 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體，而且它會當做「Analysis Services 指令碼語言」(ASSL) 節點階層中的最上層節點。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.Server>。  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
