---
title: 層級物件 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level
helpviewer_keywords:
- Level object [ADO MD]
ms.assetid: 37815869-ed30-45fd-9aea-0a986c1b305c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 27e789c4eb34ed275d6f18f62325287febb73422
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734556"
---
# <a name="level-object-ado-md"></a>Level 物件 (ADO MD)
包含一組成員，每個都有相同的陣序，在階層中。  
  
## <a name="remarks"></a>備註  
 使用集合和屬性的**層級**物件時，您可以執行下列動作：  
  
-   找出**層級**具有[名稱](../../../ado/reference/ado-md-api/name-property-ado-md.md)並[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性。  
  
-   傳回的字串顯示時，使用**層級**具有[標題](../../../ado/reference/ado-md-api/caption-property-ado-md.md)屬性。  
  
-   傳回有意義的字串，描述**層級**具有[描述](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性。  
  
-   傳回[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)構成物件**層級**具有[成員](../../../ado/reference/ado-md-api/members-collection-ado-md.md)集合。  
  
-   傳回的根層級數目**層級**具有[深度](../../../ado/reference/ado-md-api/depth-property-ado-md.md)屬性。  
  
-   使用標準的 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)來取得有關的其他資訊的集合**層級**物件。  
  
 **屬性**集合包含提供者提供的屬性。 下表列出可用的屬性。 實際的屬性清單可能與不同的提供者實作而定。 請參閱您的提供者，如需更完整清單的可用屬性的文件。  
  
|名稱|描述|  
|----------|-----------------|  
|CatalogName|這個 cube 所屬的目錄名稱。|  
|CubeName|Cube 的名稱。|  
|描述|層級的有意義描述。|  
|DimensionUniqueName|模稜兩可的名稱[維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)。|  
|HierarchyUniqueName|階層的模稜兩可的名稱。|  
|LevelCaption|標籤或層級相關聯的標題。|  
|LevelCardinality|層級中的成員數目。|  
|LevelGUID|層級的 GUID。|  
|LevelName|層級的名稱。|  
|LevelNumber|層級與階層的根之間的距離。|  
|LevelType|層級的型別。|  
|LevelUniqueName|層級的模稜兩可的名稱。|  
|SchemaName|這個 cube 所屬的結構描述名稱。|  
  
 本章節包含下列主題。  
  
-   [屬性、 方法和事件](../../../ado/reference/ado-md-api/level-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [CubeDef 範例 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Hierarchy 物件 (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)   
 [Levels 集合 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Members 集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
