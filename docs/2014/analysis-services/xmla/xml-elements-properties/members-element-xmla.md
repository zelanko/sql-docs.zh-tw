---
title: Members 元素 (XMLA) |Microsoft 文件
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
- Members Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Members
- urn:schemas-microsoft-com:xml-analysis#Members
- microsoft.xml.analysis.members
helpviewer_keywords:
- Members element
ms.assetid: 55f9ec3a-5a41-4b3a-acd6-c07598868c46
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 5d812d0eea48c4f2b54352f61a176462b280071a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132506"
---
# <a name="members-element-xmla"></a>Members 元素 (XMLA)
  包含集合[成員](member-element-xmla.md)父元素所包含[CrossProduct](crossproduct-element-xmla.md)項目。  
  
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
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CrossProduct](crossproduct-element-xmla.md)|  
|子元素|[成員](member-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|階層|需要`String`屬性。 `Members` 元素所包含之成員所屬的階層名稱。|  
  
## <a name="remarks"></a>備註  
 當用戶端應用程式設定`AxisFormat`屬性*ClusterFormat*，每個座標軸上的成員會分成的叢集，其中每個叢集代表每個階層的成員已排序集合之間的交叉乘積。 每個 `Axis` 元素都包含一個或多個 `CrossProduct` 元素。 每個 `CrossProduct` 元素都會針對該軸上的每個階層包含 `Members` 元素。 然後，`Members` 元素會針對交叉乘積中包含之指定階層的每個成員包含一個 `Member` 元素。  
  
## <a name="example"></a>範例  
 下列範例說明結構`Members`時用戶端指定項目*ClusterFormat*如`AxisFormat`XMLA 屬性，假設軸具有下列成員：  
  
||||||  
|-|-|-|-|-|  
|`Time` 階層|1999|1999|2000|2001|  
|`Category` 階層|實際|預算|預算|預算|  
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
 [屬性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  