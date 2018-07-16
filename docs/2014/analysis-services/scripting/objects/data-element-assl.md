---
title: 資料元素 (ASSL) |Microsoft Docs
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
- Data Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Data
helpviewer_keywords:
- Data element
ms.assetid: e52b1961-7e11-4029-8ab1-84d275845067
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8b31922593446e7d8aafd88cdb5667bef8b109ba
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37218278"
---
# <a name="data-element-assl"></a>Data 元素 (ASSL)
  包含 (集合中的子系[區塊項目&#40;ASSL&#41; ](block-element-assl.md)項目) 的二進位內容[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<File xsi:type="ClrAssemblyFile">  
   ...  
   <Data xsi:type="DataBlock">...</Data>  
   ...  
</ClrAssemblyFile>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[DataBlock](../data-type/datablock-data-type-assl.md)|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[檔案](file-element-assl.md)型別的[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素`Data`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.ClrAssemblyFile>。  
  
## <a name="see-also"></a>另請參閱  
 [Assembly 項目&#40;ASSL&#41;](assembly-element-assl.md)   
 [ClrAssembly 資料類型&#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [檔案項目&#40;ASSL&#41;](../collections/files-element-assl.md)   
 [封鎖項目&#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
