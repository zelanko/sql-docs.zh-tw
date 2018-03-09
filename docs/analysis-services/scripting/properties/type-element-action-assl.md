---
title: "輸入元素 (Action) (ASSL) |Microsoft 文件"
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
apiname: Type Element (Action)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: TYPE
helpviewer_keywords: Type element
ms.assetid: 534cdf99-1edf-4490-9eaa-61f189a19434
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d7dffa090a3f8b24c08329f14f22881cf45d017b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="type-element-action-assl"></a>Type 元素 (Action) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含的型別[動作](../../../analysis-services/scripting/objects/action-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Action>  
   ...  
   <Type>...</Type>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[動作](../../../analysis-services/scripting/objects/action-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|*Url*|在網際網路瀏覽器中顯示變數網頁。|  
|*Html*|在網際網路瀏覽器中執行 HTML 指令碼。|  
|*陳述式*|執行 OLE DB 命令。|  
|*鑽研*|擷取鑽研的資料列集。<br /><br /> 此值就等於*資料列集*而且會識別鑽研動作。 它只能用在動作上其[TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md)值設定為*資料格*。|  
|*資料集*|擷取資料集。|  
|*資料列集*|擷取資料列集。|  
|*命令列*|在命令提示字元中執行命令。|  
|*專屬*|使用不同於先前此表列出的介面來執行作業。|  
|*報表*|在網際網路瀏覽器中顯示變數網頁。<br /><br /> 此值就等於*Url*而且會識別報表動作。|  
  
 對應目的父代的項目**類型**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>請參閱  
 [DrillThroughAction 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)   
 [ReportAction 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
