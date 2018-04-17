---
title: Tuples 元素 (XMLA) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Tuples Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Tuples
- microsoft.xml.analysis.tuples
- urn:schemas-microsoft-com:xml-analysis#Tuples
helpviewer_keywords:
- Tuples element
ms.assetid: 5494bbaa-c1aa-43fa-b3e0-83befb2bccdd
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 05b1a2e375b7a563699243c586b866ab77fe47ca
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="tuples-element-xmla"></a>Tuples 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]包含一組[Tuple](../../../analysis-services/xmla/xml-elements-properties/tuple-element-xmla.md)物件[軸](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)項目，會使用[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)所傳回的資料類型[Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Axis>  
   ...  
   <Tuples>  
      <Tuple>...</Tuple>  
   </Tuples>  
   ...  
</Axis>  
```  
  
## <a name="element-characteristics"></a>元素特性  
  
|特性|描述|  
|--------------------|-----------------|  
|資料類型和長度|無|  
|預設值|無|  
|基數|0-1：只能出現一次的選擇性元素。|  
  
## <a name="element-relationships"></a>元素關聯性  
  
|關聯性|元素|  
|------------------|-------------|  
|父元素|[Axis](../../../analysis-services/xmla/xml-elements-properties/axis-element-xmla.md)|  
|子元素|[Tuple](../../../analysis-services/xmla/xml-elements-properties/tuple-element-xmla.md)|  
  
## <a name="remarks"></a>備註  
 當用戶端應用程式將 **AxisFormat** 屬性設為 *TupleFormat* 時，軸就會表示成 Tuple 集合。 每個 **Axis** 元素都包含代表該軸上 Tuple 集合的 **Tuples** 元素。 每個 Tuple 都會使用包含該軸上每個階層之 [Member](../../../analysis-services/xmla/xml-elements-properties/member-element-xmla.md) 元素的 **Tuple** 元素來表示。  
  
## <a name="example"></a>範例  
 下列範例說明結構**Tuple**時用戶端指定項目*TupleFormat*或*CustomFormat*如**AxisFormat** XML for Analysis (XMLA) 屬性，假設軸具有下列成員：  
  
|||||  
|-|-|-|-|  
|**時間**階層|1999|1999|2000|  
|**類別目錄**階層|實際|預算|預算|  
  
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
  
## <a name="see-also"></a>請參閱  
 [屬性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
