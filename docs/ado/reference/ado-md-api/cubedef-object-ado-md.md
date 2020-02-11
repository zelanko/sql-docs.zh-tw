---
title: CubeDef 物件（ADO MD） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CubeDef
helpviewer_keywords:
- CubeDef object [ADO MD]
ms.assetid: feb2581c-fc41-471c-bb69-29f8a55fda70
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 61795a8cb10fb0b469f89012d52dfb4723aa0a89
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67949791"
---
# <a name="cubedef-object-ado-md"></a>CubeDef 物件 (ADO MD)
代表多維架構中的 cube，其中包含一組相關維度。  
  
## <a name="remarks"></a>備註  
 使用**CubeDef**物件的集合和屬性，您可以執行下列動作：  
  
-   識別具有[Name](../../../ado/reference/ado-md-api/name-property-ado-md.md)屬性的**CubeDef** 。  
  
-   傳回描述具有[Description](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性之 cube 的字串。  
  
-   傳回使用[維度](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)集合組成 cube 的維度。  
  
-   使用標準的 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，取得**CubeDef**的其他相關資訊。  
  
 **Properties**集合包含提供者提供的屬性。 下表列出可能可用的屬性。 實際的屬性清單可能會根據提供者的執行而有所不同。 如需可用屬性的完整清單，請參閱提供者的檔。  
  
|名稱|描述|  
|----------|-----------------|  
|CatalogName|這個 cube 所屬的目錄名稱。|  
|CreatedOn|建立 cube 的日期和時間。|  
|CubeGUID|Cube GUID。|  
|CubeName|Cube 的名稱。|  
|CubeType|Cube 的類型。|  
|DataUpdatedBy|執行上次資料更新之人員的使用者識別碼。|  
|描述|Cube 的有意義描述。|  
|LastSchemaUpdate|上次架構更新的日期和時間。|  
|SchemaName|這個 cube 所屬的架構名稱。|  
|SchemaUpdatedBy|執行上次架構更新之人員的使用者識別碼。|  
  
 本章節包含下列主題。  
  
-   [屬性、方法和事件](../../../ado/reference/ado-md-api/cubedef-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [CubeDef 範例（VBScript）](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Catalog 物件（ADO MD）](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)   
 [CubeDefs 集合（ADO MD）](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)   
 [維度集合（ADO MD）](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
