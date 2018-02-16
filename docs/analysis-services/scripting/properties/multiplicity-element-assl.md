---
title: "Multiplicity 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 441e3829-9009-4b32-a8c6-fa580663387f
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9aa018ac9f692eac5de76743fb2d74c0d9832e56
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="multiplicity-element-assl"></a>Multiplicity 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
指出 RelationshipEnd 中的屬性位於關聯性的「一」端還是「多」端。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<RelationshipEnd>  
   ...  
   <Multiplicity>...</Multiplicity>  
   ...  
</RelationshipEnd>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值||  
|基數|1：只能出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[RelationshipEnd](../../../analysis-services/scripting/data-type/relationshipend-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*其中一個*|這是主索引鍵端。|  
|*許多*|這是外部索引鍵端。|  
  
 列舉型別對應至允許的值**角色**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Multiplicity>。  
  
  
