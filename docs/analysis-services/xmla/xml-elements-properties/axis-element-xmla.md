---
title: Axis 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 50d2694db85b1391602c6f8d9d9307da4e79b65b
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2018
ms.locfileid: "34574420"
---
# <a name="axis-element-xmla"></a>Axis 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含一組用來代表多維度資料集中所包含之單一軸的 tuple[座標軸](../../../analysis-services/xmla/xml-elements-properties/axes-element-xmla.md)項目，會使用[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)所傳回的資料類型[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
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
|父元素|[軸](../../../analysis-services/xmla/xml-elements-properties/axes-element-xmla.md)|  
|子元素|[CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md)或[Tuple](../../../analysis-services/xmla/xml-elements-properties/tuples-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 內容**軸**元素的值而有所不同**AxisFormat**所使用的 XMLA 屬性**Execute**方法。  
  
## <a name="tupleformat"></a>TupleFormat  
 當用戶端應用程式將 **AxisFormat** 屬性設為 *TupleFormat* 時，軸就會表示成 Tuple 集合。 每個**軸**元素包含**Tuple**代表該軸上 tuple 集合的項目。 每個 Tuple 都會使用包含該軸上每個階層之 **Member** 元素的 **Tuple** 元素來表示。  
  
## <a name="clusterformat"></a>ClusterFormat  
 當用戶端應用程式設定**AxisFormat**屬性*ClusterFormat*，每個座標軸上的成員會分成的叢集，其中每個叢集代表已排序集合之間的交叉乘積每個階層的成員。 每個**軸**元素都包含一或多個**CrossProduct**項目。 每個**CrossProduct**元素包含**成員**軸上每個階層的項目。  
  
## <a name="customformat"></a>CustomFormat  
 當用戶端應用程式設定**AxisFormat**屬性*CustomFormat*，值會被視為相同*TupleFormat* Analysis Services 執行個體的值。  
  
## <a name="examples"></a>範例  
  
### <a name="description"></a>描述  
 下列範例說明結構**軸**時用戶端指定的項目*TupleFormat*或*CustomFormat*如**AxisFormat** XMLA 屬性，假設軸具有下列成員：  
  
|||||  
|-|-|-|-|  
|**時間**階層|1999|1999|2000|  
|**類別目錄**階層|實際|預算|預算|  
  
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
 下列範例說明結構**軸**時用戶端指定的項目*ClusterFormat*如**AxisFormat**指定下列的 XMLA 屬性軸的成員：  
  
||||||  
|-|-|-|-|-|  
|**時間**階層|1999|1999|2000|2001|  
|**類別目錄**階層|實際|預算|預算|預算|  
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
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
