---
title: 軸元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Axes Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Axes
- http://schemas.microsoft.com/analysisservices/2003/engine#Axes
- microsoft.xml.analysis.axes
- urn:schemas-microsoft-com:xml-analysis#Axes
helpviewer_keywords:
- Axes element
ms.assetid: 2005d06a-f8a2-4b4f-8c0d-2f7f73eb6f5c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bdb5aa48dd3a65f99b424274fdb89b3aee8c9591
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094904"
---
# <a name="axes-element-xmla"></a>Axes 元素 (XMLA)
  包含的集合[軸](axis-element-xmla.md)項目代表所包含的軸資料[根](root-element-xmla.md)使用的項目[MDDataSet](../xml-data-types/mddataset-data-type-xmla.md)資料型別。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|任意|  
|預設值|None|  
|基數|1-1：只出現一次的必要元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[根目錄](root-element-xmla.md)|  
|子元素|[Axis](axis-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 在 `Axes` 元素底下，`Axis` 元素會按照它們出現在資料集中的順序列出，從零開始。 `AxisFormat` XMLA 屬性設定會決定如何格式化 `Axis` 元素。 如需詳細資訊`AxisFormat`屬性，請參閱 <<c2> [ 支援的 XMLA 屬性&#40;XMLA&#41;](propertylist-element-supported-xmla-properties.md)。</c2>  
  
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
  
|作業|描述|  
|---------------|-----------------|  
|成員|軸的最小單位，代表維度階層的成員。|  
|成員|來自相同維度階層之 `Member` 物件的集合。|  
|Tuple|來自不同維度階層之成員的集合。|  
|Tuples|具有相同維度性之 `Tuple` 物件的集合。|  
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
  
 用戶端會使用 `AxisFormat` 屬性來要求特定表示法。  
  
## <a name="see-also"></a>另請參閱  
 [MDDataSet 資料類型&#40;XMLA&#41;](../xml-data-types/mddataset-data-type-xmla.md)   
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
