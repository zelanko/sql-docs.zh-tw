---
title: DatabasePermission 元素 (ASSL) |Microsoft Docs
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
- DatabasePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DatabasePermission
helpviewer_keywords:
- DatabasePermission element
ms.assetid: 6dcb9136-a40d-42e3-ad3b-b8ce8c7ca78c
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0fbfd9544e5305169e0d25b1b0157197d39cc002
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37259524"
---
# <a name="databasepermission-element-assl"></a>DatabasePermission 元素 (ASSL)
  定義中的預設權限[資料庫](database-element-assl.md)特定的項目[角色](role-element-assl.md)項目。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[權限](../data-type/permission-data-type-assl.md)|  
|預設值|False|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DatabasePermissions](../collections/databasepermissions-element-assl.md)|  
|子元素|[管理](../properties/administer-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 `DatabasePermission` 物件只能針對資料庫所擁有的角色存在，而且任何角色都只能存在一個 `DatabasePermission` 物件。  
  
 此元素在 DeploymentMode 值 2 (表格式模型) 下，擁有下列驗證。  
  
-   *管理*屬性預設值設為`False`，除非使用者具有系統管理權限。 使用者若是具有系統管理權限，屬性值會設為 `True`。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.DatabasePermission>。  
  
## <a name="see-also"></a>另請參閱  
 [Role 元素&#40;ASSL&#41;](role-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
