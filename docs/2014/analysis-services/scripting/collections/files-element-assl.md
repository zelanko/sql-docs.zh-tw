---
title: 檔案元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Files Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Files
helpviewer_keywords:
- Files element
ms.assetid: 8a1327cb-1f60-42a7-b8ef-213d45a63e55
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 91fd214a87ea266a1c5849211bd30237b4313b20
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48078618"
---
# <a name="files-element-assl"></a>Files 元素 (ASSL)
  包含的集合[檔案](../objects/file-element-assl.md)構成項目[ClrAssembly](../data-type/assembly-data-type-assl.md)項目。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[組件](../objects/assembly-element-assl.md)型別的[ClrAssembly](../data-type/assembly-data-type-assl.md)|  
|子元素|[檔案](../objects/file-element-assl.md)型別的[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.ClrAssemblyFileCollection>。  
  
## <a name="see-also"></a>另請參閱  
 [伺服器項目&#40;ASSL&#41;](../objects/server-element-assl.md)   
 [資料庫項目&#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Assemblies 元素&#40;ASSL&#41;](assemblies-element-assl.md)   
 [資料元素&#40;ASSL&#41;](../objects/data-element-assl.md)   
 [DataBlock 資料類型&#40;ASSL&#41;](../data-type/datablock-data-type-assl.md)   
 [封鎖項目&#40;ASSL&#41;](blocks-element-assl.md)   
 [封鎖項目&#40;ASSL&#41;](../objects/block-element-assl.md)   
 [ComAssembly 資料類型&#40;ASSL&#41;](../data-type/comassembly-data-type-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
