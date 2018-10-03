---
title: Database 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Database Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DATABASE
helpviewer_keywords:
- Database element
ms.assetid: c3bc7eaf-ed0d-4395-a3b7-8d9cfacfe911
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 46166d77185836c65fe1d026255620dfb87c1f66
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191028"
---
# <a name="database-element-assl"></a>Database 元素 (ASSL)
  定義[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]資料庫。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Databases>  
   <Database>  
      <Name>...</Name>  
      <ID>...</ID>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastUpdate>...</LastUpdate>  
      <Description>...</Description>  
      <State>   </State>  
      <AggregationPrefix>...</AggregationPrefix>  
      <EstimatedSize>...</EstimatedSize>  
      <LastProcessed>...</LastProcessed>  
      <Language>...</Language>  
            <Collation>...</Collation>  
      <Visible>...</Visible>  
      <MasterDatasourceID>...</MasterDataSourceID>  
      <Accounts>...</Accounts>  
      <DataSources>...</DataSources>  
      <DataSourceViews>...</DataSourceViews>  
      <Dimensions>...</Dimensions>  
      <Cubes>...</Cubes>  
      <MiningStructures>...</MiningStructures>  
            <Roles>...</Roles>  
      <Assemblies>...</Assemblies>  
      <DatabasePermissions>...</DatabasePermissions>  
            <Translations>...</Translations>  
      <Annotations>...</Annotations>  
   </Database>  
</Databases>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[資料庫](../collections/databases-element-assl.md)|  
|子元素|[帳戶](../collections/accounts-element-assl.md)， [AggregationPrefix](../properties/aggregationprefix-element-assl.md)，[註解](../collections/annotations-element-assl.md)，[組件](../collections/assemblies-element-assl.md)，[定序](../properties/collation-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)， [Cube](../collections/cubes-element-assl.md)， [DatabasePermissions](../collections/databasepermissions-element-assl.md)， [DataSources](../collections/datasources-element-assl.md)， [DataSourceViews](../collections/datasourceviews-element-assl.md)，[描述](../properties/description-element-assl.md)，[維度](../collections/dimensions-element-assl.md)， [EstimatedSize](../properties/estimatedsize-element-assl.md)，[識別碼](../properties/id-element-assl.md)，[語言](../properties/language-element-assl.md)， [LastProcessed](../properties/lastprocessed-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)， [LastUpdate](../properties/lastupdate-element-assl.md)， [MasterDatasourceID](../properties/datasourceid-element-assl.md)， [MiningStructures](../collections/miningstructures-element-assl.md)，[名稱](../properties/name-element-assl.md)，[角色](../collections/roles-element-assl.md)，[狀態](../properties/state-element-assl.md)，[翻譯](../collections/translations-element-assl.md)，[可見](../properties/visible-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.Database>。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器項目&#40;ASSL&#41;](server-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
