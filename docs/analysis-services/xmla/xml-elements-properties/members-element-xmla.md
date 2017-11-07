---
title: "Members 元素 (XMLA) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Members Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Members
- urn:schemas-microsoft-com:xml-analysis#Members
- microsoft.xml.analysis.members
helpviewer_keywords:
- Members element
ms.assetid: 55f9ec3a-5a41-4b3a-acd6-c07598868c46
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 46944cc7653a603451703b016495395f8197bc82
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="members-element-xmla"></a>Members 元素 (XMLA)
  包含集合[成員](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)父元素所包含[CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CrossProduct>  
   <Members Hierarchy="string">  
      <Member>...</Member>  
   </Members>  
   ...  
</CrossProduct>  
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
|父元素|[CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md)|  
|子元素|[成員](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|Attribute|Description|  
|---------------|-----------------|  
|階層|需要**字串**屬性。 所包含的成員的階層名稱**成員**所屬項目。|  
  
## <a name="remarks"></a>備註  
 當用戶端應用程式設定**AxisFormat**屬性*ClusterFormat*，每個座標軸上的成員會分成的叢集，其中每個叢集代表已排序集合之間的交叉乘積每個階層的成員。 每個**軸**元素都包含一或多個**CrossProduct**項目。 每個**CrossProduct**元素包含**成員**軸上每個階層的項目。 **成員**項目，依序包含一個**成員**交叉乘積中包含指定階層的每個成員的項目。  
  
## <a name="example"></a>範例  
 下列範例說明結構**成員**時用戶端指定項目*ClusterFormat*如**AxisFormat**指定的 XMLA 屬性軸的下列成員：  
  
||||||  
|-|-|-|-|-|  
|**時間**階層|1999|1999|2000|2001|  
|**類別目錄**階層|實際|預算|預算|預算|  
|Clusters|叢集 1|叢集 1|叢集 1|群集 2|  
  
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
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

