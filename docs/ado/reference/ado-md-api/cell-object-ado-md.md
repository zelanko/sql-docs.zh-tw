---
title: 資料格的物件 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell
helpviewer_keywords:
- Cell object [ADO MD]
ms.assetid: dcc2f044-b785-4a29-9bc5-b673f66eedf9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df7b93e00ddff15c320152e3fa2bc1f104caa3a4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62469483"
---
# <a name="cell-object-ado-md"></a>Cell 物件 (ADO MD)
表示資料格集中所包含的軸座標交集處的資料。  
  
## <a name="remarks"></a>備註  
 A**儲存格**會傳回物件[項目](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)屬性[Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件。  
  
 使用集合和屬性的**儲存格**物件時，您可以執行下列動作：  
  
-   傳回的資料**儲存格**具有[值](../../../ado/reference/ado-md-api/value-property-ado-md.md)屬性。  
  
-   傳回字串，表示格式化的顯示**值**屬性[FormattedValue](../../../ado/reference/ado-md-api/formattedvalue-property-ado-md.md)屬性。  
  
-   傳回的序數值**儲存格**內**資料格集**具有[序數](../../../ado/reference/ado-md-api/ordinal-property-ado-md-cell.md)屬性。  
  
-   決定的位置**儲存格**內[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)具有[位置](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)集合。  
  
-   擷取有關的其他資訊**儲存格**與標準的 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
 **屬性**集合包含提供者提供的屬性。 下表列出可用的屬性。 實際的屬性清單可能與不同的提供者實作而定。 請參閱您的提供者，如需更完整清單的可用屬性的文件。  
  
|名稱|描述|  
|----------|-----------------|  
|BackColor|用來顯示儲存格的背景色彩。|  
|FontFlags|詳述影響字型的位元遮罩。|  
|FontName|顯示儲存格的值所使用的字型。|  
|FontSize|用來顯示資料格值的字型大小。|  
|ForeColor|用來顯示儲存格的前景色彩。|  
|FormatString|格式化字串中的值。|  
  
 本章節包含下列主題。  
  
-   [屬性、 方法和事件](../../../ado/reference/ado-md-api/cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Axis 範例 (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Cellset 物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Positions 集合 (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
