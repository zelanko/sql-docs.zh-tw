---
title: 項目屬性 (ADO MD Cellset) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Item
- Cellset::Item
helpviewer_keywords:
- Item property [ADO MD]
ms.assetid: 0e93d79b-b12e-4e98-889e-c2dfcca20fd0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 641a08567e990134d49d32ae7ebecaf7d2b8de5a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740204"
---
# <a name="item-property-ado-md-cellset"></a>Item 屬性 (ADO MD Cellset)
擷取資料格[資料格集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)使用其座標。  
  
## <a name="syntax"></a>語法  
  
```  
  
Set  
Cell = Cellset.Item ( Positions)  
```  
  
## <a name="parameters"></a>參數  
 *位置*  
 A **VariantArray**唯一指定的儲存格的值。 *位置*可以是下列其中之一：  
  
-   位置的數字陣列  
  
-   成員名稱的陣列  
  
-   序數位置  
  
## <a name="remarks"></a>備註  
 使用**項目**屬性，以傳回[資料格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)物件內[Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)物件。 如果**項目**屬性找不到對應至的資料格*位置*引數，則會發生錯誤。  
  
 **項目**屬性是預設屬性，如**資料格集**物件。 下列語法形式是可互換：  
  
```  
  
Cellset.Item ( Positions )Cellset ( Positions )  
```  
  
## <a name="remarks"></a>備註  
 *位置*引數會指定要傳回哪一個儲存格。 您可以指定儲存格的序數位置，或依每個軸位置。 在指定的儲存格的每個軸的位置時，您可以指定位置的數字的值或成員的名稱，每個位置。  
  
 序數位置是可唯一識別內的一個資料格的數字**資料格集**。 就概念而言，資料格會依編號**Cellset**如同**資料格集**已*p*-維陣列，其中*p*是軸的數目。 資料格的處理順序是以資料列為主。 以下是計算資料格序數的公式：  
  
 如果成員名稱會傳遞為字串至**項目**，必須以數值軸識別碼的遞增順序列出的成員。 在座標軸，必須以維度的巢狀結構的遞增順序列出的成員，-也就是最外層的維度成員視何者先，後面接著的內部的維度成員。 每個維度都應是分開的字串，來表示，應該以逗號分隔的成員字串清單。  
  
> [!NOTE]
>  擷取的資料格成員名稱可能不支援您的資料提供者中。 請參閱您的提供者，如需詳細資訊的文件。  
  
## <a name="applies-to"></a>適用於  
 [Cellset 物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)  
  
## <a name="see-also"></a>另請參閱  
 [Cell 物件 (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Cellset 物件 (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)
