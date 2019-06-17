---
title: Cellset 物件 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cellset
helpviewer_keywords:
- Cellset object [ADO MD]
ms.assetid: 5e2452c0-cac0-49b2-8099-836c35794d50
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 52ede9c21077c81dd1bd90f12acbfc3dff796d50
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66709492"
---
# <a name="cellset-object-ado-md"></a>Cellset 物件 (ADO MD)
表示多維度查詢的結果。 它是從 cube 或其他資料格集中選取的儲存格的集合。  
  
## <a name="remarks"></a>備註  
 中的資料**資料格集**會擷取使用直接、 類似陣列存取。 您可以向下鑽研至特定的成員，才能取得該成員相關的資料。 比方說，下列程式碼傳回的第一個位置中名為資料格集的第一個軸上的第一個成員的標題`cst`:  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
## <a name="remarks"></a>備註  
 沒有任何資料格集內的目前儲存格的概念。 相反地，[項目](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)屬性會擷取特定[資料格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)從資料格集的物件。 引數**項目**屬性可讓您判斷哪一個儲存格擷取。 您可以指定儲存格的唯一的序數值。 您也可以使用他們的位置數字，每個座標軸上的資料格集擷取的資料格。 如需有關如何擷取儲存格的詳細資訊，請參閱 <<c0> [ 項目](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)屬性。  
  
 使用集合、 方法和屬性的**資料格集**物件時，您可以執行下列動作：  
  
-   將與開啟的連接產生關聯**Cellset**藉由設定物件其[ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)屬性。  
  
-   執行並擷取與多維度查詢的結果[開啟](../../../ado/reference/ado-md-api/open-method-ado-md.md)方法。  
  
-   擷取**儲存格**從**資料格集**具有[項目](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)屬性。  
  
-   傳回[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)定義的物件**資料格集**具有[軸](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)集合。  
  
-   擷取用來篩選中的資料維度的相關資訊**Cellset**具有[FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md)屬性。  
  
-   傳回或指定查詢用來定義**Cellset**具有[來源](../../../ado/reference/ado-md-api/source-property-ado-md.md)屬性。  
  
-   傳回目前的狀態**Cellset** （開啟、 關閉、 執行，或連線） 與[狀態](../../../ado/reference/ado-md-api/state-property-ado-md.md)屬性。  
  
-   關閉開啟**Cellset**具有[關閉](../../../ado/reference/ado-md-api/close-method-ado-md.md)方法。  
  
-   擷取提供者專屬資訊的相關**Cellset**與標準的 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
 本章節包含下列主題。  
  
-   [屬性、 方法和事件](../../../ado/reference/ado-md-api/cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Cellset 範例 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Axes 集合 (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)   
 [Cell 物件 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
