---
title: 輸入元素 (Action) (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a82395be70c699da6fc96d3661aa71254e185883
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="type-element-action-assl"></a>Type 元素 (Action) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含的型別[動作](../../../analysis-services/scripting/objects/action-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Action>  
   ...  
   <Type>...</Type>  
   ...  
</Action>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
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
  
|值|Description|  
|-----------|-----------------|  
|*Url*|在網際網路瀏覽器中顯示變數網頁。|  
|*Html*|在網際網路瀏覽器中執行 HTML 指令碼。|  
|*Statement*|執行 OLE DB 命令。|  
|*鑽研*|擷取鑽研的資料列集。<br /><br /> 此值就等於*資料列集*而且會識別鑽研動作。 它只能用在動作上其[TargetType](../../../analysis-services/scripting/properties/targettype-element-assl.md)值設定為*資料格*。|  
|*資料集*|擷取資料集。|  
|*Rowset*|擷取資料列集。|  
|*命令列*|在命令提示字元中執行命令。|  
|*專屬*|使用不同於先前此表列出的介面來執行作業。|  
|*報表*|在網際網路瀏覽器中顯示變數網頁。<br /><br /> 此值就等於*Url*而且會識別報表動作。|  
  
 對應目的父代的項目**類型**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另請參閱  
 [DrillThroughAction 資料類型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)   
 [ReportAction 資料類型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
