---
title: "輸入元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Type Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.type
- http://schemas.microsoft.com/analysisservices/2003/engine#Type
- urn:schemas-microsoft-com:xml-analysis#Type
helpviewer_keywords:
- Type element
ms.assetid: 5d898123-a635-402a-be86-8249d7304fa4
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 40a6b965ed031572b956814e65f95198671af48b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="type-element-xmla"></a>Type 元素 (XMLA)
  決定要執行的處理類型[程序](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Process>  
...  
   <Type>...</Type>  
...  
</Process>  
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
|父元素|[處理](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如需有關可用處理選項物件的執行個體上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，請參閱[處理多維度模型 &#40;Analysis Services &#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md).  
  
 值**類型**元素僅限於一個下表所列的字串。  
  
|值|Description|  
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
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

