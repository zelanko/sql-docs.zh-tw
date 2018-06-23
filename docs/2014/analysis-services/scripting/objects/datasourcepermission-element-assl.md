---
title: DataSourcePermission 元素 (ASSL) |Microsoft 文件
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
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9ca326118ce782962b0100c310ddb308af91f21b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36034864"
---
# <a name="datasourcepermission-element-assl"></a>DataSourcePermission 元素 (ASSL)
  定義中的預設權限[DataSource](../data-type/datasource-data-type-assl.md)特定的資料型別[角色](role-element-assl.md)項目。  
  
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
  
  