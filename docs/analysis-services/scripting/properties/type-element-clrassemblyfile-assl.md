---
title: 輸入元素 (ClrAssemblyFile) (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a4cf5d0a1ef4fd627dd10d0b73ca1520980484fe
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="type-element-clrassemblyfile-assl"></a>Type 元素 (ClrAssemblyFile) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下列其中一個字串：  
  
|Value|Description|  
|-----------|-----------------|  
|*Main*|指定的檔案是組件中的主要檔案。|  
|*相依*|指定的檔案是組件中的相依檔案。|  
|*偵錯*|指定的檔案包含偵錯資訊。|  
  
 列舉型別對應至允許的值**類型**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ClrAssemblyFileType>。  
  
 對應目的父代的項目**類型**在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ClrAssemblyFile>。  
  
## <a name="see-also"></a>另請參閱  
 [File 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/file-element-assl.md)   
 [檔案項目&#40;ASSL&#41;](../../../analysis-services/scripting/collections/files-element-assl.md)   
 [ClrAssembly 資料類型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [組件元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)   
 [Assemblies 元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
