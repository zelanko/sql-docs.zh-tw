---
title: Server 元素 (ASSL) |Microsoft 文件
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
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f2bcf6e40530a67f8c1e9c846ba88f6d77648a09
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132002"
---
# <a name="server-element-assl"></a>Server 元素 (ASSL)
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[Name](../properties/name-element-assl.md), [ID](../properties/id-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md), [Description](../properties/description-element-assl.md), [Annotations](../collections/annotations-element-assl.md), [ProductName](../properties/productname-element-assl.md), [Edition](../properties/edition-element-assl.md), [EditionId](../../xmla/xml-elements-properties/editionid-element.md), [Version](../properties/version-element-assl.md), [ServerMode](../../xmla/xml-elements-properties/editionid-element.md), [ProductLevel](../../xmla/xml-elements-properties/productlabel-element.md), [Databases](../collections/databases-element-assl.md), [Assemblies](../collections/assemblies-element-assl.md), [Traces](../collections/traces-element-assl.md), [Roles](../collections/roles-element-assl.md), [ServerProperties](../collections/serverproperties-element-assl.md)>|  
  
## <a name="remarks"></a>備註  
 `Server` 元素代表 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 執行個體，而且它會當做「Analysis Services 指令碼語言」(ASSL) 節點階層中的最上層節點。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Server>。  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  