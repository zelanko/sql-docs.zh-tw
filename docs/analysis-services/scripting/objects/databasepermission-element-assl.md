---
title: DatabasePermission 元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 855c632b78beb3a5ba75ff7acf31b72fff229e95
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34035169"
---
# <a name="databasepermission-element-assl"></a>DatabasePermission 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [Role 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [物件 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
