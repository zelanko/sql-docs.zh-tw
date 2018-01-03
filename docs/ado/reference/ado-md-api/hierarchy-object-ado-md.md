---
title: "Hierarchy 物件 (ADO MD) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Hierarchy
helpviewer_keywords: Hierarchy object [ADO MD]
ms.assetid: 034af340-ac79-494e-ba5e-2b57da1cb9de
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0802ae503911ec8b84ee2f01b15de9ed7f57c4af
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="hierarchy-object-ado-md"></a>Hierarchy 物件 (ADO MD)
提供一種方法中的成員[維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)可以彙總或 「 彙總 」。 維度可彙總一或多個階層中。  
  
## <a name="remarks"></a>備註  
 集合與屬性**階層**物件，您可以執行下列：  
  
-   識別**階層**與[名稱](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性。  
  
-   傳回有意義的字串描述**階層**與[描述](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性。  
  
-   傳回[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)構成物件**階層**與[層級](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)集合。  
  
-   使用標準的 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，以取得其他資訊有關**階層**物件。  
  
 **屬性**集合包含提供者提供的屬性。 下表列出可供使用的屬性。 實際的屬性清單可能與不同的提供者實作而定。 請參閱您的提供者，如需更完整清單可用內容的文件。  
  
|[屬性]|描述|  
|----------|-----------------|  
|AllMember|彙總套件階層架構中的最高的層級成員。|  
|CatalogName|此 cube 所屬的目錄的名稱。|  
|CubeName|Cube 的名稱。|  
|DefaultMember|此階層的預設成員唯一名稱。|  
|描述|階層有意義的描述。|  
|DimensionType|此階層所屬的維度的類型。|  
|DimensionUniqueName|維度的模稜兩可的名稱。|  
|HierarchyCaption|與階層關聯的標籤或標題。|  
|HierarchyCardinality|階層中的成員數目。|  
|HierarchyGUID|階層的 GUID。|  
|HierarchyName|階層的名稱。|  
|HierarchyUniqueName|階層的模稜兩可的名稱。|  
|SchemaName|此 cube 所屬的結構描述名稱。|  
  
 本章節包含下列主題。  
  
-   [屬性、 方法和事件](../../../ado/reference/ado-md-api/hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>請參閱  
 [CubeDef 範例 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [維度物件 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [Hierarchies 集合 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [層級集合 (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
