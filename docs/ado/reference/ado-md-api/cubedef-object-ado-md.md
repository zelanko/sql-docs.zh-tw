---
title: CubeDef 物件 (ADO MD) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: d1027fc76cb09f7b846e1b8edad52a3cb5dbf2bc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63225910"
---
# <a name="cubedef-object-ado-md"></a>CubeDef 物件 (ADO MD)
表示從多維度的結構描述，其中包含一組相關的維度的 cube。  
  
## <a name="remarks"></a>備註  
 使用集合和屬性的**CubeDef**物件時，您可以執行下列動作：  
  
-   找出**CubeDef**具有[名稱](../../../ado/reference/ado-md-api/name-property-ado-md.md)屬性。  
  
-   傳回字串，描述 cube[描述](../../../ado/reference/ado-md-api/description-property-ado-md.md)屬性。  
  
-   傳回構成 cube 的維度[維度](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)集合。  
  
-   取得有關的其他資訊**CubeDef**與標準的 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
 **屬性**集合包含提供者提供的屬性。 下表列出可用的屬性。 實際的屬性清單可能與不同的提供者實作而定。 請參閱您的提供者，如需更完整清單的可用屬性的文件。  
  
|名稱|描述|  
|----------|-----------------|  
|CatalogName|這個 cube 所屬的目錄名稱。|  
|CreatedOn|日期和時間的 cube 建立。|  
|CubeGUID|Cube 的 GUID。|  
|CubeName|Cube 的名稱。|  
|CubeType|Cube 的類型。|  
|DataUpdatedBy|執行最後的資料更新之人員的使用者識別碼。|  
|描述|Cube 有意義描述。|  
|LastSchemaUpdate|日期和時間的最後一個結構描述更新。|  
|SchemaName|這個 cube 所屬的結構描述名稱。|  
|SchemaUpdatedBy|執行最新的結構描述更新之人員的使用者識別碼。|  
  
 本章節包含下列主題。  
  
-   [屬性、 方法和事件](../../../ado/reference/ado-md-api/cubedef-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [CubeDef 範例 (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Catalog 物件 (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)   
 [CubeDefs 集合 (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)   
 [Dimensions 集合 (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
