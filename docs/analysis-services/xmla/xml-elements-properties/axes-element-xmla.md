---
title: "座標軸會元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Axes Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Axes
- http://schemas.microsoft.com/analysisservices/2003/engine#Axes
- microsoft.xml.analysis.axes
- urn:schemas-microsoft-com:xml-analysis#Axes
helpviewer_keywords:
- Axes element
ms.assetid: 2005d06a-f8a2-4b4f-8c0d-2f7f73eb6f5c
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3fd10148d82ac0be83bfab721653cc1e200464fa
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="axes-element-xmla"></a>Axes 元素 (XMLA)
  包含集合[軸](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)項目代表所包含的軸資料[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)項目，會使用[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)資料型別。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">  
   ...  
   <Axes>  
      <Axis>...</Axis>  
   </Axes>  
   ...  
</root>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|任意|  
|預設值|無|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)|  
|子元素|[Axis](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 在下**座標軸**項目，**軸**項目會出現在資料集中，由零開始的順序列出。 **AxisFormat** XMLA 屬性設定會決定如何**軸**格式化的項目。 如需有關**AxisFormat**屬性，請參閱[支援 XMLA 屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md).  
  
 軸代表 Tuple 集合，而且集合中的所有 Tuple 都具有相同的維度性。 您可以使用不同的方式來表示集合，而且會產生不同的優點。 例如，下列四個 Tuple 的集合可以表示成二維 Tuple 的集合或兩個一維集合的笛卡兒乘積。  
  
|1999|1999|2000|2000|  
|----------|----------|----------|----------|  
|實際|預算|實際|預算|  
  
 這個 Tuple 集合可以表示成二維 Tuple 的集合：  
  
```  
{ ( 1999, Actual ), ( 1999, Budget ), ( 2000, Actual ), ( 2000, Budget ) }  
```  
  
 這個集合也可以表示成兩個一維集合的笛卡兒乘積：  
  
```  
{ 1999, 2000 } x { Actual, Budget }  
```  
  
 第一種表示法 (二維 Tuple) 會讓用戶端工具更方便使用。 第二種表示法 (一維集合的笛卡兒乘積) 會使用較少的空間並保留集合的多維度本質。  
  
 下表將列出可用來定義和描繪軸結構與成員的作業。  
  
|作業|Description|  
|---------------|-----------------|  
|成員|軸的最小單位，代表維度階層的成員。|  
|成員|集合**成員**物件從相同維度階層。|  
|Tuple|來自不同維度階層之成員的集合。|  
|Tuples|集合**Tuple**物件具有相同維度性。|  
|Union|集合的聯集。|  
|交叉聯結|集合的笛卡兒乘積。|  
  
 這些作業會將二維 Tuple 和一維集合的笛卡兒乘積轉譯成下列項目。  
  
## <a name="two-dimensional-tuples"></a>二維 Tuple  
  
```  
Tuples (  
   Tuple( Member(1999), Member(Actual) ),  
   Tuple( Member(1999), Member(Budget) ),  
   Tuple( Member(2000), Member(Actual) ),  
   Tuple( Member(2000), Member(Budget) )  
```  
  
## <a name="cartesian-product-of-one-dimensional-sets"></a>一維集合的笛卡兒乘積  
  
```  
CrossProduct (  
   Members( Member(1999), Member(2000) ),  
   Members( Member(Actual), Member(Budget) )  
```  
  
 用戶端可使用**AxisFormat**屬性來要求特定表示法。  
  
## <a name="see-also"></a>另請參閱  
 [MDDataSet 資料類型 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)   
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

