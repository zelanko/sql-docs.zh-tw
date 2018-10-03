---
title: Annotation 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Annotation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Annotation
helpviewer_keywords:
- Annotation element
ms.assetid: 7d75291a-47b4-498a-8ba4-3d093b8513b2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3c8c8b70e9e15e01a0864cd9f3491aa188be6777
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48103398"
---
# <a name="annotation-element-assl"></a>Annotation 元素 (ASSL)
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|None|  
|預設值|None|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[註解](../collections/annotations-element-assl.md)|  
|子元素|[名稱](../properties/name-element-assl.md)，[值](../properties/value-element-assl.md)，[可見性](../properties/visibility-element-assl.md)|  
  
## <a name="remarks"></a>備註  
 `Annotation` 元素會針對所有物件提供 ASSL 結構描述的擴充性，但單獨用來定義複雜資料類型的物件除外。 `Value` 元素的 `Annotation` 元素可以包含任何 XML 命名空間的有效 XML (ASSL 除外)，不過會受限於下列規則：  
  
-   XML 只能包含元素。  
  
-   每個元素都必須具有唯一的名稱。 建議讓 `Name` 元素之 `Annotation` 元素的值參考目標命名空間。  
  
 加諸這些規則的目的是為了允許透過其他介面 (例如，決策支援物件 (DSO)) 將 `Annotation` 元素的內容公開成名稱/值組的集合。  
  
 `Annotation` 元素內部沒有用子元素括住的註解和空格無法保留下來。 此外，所有元素都必須是可讀寫，因為唯讀的元素將會被忽略。  
  
 在 「 分析管理物件 (AMO) 物件模型的對應元素是<xref:Microsoft.AnalysisServices.Annotation>。  
  
## <a name="see-also"></a>另請參閱  
 [物件&#40;ASSL&#41;](objects-assl.md)  
  
  
