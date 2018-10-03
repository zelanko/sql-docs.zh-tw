---
title: 封鎖元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Blocks Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Blocks
helpviewer_keywords:
- Blocks element
ms.assetid: d6fd4e6b-b5bd-43cd-9c28-48af57cf977c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6b1030bf5efbfb86319d83a19913f58d834f85fc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082718"
---
# <a name="blocks-element-assl"></a>Blocks 元素 (ASSL)
  包含的二進位表示的二進位內容的資料區塊集合[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Data xsi:type="DataBlock">  
   ...  
   <Blocks>  
      <Block>...</Block>  
   </Blocks>  
   ...  
</File>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[資料](../objects/data-element-assl.md)型別的[DataBlock](../data-type/datablock-data-type-assl.md)|  
|子元素|[區塊](../objects/block-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素`Blocks`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.ClrAssemblyFile>。  
  
## <a name="see-also"></a>另請參閱  
 [Assembly 項目&#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [ClrAssembly 資料類型&#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [檔案項目&#40;ASSL&#41;](files-element-assl.md)   
 [檔案項目&#40;ASSL&#41;](../objects/file-element-assl.md)   
 [ClrAssemblyFile 資料類型&#40;ASSL&#41;](../data-type/clrassemblyfile-data-type-assl.md)   
 [資料元素&#40;ASSL&#41;](../objects/data-element-assl.md)   
 [DataBlock 資料類型&#40;ASSL&#41;](../data-type/datablock-data-type-assl.md)   
 [Blocks 元素](blocks-element-assl.md)   
 [封鎖項目&#40;ASSL&#41;](../objects/block-element-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
