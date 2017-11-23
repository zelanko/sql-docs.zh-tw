---
title: "資料格集物件 (ADO MD) |Microsoft 文件"
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
f1_keywords: Cellset
helpviewer_keywords: Cellset object [ADO MD]
ms.assetid: 5e2452c0-cac0-49b2-8099-836c35794d50
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c860f9b84514cc84c73c52e10978ad76365cc6ed
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="cellset-object-ado-md"></a>資料格集物件 (ADO MD)
代表多維度查詢的結果。 它是從 cube 或其他資料格集中選取的儲存格的集合。  
  
## <a name="remarks"></a>備註  
 中的資料**資料格集**擷取使用直接、 類似陣列的存取。 您可以向下鑽研至特定的成員，以取得有關該成員的資料。 例如，下列程式碼傳回的第一個位置中名為資料格集的第一個軸上的第一個成員的標題`cst`:  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
## <a name="remarks"></a>備註  
 沒有資料格集內的目前儲存格的概念。 相反地，[項目](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)屬性擷取特定[儲存格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)從資料格集的物件。 引數**項目**屬性決定擷取哪些資料格。 您可以指定唯一的序數值的儲存格。 您也可以使用其位置數字，每個座標軸上的資料格集擷取的資料格。 如需有關擷取的資料格的詳細資訊，請參閱[項目](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)屬性。  
  
 使用集合、 方法和屬性的**資料格集**物件，您可以執行下列：  
  
-   建立與開啟的連接關聯**資料格集**物件藉由設定其[ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md)屬性。  
  
-   執行並擷取與多維度查詢的結果[開啟](../../../ado/reference/ado-md-api/open-method-ado-md.md)方法。  
  
-   擷取**儲存格**從**資料格集**與[項目](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md)屬性。  
  
-   傳回[軸](../../../ado/reference/ado-md-api/axis-object-ado-md.md)物件，以定義**資料格集**與[座標軸](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)集合。  
  
-   擷取用來篩選中的資料維度的詳細資訊**資料格集**與[FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md)屬性。  
  
-   傳回或指定用來定義查詢**資料格集**與[來源](../../../ado/reference/ado-md-api/source-property-ado-md.md)屬性。  
  
-   傳回目前的狀態**資料格集**（開啟、 關閉、 執行，或連線） 與[狀態](../../../ado/reference/ado-md-api/state-property-ado-md.md)屬性。  
  
-   關閉開啟**資料格集**與[關閉](../../../ado/reference/ado-md-api/close-method-ado-md.md)方法。  
  
-   擷取提供者特定資訊**資料格集**與標準 ADO[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
 本章節包含下列主題。  
  
-   [屬性、 方法和事件](../../../ado/reference/ado-md-api/cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>請參閱＜  
 [資料格集範例 (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Axes 集合 (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)   
 [資料格物件 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
