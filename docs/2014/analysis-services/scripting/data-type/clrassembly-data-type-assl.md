---
title: ClrAssembly 資料類型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ClrAssembly Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ClrAssembly
helpviewer_keywords:
- ClrAssembly data type
ms.assetid: 3f5dc5a1-ebd6-41b8-ac04-91d4de137eb4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a9171832bac6653e7c1d86915ae006c65022668a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48159248"
---
# <a name="clrassembly-data-type-assl"></a>ClrAssembly 資料類型 (ASSL)
  定義衍生的資料類型，表示[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]相關聯的組件[資料庫](../objects/database-element-assl.md)或是[Server](../objects/server-element-assl.md)項目  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ClrAssembly>  
      <!-- The following elements extend Assembly -->  
   <Files>...</Files>  
      <PermissionSet>...</PermissionSet>  
</ClrAssembly>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[組件](../objects/assembly-element-assl.md)|  
|衍生資料類型|None|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無 (抽象類型)|  
|子元素|[檔案](../collections/files-element-assl.md)， [PermissionSet](../properties/permissionset-element-assl.md)|  
|衍生的元素|請參閱[組件](../objects/assembly-element-assl.md)([組件](../collections/assemblies-element-assl.md)集合[資料庫](../objects/database-element-assl.md)或是[Server](../objects/server-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 `ClrAssembly`項目包含重新建立所需的檔案[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]組件，相關聯的執行個體[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]或與特定資料庫的執行個體上[!INCLUDE[ssAS](../../../includes/ssas-md.md)]，以及執行組件所需的權限。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.ClrAssembly>。  
  
## <a name="see-also"></a>另請參閱  
 [檔案項目&#40;ASSL&#41;](../objects/file-element-assl.md)   
 [ClrAssemblyFile 資料類型&#40;ASSL&#41;](clrassemblyfile-data-type-assl.md)   
 [資料元素&#40;ASSL&#41;](../objects/data-element-assl.md)   
 [DataBlock 資料類型&#40;ASSL&#41;](datablock-data-type-assl.md)   
 [封鎖項目&#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [封鎖項目&#40;ASSL&#41;](../objects/block-element-assl.md)   
 [ComAssembly 資料類型&#40;ASSL&#41;](assembly-data-type-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
