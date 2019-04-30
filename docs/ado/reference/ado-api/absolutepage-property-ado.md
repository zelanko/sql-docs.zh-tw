---
title: AbsolutePage 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePage
helpviewer_keywords:
- AbsolutePage property [ADO]
ms.assetid: ddb58a35-ec3a-423c-a504-3c65e62c23d4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: efdbd68bf464fea3a0d59396380b082eb66375b8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156580"
---
# <a name="absolutepage-property-ado"></a>AbsolutePage 屬性 (ADO)
指出目前記錄位於哪一頁。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 針對 32 位元程式碼，設定或傳回**長**值從 1 中的頁數[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件 ([PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md))，或傳回的其中一個[PositionEnum](../../../ado/reference/ado-api/positionenum.md)值。  
  
 針對 64 位元程式碼，使用提供的 64 位元值的儲存體的資料類型。 例如，您可以使用**長**或另一個可以是 DBORDINAL 等的 64 位元長度的值。 請勿使用**PositionEnum**值，因為它們被限制為 32 位元長度。  
  
## <a name="remarks"></a>備註  
 這個屬性可用來識別目前的記錄所在的頁面數目。 它會使用[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)屬性來以邏輯方式分割的總資料列集計數**Recordset**成一連串的頁面，每個都有相等的記錄數目的物件**PageSize**（除了最後一頁，可能會有較少的記錄）。 提供者必須支援這個屬性才能使用適當的功能。  
  
-   取得或設定當**AbsolutePage**屬性，ADO 會使用[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)屬性和[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)屬性在一起，如下所示：  
  
-   若要取得**AbsolutePage**，第一次擷取 ADO **AbsolutePosition**，並接著會將它**PageSize**。  
  
-   若要設定**AbsolutePage**，ADO 移動**AbsolutePosition** ，如下所示： 它會將**PageSize**新**AbsolutePage**值，並接著將的值加 1。 如此一來中的目前位置**資料錄集**順利設定之後**AbsolutePage**是網頁上的第一筆記錄。  
  
 像是**AbsolutePosition**屬性， **AbsolutePage**是以 1 為基礎，並等於 1，當目前的記錄中的第一個記錄**資料錄集**。 設定這個屬性，以移至特定的頁面上第一筆記錄。 取得從總頁數**PageCount**屬性。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [AbsolutePage、 PageCount、 和 PageSize 屬性範例 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、 PageCount、 和 PageSize 屬性範例 （VC + +）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePosition 屬性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [PageCount 屬性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [PageSize 屬性 (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)
