---
title: Dimension 物件（ADO MD） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Dimension
helpviewer_keywords:
- Dimension object [ADO MD]
ms.assetid: 66adbbd2-23a3-4c19-a91b-84c31309aa1b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f7a13ad87d56f5e7855070d8fe577bb408d6ce9e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67938532"
---
# <a name="dimension-object-ado-md"></a>Dimension 物件 (ADO MD)
表示多維度 cube 的其中一個維度，其中包含一或多個成員的階層。  
  
## <a name="remarks"></a>備註  
 使用**維度**物件的集合和屬性，您可以執行下列動作：  
  
-   識別具有[Name](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性的**維度**。  
  
-   傳回有意義的字串，其中描述具有[Description](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性的**維度**。  
  
-   傳回使用[階層集合組成](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)**維度**[的階層物件。](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)  
  
-   使用標準 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合來取得有關**維度**物件的其他資訊。  
  
 **Properties**集合包含提供者提供的屬性。 下表列出可能可用的屬性。 實際的屬性清單可能會根據提供者的執行而有所不同。 如需可用屬性的完整清單，請參閱提供者的檔。  
  
|名稱|描述|  
|----------|-----------------|  
|CatalogName|這個 cube 所屬的目錄名稱。|  
|CubeName|Cube 的名稱。|  
|DefaultHierarchy|預設階層的唯一名稱。|  
|描述|Cube 的有意義描述。|  
|DimensionCaption|與維度相關聯的標籤或標題。|  
|DimensionCardinality|維度中的成員數目。|  
|DimensionGUID|維度的 GUID。|  
|DimensionName|維度的名稱。|  
|DimensionOrdinal|形成 cube 的維度群組之間的維度序號。|  
|DimensionType|維度類型。|  
|DimensionUniqueName|維度的明確名稱。|  
|SchemaName|這個 cube 所屬的架構名稱。|  
  
 本章節包含下列主題。  
  
-   [屬性、方法和事件](../../../ado/reference/ado-md-api/dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [CubeDef 範例（VBScript）](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [CubeDef 物件（ADO MD）](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)   
 [維度集合（ADO MD）](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [階層集合（ADO MD）](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
