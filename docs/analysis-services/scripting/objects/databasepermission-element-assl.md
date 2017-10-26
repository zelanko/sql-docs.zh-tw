---
title: "DatabasePermission 元素 (ASSL) |Microsoft 文件"
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
- DatabasePermission Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DatabasePermission
helpviewer_keywords:
- DatabasePermission element
ms.assetid: 6dcb9136-a40d-42e3-ad3b-b8ce8c7ca78c
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b33711fc326cf8256cc9c641c047c90a1686505a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="databasepermission-element-assl"></a>DatabasePermission 元素 (ASSL)
  定義中的預設權限[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)特定的項目[角色](../../../analysis-services/scripting/objects/role-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DatabasePermissions>  
      <DatabasePermission xsi:type="Permission">  
      <!-- The following elements extend Permission -->  
      <Administer>...</Administer>  
...</DatabasePermission>  
</DatabasePermissions>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|[權限](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|預設值|False|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DatabasePermissions](../../../analysis-services/scripting/collections/databasepermissions-element-assl.md)|  
|子元素|[管理](../../../analysis-services/scripting/properties/administer-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 **DatabasePermission** 物件只能針對資料庫所擁有的角色存在，而且任何角色都只能存在一個 **DatabasePermission** 物件。  
  
 此元素在 DeploymentMode 值 2 (表格式模型) 下，擁有下列驗證。  
  
-   除非使用者具有系統管理權限，否則*Administer* 屬性預設值設為 **False**。 使用者若是具有系統管理權限，屬性值會設為 **True**。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.DatabasePermission>。  
  
## <a name="see-also"></a>另請參閱  
 [Role 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

