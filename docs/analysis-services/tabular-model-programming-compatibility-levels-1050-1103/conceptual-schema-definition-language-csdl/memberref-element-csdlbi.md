---
title: MemberRef 元素 (CSDLBI) |Microsoft 文件
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 79b6f2684dabcb45cfddac626bc2a6aa140298f3
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="memberref-element-csdlbi"></a>MemberRef 元素 (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  MemberRef 元素會識別做為參考目標之屬性的名稱。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 MemberRef 元素的元素和屬性。  
  
|名稱|是否必要|說明|  
|----------|-----------------|-----------------|  
|名稱|是|MemberRef 元素中包含之屬性的名稱。|  
  
## <a name="memberrefs-element"></a>MemberRefs 元素  
 MemberRefs 是複雜類型，用於定義成員集合，其中每個成員都包含在 MemberRef 元素中。  
  
 下表列出 MemberRefs 類型的元素和屬性。  
  
|名稱|是否必要|說明|  
|----------|-----------------|-----------------|  
|MemberRef|是|包含成員參考的字串。|  
  
## <a name="example"></a>範例  
 **表格式**  
  
 下列 CSDLBI 1.1 版中的範例代表 AdventureWorks 範本資料模型中定義 Products 資料表的部分。 這裡的 MemberRef 元素用於每個包含在模型的預設欄位集中的資料行。  
  
```  
  
<bi:EntityType>  
   <bi:DefaultDetails>  
     <bi:MemberRef Name="Color" />  
     <bi:MemberRef Name="DealerPrice" />  
     <bi:MemberRef Name="Status" />  
   </bi:DefaultDetails>  
  
```  
  
## <a name="example"></a>範例  
 **多維度**  
  
 下列 CSDLBI 1.1 版中的範例代表 Contoso Operations Cube 中定義 Bikes 資料表的部分。 在此範例中，某一個 MemberRef 元素用來指定做為報表中預設欄位集之資料行的名稱，而另一個 MemberRef 元素則用來參考提供排序次序的資料行。  
  
```  
  
<bi:DefaultDetails>  
   <bi:MemberRef Name="Color" />  
</bi:DefaultDetails>  
  
<bi:SortMembers>  
   <bi:MemberRef Name="Color" />  
</bi:SortMembers>  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [Csdl 的 BI 註解的技術參考](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
