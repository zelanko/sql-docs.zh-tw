---
description: Dimension 物件 (ADO MD)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 73feb1e20320a418804666e11cb2410ab4451c52
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778197"
---
# <a name="dimension-object-ado-md"></a>Dimension 物件 (ADO MD)
表示多維度 cube 的其中一個維度，其中包含一或多個成員階層。  
  
## <a name="remarks"></a>備註  
 使用 **維度** 物件的集合和屬性，您可以執行下列動作：  
  
-   識別具有[Name](./name-property-ado-md.md)和[UniqueName](./uniquename-property-ado-md.md)屬性的**維度**。  
  
-   傳回描述具有[Description](./description-property-ado-md.md)屬性之**維度**的有意義字串。  
  
-   傳回組成**維度**[集合的階層物件。](./hierarchy-object-ado-md.md) [Hierarchies](./hierarchies-collection-ado-md.md)  
  
-   您可以使用標準 ADO [屬性](../ado-api/properties-collection-ado.md) 集合，取得有關 **維度** 物件的其他資訊。  
  
 **Properties**集合包含提供者提供的屬性。 下表列出可能可用的屬性。 實際的屬性清單可能會因提供者的執行而有所不同。 如需可用屬性的完整清單，請參閱提供者的檔。  
  
|Name|描述|  
|----------|-----------------|  
|CatalogName|此 cube 所屬之目錄的名稱。|  
|CubeName|Cube 的名稱。|  
|DefaultHierarchy|預設階層的唯一名稱。|  
|描述|Cube 的有意義描述。|  
|DimensionCaption|與維度相關聯的標籤或標題。|  
|DimensionCardinality|維度中的成員數目。|  
|DimensionGUID|維度的 GUID。|  
|DimensionName|維度名稱。|  
|DimensionOrdinal|形成 cube 的維度群組之間的維度序號。|  
|DimensionType|維度類型。|  
|DimensionUniqueName|維度的明確名稱。|  
|SchemaName|此 cube 所屬的架構名稱。|  
  
 本節包含下列主題。  
  
-   [屬性、方法和事件](./dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [CubeDef 範例 (VBScript) ](./cubedef-example-vbscript.md)   
 [CubeDef 物件 (ADO MD) ](./cubedef-object-ado-md.md)   
 [維度集合 (ADO MD) ](./dimensions-collection-ado-md.md)   
 [階層集合 (ADO MD) ](./hierarchies-collection-ado-md.md)   
 [Properties 集合 (ADO)](../ado-api/properties-collection-ado.md)