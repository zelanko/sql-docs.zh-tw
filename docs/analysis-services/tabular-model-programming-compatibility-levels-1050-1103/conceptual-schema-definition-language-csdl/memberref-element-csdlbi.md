---
title: "MemberRef 元素 (CSDLBI) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 399aaa34-896c-48e7-aacb-18564f31b568
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 345a9df28803736c1dc7cf1b075bc101cb76ed27
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="memberref-element-csdlbi"></a>MemberRef 元素 (CSDLBI)
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
  
## <a name="see-also"></a>請參閱＜  
 [CSDL 之 BI 註解的技術參考](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
