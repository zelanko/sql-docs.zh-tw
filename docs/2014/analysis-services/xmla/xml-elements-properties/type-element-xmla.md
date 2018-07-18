---
title: 輸入元素 (XMLA) |Microsoft Docs
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
- Type Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.type
- http://schemas.microsoft.com/analysisservices/2003/engine#Type
- urn:schemas-microsoft-com:xml-analysis#Type
helpviewer_keywords:
- Type element
ms.assetid: 5d898123-a635-402a-be86-8249d7304fa4
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 336266b8290f1a4eb10d200d8c1c31bf00f96879
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37193778"
---
# <a name="type-element-xmla"></a>Type 元素 (XMLA)
  決定要執行的處理類型[程序](../xml-elements-commands/process-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Process>  
...  
   <Type>...</Type>  
...  
</Process>  
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
|父元素|[處理](../xml-elements-commands/process-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如需有關可用處理選項物件的執行個體上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，請參閱[多維度模型物件處理](../../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
 `Type` 元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*ProcessFull*|卸除受影響物件中的所有資料，然後處理受影響的物件。|  
|*ProcessAdd*|將新的資料加入至受影響的物件。|  
|*ProcessUpdate*|重新整理受影響物件中的資料。|  
|*ProcessIndexes*|在受影響的物件中建立或重建索引和彙總。|  
|*ProcessScriptCache*|如果此 Cube 已經過處理，伺服器將重建 MDX 指令碼快取。 如果沒有，就會引發錯誤。<br /><br /> **請注意**只適用於 cube。|  
|*ProcessData*|只處理受影響物件中的資料。|  
|*ProcessDefault*|偵測受影響物件的狀態，然後針對受影響的物件執行適當的處理選項，以便完整最佳化此物件並讓它返回完整處理狀態。|  
|*ProcessClear*|卸除受影響物件與所有相關物件中的資料。|  
|*ProcessStructure*|只處理受影響物件的結構。|  
|*ProcessClearStructureOnly*|只清除受影響物件中的資料。|  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
