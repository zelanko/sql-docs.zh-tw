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
ms.openlocfilehash: c53b22dc0b5129fc822c4a012eefcf99041f5b45
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777997"
---
# <a name="member-object-ado-md"></a>Member 物件 (ADO MD)
表示 cube 中層級的成員、層級成員的子系，或是沿著資料格集軸的位置成員。  
  
## <a name="remarks"></a>備註  
 **成員**的屬性會根據使用它的內容而有所不同。 [CubeDef](./cubedef-object-ado-md.md)中[層級](./level-object-ado-md.md)的**成員**具有[子](./children-property-ado-md.md)系屬性，可從目前的**成員**傳回階層中下一個較低層級的**成員**。 若為某個[位置](./position-object-ado-md.md)的**成員**，**子**集合一律為空白。 此外， [Type](./type-property-ado-md.md)屬性只適用于**層級**的**成員**。  
  
 **Position**的**成員**有兩個屬性，在顯示[儲存格格](./cellset-object-ado-md.md)時很有用： [DrilledDown](./drilleddown-property-ado-md.md)和[ParentSameAsPrev](./parentsameasprev-property-ado-md.md)。 如果在**層級**的**成員**上存取這些屬性，就會發生錯誤。  
  
 使用**層級**之**成員**物件的集合和屬性，您可以執行下列動作：  
  
-   識別具有[Name](./name-property-ado-md.md)和[UniqueName](./uniquename-property-ado-md.md)屬性的**成員**。  
  
-   傳回使用[Caption](./caption-property-ado-md.md)屬性顯示**成員**時所要使用的字串。  
  
-   傳回以[Description](./description-property-ado-md.md)屬性描述量值或公式**成員**的有意義字串。  
  
-   使用[Type](./type-property-ado-md.md)屬性判斷**成員**的本質。  
  
-   使用[LevelDepth](./leveldepth-property-ado-md.md)和[LevelName](./levelname-property-ado-md.md)屬性取得**成員****層級**的相關資訊。  
  
-   取得具有[父系](./parent-property-ado-md.md)和[子](./children-property-ado-md.md)系屬性之階層[中的相關](./hierarchy-object-ado-md.md)**成員**。  
  
-   使用[ChildCount](./childcount-property-ado-md.md)屬性計算**成員**的子系。  
  
-   您可以使用標準 ADO [屬性](../ado-api/properties-collection-ado.md) 集合來取得 **層級** 物件的其他資訊。  
  
 透過[軸](./axis-object-ado-md.md)上某個**位置****成員**的集合和屬性，您可以執行下列動作：  
  
-   識別具有[Name](./name-property-ado-md.md)和[UniqueName](./uniquename-property-ado-md.md)屬性的**成員**。  
  
-   傳回使用[Caption](./caption-property-ado-md.md)屬性顯示**成員**時所要使用的字串。  
  
-   傳回以[Description](./description-property-ado-md.md)屬性描述量值或公式**成員**的有意義字串。  
  
-   使用[LevelDepth](./leveldepth-property-ado-md.md)和[LevelName](./levelname-property-ado-md.md)屬性取得**成員****層級**的相關資訊。  
  
-   使用[ChildCount](./childcount-property-ado-md.md)屬性計算**成員**的子系。  
  
-   您可以使用[DrilledDown](./drilleddown-property-ado-md.md)屬性來判斷緊接在這個**成員**後面的**座標軸**上是否至少有一個子系。  
  
-   您可以使用 [ParentSameAsPrev](./parentsameasprev-property-ado-md.md) 屬性來判斷這個 **成員** 的父系是否與前一個 **成員**的父系相同。  
  
-   您可以使用標準 ADO [屬性](../ado-api/properties-collection-ado.md) 集合來取得 **層級** 物件的其他資訊。  
  
 **Properties**集合包含提供者提供的屬性。 下表列出可能可用的屬性。 實際的屬性清單可能會因提供者的執行而有所不同。 如需可用屬性的完整清單，請參閱提供者的檔。  
  
|Name|描述|  
|----------|-----------------|  
|CatalogName|此 cube 所屬之目錄的名稱。|  
|ChildrenCardinality|成員擁有的子系數目。|  
|CubeName|Cube 的名稱。|  
|描述|成員的有意義描述。|  
|DimensionUniqueName|[維度](./dimension-object-ado-md.md)的明確名稱。|  
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
  
-   [屬性、方法和事件](./member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的目錄範例 ](./catalog-example-vb.md)   
 [成員集合 (ADO MD) ](./members-collection-ado-md.md)   
 [Properties 集合 (ADO)](../ado-api/properties-collection-ado.md)