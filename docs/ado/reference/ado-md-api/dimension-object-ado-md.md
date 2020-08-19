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
ms.openlocfilehash: fc3661ef36c0b763ca6b0f04f52e4713d59b9a19
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441110"
---
# <a name="dimension-object-ado-md"></a>Dimension 物件 (ADO MD)
表示多維度 cube 的其中一個維度，其中包含一或多個成員階層。  
  
## <a name="remarks"></a>備註  
 使用 **維度** 物件的集合和屬性，您可以執行下列動作：  
  
-   識別具有[Name](../../../ado/reference/ado-md-api/name-property-ado-md.md)和[UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)屬性的**維度**。  
  
-   傳回描述具有[Description](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性之**維度**的有意義字串。  
  
-   傳回組成**維度**[集合的階層物件。](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) [Hierarchies](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)  
  
-   您可以使用標準 ADO [屬性](../../../ado/reference/ado-api/properties-collection-ado.md) 集合，取得有關 **維度** 物件的其他資訊。  
  
 **Properties**集合包含提供者提供的屬性。 下表列出可能可用的屬性。 實際的屬性清單可能會因提供者的執行而有所不同。 如需可用屬性的完整清單，請參閱提供者的檔。  
  
|名稱|描述|  
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
  
-   [屬性、方法和事件](../../../ado/reference/ado-md-api/dimension-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [CubeDef 範例 (VBScript) ](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [CubeDef 物件 (ADO MD) ](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)   
 [維度集合 (ADO MD) ](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [階層集合 (ADO MD) ](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
