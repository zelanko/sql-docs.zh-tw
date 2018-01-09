---
title: "HideMemberIf 元素 (ASSL) |Microsoft 文件"
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
apiname: HideMemberIf Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: HideMemberIf
helpviewer_keywords: HideMemberIf element
ms.assetid: ff0e6b19-6216-43ac-ba76-1628da8c333b
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a5a53e8896e389b2b0cb4b478ef8a9e8ff9bd45a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="hidememberif-element-assl"></a>HideMemberIf 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]指出是否以及何時應向用戶端應用程式隱藏層級中的成員。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Level>  
   ...  
   <HideMemberIf>...</HideMemberIf>  
   ...  
</Level>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*永遠不會*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Level](../../../analysis-services/scripting/objects/level-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*永遠不會*|永不隱藏成員。|  
|*OnlyChildWithNoName*|當成員是其父系的唯一子系，而且其名稱為空白時，就會隱藏成員。|  
|*OnlyChildWithParentName*|當成員是父系的唯一子系，而且其名稱與其父系名稱完全相同時，就會隱藏成員。|  
|*NoName*|當成員名稱為空白時，就會隱藏成員。|  
|*ParentName*|當成員名稱與其父系名稱完全相同時，就會隱藏成員。|  
  
## <a name="remarks"></a>備註  
 列舉型別對應至允許的值**HideMemberIf**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.HideIfValue>。  
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
