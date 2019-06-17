---
title: Hierarchy 物件 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Hierarchy
helpviewer_keywords:
- Hierarchy object [ADO MD]
ms.assetid: 034af340-ac79-494e-ba5e-2b57da1cb9de
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5915102164afccd8e2055e14d0ef9d63b2cf5937
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66709143"
---
# <a name="hierarchy-object-ado-md"></a>Hierarchy 物件 (ADO MD)
提供一種方法，在其中的成員[維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)可以彙總或 「 彙總 」。 維度可以加以彙總一或多個階層。  
  
## <a name="remarks"></a>備註  
 使用集合和屬性的**階層**物件時，您可以執行下列動作：  
  
-   找出**階層**具有[名稱](../../../ado/reference/ado-md-api/name-property-ado-md.md)並[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性。  
  
-   傳回有意義的字串，描述**階層**具有[描述](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性。  
  
-   傳回[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)構成物件**階層**具有[層級](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)集合。  
  
-   使用標準的 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)來取得有關的其他資訊的集合**階層**物件。  
  
 **屬性**集合包含提供者提供的屬性。 下表列出可用的屬性。 實際的屬性清單可能與不同的提供者實作而定。 請參閱您的提供者，如需更完整清單的可用屬性的文件。  
  
|名稱|描述|  
|----------|-----------------|  
|AllMember|最高層級的彙總套件階層架構中的成員。|  
|CatalogName|這個 cube 所屬的目錄名稱。|  
|CubeName|Cube 的名稱。|  
|DefaultMember|此階層的預設成員唯一名稱。|  
|描述|階層的有意義描述。|  
|DimensionType|此階層所屬的維度的類型。|  
|DimensionUniqueName|維度的模稜兩可的名稱。|  
|HierarchyCaption|與階層關聯的標籤或標題。|  
|HierarchyCardinality|階層中的成員數目。|  
|HierarchyGUID|階層的 GUID。|  
|HierarchyName|階層的名稱。|  
|HierarchyUniqueName|階層的模稜兩可的名稱。|  
|SchemaName|這個 cube 所屬的結構描述名稱。|  
  
 本章節包含下列主題。  
  
-   [屬性、 方法和事件](../../../ado/reference/ado-md-api/hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [CubeDef 範例 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [維度物件 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [Hierarchies 集合 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Levels 集合 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
