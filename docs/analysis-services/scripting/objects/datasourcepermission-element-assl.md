---
title: "DataSourcePermission 元素 (ASSL) |Microsoft 文件"
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
- DataSourcePermission Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DataSourcePermission element
ms.assetid: 6dc6fb13-034e-479a-902e-27f3fb78c33f
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fd41a100589e86a889698253bbb5f256b3bc788b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="datasourcepermission-element-assl"></a>DataSourcePermission 元素 (ASSL)
  定義中的預設權限[DataSource](../../../analysis-services/scripting/data-type/datasource-data-type-assl.md)特定的資料型別[角色](../../../analysis-services/scripting/objects/role-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataSourcePermissions>  
   <DataSourcePermission xsi:type="Permission">  
      <!-- No child elements other than those from Permission are defined -->  
...</DataSourcePermission>  
</DataSourcePermissions>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|[權限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|預設值|無|  
|基數|0-n：只能出現一次或出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DataSourcePermissions](../../../analysis-services/scripting/collections/datasourcepermissions-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 **DataSourcePermission** 物件只能針對資料庫所擁有的角色存在，而且任何角色都只能存在一個 **DataSourcePermission** 物件。  
  
## <a name="see-also"></a>另請參閱  
 [Role 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

