---
title: Cell 物件（ADO MD） |Microsoft Docs
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
ms.openlocfilehash: bbf97a4095f2295b8851f87ba20ab083938e70ed
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67947740"
---
# <a name="cell-object-ado-md"></a>Cell 物件 (ADO MD)
代表資料格集內所包含之軸座標交集處的資料。  
  
## <a name="remarks"></a>備註  
 資料**格**[集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件的[Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)屬性會傳回 Cell 物件。  
  
 利用**Cell**物件的集合和屬性，您可以執行下列動作：  
  
-   使用[Value](../../../ado/reference/ado-md-api/value-property-ado-md.md)屬性傳回**儲存格中**的資料。  
  
-   傳回字串，表示具有[FormattedValue](../../../ado/reference/ado-md-api/formattedvalue-property-ado-md.md)屬性之**Value**屬性的格式化顯示。  
  
-   傳回資料格**集**內具有[ordinal](../../../ado/reference/ado-md-api/ordinal-property-ado-md-cell.md)屬性的資料**格**序數值。  
  
-   使用 [[位置](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)] 集合判斷[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)內**儲存格**的位置。  
  
-   使用標準 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，抓取資料**格**的其他相關資訊。  
  
 **Properties**集合包含提供者提供的屬性。 下表列出可能可用的屬性。 實際的屬性清單可能會根據提供者的執行而有所不同。 如需可用屬性的完整清單，請參閱提供者的檔。  
  
|名稱|描述|  
|----------|-----------------|  
|BackColor|顯示儲存格時使用的背景色彩。|  
|FontFlags|位元遮罩詳述字型的效果。|  
|FontName|用來顯示資料格值的字型。|  
|FontSize|用來顯示資料格值的字型大小。|  
|ForeColor|顯示儲存格時使用的前景色彩。|  
|FormatString|格式化字串中的值。|  
  
 本章節包含下列主題。  
  
-   [屬性、方法和事件](../../../ado/reference/ado-md-api/cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Axis 範例（VBScript）](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [格集物件（ADO MD）](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [位置集合（ADO MD）](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
