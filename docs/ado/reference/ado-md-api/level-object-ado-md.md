---
title: Level 物件（ADO MD） |Microsoft Docs
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
ms.openlocfilehash: 4a44060ae4ffd9399c34d4cd8133f5ad7404ed5a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949606"
---
# <a name="level-object-ado-md"></a>Level 物件 (ADO MD)
包含一組成員，其中每一個都在階層內具有相同的次序。  
  
## <a name="remarks"></a>備註  
 使用**Level**物件的集合和屬性，您可以執行下列動作：  
  
-   使用[Name](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性來識別**層級**。  
  
-   傳回搭配[Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md)屬性顯示**層級**時所要使用的字串。  
  
-   傳回有意義的字串，其中描述具有[Description](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性的**層級**。  
  
-   傳回以[成員](../../../ado/reference/ado-md-api/members-collection-ado-md.md)集合組成**層級**的[成員](../../../ado/reference/ado-md-api/member-object-ado-md.md)物件。  
  
-   傳回具有[Depth](../../../ado/reference/ado-md-api/depth-property-ado-md.md)屬性之**層級**根的層級數目。  
  
-   使用標準 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合來取得有關**層級**物件的其他資訊。  
  
 **Properties**集合包含提供者提供的屬性。 下表列出可能可用的屬性。 實際的屬性清單可能會根據提供者的執行而有所不同。 如需可用屬性的完整清單，請參閱提供者的檔。  
  
|名稱|描述|  
|----------|-----------------|  
|CatalogName|這個 cube 所屬的目錄名稱。|  
|CubeName|Cube 的名稱。|  
|描述|層級有意義的描述。|  
|DimensionUniqueName|[維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)的明確名稱。|  
|HierarchyUniqueName|階層的明確名稱。|  
|LevelCaption|與層級相關聯的標籤或標題。|  
|LevelCardinality|層級中的成員數目。|  
|LevelGUID|層級的 GUID。|  
|LevelName|層級的名稱。|  
|LevelNumber|層級和階層根之間的距離。|  
|LevelType|層級的類型。|  
|LevelUniqueName|層級的明確名稱。|  
|SchemaName|這個 cube 所屬的架構名稱。|  
  
 本章節包含下列主題。  
  
-   [屬性、方法和事件](../../../ado/reference/ado-md-api/level-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [CubeDef 範例（VBScript）](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [階層物件（ADO MD）](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)   
 [層級集合（ADO MD）](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Members 集合（ADO MD）](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
