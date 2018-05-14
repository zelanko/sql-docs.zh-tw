---
title: CrossProduct 元素 (XMLA) |Microsoft 文件
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 07e34958589bd9366cda6b42207c289bfda72453
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="crossproduct-element-xmla"></a>CrossProduct 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含每個階層的成員已排序集合之間的交叉乘積[軸](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)項目，會使用[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)所傳回的資料類型[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
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
  
|特性|說明|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-n：出現一次以上的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[軸](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)|  
|子元素|[成員](../../../analysis-services/xmla/xml-elements-properties/members-element-xmla.md)|  
  
## <a name="attributes"></a>屬性  
  
|Attribute|Description|  
|---------------|-----------------|  
|大小|需要**整數**屬性。 表示所代表之交叉乘積內包含的 tuple 數目**CrossProduct**項目。|  
  
## <a name="remarks"></a>備註  
 當用戶端應用程式設定**AxisFormat**屬性*ClusterFormat*，每個座標軸上的成員會分成的叢集，其中每個叢集代表已排序集合之間的交叉乘積每個階層的成員。 每個叢集由**CrossProduct**項目。 每個**CrossProduct**元素包含**成員**軸上每個階層的項目。 A **CrossProduct**項目可以包含來自單一階層的成員。  
  
## <a name="example"></a>範例  
 下列範例說明結構**CrossProduct**時用戶端指定項目*ClusterFormat*如**AxisFormat**指定的 XMLA 屬性軸的下列成員：  
  
||||||  
|-|-|-|-|-|  
|**時間**階層|1999|1999|2000|2001|  
|**類別目錄**階層|實際|預算|預算|預算|  
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
 [屬性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
