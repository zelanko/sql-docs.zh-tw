---
title: 層級物件 (ADO MD) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Level
helpviewer_keywords:
- Level object [ADO MD]
ms.assetid: 37815869-ed30-45fd-9aea-0a986c1b305c
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 02a1a7e433c13c52db6c1e9112437470769c76be
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="level-object-ado-md"></a>層級物件 (ADO MD)
包含一組成員，每一個都有相同的陣序，在階層中。  
  
## <a name="remarks"></a>備註  
 集合與屬性**層級**物件，您可以執行下列：  
  
-   識別**層級**與[名稱](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性。  
  
-   傳回的字串顯示時，使用**層級**與[標題](../../../ado/reference/ado-md-api/caption-property-ado-md.md)屬性。  
  
-   傳回有意義的字串描述**層級**與[描述](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性。  
  
-   傳回[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)構成物件**層級**與[成員](../../../ado/reference/ado-md-api/members-collection-ado-md.md)集合。  
  
-   傳回層級數目的根目錄**層級**與[深度](../../../ado/reference/ado-md-api/depth-property-ado-md.md)屬性。  
  
-   使用標準的 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，以取得其他資訊有關**層級**物件。  
  
 **屬性**集合包含提供者提供的屬性。 下表列出可供使用的屬性。 實際的屬性清單可能與不同的提供者實作而定。 請參閱您的提供者，如需更完整清單可用內容的文件。  
  
|名稱|Description|  
|----------|-----------------|  
|CatalogName|此 cube 所屬的目錄的名稱。|  
|CubeName|Cube 的名稱。|  
|Description|層級有意義的描述。|  
|DimensionUniqueName|模稜兩可的名稱[維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)。|  
|HierarchyUniqueName|階層的模稜兩可的名稱。|  
|LevelCaption|標籤或層級相關聯的標題。|  
|LevelCardinality|層級中的成員數目。|  
|LevelGUID|層級的 GUID。|  
|LevelName|層級的名稱。|  
|LevelNumber|之間的層級和階層的根的距離。|  
|LevelType|層級的類型。|  
|LevelUniqueName|層級的模稜兩可的名稱。|  
|SchemaName|此 cube 所屬的結構描述名稱。|  
  
 本章節包含下列主題。  
  
-   [屬性、 方法和事件](../../../ado/reference/ado-md-api/level-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [CubeDef 範例 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Hierarchy 物件 (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)   
 [層級集合 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [成員集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
