---
description: Member 物件 (ADO MD)
title: " (ADO MD) 的成員物件 |Microsoft Docs"
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
ms.openlocfilehash: 6e0797a4d273c51b950e3973d1864480755a20d1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440920"
---
# <a name="member-object-ado-md"></a>Member 物件 (ADO MD)
表示 cube 中層級的成員、層級成員的子系，或是沿著資料格集軸的位置成員。  
  
## <a name="remarks"></a>備註  
 **成員**的屬性會根據使用它的內容而有所不同。 [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)中[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)的**成員**具有[子](../../../ado/reference/ado-md-api/children-property-ado-md.md)系屬性，可從目前的**成員**傳回階層中下一個較低層級的**成員**。 若為某個[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)的**成員**，**子**集合一律為空白。 此外， [Type](../../../ado/reference/ado-md-api/type-property-ado-md.md)屬性只適用于**層級**的**成員**。  
  
 **Position**的**成員**有兩個屬性，在顯示[儲存格格](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)時很有用： [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md)和[ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)。 如果在**層級**的**成員**上存取這些屬性，就會發生錯誤。  
  
 使用**層級**之**成員**物件的集合和屬性，您可以執行下列動作：  
  
-   識別具有[Name](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性的**成員**。  
  
-   傳回使用[Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md)屬性顯示**成員**時所要使用的字串。  
  
-   傳回以[Description](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性描述量值或公式**成員**的有意義字串。  
  
-   使用[Type](../../../ado/reference/ado-md-api/type-property-ado-md.md)屬性判斷**成員**的本質。  
  
-   使用[LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md)和[LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md)屬性取得**成員****層級**的相關資訊。  
  
-   取得具有[父系](../../../ado/reference/ado-md-api/parent-property-ado-md.md)和[子](../../../ado/reference/ado-md-api/children-property-ado-md.md)系屬性之階層[中的相關](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)**成員**。  
  
-   使用[ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)屬性計算**成員**的子系。  
  
-   您可以使用標準 ADO [屬性](../../../ado/reference/ado-api/properties-collection-ado.md) 集合來取得 **層級** 物件的其他資訊。  
  
 透過[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)上某個**位置****成員**的集合和屬性，您可以執行下列動作：  
  
-   識別具有[Name](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性的**成員**。  
  
-   傳回使用[Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md)屬性顯示**成員**時所要使用的字串。  
  
-   傳回以[Description](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性描述量值或公式**成員**的有意義字串。  
  
-   使用[LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md)和[LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md)屬性取得**成員****層級**的相關資訊。  
  
-   使用[ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)屬性計算**成員**的子系。  
  
-   您可以使用[DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md)屬性來判斷緊接在這個**成員**後面的**座標軸**上是否至少有一個子系。  
  
-   您可以使用 [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md) 屬性來判斷這個 **成員** 的父系是否與前一個 **成員**的父系相同。  
  
-   您可以使用標準 ADO [屬性](../../../ado/reference/ado-api/properties-collection-ado.md) 集合來取得 **層級** 物件的其他資訊。  
  
 **Properties**集合包含提供者提供的屬性。 下表列出可能可用的屬性。 實際的屬性清單可能會因提供者的執行而有所不同。 如需可用屬性的完整清單，請參閱提供者的檔。  
  
|名稱|描述|  
|----------|-----------------|  
|CatalogName|此 cube 所屬之目錄的名稱。|  
|ChildrenCardinality|成員擁有的子系數目。|  
|CubeName|Cube 的名稱。|  
|描述|成員的有意義描述。|  
|DimensionUniqueName|[維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)的明確名稱。|  
|HierarchyUniqueName|階層的明確名稱。|  
|LevelNumber|階層的層級和根目錄之間的距離。|  
|LevelUniqueName|層級的明確名稱。|  
|MemberCaption|與該成員關聯的標籤或標題。|  
|MemberGUID|成員的 GUID。|  
|MemberName|成員的名稱。|  
|MemberOrdinal|成員的序數。|  
|MemberType|成員的類型。|  
|MemberUniqueName|成員的明確名稱。|  
|ParentCount|這個成員擁有的父系數目計數。|  
|ParentLevel|成員父系的層級編號。|  
|ParentUniqueName|成員父系的明確名稱。|  
|SchemaName|此 cube 所屬的架構名稱。|  
  
 本節包含下列主題。  
  
-   [屬性、方法和事件](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的目錄範例 ](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [成員集合 (ADO MD) ](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
