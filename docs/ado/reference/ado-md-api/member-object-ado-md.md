---
title: "成員物件 (ADO MD) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Member
helpviewer_keywords:
- Member object [ADO MD], members
ms.assetid: 3dedf755-0741-4c3f-8b4e-bff8ff8809c8
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ca510493f83f7cfcc97b37586c1e26aee7c3ab24
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="member-object-ado-md"></a>成員物件 (ADO MD)
代表在 cube 中，層級成員的層級、 成員或成員的資料格集沿座標軸的位置的子系。  
  
## <a name="remarks"></a>備註  
 內容**成員**使用它的內容而有所不同。 A**成員**的[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)中[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)具有[子系](../../../ado/reference/ado-md-api/children-property-ado-md.md)屬性，傳回**成員**上從目前階層中的下一層**成員**。 如**成員**的[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)、**子系**永遠是空的集合。 此外，[類型](../../../ado/reference/ado-md-api/type-property-ado-md.md)屬性僅適用於**成員**的**層級**。  
  
 A**成員**的**位置**有兩個屬性顯示時非常實用[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md): [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md)和[ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)。 如果上存取這些屬性，會發生錯誤**成員**的**層級**。  
  
 集合與屬性**成員**物件**層級**，您可以執行下列：  
  
-   識別**成員**與[名稱](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性。  
  
-   傳回的字串顯示時，使用**成員**與[標題](../../../ado/reference/ado-md-api/caption-property-ado-md.md)屬性。  
  
-   傳回有意義的字串，其中描述量值或公式**成員**與[描述](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性。  
  
-   判斷的本質**成員**與[類型](../../../ado/reference/ado-md-api/type-property-ado-md.md)屬性。  
  
-   取得相關資訊**層級**的**成員**與[LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md)和[LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md)屬性。  
  
-   取得相關**成員**中[階層](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)與[父](../../../ado/reference/ado-md-api/parent-property-ado-md.md)和[子系](../../../ado/reference/ado-md-api/children-property-ado-md.md)屬性。  
  
-   計算的子系**成員**與[ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)屬性。  
  
-   使用標準的 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，以取得其他資訊有關**層級**物件。  
  
 集合與屬性**成員**的**位置**沿著[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)，您可以執行下列：  
  
-   識別**成員**與[名稱](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性。  
  
-   傳回的字串顯示時，使用**成員**與[標題](../../../ado/reference/ado-md-api/caption-property-ado-md.md)屬性。  
  
-   傳回有意義的字串，其中描述量值或公式**成員**與[描述](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性。  
  
-   取得相關資訊**層級**的**成員**與[LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md)和[LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md)屬性。  
  
-   計算的子系**成員**與[ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)屬性。  
  
-   使用[DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md)屬性來判斷是否有至少一個子系上**軸**緊接這**成員**。  
  
-   使用[ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)屬性來判斷是否的父系**成員**立即先前的父系相同**成員**。  
  
-   使用標準的 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，以取得其他資訊有關**層級**物件。  
  
 **屬性**集合包含提供者提供的屬性。 下表列出可供使用的屬性。 實際的屬性清單可能與不同的提供者實作而定。 請參閱您的提供者，如需更完整清單可用內容的文件。  
  
|名稱|Description|  
|----------|-----------------|  
|CatalogName|此 cube 所屬的目錄的名稱。|  
|ChildrenCardinality|成員擁有的子系數目。|  
|CubeName|Cube 的名稱。|  
|Description|成員有意義的描述。|  
|DimensionUniqueName|模稜兩可的名稱[維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)。|  
|HierarchyUniqueName|階層的模稜兩可的名稱。|  
|LevelNumber|之間的層級和階層的根的距離。|  
|了 LevelUniqueName|層級的模稜兩可的名稱。|  
|MemberCaption|與該成員關聯的標籤或標題。|  
|MemberGUID|成員的 GUID。|  
|MemberName|成員的名稱。|  
|MemberOrdinal|成員的序號。|  
|MemberType|成員的類型。|  
|MemberUniqueName|成員模稜兩可的名稱。|  
|ParentCount|這個成員的父系數目計數。|  
|ParentLevel|成員的父層級數目。|  
|ParentUniqueName|成員的父系模稜兩可的名稱。|  
|SchemaName|此 cube 所屬的結構描述名稱。|  
  
 本章節包含下列主題。  
  
-   [屬性、 方法和事件](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [目錄 (VB) 範例](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [成員集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)

