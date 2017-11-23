---
title: "資料格物件 (ADO MD) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Cell
helpviewer_keywords: Cell object [ADO MD]
ms.assetid: dcc2f044-b785-4a29-9bc5-b673f66eedf9
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e35b30a2474f43ee1d46e23ae4a4323cca47f16b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="cell-object-ado-md"></a>資料格物件 (ADO MD)
表示資料格集中所包含的軸座標交集處的資料。  
  
## <a name="remarks"></a>備註  
 A**儲存格**物件由[項目](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)屬性[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件。  
  
 集合與屬性**儲存格**物件，您可以執行下列：  
  
-   在將資料傳回**儲存格**與[值](../../../ado/reference/ado-md-api/value-property-ado-md.md)屬性。  
  
-   傳回字串，代表格式化的顯示**值**屬性[FormattedValue](../../../ado/reference/ado-md-api/formattedvalue-property-ado-md.md)屬性。  
  
-   傳回的序數值**儲存格**內**資料格集**與[序數](../../../ado/reference/ado-md-api/ordinal-property-ado-md-cell.md)屬性。  
  
-   決定位置的**儲存格**內[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)與[位置](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)集合。  
  
-   擷取其他資訊**儲存格**與標準 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
 **屬性**集合包含提供者提供的屬性。 下表列出可供使用的屬性。 實際的屬性清單可能與不同的提供者實作而定。 請參閱您的提供者，如需更完整清單可用內容的文件。  
  
|名稱|Description|  
|----------|-----------------|  
|BackColor|用來顯示資料格的背景色彩。|  
|FontFlags|詳述影響字型的位元遮罩。|  
|FontName|用來顯示資料格的值的字型。|  
|FontSize|用來顯示資料格的值的字型大小。|  
|ForeColor|用來顯示資料格的前景色彩。|  
|FormatString|格式化字串中的值。|  
  
 本章節包含下列主題。  
  
-   [屬性、 方法和事件](../../../ado/reference/ado-md-api/cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>請參閱＜  
 [軸範例 (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [資料格集物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [位置集合 (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
