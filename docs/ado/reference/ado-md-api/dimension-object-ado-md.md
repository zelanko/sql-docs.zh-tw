---
title: 維度物件 (ADO MD) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: f69acfa84272e73bcafb370eb85c6a14614a367c
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709441"
---
# <a name="dimension-object-ado-md"></a>Dimension 物件 (ADO MD)
代表其中一個維度的多維度 cube，其中包含一或多個階層的成員。  
  
## <a name="remarks"></a>備註  
 使用集合和屬性的**維度**物件時，您可以執行下列動作：  
  
-   找出**維度**具有[名稱](../../../ado/reference/ado-md-api/name-property-ado-md.md)並[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性。  
  
-   傳回有意義的字串，描述**維度**具有[描述](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性。  
  
-   傳回[階層](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)構成物件**維度**具有[階層](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)集合。  
  
-   使用標準的 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)來取得有關的其他資訊的集合**維度**物件。  
  
 **屬性**集合包含提供者提供的屬性。 下表列出可用的屬性。 實際的屬性清單可能與不同的提供者實作而定。 請參閱您的提供者，如需更完整清單的可用屬性的文件。  
  
|名稱|描述|  
|----------|-----------------|  
|CatalogName|這個 cube 所屬的目錄名稱。|  
|CubeName|Cube 的名稱。|  
|DefaultHierarchy|預設階層的唯一名稱。|  
|描述|Cube 有意義描述。|  
|DimensionCaption|標籤或標題與維度相關聯。|  
|DimensionCardinality|在維度中的成員數目。|  
|DimensionGUID|維度的 GUID。|  
|DimensionName|維度的名稱。|  
|DimensionOrdinal|維度的構成 cube 的維度群組之間的序數。|  
|DimensionType|維度類型。|  
|DimensionUniqueName|維度的模稜兩可的名稱。|  
|SchemaName|這個 cube 所屬的結構描述名稱。|  
  
 本章節包含下列主題。  
  
-   [屬性、 方法和事件](../../../ado/reference/ado-md-api/dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [CubeDef 範例 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [CubeDef 物件 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)   
 [Dimensions 集合 (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Hierarchies 集合 (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
