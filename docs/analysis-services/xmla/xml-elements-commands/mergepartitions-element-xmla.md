---
title: "MergePartitions 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: xmla
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: MergePartitions Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#MergePartitions
- microsoft.xml.analysis.mergepartitions
- urn:schemas-microsoft-com:xml-analysis#MergePartitions
helpviewer_keywords: MergePartitions command
ms.assetid: cf538189-0629-49b3-8e01-32afba7b020d
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cc2b0bd7644d9142124c54cef12909174c1cf723
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="mergepartitions-element-xmla"></a>MergePartitions 元素 (XMLA)
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
  
## <a name="see-also"></a>請參閱＜  
 [命令 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
