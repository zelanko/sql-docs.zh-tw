---
title: KeyNotFound 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- KeyNotFound Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- KeyNotFound
helpviewer_keywords:
- KeyNotFound element
ms.assetid: 2a93bbfa-2409-4e94-8b68-926532895a4c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7e8a2233797d3d9ddeecc91d5c2b5f096866d624
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48156598"
---
# <a name="keynotfound-element-assl"></a>KeyNotFound 元素 (ASSL)
  指定如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]遇到參考完整性錯誤時的回應。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ErrorConfiguration>  
   ...  
      <KeyNotFound>...</KeyNotFound>  
   ...  
</ErrorConfiguration>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|*ReportAndContinue*|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ErrorConfiguration](../objects/errorconfiguration-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 當相依資料表的外部索引鍵值在父資料表中沒有對應的項目時，就會發生參考完整性錯誤。 發生這個錯誤的情況包括：當 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 處理某個維度，其中事實資料表參考該維度之維度資料表中不存在的外部索引鍵值時，或者當 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 處理某個資料分割時，如果包含在此資料分割中之維度的維度主資料表參考另一個相關聯維度資料表中不存在的索引鍵值  (在具有父子式階層和父屬性之維度的情況中，如果包含在此資料分割中之維度的維度主資料表參考相同維度資料表中不存在的索引鍵值，也可能會發生這個錯誤)。  
  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|描述|  
|-----------|-----------------|  
|*IgnoreError*|處理時應該忽略錯誤並繼續。|  
|*ReportAndContinue*|處理時應該報告錯誤並繼續。|  
|*ReportAndStop*|處理時應該報告錯誤並停止。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `KeyNotFound` 允許值的列舉是 <xref:Microsoft.AnalysisServices.ErrorOption>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
