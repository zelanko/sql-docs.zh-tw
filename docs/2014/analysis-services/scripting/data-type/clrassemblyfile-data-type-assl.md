---
title: ClrAssemblyFile 資料類型 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ClrAssemblyFile Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ClrAssemblyFile
helpviewer_keywords:
- ClrAssemblyFile data type
ms.assetid: 91074677-c149-483b-a56d-0e35d959d9eb
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b542c4193d80fa80cc9aed6663f41e102266000b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030893"
---
# <a name="clrassemblyfile-data-type-assl"></a>ClrAssemblyFile 資料類型 (ASSL)
  定義代表其中一個檔案組成的基本資料類型[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] `Assembly` ([ClrAssembly](assembly-data-type-assl.md)項目)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ClrAssemblyFile>  
   <Name>...</Name>  
      <Type>...</Type>  
      <Data>...</Data>  
</ClrAssemblyFile>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|無|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[資料](../objects/data-element-assl.md)，[名稱](../properties/name-element-assl.md)，[類型](../properties/type-element-clrassemblyfile-assl.md)|  
|衍生的元素|[檔案](../objects/file-element-assl.md)([檔案](../collections/files-element-assl.md)集合[ClrAssembly](assembly-data-type-assl.md))|  
  
## <a name="remarks"></a>備註  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.ClrAssemblyFile>。  
  
## <a name="see-also"></a>另請參閱  
 [Server 元素&#40;ASSL&#41;](../objects/server-element-assl.md)   
 [Database 元素&#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Assemblies 元素&#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [Assembly 項目&#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [DataBlock 資料類型&#40;ASSL&#41;](datablock-data-type-assl.md)   
 [封鎖項目&#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [封鎖項目&#40;ASSL&#41;](../objects/block-element-assl.md)   
 [ComAssembly 資料類型&#40;ASSL&#41;](comassembly-data-type-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  