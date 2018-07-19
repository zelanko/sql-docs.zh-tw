---
title: DefaultDetails 元素 (CSDLBI) |Microsoft Docs
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
ms.assetid: 05a08baa-23cc-4011-9c2e-f60a20bb87da
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 708e829f1af3ebc9d727e3abfd6643913cd460f2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37330228"
---
# <a name="defaultdetails-element-csdlbi"></a>DefaultDetails 元素 (CSDLBI)
  DefaultDetails 元素代表屬性參考清單，這些屬性參考會共同定義資料表中資料行的「預設欄位集」。 每個屬性只能參考一個量值或資料行。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出定義 DefaultDetails 元素的元素和屬性。  
  
|名稱|是否必要|描述|  
|----------|-----------------|-----------------|  
|DefaultDetailsPosition|否|指出在集合中存在與位置的正整數。|  
  
## <a name="example"></a>範例  
 **表格式**  
  
 下列 CSDLBI 1.1 版中的範例顯示 AdventureWorks 範本資料模型中的摘錄。 Employees 資料表 (標題) 只有一個預設資料行集。 不過，有三個資料行定義為 Products 資料表的預設欄位集。  
  
```  
  
<EntityType   
    Name="DimEmployee">  
....  
   <bi:DefaultDetails>  
      <bi:MemberRef Name="Title" />  
   </bi:DefaultDetails>  
.....  
<EntityType   
    Name="Products">  
.....  
   <bi:DefaultDetails>  
      <bi:MemberRef Name="Color" />  
      <bi:MemberRef Name="DealerPrice" />  
      <bi:MemberRef Name="Status" />  
   </bi:DefaultDetails>  
  
```  
  
## <a name="example"></a>範例  
 **多維度**  
  
 下列 CSDLBI 1.1 版中的範例顯示 Contoso Operations Cube 中 Bike 資料表定義的摘錄。 此註解指出，如果未指定其他顯示資料行，則預設應顯示 Color 資料行。  
  
```  
  
<EntityType Name="Bike">  
   <Key>  
   <PropertyRef Name="RowNumber" />  
   </Key>  
....  
<bi:EntityType>  
   <bi:DisplayKey>  
      <bi:MemberRef Name="Color" />  
   </bi:DisplayKey>  
   <bi:DefaultDetails>  
      <bi:MemberRef Name="Color" />  
   </bi:DefaultDetails>  
   <bi:SortMembers>  
      <bi:MemberRef Name="Color" />  
   </bi:SortMembers>  
....  
</bi:EntityType>  
</EntityType>  
```  
  
## <a name="see-also"></a>另請參閱  
 [了解表格式物件模型](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [CSDLBI 概念](../csdlbi-concepts.md)  
  
  
