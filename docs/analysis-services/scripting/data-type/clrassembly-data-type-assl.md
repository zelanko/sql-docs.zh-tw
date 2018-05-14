---
title: ClrAssembly 資料類型 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f6fb3493fc7add4ece9ef2d5acacd772d5911ebd
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="clrassembly-data-type-assl"></a>ClrAssembly 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義衍生的資料類型，表示[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]與相關聯的組件[資料庫](../../../analysis-services/scripting/objects/database-element-assl.md)或[伺服器](../../../analysis-services/scripting/objects/server-element-assl.md)項目  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ClrAssembly>  
      <!-- The following elements extend Assembly -->  
   <Files>...</Files>  
      <PermissionSet>...</PermissionSet>  
</ClrAssembly>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|[組件](../../../analysis-services/scripting/objects/assembly-element-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無 (抽象類型)|  
|子元素|[檔案](../../../analysis-services/scripting/collections/files-element-assl.md)，[使用權限集合](../../../analysis-services/scripting/properties/permissionset-element-assl.md)|  
|衍生的元素|請參閱＜ [Assembly](../../../analysis-services/scripting/objects/assembly-element-assl.md) ([Database](../../../analysis-services/scripting/collections/assemblies-element-assl.md) 或 [Server](../../../analysis-services/scripting/objects/database-element-assl.md) 的 [Assemblies](../../../analysis-services/scripting/objects/server-element-assl.md)集合)＞|  
  
## <a name="remarks"></a>備註  
 **ClrAssembly**元素包含重新建立所需的檔案[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]組件，相關聯的執行個體與[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]或的執行個體上的特定資料庫[!INCLUDE[ssAS](../../../includes/ssas-md.md)]，以及執行該組件所需的權限。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.ClrAssembly>。  
  
## <a name="see-also"></a>另請參閱  
 [File 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/file-element-assl.md)   
 [ClrAssemblyFile 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)   
 [資料元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/data-element-assl.md)   
 [DataBlock 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)   
 [Blocks 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/blocks-element-assl.md)   
 [Block 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/block-element-assl.md)   
 [ComAssembly 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
