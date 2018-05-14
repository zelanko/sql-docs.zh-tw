---
title: UserDefinedGroupBinding 資料類型 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 77f5e9e1aa2d097211645e4e1583a8f5c9478e78
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="userdefinedgroupbinding-data-type-assl"></a>UserDefinedGroupBinding 資料類型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定義代表某個屬性之使用者定義群組的衍生資料類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<UserDefinedGroupBinding>  
   <!-- The following elements extend Binding -->  
      <AttributeID>...</AttributeID>  
      <Groups>...</Groups>  
</UserDefinedGroupBinding>  
```  
  
## <a name="data-type-characteristics"></a>資料類型特性  
  
|特性|說明|  
|--------------------|-----------------|  
|基底資料類型|[繫結](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|衍生資料類型|無|  
  
## <a name="data-type-relationships"></a>資料類型關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|無|  
|子元素|[AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md)，[群組](../../../analysis-services/scripting/collections/groups-element-assl.md)|  
|衍生的元素|請參閱[繫結](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>備註  
 **UserDefinedGroupBinding**可自動視為[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)、 其[類型](../../../analysis-services/scripting/properties/type-element-binding-assl.md)元素設定為*所有*。  
  
 如需有關**繫結**型別，包括之 Analysis Services 指令碼語言 (ASSL) 物件的資料表**繫結**型別和繼承階層架構的**繫結**類型，請參閱[繫結資料型別&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)。  
  
 如需 ASSL 中資料繫結的概觀，請參閱[資料來源和繫結 & #40;SSAS 多維度 & #41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.UserDefinedGroupBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言 XML 資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
