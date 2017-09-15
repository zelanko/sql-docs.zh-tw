---
title: "項目屬性 （ADO MD 資料格集） |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Item
- Cellset::Item
helpviewer_keywords:
- Item property [ADO MD]
ms.assetid: 0e93d79b-b12e-4e98-889e-c2dfcca20fd0
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0fb324383dc9321129fdb84475369d899d61adcb
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="item-property-ado-md-cellset"></a>項目屬性 （ADO MD 資料格集）
擷取從資料格[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)使用其座標。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set  
Cell = Cellset.Item ( Positions)  
```  
  
## <a name="parameters"></a>參數  
 *位置*  
 A **VariantArray**唯一指定的儲存格的值。 *位置*可以是下列其中之一：  
  
-   位置編號的陣列  
  
-   成員名稱的陣列  
  
-   序數位置  
  
## <a name="remarks"></a>備註  
 使用**項目**屬性，以傳回[儲存格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)物件內[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件。 如果**項目**屬性找不到對應至的資料格*位置*引數，就會發生錯誤。  
  
 **項目**屬性是預設屬性**資料格集**物件。 下列語法形式是可互換的：  
  
```  
  
Cellset.Item ( Positions )Cellset ( Positions )  
```  
  
## <a name="remarks"></a>備註  
 *位置*引數會指定要傳回哪一個儲存格。 您可以指定儲存格的序數位置，或依每個軸位置。 在指定的儲存格的每個軸的位置時，您可以指定位置的數字值或成員的名稱，每個位置。  
  
 序數位置是可唯一識別一個資料格內的數字**資料格集**。 就概念而言，資料格會以編號**資料格集**如同**資料格集**已*p*-維陣列，其中*p*是軸的數目。 資料格的處理順序是以資料列為主。 以下是計算資料格序數的公式：  
  
 如果成員名稱傳遞為字串至**項目**，必須以遞增的數值座標軸識別項的順序列出的成員。 必須以遞增順序排列的維度巢狀列出的成員內座標軸，— 也就是最外層的維度成員先出現，後面接著內部維度的成員。 每個維度應該由個別的字串，並應該以逗號分隔的成員字串清單。  
  
> [!NOTE]
>  擷取的資料格成員名稱可能不支援您的資料提供者中。 請參閱您的提供者，如需詳細資訊的文件。  
  
## <a name="applies-to"></a>適用於  
 [資料格集物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料格物件 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [資料格集物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)
