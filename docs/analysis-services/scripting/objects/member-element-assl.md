---
title: "Member 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Member Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Member
helpviewer_keywords: Member element
ms.assetid: 03b4cfcb-ce87-452f-9e25-8745c0423f56
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2aff86cc4c63ffd23a2f1385007d1e397d1d1e28
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="member-element-assl"></a>Member 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含的成員名稱[群組](../../../analysis-services/scripting/objects/group-element-assl.md)項目或[角色](../../../analysis-services/scripting/objects/role-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Members>  
   <Member>  
      <Name>...</Name>  
   </Member>  
</Members>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[成員](../../../analysis-services/scripting/collections/members-element-assl.md)|  
|子元素|[[名稱]](../../../analysis-services/scripting/properties/name-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 對應至父系的項目**成員**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Group>和<xref:Microsoft.AnalysisServices.Role>。  
  
## <a name="see-also"></a>請參閱  
 [物件 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
