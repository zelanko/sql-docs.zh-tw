---
title: "DSVTableBinding 資料類型 (ASSL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DSVTableBinding Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: DSVTableBinding
helpviewer_keywords: DSVTableBinding data type
ms.assetid: 149e753f-6218-4805-9223-7155b6827e64
caps.latest.revision: "41"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 235a6953404e1d421ea777fe3320fceeeae05f57
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="dsvtablebinding-data-type-assl"></a>DSVTableBinding 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定義代表資料表之間的繫結的衍生的資料類型和[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<DSVTableBinding>  
   <!-- The following elements extend TabularBinding -->  
   <DataSourceViewID>...</DataSourceViewID>  
   <TableID>...</TableID>  
</DSVTableBinding>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|描述|  
|--------------------|-----------------|  
|基底資料類型|[TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[DataSourceViewID](../../../analysis-services/scripting/properties/datasourceviewid-element-assl.md)， [TableID](../../../analysis-services/scripting/properties/tableid-element-assl.md)|  
|衍生的元素|請參閱[繫結](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 如需有關**繫結**型別，包括之 Analysis Services 指令碼語言 (ASSL) 物件的資料表**繫結**型別和繼承階層架構的**繫結**類型，請參閱[繫結](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)項目。  
  
 如需 ASSL 中資料繫結的概觀，請參閱[資料來源和繫結 &#40;SSAS 多維度 &#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.DSVTableBinding>。  
  
## <a name="see-also"></a>請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
