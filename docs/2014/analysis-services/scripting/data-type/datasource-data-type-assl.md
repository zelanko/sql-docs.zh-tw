---
title: DataSource 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DataSource Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DataSource data type
ms.assetid: 05e8de8d-452d-4128-98a6-4437df227fec
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b498ddc2dcfb4ef2a93d1da98401b4e0c57bdfa7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37273364"
---
# <a name="datasource-data-type-assl"></a>DataSource 資料類型 (ASSL)
  定義表示中的資料來源的抽象基本資料類型[資料庫](../objects/database-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataSource>  
   <Name>...</Name>  
   <ID>...</ID>  
   <CreatedTimestamp>...</CreateTimestamp>  
   <LastSchemaUpdate>...</LastSchemaUpdate>  
   <ManagedProvider>...</ManagedProvider>  
   <ConnectionString>...</ConnectionString>  
   <ConnectionStringSecurity>...</ConnectionStringSecurity>  
   <ImpersonationInfo>...</ImpersonationInfo>  
   <Isolation>...</Isolation>  
   <MaxActiveConnections>...</MaxActiveConnections>  
   <Description>...</Description>  
   <Timeout>...</Timeout>  
   <Annotations>...</Annotations>  
   <DataSourcePermission>...</DataSourcePermission>  
</DataSource>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|[RelationalDataSource](datasource-data-type-assl.md)， [OlapDataSource](olapdatasource-data-type-assl.md)， [PushedDataSource](pusheddatasource-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[註釋](../collections/annotations-element-assl.md)， [ConnectionString](../properties/connectionstring-element-assl.md)， [ConnectionStringSecurity](../properties/connectionstringsecurity-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)， [DataSourcePermission](../collections/datasourcepermissions-element-assl.md)，[描述](../properties/description-element-assl.md)，[識別碼](../properties/id-element-assl.md)， [ImpersonationInfo](../properties/impersonationinfo-element-assl.md)，[隔離](../properties/isolation-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)， [ManagedProvider](../properties/managedprovider-element-assl.md)， [MaxActiveConnections](../properties/maxactiveconnections-element-assl.md)，[名稱](../properties/name-element-assl.md)，[逾時](../properties/timeout-element-assl.md)|  
|衍生的元素|無|  
  
## <a name="remarks"></a>備註  
 定義非正規 (out-of-line) 繫結時，`Name` 元素是選擇性的。 不需要指定 `Name` 元素的做法可讓您在 Cube、資料分割等項目的繫結內部定義資料來源。 若為 `Database` 元素所包含的資料來源，`Name` 就是必要的元素。  
  
 如需資料來源的詳細資訊，請參閱 [多維度模型中的資料來源](../../multidimensional-models/data-sources-in-multidimensional-models.md)。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.DataSource>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
