---
title: Annotation 元素 (ASSL) |Microsoft 文件
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 882e3a5521a8f4359c770c7fba129418ec5620fa
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="annotation-element-assl"></a>Annotation 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含用來擴充「Analysis Services 指令碼語言」(ASSL) 結構描述的元素。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Annotations>  
   <Annotation>  
      <Name>...</Name>  
      <Visibility>...</Visibility>  
      <Value>...</Value>  
   </Annotation>  
</Annotations >  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[註解](../../../analysis-services/scripting/collections/annotations-element-assl.md)|  
|子元素|[名稱](../../../analysis-services/scripting/properties/name-element-assl.md)，[值](../../../analysis-services/scripting/properties/value-element-assl.md)，[可見性](../../../analysis-services/scripting/properties/visibility-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 **註解**項目會提供這些但單獨用來定義複雜的資料類型以外的所有物件之 ASSL 結構描述的擴充性。 **值**元素**註解**項目可以包含有效的 XML，從任何 XML 的命名空間以外 ASSL，受限於下列規則：  
  
-   XML 只能包含元素。  
  
-   每個元素都必須具有唯一的名稱。 建議的值**名稱**元素**註解**項目參考的目標命名空間。  
  
 若要允許的內容會加諸這些規則**註解**公開成名稱/值組的項目組透過其他介面，例如決策支援物件 (DSO)。  
  
 註解和空格**註解**無法保留未加上的子元素內的項目。 此外，所有元素都必須是可讀寫，因為唯讀的元素將會被忽略。  
  
 分析管理物件 (AMO) 物件模型中的對應元素是<xref:Microsoft.AnalysisServices.Annotation>。  
  
## <a name="see-also"></a>另請參閱  
 [物件 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
