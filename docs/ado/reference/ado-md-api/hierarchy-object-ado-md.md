---
title: 階層物件（ADO MD） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1232d228d597188364cb20a7f60dfaa11c8af21a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82753963"
---
# <a name="hierarchy-object-ado-md"></a>Hierarchy 物件 (ADO MD)
表示[維度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)成員可以匯總或「匯總」的一種方式。 維度可以沿著一或多個階層匯總。  
  
## <a name="remarks"></a>備註  
 使用**階層物件的**集合和屬性，您可以執行下列動作：  
  
-   **使用** [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性來識別階層。  
  
-   傳回有意義的字串，其中**描述具有** [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性的階層。  
  
-   傳回組成階層的[層級](../../../ado/reference/ado-md-api/level-object-ado-md.md)物件，**其具有**[層](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)級集合。  
  
-   使用標準 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合來取得有關**階層物件的**其他資訊。  
  
 **Properties**集合包含提供者提供的屬性。 下表列出可能可用的屬性。 實際的屬性清單可能會根據提供者的執行而有所不同。 如需可用屬性的完整清單，請參閱提供者的檔。  
  
|Name|說明|  
|----------|-----------------|  
|AllMember|階層中匯總最高層級的成員。|  
|CatalogName|這個 cube 所屬的目錄名稱。|  
|CubeName|Cube 的名稱。|  
|DefaultMember|這個階層之預設成員的唯一名稱。|  
|說明|階層的有意義描述。|  
|DimensionType|此階層所屬的維度類型。|  
|DimensionUniqueName|維度的明確名稱。|  
|HierarchyCaption|與階層關聯的標籤或標題。|  
|HierarchyCardinality|階層中的成員數目。|  
|HierarchyGUID|階層的 GUID。|  
|HierarchyName|階層的名稱。|  
|HierarchyUniqueName|階層的明確名稱。|  
|SchemaName|這個 cube 所屬的架構名稱。|  
  
 本章節包含下列主題。  
  
-   [屬性、方法和事件](../../../ado/reference/ado-md-api/hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [CubeDef 範例（VBScript）](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Dimension 物件（ADO MD）](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [階層集合（ADO MD）](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [層級集合（ADO MD）](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
