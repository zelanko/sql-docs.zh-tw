---
title: "DisplayKey 元素 (CSDLBI) |Microsoft 文件"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 7d881278-1e77-42e1-8cfc-f1bbd9ec2340
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6c3e0be2d677f87afae5bbdff84947b3d013c23f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2018
---
# <a name="displaykey-element-csdlbi"></a>DisplayKey 元素 (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
DisplayKey 元素會包含共同構成強式識別碼之下列元素的清單。 DisplayKey 只會顯示成 EntityType 元素的子系。 它可以參考資料行或角色端。  
  
## <a name="elements-and-attributes"></a>元素和屬性  
 下表列出 DisplayKey 元素的屬性。  
  
|名稱|是否必要|說明|  
|----------|-----------------|-----------------|  
|IsDisplayKey|否|True 或 false。|  
  
## <a name="remarks"></a>備註  
 此元素適用於報表。 您套用此屬性的元素不需要是實際的資料表索引鍵，只要是您將呈現為索引鍵的元素即可。 不過，用於 DisplayKey 的資料行必須包含唯一值。  
  
## <a name="example"></a>範例  
 **表格式**  
  
 下列 CSDLBI 1.1 版中的範例顯示 AdventureWorks 範本資料模型中已指定為資料表之 DisplayKey 的資料行。  
  
```  
<sample in progress>  
```  
  
## <a name="example"></a>範例  
 **多維度**  
  
 下列 CSDLBI 1.1 版中的範例顯示 Contoso Operations Cube 表示的摘錄。 在此模型中，Color 資料行已標示為 Bikes 資料表的顯示索引鍵。  
  
```  
  
<EntityType   
    Name="Bike">  
.. .. ..  
<Property   
    Name="Color"   
    Type="String"   
    MaxLength="Max"   
    Unicode="true"   
    FixedLength="false">  
<bi:Property   
    ContextualNameRule="Context"   
    Alignment="Left" Units="counts"   
    SortDirection="Descending"   
    IsRightToLeft="true"   
    DefaultAggregateFunction="Max" />  
</Property>  
.. .. ..  
<bi:EntityType>  
   <bi:DisplayKey>  
      <bi:MemberRef Name="Color" />  
   </bi:DisplayKey>>  
.. .. ..  
</bi:EntityType>  
</EntityType>  
```  
  
## <a name="see-also"></a>另請參閱  
 [了解表格式物件模型在相容性層級 1050年透過 1103](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [CSDLBI 概念](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdlbi-concepts.md)  
  
  
