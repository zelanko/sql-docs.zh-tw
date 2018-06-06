---
title: CubeDef 物件 (ADO MD) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CubeDef
helpviewer_keywords:
- CubeDef object [ADO MD]
ms.assetid: feb2581c-fc41-471c-bb69-29f8a55fda70
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31e2bf587c19ab8088b0ab702be60fde54247aec
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="cubedef-object-ado-md"></a>CubeDef 物件 (ADO MD)
代表多維度結構描述，其中包含一組相關維度的 cube。  
  
## <a name="remarks"></a>備註  
 集合與屬性**CubeDef**物件，您可以執行下列：  
  
-   識別**CubeDef**與[名稱](../../../ado/reference/ado-md-api/name-property-ado-md.md)屬性。  
  
-   傳回字串，描述具有 cube[描述](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性。  
  
-   傳回組成具有 cube 的維度[維度](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)集合。  
  
-   取得其他資訊有關**CubeDef**與標準 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
 **屬性**集合包含提供者提供的屬性。 下表列出可供使用的屬性。 實際的屬性清單可能與不同的提供者實作而定。 請參閱您的提供者，如需更完整清單可用內容的文件。  
  
|名稱|Description|  
|----------|-----------------|  
|CatalogName|此 cube 所屬的目錄的名稱。|  
|CreatedOn|日期和時間的 cube 建立。|  
|CubeGUID|Cube 的 GUID。|  
|CubeName|Cube 的名稱。|  
|CubeType|Cube 的類型。|  
|DataUpdatedBy|進行最後的資料更新的人員的使用者識別碼。|  
|Description|Cube 有意義的描述。|  
|LastSchemaUpdate|日期和時間的最後一個結構描述更新。|  
|SchemaName|此 cube 所屬的結構描述名稱。|  
|SchemaUpdatedBy|進行最後一個結構描述更新的人員的使用者識別碼。|  
  
 本章節包含下列主題。  
  
-   [屬性、 方法和事件](../../../ado/reference/ado-md-api/cubedef-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [CubeDef 範例 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [目錄物件 (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)   
 [CubeDefs 集合 (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)   
 [維度集合 (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
