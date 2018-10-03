---
title: Roles 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Roles Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Roles
helpviewer_keywords:
- Roles element
ms.assetid: 4191b7ce-bae4-4200-8550-3904420efafd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 33af9f6cb9ff1d85bdd9de200b66cfb0784fa432
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168168"
---
# <a name="roles-element-assl"></a>Roles 元素 (ASSL)
  包含在父元素底下定義之 [Role](../objects/role-element-assl.md) 元素的集合。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Database> <!-- or Server -->  
   ...  
   <Roles>  
      <Role>...</Role>  
   </Roles>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Database](../objects/database-element-assl.md)、 [Server](../objects/server-element-assl.md)|  
|子元素|[角色](../objects/role-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 與 `Roles` 元素相關聯的 `Server` 元素僅包含一個名為 Administrators 的角色，它代表伺服器管理員角色。 您無法變更或刪除此伺服器管理員角色，也無法在集合中加入其他角色。  
  
 與 `Roles` 元素相關聯的 `Database` 元素包含針對該資料庫定義的角色。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.RoleCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
