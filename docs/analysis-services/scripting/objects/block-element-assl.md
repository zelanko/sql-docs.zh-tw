---
title: 封鎖元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6eff6e6161525101b291e3c78d3aef466b7772a8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "34030609"
---
# <a name="block-element-assl"></a>Block 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含所有或部分二進位內容的[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Blocks>  
   <Block>...</Block>  
</Blocks>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|Base64Binary|  
|預設值|無|  
|基數|1-n：出現一次以上的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[區塊](../../../analysis-services/scripting/collections/blocks-element-assl.md)|  
|子元素|無|  
  
## <a name="see-also"></a>另請參閱  
 [組件元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)   
 [ClrAssembly 資料類型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [檔案項目&#40;ASSL&#41;](../../../analysis-services/scripting/collections/files-element-assl.md)   
 [File 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/file-element-assl.md)   
 [ClrAssemblyFile 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)   
 [資料元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/data-element-assl.md)   
 [DataBlock 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)   
 [物件 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
