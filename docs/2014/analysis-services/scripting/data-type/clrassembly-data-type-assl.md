---
title: ClrAssembly 資料類型 (ASSL) |Microsoft 文件
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
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e17992a5d15113ec0de5dd75978f932cb83d11c8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36033362"
---
# <a name="clrassembly-data-type-assl"></a>ClrAssembly 資料類型 (ASSL)
  定義衍生的資料類型，表示[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]與相關聯的組件[資料庫](../objects/database-element-assl.md)或[伺服器](../objects/server-element-assl.md)項目  
  
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
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無 (抽象類型)|  
|子元素|[檔案](../collections/files-element-assl.md)，[使用權限集合](../properties/permissionset-element-assl.md)|  
|衍生的元素|請參閱[組件](../objects/assembly-element-assl.md)([組件](../collections/assemblies-element-assl.md)集合[資料庫](../objects/database-element-assl.md)或[伺服器](../objects/server-element-assl.md))|  
  
## <a name="remarks"></a>備註  
 `ClrAssembly`元素包含重新建立所需的檔案[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]組件，相關聯的執行個體與[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]或具有特定資料庫執行個體上[!INCLUDE[ssAS](../../../includes/ssas-md.md)]，以及執行組件所需的權限。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.ClrAssembly>。  
  
## <a name="see-also"></a>另請參閱  
 [檔案項目&#40;ASSL&#41;](../objects/file-element-assl.md)   
 [ClrAssemblyFile 資料類型&#40;ASSL&#41;](clrassemblyfile-data-type-assl.md)   
 [資料元素&#40;ASSL&#41;](../objects/data-element-assl.md)   
 [DataBlock 資料類型&#40;ASSL&#41;](datablock-data-type-assl.md)   
 [封鎖項目&#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [封鎖項目&#40;ASSL&#41;](../objects/block-element-assl.md)   
 [ComAssembly 資料類型&#40;ASSL&#41;](assembly-data-type-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  