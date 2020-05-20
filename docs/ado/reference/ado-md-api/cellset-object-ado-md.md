---
title: 格集物件（ADO MD） |Microsoft Docs
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
ms.openlocfilehash: e50fb60fbde205171c066380a2c2023d485a5a09
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761766"
---
# <a name="cellset-object-ado-md"></a>Cellset 物件 (ADO MD)
表示多維度查詢的結果。 這是從 cube 或其他資料格集中選取的資料格集合。  
  
## <a name="remarks"></a>備註  
 資料**格集**內的資料會使用直接、類似陣列的存取來抓取。 您可以向下切入到特定的成員，以取得該成員的相關資料。 例如，下列程式碼會傳回名為之集格第一個軸上第一個位置的第一個成員的標題 `cst` ：  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
## <a name="remarks"></a>備註  
 資料格集內目前的儲存格沒有任何概念。 相反地， [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)屬性會從資料格集抓取特定的[Cell](../../../ado/reference/ado-md-api/cell-object-ado-md.md)物件。 **Item**屬性的引數會決定要抓取的儲存格。 您可以指定資料格的唯一序數值。 您也可以在資料格集的每個軸上，使用其位置數位來抓取儲存格。 如需有關抓取資料格的詳細資訊，請參閱[Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)屬性。  
  
 您可以使用集合、方法和內容**集**物件的屬性，執行下列動作：  
  
-   藉由設定其[ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)屬性，讓開啟的連接與控制項**集**物件產生關聯。  
  
-   使用[Open](../../../ado/reference/ado-md-api/open-method-ado-md.md)方法執行和取出多維度查詢的結果。  
  
-   使用[Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)屬性，從資料**格集**取出**儲存格**。  
  
-   傳回使用[軸](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)集合定義**儲存格集**的[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)物件。  
  
-   使用[FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md)屬性，抓取資料**格集**內用來篩選資料之維度的相關資訊。  
  
-   傳回或指定用來定義具有[Source](../../../ado/reference/ado-md-api/source-property-ado-md.md)屬性之**儲存格集**的查詢。  
  
-   使用[state](../../../ado/reference/ado-md-api/state-property-ado-md.md)屬性，傳回**儲存格集**的目前狀態（開啟、關閉、執行或連接）。  
  
-   使用[close](../../../ado/reference/ado-md-api/close-method-ado-md.md)方法關閉開啟的**儲存格**。  
  
-   使用標準的 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合，抓取資料**格集**的相關提供者特定資訊。  
  
 本章節包含下列主題。  
  
-   [屬性、方法和事件](../../../ado/reference/ado-md-api/cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [格集範例（VB）](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [軸集合（ADO MD）](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)   
 [Cell 物件（ADO MD）](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Connection 物件（ADO）](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
