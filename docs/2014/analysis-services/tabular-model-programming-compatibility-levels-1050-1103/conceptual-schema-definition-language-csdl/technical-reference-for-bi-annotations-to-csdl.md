---
title: Csdl 的 BI 註解的技術參考資料 |Microsoft 文件
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
ms.assetid: 63b3e069-6ba5-474e-b769-47b7cc87b7dd
caps.latest.revision: 15
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 27ed1339d64dd3c4035288a96b31ae163a304733
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36032173"
---
# <a name="technical-reference-for-bi-annotations-to-csdl"></a>CSDL 之 BI 註解的技術參考
  本節列出了 CSDL 中用於表示 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 表格式模型的元素、屬性 (Attribute) 和屬性 (Property)。 某些元素是新增的，其他元素則已加上註解或擴充，可支援商業智慧模型。  
  
 如需表格式模型，以及如何在 CSDL 中表示實體、 關聯性和公式的概觀，請參閱[商業智慧的 CSDL 註解&#40;CSDLBI&#41;](../csdl-annotations-for-business-intelligence-csdlbi.md)。  
  
## <a name="extended-csdl-elements-complex-types"></a>擴充的 CSDL 元素：複雜類型  
 下列 CSDL 元素已經加入或擴充，可支援表格式與多維度商業智慧資料模型。  
  
-   [AssociationSet 元素&#40;CSDLBI&#41;](associationset-element-csdlbi.md)  
  
-   [BaseProperty 元素&#40;CSDLBI&#41;](property-element-csdlbi.md)  
  
-   [DefaultDetails 元素&#40;CSDLBI&#41;](defaultdetails-element-csdlbi.md)  
  
-   [DisplayKey 元素&#40;CSDLBI&#41;](displaykey-element-csdlbi.md)  
  
-   [EntityContainer 元素&#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)  
  
-   [EntitySet 元素&#40;CSDLBI&#41;](entityset-element-csdlbi.md)  
  
-   [EntityType 元素&#40;CSDLBI&#41;](entitytype-element-csdlbi.md)  
  
-   [Hierarchy 元素&#40;CSDLBI&#41;](hierarchy-element-csdlbi.md)  
  
-   [KPI 元素&#40;CSDLBI&#41;](kpi-element-csdlbi.md)  
  
-   [KpiGoal 元素&#40;CSDLBI&#41;](kpigoal-element-csdlbi.md)  
  
-   [KpiStatus 元素&#40;CSDLBI&#41;](kpistatus-element-csdlbi.md)  
  
-   [項目層級&#40;CSDLBI&#41;](level-element-csdlbi.md)  
  
-   [量值的項目&#40;CSDLBI&#41;](measure-element-csdlbi.md)  
  
-   [Member 元素&#40;CSDLBI&#41;](member-element-csdlbi.md)  
  
-   [MemberRef 元素&#40;CSDLBI&#41;](memberref-element-csdlbi.md)  
  
-   [NavigationProperty 元素&#40;CSDLBI&#41;](navigationproperty-element-csdlbi.md)  
  
-   [屬性項目&#40;CSDLBI&#41;](property-element-csdlbi.md)  
  
-   [PropertyRef 元素&#40;CSDLBI&#41;](propertyref-element-csdlbi.md)  
  
## <a name="simple-type-and-subtypes"></a>簡單類型與子類型  
 下表列出上面所列複雜類型的定義中包含的一些簡單類型和一些次要複雜類型。 左邊資料行中所列的每個簡單類型或子類型的文件，都會在右邊資料行中所列的父元素中提供。  
  
|簡單類型|主題中找到|  
|-----------------|--------------------|  
|Alignment|[BaseProperty 元素&#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|CompareOptions|[EntityContainer 元素&#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)|  
|目錄|[EntityType 元素&#40;CSDLBI&#41;](entitytype-element-csdlbi.md)|  
|ContextualNameRule|[Member 元素&#40;CSDLBI&#41;](member-element-csdlbi.md)|  
|DefaultAggregationFunction|[屬性項目&#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|DirectQueryMode|[EntityContainer 元素&#40;CSDLBI&#41;](entitycontainer-element-csdlbi.md)|  
|GroupingBehavior|[屬性項目&#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|MemberRefs|[MemberRef 元素&#40;CSDLBI&#41;](memberref-element-csdlbi.md)|  
|PropertyRefs|[PropertyRef 元素&#40;CSDLBI&#41;](propertyref-element-csdlbi.md)|  
|SortDirection|[BaseProperty 元素&#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|State|[AssociationSet 元素&#40;CSDLBI&#41;](associationset-element-csdlbi.md)|  
|Stability|[屬性項目&#40;CSDLBI&#41;](property-element-csdlbi.md)|  
|SortDirection|[BaseProperty 元素&#40;CSDLBI&#41;](property-element-csdlbi.md)|  
  
## <a name="see-also"></a>另請參閱  
 [CSDLBI 概念](../csdlbi-concepts.md)  
  
  