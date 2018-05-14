---
title: 輸入元素 (Binding) (ASSL) |Microsoft 文件
ms.date: 5/8/2018
ms.prod: sql
ms.custom: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6f125c950c65f34c139e3b98ad4ca59b392ed2b9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="type-element-binding-assl"></a>Type 元素 (Binding) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含屬性繫結的類型。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<AttributeBinding> <!-- or CubeAttributeBinding -->  
   ...  
   <Type>...</Type>  
   ...  
</AttributeBinding>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|字串 (列舉)|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md)， [CubeAttributeBinding](../../../analysis-services/scripting/data-type/cubeattributebinding-data-type-assl.md)|  
|子元素|無|  
  
## <a name="remarks"></a>備註  
 這個元素的值限制為下表所列的其中一個字串。  
  
|值|Description|  
|-----------|-----------------|  
|*全部*|所有層級|  
|*索引鍵*|成員索引鍵|  
|*名稱*|成員名稱|  
|*值*|成員值|  
|*轉譯*|成員翻譯|  
|*UnaryOperator*|一元運算子|  
|*SkippedLevels*|略過的層級|  
|*CustomRollup*|自訂積存公式|  
|*CustomRollupProperties*|自訂積存屬性|  
  
 對應至父系的項目**類型**在 「 分析管理物件 (AMO) 物件模型是<xref:Microsoft.AnalysisServices.AttributeBinding>和<xref:Microsoft.AnalysisServices.CubeAttributeBinding>。  
  
## <a name="see-also"></a>另請參閱  
 [繫結資料類型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)   
 [屬性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
