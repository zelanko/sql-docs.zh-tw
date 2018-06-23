---
title: 封鎖元素 (ASSL) |Microsoft 文件
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
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: bf944cc053e7a8c32efec50d10f6cc176942cce1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033353"
---
# <a name="blocks-element-assl"></a>Blocks 元素 (ASSL)
  包含代表的二進位內容的二進位資料區塊集合[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)項目。  
  
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
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[資料](../objects/data-element-assl.md)型別的[DataBlock](../data-type/datablock-data-type-assl.md)|  
|子元素|[區塊](../objects/block-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目`Blocks`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ClrAssemblyFile>。  
  
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
  
  