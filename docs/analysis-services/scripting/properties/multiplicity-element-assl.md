---
title: Multiplicity 元素 (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2740e920332d55fd2826b8d91d6f7434d2f59e91
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
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
  
  
