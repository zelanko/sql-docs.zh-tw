---
title: DataSourcePermission 元素 (ASSL) |Microsoft Docs
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
- DataSourcePermission Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- DataSourcePermission element
ms.assetid: 6dc6fb13-034e-479a-902e-27f3fb78c33f
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d88f18a752e96e5081462056d831bc968dc605df
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37241358"
---
# <a name="datasourcepermission-element-assl"></a>DataSourcePermission 元素 (ASSL)
  定義中的預設權限[DataSource](../data-type/datasource-data-type-assl.md)特定的資料類型[角色](role-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataSourcePermissions>  
   <DataSourcePermission xsi:type="Permission">  
      <!-- No child elements other than those from Permission are defined -->  
...</DataSourcePermission>  
</DataSourcePermissions>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[權限](../data-type/permission-data-type-assl.md)|  
|預設值|無|  
|基數|0-n：只能出現一次或出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[DataSourcePermissions](../collections/datasourcepermissions-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 `DataSourcePermission` 物件只能針對資料庫所擁有的角色存在，而且任何角色都只能存在一個 `DataSourcePermission` 物件。  
  
## <a name="see-also"></a>另請參閱  
 [Role 元素&#40;ASSL&#41;](role-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
