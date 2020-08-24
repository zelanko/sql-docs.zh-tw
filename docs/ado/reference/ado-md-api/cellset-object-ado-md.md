---
description: Cellset 物件 (ADO MD)
title: ADO MD) 的 (格集物件 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 65e5e28443fd4656aa2b953f18b07c952bcbb66a
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778307"
---
# <a name="cellset-object-ado-md"></a>Cellset 物件 (ADO MD)
表示多維度查詢的結果。 它是從 cube 或其他資料格集選取的儲存格集合。  
  
## <a name="remarks"></a>備註  
 資料 **格集** 內的資料會使用直接、類似陣列的存取權進行抓取。 您可以向下切入到特定成員，以取得該成員的相關資料。 例如，下列程式碼會傳回名為之儲存格第一個座標軸第一個位置第一個成員的標題 `cst` ：  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
## <a name="remarks"></a>備註  
 資料格集內目前的儲存格沒有任何概念。 [專案](./item-property-ado-md-cellset.md)屬性會改為從資料格集抓取特定的[Cell](./cell-object-ado-md.md)物件。 **Item**屬性的引數會決定要抓取的儲存格。 您可以指定資料格的唯一序數值。 您也可以使用資料格集的每個軸上的位置數位來抓取儲存格。 如需有關如何取出資料格的詳細資訊，請參閱 [Item](./item-property-ado-md-cellset.md) 屬性。  
  
 使用 **儲存格** 物件的集合、方法和屬性，您可以執行下列動作：  
  
-   藉由設定[ActiveConnection](./activeconnection-property-ado-md.md)屬性，將開啟的連接與**儲存格**物件建立關聯。  
  
-   使用 [Open](./open-method-ado-md.md) 方法執行和取出多維度查詢的結果。  
  
-   使用[Item](./item-property-ado-md-cellset.md)屬性從資料格**集**取出**儲存格**。  
  
-   傳回以[軸](./axes-collection-ado-md.md)集合定義**儲存格**的[座標軸](./axis-object-ado-md.md)物件。  
  
-   使用[FilterAxis](./filteraxis-property-ado-md.md)屬性，抓取用來篩選資料**格集**內資料的維度相關資訊。  
  
-   傳回或指定用來定義[來源](./source-property-ado-md.md)屬性之**儲存格**的查詢。  
  
-   傳回目前的 **儲存格** 狀態 (開啟、關閉、執行，或以 [state](./state-property-ado-md.md) 屬性連接) 。  
  
-   使用[close](./close-method-ado-md.md)方法關閉開啟的**儲存格**。  
  
-   使用標準的 ADO[屬性](../ado-api/properties-collection-ado.md)集合，取得有關資料**格集**的提供者特定資訊。  
  
 本節包含下列主題。  
  
-   [屬性、方法和事件](./cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的集格範例 ](./cellset-example-vb.md)   
 [軸集合 (ADO MD) ](./axes-collection-ado-md.md)   
 [資料格物件 (ADO MD) ](./cell-object-ado-md.md)   
 [ (ADO) 的 Connection 物件 ](../ado-api/connection-object-ado.md)   
 [Properties 集合 (ADO)](../ado-api/properties-collection-ado.md)