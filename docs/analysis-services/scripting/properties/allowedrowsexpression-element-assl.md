---
title: AllowedRowsExpression 元素 (ASSL) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7bca46eeaafa4f0e028b08d9f70903f1e6e84b9f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="allowedrowsexpression-element-assl"></a>AllowedRowsExpression 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含定義父元素內容之布林類型的資料分析運算式 (DAX)。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CellPermission> <!-- or StandardAction -->  
   ...  
   <Expression>...</Expression>  
   ...  
</CellPermission>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CellPermission](../../../analysis-services/scripting/objects/cellpermission-element-assl.md)， [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 如**CellPermission**項目，**運算式**元素包含邏輯 MDX 運算式來識別適用於所指定的權限的資料格[存取](../../../analysis-services/scripting/properties/access-element-assl.md)項目**CellPermission**項目。 如果值**運算式**元素**CellPermission**元素是空的**CellPermission**項目會被忽略。  
  
 如**StandardAction**項目，**運算式**元素包含 MDX 運算式，表示動作的內容。 如果值**運算式**元素**StandardAction**元素是空的**StandardAction**項目會被忽略。  
  
 在「分析管理物件」(AMO) 物件模型中對應至父系的元素是 <xref:Microsoft.AnalysisServices.CellPermission> 和 <xref:Microsoft.AnalysisServices.StandardAction>。  
  
## <a name="see-also"></a>另請參閱  
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
