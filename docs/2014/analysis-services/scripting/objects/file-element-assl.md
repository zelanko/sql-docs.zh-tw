---
title: 檔案元素 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- File Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- File
helpviewer_keywords:
- File element
ms.assetid: 21c70707-d2f8-4040-9acb-cbce23076bcc
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 645882666ba82f965fddff9e1c886e97ff092a90
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031503"
---
# <a name="file-element-assl"></a>File 元素 (ASSL)
  撰寫的檔案會定義[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] [ClrAssembly](../data-type/assembly-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Files>  
   <File xsi:type="ClrAssemblyFile">...</File>  
</Files>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
|預設值|無|  
|基數|1-n：出現一次以上的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[檔案](../collections/files-element-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 對應目的父代的項目`Files`在 「 分析管理物件 (AMO) 物件模型而言， <xref:Microsoft.AnalysisServices.ClrAssemblyFile>。  
  
## <a name="see-also"></a>另請參閱  
 [Server 元素&#40;ASSL&#41;](server-element-assl.md)   
 [Database 元素&#40;ASSL&#41;](database-element-assl.md)   
 [Assemblies 元素&#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [Assembly 項目&#40;ASSL&#41;](assembly-element-assl.md)   
 [ClrAssembly 資料類型&#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [資料元素&#40;ASSL&#41;](data-element-assl.md)   
 [DataBlock 資料類型&#40;ASSL&#41;](../data-type/datablock-data-type-assl.md)   
 [封鎖項目&#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [封鎖項目&#40;ASSL&#41;](block-element-assl.md)   
 [ComAssembly 資料類型&#40;ASSL&#41;](../data-type/comassembly-data-type-assl.md)   
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  