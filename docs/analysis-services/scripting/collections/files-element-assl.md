---
title: 檔案元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 658f2a556821f5560e7a20c650a621b744416357
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="files-element-assl"></a>Files 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含集合[檔案](../../../analysis-services/scripting/objects/file-element-assl.md)構成項目[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Assembly xsi:type="ClrAssembly">  
   ...  
   <Files>  
      <File xsi:type="ClrAssemblyFile">...</File>  
   </Files>  
   ...  
</Assembly>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[組件](../../../analysis-services/scripting/objects/assembly-element-assl.md)型別的[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)|  
|子元素|[檔案](../../../analysis-services/scripting/objects/file-element-assl.md)型別的[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.ClrAssemblyFileCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [Server 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [Database 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Assemblies 元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [資料元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/data-element-assl.md)   
 [DataBlock 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)   
 [Blocks 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/blocks-element-assl.md)   
 [Block 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/block-element-assl.md)   
 [ComAssembly 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)   
 [集合 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
