---
title: 輸入元素 (ClrAssemblyFile) (ASSL) |Microsoft Docs
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
- Type Element (ClrAssemblyFile)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: ab9e1e2c-ab06-4cd1-b007-16d738dc5604
caps.latest.revision: 38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 02a32dffab7d0274b98a5dcae3099703446b184b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37218018"
---
# <a name="type-element-clrassemblyfile-assl"></a>Type 元素 (ClrAssemblyFile) (ASSL)
  指定的其中一個屬於檔案的檔案類型[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 組件。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ClrAssemblyFile>  
      ...  
      <Type>...</Type>  
   ...  
</ClrAssemblyFile>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下列其中一個字串：  
  
|值|描述|  
|-----------|-----------------|  
|*Main*|指定的檔案是組件中的主要檔案。|  
|*相依*|指定的檔案是組件中的相依檔案。|  
|*偵錯*|指定的檔案包含偵錯資訊。|  
  
 在「分析管理物件」(AMO) 物件模型中對應至 `Type` 允許值的列舉是 <xref:Microsoft.AnalysisServices.ClrAssemblyFileType>。  
  
 對應至父系的元素`Type`在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.ClrAssemblyFile>。  
  
## <a name="see-also"></a>另請參閱  
 [檔案項目&#40;ASSL&#41;](../objects/file-element-assl.md)   
 [檔案項目&#40;ASSL&#41;](../collections/files-element-assl.md)   
 [ClrAssembly 資料類型&#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [Assembly 項目&#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [Assemblies 元素&#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [屬性&#40;ASSL&#41;](properties-assl.md)  
  
  
