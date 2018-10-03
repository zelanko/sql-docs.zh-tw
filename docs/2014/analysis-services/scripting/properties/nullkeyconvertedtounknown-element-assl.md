---
title: NullKeyConvertedToUnknown 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- NullKeyConvertedToUnknown Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NullKeyConvertedToUnknown
helpviewer_keywords:
- NullKeyConvertedToUnknown element
ms.assetid: 1a6cde33-01ba-4095-b464-16d1ad3c6905
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6aaf78e4081b0f2fe04bf9b4037639f5b86f5311
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48121718"
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*IgnoreError*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ErrorConfiguration](../objects/errorconfiguration-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 在索引鍵資料行中遇到 Null 值而且此值解譯為 `Unknown` 成員時，就會發生 Null 轉換錯誤。 不過，會發生這個錯誤，才[NullProcessing](nullprocessing-element-assl.md)項目[DataItem](../data-type/dataitem-data-type-assl.md)的上階`ErrorConfiguration`父項目設為*UnknownMember*。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*IgnoreError*|處理時忽略錯誤並繼續。|  
|*ReportAndContinue*|處理時報告錯誤並繼續。|  
|*ReportAndStop*|處理時報告錯誤並停止。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `NullKeyConvertedToUnknown` 允許值的列舉是 <xref:Microsoft.AnalysisServices.ErrorOption>。  
  
## <a name="see-also"></a>另請參閱  
 [ErrorConfiguration 元素&#40;ASSL&#41;](../objects/errorconfiguration-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
