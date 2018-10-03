---
title: Source 元素 (ComAssembly) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Source Element (ComAssembly)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Source
helpviewer_keywords:
- Source element
ms.assetid: 5c9209e8-ace6-4688-a64d-4987a7648ab9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b7c6259d5bec6c2c1e371df5d9412ccdbc5489a1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106508"
---
# <a name="source-element-comassembly-assl"></a>Source 元素 (ComAssembly) (ASSL)
  包含元件物件模型 (COM) 元件的檔案名稱或程式設計識別碼 (ProgID)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ComAssembly>  
   ...  
   <Source>...</Source>  
   ...  
</ComAssembly>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|String|  
|預設值|None|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ComAssembly](../data-type/assembly-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>備註  
 對應至父系的元素`Source`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.ComAssembly>。  
  
## <a name="see-also"></a>另請參閱  
 [Assembly 項目&#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [ClrAssembly 資料類型&#40;ASSL&#41;](../data-type/clrassembly-data-type-assl.md)   
 [Assemblies 元素&#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [資料庫項目&#40;ASSL&#41;](../objects/database-element-assl.md)   
 [伺服器項目&#40;ASSL&#41;](../objects/server-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
