---
title: "EntitySet 元素 (CSDLBI) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: d4703c9e-5594-472e-a85b-0f5bd0d73d6f
caps.latest.revision: "10"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4ae8366ecec5bf25e1fd27a63d22ac796c080660
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="entityset-element-csdlbi"></a>EntitySet 元素 (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]EntitySet 元素會定義 CSDLBI 資料模型中實體的特定類型的集合。  
  
 EntitySet 必須指定資料模型中包含的每個實體類型。 有關這些模型實體的資訊是透過列出 Entity 元素類型的子實體來指定。 如需詳細資訊，請參閱 [EntityType 元素 &#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md)。  
  
 定序和語言等屬性是在 EntityContainer 層級定義的，而非針對個別物件所定義。 不過，模型中的資料行和文字屬性可以具有採用其他語言的標題或翻譯。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 EntitySet 的元素和屬性。  
  
|屬性名稱|是否必要|描述|  
|--------------------|-----------------|-----------------|  
|Caption|否|使用者易記的實體集描述。|  
|CollectionCaption|否|包含複數實體名稱的字串。|  
|ReferenceName|否|包含實體的未合併完整名稱。 在多維度模型中，此名稱對應至 CubeDimension 名稱。|  
|Hidden|否|指出是否隱藏實體。 根據預設，實體不會隱藏。|  
  
## <a name="example"></a>範例  
 **表格式**  
  
 下列 CSDLBI 1.1 版的範例顯示 AdventureWorks 表格式模型中 Date 和 Geography 資料表的定義。  
  
```  
  
<EntitySet   
   Name="Date"   
   EntityType="Sandbox. Date">  
<bi:EntitySet />  
</EntitySet>  
  
<EntitySet   
   Name="Geography"   
   EntityType="Sandbox.Geography">  
<bi:EntitySet />  
</EntitySet>  
```  
  
## <a name="example"></a>範例  
 **多維度**  
  
 下列 CSDLBI 1.1 版中的範例顯示 Contoso Retail Operations Cube 中的數個 EntitySet 元素。  
  
```  
  
<EntitySet Name="Outage" EntityType="Sandbox.Outage">  
       <bi:EntitySet />  
</EntitySet>  
  
<EntitySet Name="Store" EntityType="Sandbox.Store">  
     <bi:EntitySet />  
</EntitySet>  
```  
  
## <a name="see-also"></a>請參閱  
 [CSDL 之 BI 註解的技術參考](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
