---
description: Cell 物件 (ADO MD)
title: 資料格物件 (ADO MD) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 28058d792b0525aafe8850158a71afcc4423b38f
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778327"
---
# <a name="cell-object-ado-md"></a>Cell 物件 (ADO MD)
代表資料格集內所含座標軸座標交集處的資料。  
  
## <a name="remarks"></a>備註  
 資料**格**物件是由資料格[集](./cellset-object-ado-md.md)物件的[Item](./item-property-ado-md-cellset.md)屬性所傳回。  
  
 使用 **Cell** 物件的集合和屬性，您可以執行下列動作：  
  
-   使用[Value](./value-property-ado-md.md)屬性傳回資料**格中**的資料。  
  
-   傳回字串，表示具有[FormattedValue](./formattedvalue-property-ado-md.md)屬性之**Value**屬性的格式化顯示。  
  
-   使用[序數](./ordinal-property-ado-md-cell.md)屬性，傳回資料格**集**內**儲存格**的序數值。  
  
-   使用[位置](./positions-collection-ado-md.md)集合判斷[CubeDef](./cubedef-object-ado-md.md)中**儲存格**的位置。  
  
-   使用標準 ADO[屬性](../ado-api/properties-collection-ado.md)集合抓取資料**格**的其他相關資訊。  
  
 **Properties**集合包含提供者提供的屬性。 下表列出可能可用的屬性。 實際的屬性清單可能會因提供者的執行而有所不同。 如需可用屬性的完整清單，請參閱提供者的檔。  
  
|Name|描述|  
|----------|-----------------|  
|BackColor|顯示儲存格時使用的背景色彩。|  
|FontFlags|用以詳述字型效果的位元遮罩。|  
|FontName|用來顯示資料格值的字型。|  
|FontSize|用來顯示資料格值的字型大小。|  
|ForeColor|顯示儲存格時使用的前景色彩。|  
|FormatString|格式化字串中的值。|  
  
 本節包含下列主題。  
  
-   [屬性、方法和事件](./cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VBScript) 的座標軸範例 ](./axis-example-vbscript.md)   
 [ (ADO MD) 的儲存格集物件 ](./cellset-object-ado-md.md)   
 [位置集合 (ADO MD) ](./positions-collection-ado-md.md)   
 [Properties 集合 (ADO)](../ado-api/properties-collection-ado.md)