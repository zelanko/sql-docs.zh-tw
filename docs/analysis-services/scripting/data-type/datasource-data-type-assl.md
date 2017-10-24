---
title: "DataSource 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DataSource Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DataSource data type
ms.assetid: 05e8de8d-452d-4128-98a6-4437df227fec
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 07e642876743b47abd18f87313416613ed5d22b2
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="datasource-data-type-assl"></a>DataSource 資料類型 (ASSL)
  定義表示中的資料來源的抽象基本資料類型[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)項目。  
  
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
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|[RelationalDataSource](../../../analysis-services/scripting/data-type/relationaldatasource-data-type-assl.md)， [OlapDataSource](../../../analysis-services/scripting/data-type/olapdatasource-data-type-assl.md)， [PushedDataSource](../../../analysis-services/scripting/data-type/pusheddatasource-data-type-assl.md)|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [ConnectionString](../../../analysis-services/scripting/properties/connectionstring-element-assl.md)， [ConnectionStringSecurity](../../../analysis-services/scripting/properties/connectionstringsecurity-element-assl.md)， [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)， [DataSourcePermission](../../../analysis-services/scripting/collections/datasourcepermissions-element-assl.md)，[描述](../../../analysis-services/scripting/properties/description-element-assl.md)，[識別碼](../../../analysis-services/scripting/properties/id-element-assl.md)， [ImpersonationInfo](../../../analysis-services/scripting/properties/impersonationinfo-element-assl.md)，[隔離](../../../analysis-services/scripting/properties/isolation-element-assl.md)， [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)， [ManagedProvider](../../../analysis-services/scripting/properties/managedprovider-element-assl.md)， [MaxActiveConnections](../../../analysis-services/scripting/properties/maxactiveconnections-element-assl.md)，[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)，[逾時](../../../analysis-services/scripting/properties/timeout-element-assl.md)|  
|衍生的元素|無|  
  
## <a name="remarks"></a>備註  
 當定義-單行繫結，**名稱**是選擇性項目。 不需要指定**名稱**項目可讓 cube、 資料分割，以及其他繫結內部定義的資料來源。 所包含的資料來源的**資料庫**項目，**名稱**是必要項目。  
  
 如需資料來源的詳細資訊，請參閱 [多維度模型中的資料來源](../../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.DataSource>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

