---
title: 輸入元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ca05cb4bc5ea8951db028ed4da53ee3bfd7131dc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="type-element-xmla"></a>Type 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
 如需有關可用處理選項物件的執行個體上[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，請參閱[處理多維度模型&#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)。  
  
 值**類型**元素僅限於一個下表所列的字串。  
  
|Value|描述|  
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
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
