---
title: DataBlock 資料類型 (ASSL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DataBlock Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DataBlock
helpviewer_keywords:
- DataBlock data type
ms.assetid: 4192b388-613a-472b-881c-f9c02215aa81
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7259e2a8cf26b79301004486b114ed95255f24db
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="datablock-data-type-assl"></a>DataBlock 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定義代表用來儲存的二進位內容資料區塊集合的基本資料類型[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DataBlock>  
   <Blocks>...</Blocks>  
</DataBlock>  
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
|子元素|[區塊](../../../analysis-services/scripting/collections/blocks-element-assl.md)|  
|衍生的元素|[資料](../../../analysis-services/scripting/objects/data-element-assl.md)元素[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)類型 ([檔案](../../../analysis-services/scripting/collections/files-element-assl.md)集合[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)類型)|  
  
## <a name="see-also"></a>請參閱  
 [組件元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)   
 [File 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/file-element-assl.md)   
 [Block 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/block-element-assl.md)   
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
