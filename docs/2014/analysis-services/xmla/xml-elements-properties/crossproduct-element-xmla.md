---
title: CrossProduct 元素 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- CrossProduct Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#CrossProduct
- microsoft.xml.analysis.crossproduct
- urn:schemas-microsoft-com:xml-analysis#CrossProduct
helpviewer_keywords:
- CrossProduct element
ms.assetid: a9a1584e-d2dd-45db-a918-d694c20d8189
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 1324a3c9449383301242ab6d0e76f94c636d9b5e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030161"
---
# <a name="crossproduct-element-xmla"></a>CrossProduct 元素 (XMLA)
  包含每個階層的成員已排序集合之間的交叉乘積[軸](axis-element-xmla.md)項目，會使用[MDDataSet](../xml-data-types/mddataset-data-type-xmla.md)所傳回的資料類型[Execute](../xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Axis>  
   ...  
   <CrossProduct Size="integer">  
      <Members>...</Members>  
   </CrossProduct>  
   ...  
</Axis>  
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
|父元素|[Axis](axis-element-xmla.md)|  
|子元素|[成員](members-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|大小|需要`Integer`屬性。 指出 `CrossProduct` 元素所代表之交叉乘積內包含的 Tuple 數目。|  
  
## <a name="remarks"></a>備註  
 當用戶端應用程式設定`AxisFormat`屬性*ClusterFormat*，每個座標軸上的成員會分成的叢集，其中每個叢集代表每個階層的成員已排序集合之間的交叉乘積。 每個叢集都由一個 `CrossProduct` 元素表示。 每個 `CrossProduct` 元素都會針對該軸上的每個階層包含 `Members` 元素。 `CrossProduct` 元素可以包含來自單一階層的成員。  
  
## <a name="example"></a>範例  
 下列範例說明結構`CrossProduct`時用戶端指定項目*ClusterFormat*如`AxisFormat`XMLA 屬性，假設軸具有下列成員：  
  
||||||  
|-|-|-|-|-|  
|`Time` 階層|1999|1999|2000|2001|  
|`Category` 階層|實際|預算|預算|預算|  
|Clusters|叢集 1|叢集 1|叢集 1|群集 2|  
  
```  
<Axes>  
   <Axis name="Axis0">  
      <CrossProduct Size="4">  
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
      <CrossProduct Size="1">  
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
  
  