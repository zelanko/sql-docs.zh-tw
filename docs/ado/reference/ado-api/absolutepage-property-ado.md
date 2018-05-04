---
title: AbsolutePage 屬性 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePage
helpviewer_keywords:
- AbsolutePage property [ADO]
ms.assetid: ddb58a35-ec3a-423c-a504-3c65e62c23d4
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b87d45f01948cf5cdfa60ed1bf185a96be4c495c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="absolutepage-property-ado"></a>AbsolutePage 屬性 (ADO)
指出目前記錄位於哪一頁。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 32 位元程式碼，設定或傳回**長**1 中的頁數的值[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件 ([PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md))，或傳回的其中一個[PositionEnum](../../../ado/reference/ado-api/positionenum.md)值。  
  
 64 位元程式碼，使用資料類型，提供儲存區的 64 位元值。 例如，您可以使用**長**或另一個值，例如 DBORDINAL 64 位元長度。 請勿使用**PositionEnum**值，因為它們會限制為 32 位元長度。  
  
## <a name="remarks"></a>備註  
 這個屬性可以用來識別目前的記錄所在的頁碼。 它會使用[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)屬性以邏輯方式將總計資料列集的計數**資料錄集**成一連串的頁面，每一個都有相等的記錄數目的物件**PageSize**（除了最後一個頁面上，這可能會有較少的記錄）。 提供者必須支援這個屬性才能使用適當的功能。  
  
-   取得或設定當**AbsolutePage**屬性、 ADO 使用[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)屬性和[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)屬性在一起，如下所示：  
  
-   若要取得**AbsolutePage**，ADO 會先擷取**AbsolutePosition**，，然後將它**PageSize**。  
  
-   若要設定**AbsolutePage**，ADO 移**AbsolutePosition** ，如下所示： 它乘以**PageSize**新**AbsolutePage**值，並再將 1 的值。 如此一來中的目前位置**資料錄集**成功設定之後**AbsolutePage**是第一筆記錄，在該頁面。  
  
 像**AbsolutePosition**屬性， **AbsolutePage**是以 1 為基礎，並且等於 1，目前的記錄時的第一個記錄**資料錄集**。 設定這個屬性，以移至特定頁面的第一個記錄。 取得從總頁數**PageCount**屬性。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [AbsolutePage、 PageCount 和 PageSize 屬性範例 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、 PageCount 和 PageSize 屬性範例 （VC + +）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePosition 屬性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [PageCount 屬性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [PageSize 屬性 (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)
