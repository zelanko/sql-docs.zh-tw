---
title: Members 元素 (XMLA) |Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5ae4326e00ba98075a86079157484c5963d0147d
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37994710"
---
# <a name="members-element-xmla"></a>Members 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含的集合[成員](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)父元素所包含的項目[CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md)項目。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<CrossProduct>  
   <Members Hierarchy="string">  
      <Member>...</Member>  
   </Members>  
   ...  
</CrossProduct>  
```  
  
## <a name="element-characteristics"></a>項目特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>項目關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[CrossProduct](../../../analysis-services/xmla/xml-elements-properties/crossproduct-element-xmla.md)|  
|子元素|[成員](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|attribute|描述|  
|---------------|-----------------|  
|階層|所需**字串**屬性。 階層的成員包含所要的名稱**成員**所屬項目。|  
  
## <a name="remarks"></a>備註  
 當用戶端應用程式設定**AxisFormat**屬性設*ClusterFormat*，每個座標軸上的為成員會分成的叢集，其中每個叢集代表已排序集合之間的交叉乘積每個階層的成員。 每個**軸**項目包含一個或多個**CrossProduct**項目。 每隔**CrossProduct**項目包含**成員**軸上每個階層的項目。 **成員**項目，依序包含一個**成員**交叉乘積中包含指定階層的每個成員的項目。  
  
## <a name="example"></a>範例  
 下列範例說明的結構**成員**用戶端指定的項目*ClusterFormat* for **AxisFormat** XMLA 屬性軸的下列成員：  
  
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
 [屬性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
