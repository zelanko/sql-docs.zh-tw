---
title: EntitySet 元素 (CSDLBI) |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0a38bf011a6a98ca89b8b574323b522060ff4620
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2018
---
# <a name="entityset-element-csdlbi"></a>EntitySet 元素 (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  EntitySet 元素會定義 CSDLBI 資料模型中特殊類型的實體集合。  
  
 EntitySet 必須指定資料模型中包含的每個實體類型。 有關這些模型實體的資訊是透過列出 Entity 元素類型的子實體來指定。 如需詳細資訊，請參閱 [EntityType 元素 &#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md)。  
  
 定序和語言等屬性是在 EntityContainer 層級定義的，而非針對個別物件所定義。 不過，模型中的資料行和文字屬性可以具有採用其他語言的標題或翻譯。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 EntitySet 的元素和屬性。  
  
|屬性名稱|是否必要|說明|  
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
  
## <a name="see-also"></a>另請參閱  
 [Csdl 的 BI 註解的技術參考](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
