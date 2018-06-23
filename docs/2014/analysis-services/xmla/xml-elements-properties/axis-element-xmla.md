---
title: Axis 元素 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Axis Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.axis
- http://schemas.microsoft.com/analysisservices/2003/engine#Axis
helpviewer_keywords:
- Axis element
ms.assetid: 336895e1-4a57-4b43-9a53-e31569866e6c
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: e30ff03b6e1a58a079d35f8e846ed176c42a3a31
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36036629"
---
# <a name="axis-element-xmla"></a>Axis 元素 (XMLA)
  包含一組用來代表多維度資料集中所包含之單一軸的 tuple[座標軸](axes-element-xmla.md)項目，會使用[MDDataSet](../xml-data-types/mddataset-data-type-xmla.md)所傳回的資料類型[Execute](../xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Axes>  
   ...  
   <Axis> <!-- when AxisFormat XMLA property is set to ClusterFormat -->  
      <CrossProduct>...</CrossProduct>  
   </Axis>  
   <Axis> <!-- when AxisFormat XMLA property is set to TupleFormat or CustomFormat -->  
      <Tuples>...</Tuples>  
   </Axis>  
   ...  
</Axes>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[軸](axes-element-xmla.md)|  
|子元素|[CrossProduct](crossproduct-element-xmla.md)或[Tuple](tuples-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 `Axis` 元素的內容會因 `AxisFormat` 方法所使用的 `Execute` XMLA 屬性值而不同。  
  
## <a name="tupleformat"></a>TupleFormat  
 當用戶端應用程式設定`AxisFormat`屬性*TupleFormat*，軸就會表示為一組 tuple。 每個 `Axis` 元素都包含代表該軸上 Tuple 集合的 `Tuples` 元素。 每個 Tuple 都會使用包含該軸上每個階層之 `Tuple` 元素的 `Member` 元素來表示。  
  
## <a name="clusterformat"></a>ClusterFormat  
 當用戶端應用程式設定`AxisFormat`屬性*ClusterFormat*，每個座標軸上的成員會分成的叢集，其中每個叢集代表每個階層的成員已排序集合之間的交叉乘積。 每個 `Axis` 元素都包含一個或多個 `CrossProduct` 元素。 每個 `CrossProduct` 元素都會針對該軸上的每個階層包含 `Members` 元素。  
  
## <a name="customformat"></a>CustomFormat  
 當用戶端應用程式設定`AxisFormat`屬性*CustomFormat*，值會被視為相同*TupleFormat* Analysis Services 執行個體的值。  
  
## <a name="examples"></a>範例  
  
### <a name="description"></a>描述  
 下列範例說明結構`Axis`時用戶端指定的項目*TupleFormat*或*CustomFormat*如`AxisFormat`指定下列的 XMLA 屬性軸的成員：  
  
|||||  
|-|-|-|-|  
|`Time` 階層|1999|1999|2000|  
|`Category` 階層|實際|預算|預算|  
  
### <a name="code"></a>程式碼  
  
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
  
### <a name="description"></a>描述  
 下列範例說明結構`Axis`時用戶端指定的項目*ClusterFormat*如`AxisFormat`XMLA 屬性，假設軸具有下列成員：  
  
||||||  
|-|-|-|-|-|  
|`Time` 階層|1999|1999|2000|2001|  
|`Category` 階層|實際|預算|預算|預算|  
|Clusters|叢集 1|叢集 1|叢集 1|群集 2|  
  
### <a name="code"></a>程式碼  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <CrossProduct Size = "4">  
         <Members Hierarchy="Time">  
            <Member>  
               <UName>[Time].[1999]</UName>  
               ...  
            </Member>  
            <Member>  
               <UName>[Time].[2000]</UName>  
               ...  
            </Member>  
         </Members>  
         <Members Hierarchy="Category">  
            <Member>  
               <UName>[Scenario].[Actual]</UName>  
               ...  
            </Member>  
            <Member>  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Members>  
      </CrossProduct>  
      <CrossProduct Size = "1">  
         <Members Hierarchy="Time">  
            <Member>  
               <UName>[Time].[2001]</UName>  
               ...  
            </Member>  
         </Members>  
         <Members Hierarchy="Category">  
            <Member>  
               <UName>[Scenario].[Budget]</UName>  
               ...  
            </Member>  
         </Members>  
      </CrossProduct>  
   </Axis>  
   ...  
</Axes>  
```  
  
## <a name="see-also"></a>另請參閱  
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  