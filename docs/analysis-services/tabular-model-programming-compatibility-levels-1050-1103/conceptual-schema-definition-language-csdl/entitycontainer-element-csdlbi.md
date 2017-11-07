---
title: "EntityContainer 元素 (CSDLBI) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: e328558e-16b0-4d4a-a79a-fdd3c9493595
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: abb371783474c7a0580d5694e7ad2afeabce3a4c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="entitycontainer-element-csdlbi"></a>EntityContainer 元素 (CSDLBI)
  EntityContainer 元素是以 CSDL 類型 EntityContainer 為基礎的複雜類型，會定義單一資料模型中實體的集合。 在商業智慧應用程式中，EntityContainer 所代表的資料模型可能包含多個以關聯性連結資料行的資料表，以及計算、量值和 KPI。 它在概念上與資料庫或資料來源類似。  
  
 EntityContainer 必須指定資料模型中包含的每個實體類型，包括資料表和關聯性。 有關這些模型實體的資訊是透過列出 Entity 元素類型的子實體來指定。 如需詳細資訊，請參閱 [EntityType 元素 &#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md)。  
  
 定序和語言等屬性是在 EntityContainer 層級定義的，而非針對個別物件所定義。 不過，模型中的資料行和文字屬性可以具有採用其他語言的標題或翻譯。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表描述定義 EntityContainer 的元素和屬性。  
  
|名稱|是否必要|說明|  
|----------|-----------------|-----------------|  
|名稱|是|資料模型的名稱。|  
|Caption|否|資料庫或資料模型的描述。|  
|Culture|是|包含要求 LCID 的字串。|  
|CompareOptions|是|模型的語言特有排序和字串比較選項。|  
|DirectQueryMode|否|列舉，指出模型使用 DirectQuery 模式時的查詢模式。|  
|EntitySet 元素|是|[EntitySet 元素 &#40;CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entityset-element-csdlbi.md)|  
|AssociationSet 元素|否|[AssociationSet 元素 &#40;CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/associationset-element-csdlbi.md)|  
  
## <a name="compareoptions-element"></a>CompareOptions 元素  
 CompareOptions 屬性 (Attribute) 會定義套用至資料模型的定序屬性 (Property)。 CompareOptions 所定義的屬性衍生自模型設計階段在 Analysis Services 資料庫中設定之排序次序、區分假名和區分大小寫的設定。 下表描述了當做 CompareOptions 屬性一部分加入的值。  
  
|Value|說明|  
|-----------|-----------------|  
|IgnoreCase|布林值，指出字串比較是否應忽略大小寫。|  
|IgnoreNonSpace|布林值，指出字串比較是否應忽略不佔空間的合併字元，例如變音符號。|  
|IgnoreKanaType|布林值，指出字串比較是否應忽略假名類型。|  
|IgnoreWidth|布林值，指出字串比較是否應忽略字元寬度。|  
  
## <a name="directquerymode"></a>DirectQueryMode  
 **DirectQueryMode**  
  
 簡單類型 DirectQueryMode 會定義模型可直接從關聯式資料來源接收資料時，預設使用的查詢類型。 此屬性只適用於以 DirectQuery 模式執行的表格式模型。 下表列出 DirectQuery 模式列舉的可能值。  
  
|Value|說明|  
|-----------|-----------------|  
|InMemory|指出對照模型的查詢將使用快取中的資料。|  
|InMemoryWithDirectQuery|指出對照模型的查詢預設將使用來自關聯式資料來源的資料。|  
|DirectQueryWithInMemory|指出對照模型的查詢預設將使用快取中的資料。|  
|DirectQuery|指出對照模型的查詢將只會使用關聯式資料來源中的資料。|  
  
## <a name="example"></a>範例  
 **表格式**  
  
 下列 CSDLBI 1.1 版的範例代表 AdventureWorks 表格式資料模型的一部分。  
  
```  
  
<EntityContainer   
     Name="Sandbox">  
   <EntitySet   
       Name="DimEmployee"   
       EntityType="Sandbox.DimEmployee">  
   <bi:EntitySet />  
   </EntitySet>  
  
   <EntitySet   
     Name="DimProduct"   
       EntityType="Sandbox.DimProduct">  
    <bi:EntitySet />  
    </EntitySet>  
  
<bi:EntityContainer Caption="AWSimple" Culture="en-US">  
  
```  
  
## <a name="example"></a>範例  
 **多維度**  
  
 下列 CSDLBI 1.1 版的範例為 Contoso Operations Cube 的摘錄。  
  
```  
  
<EntityContainer   
     Name="Sandbox">  
   <EntitySet   
      Name="Bike"   
      EntityType="Sandbox.Bike">  
    <bi:EntitySet Hidden="true" />  
   </EntitySet>  
…  
<bi:EntityContainer   
   Caption="CSDLTest"   
   Culture="en-US">  
<bi:CompareOptions   
   IgnoreCase="true" />  
</bi:EntityContainer>  
</EntityContainer>  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [EntitySet 元素 &#40;CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entityset-element-csdlbi.md)  
  
  

