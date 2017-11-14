---
title: "NullKeyConvertedToUnknown 元素 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- NullKeyConvertedToUnknown Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- NullKeyConvertedToUnknown
helpviewer_keywords:
- NullKeyConvertedToUnknown element
ms.assetid: 1a6cde33-01ba-4095-b464-16d1ad3c6905
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 77c93a56563f621d357943348cf436846f213068
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="nullkeyconvertedtounknown-element-assl"></a>NullKeyConvertedToUnknown 元素 (ASSL)
  指定遇到 Null 轉換錯誤時要採取的動作。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <NullKeyConvertedToUnknown>...</NullKeyConvertedToUnknown>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*IgnoreError*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 索引鍵資料行中遇到 null 值，並解譯為時，會發生 null 轉換錯誤**未知**成員。 不過，此錯誤時才會發生[NullProcessing](../../../analysis-services/scripting/properties/nullprocessing-element-assl.md)元素[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)的上階**ErrorConfiguration**父項目設定為*UnknownMember*。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|說明|  
|-----------|-----------------|  
|*IgnoreError*|處理時忽略錯誤並繼續。|  
|*ReportAndContinue*|處理時報告錯誤並繼續。|  
|*ReportAndStop*|處理時報告錯誤並停止。|  
  
 列舉型別對應至允許的值**NullKeyConvertedToUnknown**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ErrorOption>。  
  
## <a name="see-also"></a>另請參閱  
 [ErrorConfiguration 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)   
 [屬性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

