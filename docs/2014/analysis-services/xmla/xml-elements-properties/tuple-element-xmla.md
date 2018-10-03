---
title: Tuple 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Tuple Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.tuple
- urn:schemas-microsoft-com:xml-analysis#Tuple
- http://schemas.microsoft.com/analysisservices/2003/engine#Tuple
helpviewer_keywords:
- Tuple element
ms.assetid: d65aba10-55e1-49c1-81bc-0756c39c0da2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 32dc7b75f47acf69a8d16e33bc25ac505b1c9333
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061338"
---
# <a name="tuple-element-xmla"></a>Tuple 元素 (XMLA)
  包含 [Tuples](tuples-element-xmla.md) 父元素所包含之 [Member](member-element-xmla.md) 元素的集合。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Tuples>  
   <Tuple>  
      <Member>...</Member>  
   </Tuple>  
   ...  
</Tuples>  
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
|父元素|[Tuple](tuples-element-xmla.md)|  
|子元素|[成員](member-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 當用戶端應用程式設定`AxisFormat`屬性，以*TupleFormat*，軸就會表示為一組 tuple。 每個 `Axis` 元素都包含代表該軸上 Tuple 集合的 `Tuples` 元素。 每個 Tuple 都會使用包含該軸上每個階層之 `Tuple` 元素的 `Member` 元素來表示。  
  
## <a name="example"></a>範例  
 下列範例說明的結構`Tuple`時用戶端指定的項目*TupleFormat*或是*CustomFormat*的`AxisFormat`指定下列的 XMLA 屬性座標軸的成員：  
  
|||||  
|-|-|-|-|  
|`Time` 階層|1999|1999|2000|  
|`Category` 階層|實際|預算|預算|  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <Tuples>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Actual]</UName>  
               ...  
            </Member>  
         </Tuple>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Tuple>  
         <Tuple>  
            <Member Hierarchy="Time">  
               <UName>[Time].[2000]</UName>  
               ...  
            </Member>  
            <Member Hierarchy="Category">  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Tuple>  
      </Tuples>  
   </Axis>  
   ...  
</Axes>  
```  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
