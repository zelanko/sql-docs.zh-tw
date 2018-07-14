---
title: 輸入元素 (Action) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Type Element (Action)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: 534cdf99-1edf-4490-9eaa-61f189a19434
caps.latest.revision: 35
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 99147acb4b2a1b467913087f4e4df14469de9a03
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249079"
---
# <a name="type-element-action-assl"></a>Type 元素 (Action) (ASSL)
  包含的型別[動作](../objects/action-element-assl.md)項目。  
  
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
|父元素|[動作](../objects/action-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*Url*|在網際網路瀏覽器中顯示變數網頁。|  
|*Html*|在網際網路瀏覽器中執行 HTML 指令碼。|  
|*陳述式*|執行 OLE DB 命令。|  
|*鑽研*|擷取鑽研的資料列集。<br /><br /> 這個值等於*資料列集*而且會識別鑽研動作。 它只能用在動作上其[TargetType](targettype-element-assl.md)值設定為*資料格*。|  
|*資料集*|擷取資料集。|  
|*Rowset*|擷取資料列集。|  
|*命令列*|在命令提示字元中執行命令。|  
|*專屬*|使用不同於先前此表列出的介面來執行作業。|  
|*報表*|在網際網路瀏覽器中顯示變數網頁。<br /><br /> 這個值等於*Url*而且會識別報表動作。|  
  
 對應至父系的元素`Type`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.Action>。  
  
## <a name="see-also"></a>另請參閱  
 [DrillThroughAction 資料類型&#40;ASSL&#41;](../data-type/action-data-type-assl.md)   
 [ReportAction 資料類型&#40;ASSL&#41;](../data-type/reportaction-data-type-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
