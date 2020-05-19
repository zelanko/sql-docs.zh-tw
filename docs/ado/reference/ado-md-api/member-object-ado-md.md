---
title: 成員物件（ADO MD） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: d4d512d651c8162124c935ffdb260c4abe4ecb14
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82753202"
---
# <a name="member-object-ado-md"></a>Member 物件 (ADO MD)
代表 cube 中層級的成員、層級成員的子系，或沿著資料格集軸之位置的成員。  
  
## <a name="remarks"></a>備註  
 **成員**的屬性會根據其使用的內容而有所不同。 在[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)中，[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)的**成員**具有[子](../../../ado/reference/ado-md-api/children-property-ado-md.md)屬性，會從目前**成員**傳回階層中下一個較低層級的**成員**。 對於[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)的**成員**而言，**子**集合一律是空的。 此外， [Type](../../../ado/reference/ado-md-api/type-property-ado-md.md)屬性僅適用于**層級**的**成員**。  
  
 **Position**的**成員**有兩個屬性，在顯示[儲存格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)時很有用： [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md)和[ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)。 如果在**層級**的**成員**上存取這些屬性，則會發生錯誤。  
  
 使用**層級****成員**物件的集合和屬性，您可以執行下列動作：  
  
-   使用[Name](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性來識別**成員**。  
  
-   傳回要在使用[Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md)屬性顯示**成員**時使用的字串。  
  
-   傳回有意義的字串，其中描述具有[Description](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性的量值或公式**成員**。  
  
-   使用[Type](../../../ado/reference/ado-md-api/type-property-ado-md.md)屬性判斷**成員**的本質。  
  
-   使用[LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md)和[LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md)屬性取得**成員****層級**的相關資訊。  
  
-   取得階層中具有[父系](../../../ado/reference/ado-md-api/parent-property-ado-md.md)和[子](../../../ado/reference/ado-md-api/children-property-ado-md.md)系[屬性的相關](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)**成員**。  
  
-   使用[ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)屬性計算**成員**的子系。  
  
-   使用標準 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合來取得有關**層級**物件的其他資訊。  
  
 透過[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)上某個**位置****成員**的集合和屬性，您可以執行下列動作：  
  
-   使用[Name](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性來識別**成員**。  
  
-   傳回要在使用[Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md)屬性顯示**成員**時使用的字串。  
  
-   傳回有意義的字串，其中描述具有[Description](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性的量值或公式**成員**。  
  
-   使用[LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md)和[LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md)屬性取得**成員****層級**的相關資訊。  
  
-   使用[ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)屬性計算**成員**的子系。  
  
-   使用[DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md)屬性，判斷在此**成員**之後的**軸**上是否至少有一個子系。  
  
-   使用[ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)屬性來判斷這個**成員**的父系是否與緊接在**成員**前面的父系相同。  
  
-   使用標準 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合來取得有關**層級**物件的其他資訊。  
  
 **Properties**集合包含提供者提供的屬性。 下表列出可能可用的屬性。 實際的屬性清單可能會根據提供者的執行而有所不同。 如需可用屬性的完整清單，請參閱提供者的檔。  
  
|Name|描述|  
|----------|-----------------|  
|CatalogName|這個 cube 所屬的目錄名稱。|  
|ChildrenCardinality|成員擁有的子系數目。|  
|CubeName|Cube 的名稱。|  
|描述|成員的有意義描述。|  
|DimensionUniqueName|[維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)的明確名稱。|  
|HierarchyUniqueName|階層的明確名稱。|  
|LevelNumber|層級和階層根之間的距離。|  
|LevelUniqueName|層級的明確名稱。|  
|MemberCaption|與該成員關聯的標籤或標題。|  
|MemberGUID|成員的 GUID。|  
|MemberName|成員的名稱。|  
|MemberOrdinal|成員的序數。|  
|MemberType|成員的類型。|  
|MemberUniqueName|成員的明確名稱。|  
|ParentCount|這個成員具有的父系數目計數。|  
|ParentLevel|成員父系的層級編號。|  
|ParentUniqueName|成員父系的明確名稱。|  
|SchemaName|這個 cube 所屬的架構名稱。|  
  
 本章節包含下列主題。  
  
-   [屬性、方法和事件](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Catalog 範例（VB）](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Members 集合（ADO MD）](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
