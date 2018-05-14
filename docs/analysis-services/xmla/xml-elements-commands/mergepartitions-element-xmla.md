---
title: MergePartitions 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3717dc967dbcb1f1523f2cc4efe535b928a663c3
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="mergepartitions-element-xmla"></a>MergePartitions 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  將一個或多個來源資料分割的資料合併至目標資料分割中，然後刪除來源資料分割。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Command>  
   <MergePartitions>  
      <Sources>...</Sources>  
      <Target>...</Target>  
   </MergePartitions>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[來源](../../../analysis-services/xmla/xml-elements-properties/sources-element-xmla.md)，[目標](../../../analysis-services/xmla/xml-elements-properties/target-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 所有物件參考中的**來源**和**目標**項目必須指向相同的量值群組中的不同資料分割。 否則，系統將發生錯誤。  
  
## <a name="see-also"></a>另請參閱  
 [命令 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
