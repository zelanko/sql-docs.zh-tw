---
title: "Roles 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Roles Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Roles
helpviewer_keywords: Roles element
ms.assetid: 4191b7ce-bae4-4200-8550-3904420efafd
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4d125df9535303152449ad54ef577995a1da9b6d
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/08/2017
---
# <a name="roles-element-assl"></a>Roles 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含集合[角色](../../../analysis-services/scripting/objects/role-element-assl.md)父元素底下定義的項目。  
  
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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Database](../../../analysis-services/scripting/objects/database-element-assl.md)、 [Server](../../../analysis-services/scripting/objects/server-element-assl.md)|  
|子元素|[角色](../../../analysis-services/scripting/objects/role-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 與 **Server** 元素相關聯的 **Roles** 元素僅包含一個名為 Administrators 的角色，它代表伺服器管理員角色。 您無法變更或刪除此伺服器管理員角色，也無法在集合中加入其他角色。  
  
 與 **Database** 元素相關聯的 **Roles** 元素包含針對該資料庫定義的角色。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.RoleCollection>。  
  
## <a name="see-also"></a>請參閱  
 [集合 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
