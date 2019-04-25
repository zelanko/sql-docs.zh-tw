---
title: 成員物件 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member
helpviewer_keywords:
- Member object [ADO MD], members
ms.assetid: 3dedf755-0741-4c3f-8b4e-bff8ff8809c8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b1f11919ab6dcc89da188601867f8a49a1aa48f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740078"
---
# <a name="member-object-ado-md"></a>Member 物件 (ADO MD)
代表在 cube 中，層級成員的層級、 成員或成員的資料格集沿著座標軸的位置的子系。  
  
## <a name="remarks"></a>備註  
 屬性**成員**使用的內容而有所不同。 A**成員**的[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)中[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)具有[子系](../../../ado/reference/ado-md-api/children-property-ado-md.md)屬性，傳回**成員**上從目前的階層中的下一步 較低層級**成員**。 針對**成員**的[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)，則**子系**永遠是空的集合。 此外，[型別](../../../ado/reference/ado-md-api/type-property-ado-md.md)屬性僅適用於**成員**的**層級**。  
  
 A**成員**的**位置**有兩個屬性顯示時非常實用[Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md):[DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md)並[ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)。 如果在存取這些屬性，會發生錯誤**成員**的**層級**。  
  
 使用集合和屬性的**成員**的物件**層級**，您可以執行下列動作：  
  
-   找出**成員**具有[名稱](../../../ado/reference/ado-md-api/name-property-ado-md.md)並[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性。  
  
-   傳回的字串顯示時，使用**成員**具有[標題](../../../ado/reference/ado-md-api/caption-property-ado-md.md)屬性。  
  
-   傳回有意義的字串，描述量值或公式**成員**具有[描述](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性。  
  
-   判斷本質**成員**具有[型別](../../../ado/reference/ado-md-api/type-property-ado-md.md)屬性。  
  
-   取得相關資訊**層級**的**成員**具有[LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md)並[LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md)屬性。  
  
-   取得相關**成員**中[階層](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)具有[父](../../../ado/reference/ado-md-api/parent-property-ado-md.md)並[子系](../../../ado/reference/ado-md-api/children-property-ado-md.md)屬性。  
  
-   計算的子系**成員**具有[ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)屬性。  
  
-   使用標準的 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)來取得有關的其他資訊的集合**層級**物件。  
  
 使用集合和屬性的**成員**的**位置**沿著[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)，您可以執行下列動作：  
  
-   找出**成員**具有[名稱](../../../ado/reference/ado-md-api/name-property-ado-md.md)並[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性。  
  
-   傳回的字串顯示時，使用**成員**具有[標題](../../../ado/reference/ado-md-api/caption-property-ado-md.md)屬性。  
  
-   傳回有意義的字串，描述量值或公式**成員**具有[描述](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性。  
  
-   取得相關資訊**層級**的**成員**具有[LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md)並[LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md)屬性。  
  
-   計算的子系**成員**具有[ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)屬性。  
  
-   使用[DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md)屬性來判斷上是否有至少一個子系**軸**緊接這個**成員**。  
  
-   使用[ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)屬性來判斷是否這個父**成員**立即先前的父代相同**成員**。  
  
-   使用標準的 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)來取得有關的其他資訊的集合**層級**物件。  
  
 **屬性**集合包含提供者提供的屬性。 下表列出可用的屬性。 實際的屬性清單可能與不同的提供者實作而定。 請參閱您的提供者，如需更完整清單的可用屬性的文件。  
  
|名稱|描述|  
|----------|-----------------|  
|CatalogName|這個 cube 所屬的目錄名稱。|  
|ChildrenCardinality|成員擁有的子系數目。|  
|CubeName|Cube 的名稱。|  
|描述|成員有意義描述。|  
|DimensionUniqueName|模稜兩可的名稱[維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)。|  
|HierarchyUniqueName|階層的模稜兩可的名稱。|  
|LevelNumber|層級與階層的根之間的距離。|  
|LevelUniqueName|層級的模稜兩可的名稱。|  
|MemberCaption|與該成員關聯的標籤或標題。|  
|MemberGUID|成員的 GUID。|  
|MemberName|成員的名稱。|  
|MemberOrdinal|成員的序數。|  
|MemberType|成員的類型。|  
|MemberUniqueName|成員模稜兩可的名稱。|  
|ParentCount|這個成員的父系數目計數。|  
|ParentLevel|成員的父層級數目。|  
|ParentUniqueName|成員的父系模稜兩可的名稱。|  
|SchemaName|這個 cube 所屬的結構描述名稱。|  
  
 本章節包含下列主題。  
  
-   [屬性、 方法和事件](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Catalog 範例 (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Members 集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
