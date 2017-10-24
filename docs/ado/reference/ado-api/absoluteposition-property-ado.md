---
title: "AbsolutePosition 屬性 (ADO) |Microsoft 文件"
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
- Recordset15::AbsolutePosition
helpviewer_keywords:
- AbsolutePosition property [ADO]
ms.assetid: 79f8ee5e-fc70-46d8-8c29-ebf943c66592
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9c8a31bd7b0fbf2809b09b10b2ebcb983d7c811c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="absoluteposition-property-ado"></a>AbsolutePosition 屬性 (ADO)
指出的序數位置[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件的目前記錄。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 32 位元程式碼，設定或傳回**長**1 中的記錄數目的值**資料錄集**物件 ([RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md))，或傳回的其中一個[PositionEnum](../../../ado/reference/ado-api/positionenum.md)值。  
  
 64 位元程式碼，使用資料類型，提供儲存區的 64 位元值。 例如，您可能會使用長時間或另一個值為 64 位元長度，例如 DBORDINAL。 請勿使用**PositionEnum**值，因為它們會限制為 32 位元長度。  
  
## <a name="remarks"></a>備註  
 若要設定**AbsolutePosition**屬性，ADO 需要您使用的 OLE DB 提供者實作[IRowsetLocate:IRowset](https://msdn.microsoft.com/library/windows/desktop/ms721190.aspx)介面。  
  
 存取**AbsolutePosition**屬性**資料錄集**，以開啟 順向動態資料指標就會引發錯誤或**adErrFeatureNotAvailable**。 其他資料指標類型，正確的位置將會傳回，只要 OLE DB 提供者支援**IRowsetScroll:IRowsetLocate**介面。 如果提供者不支援**IRowsetScroll**介面的屬性設定為**adPosUnknown**。 請參閱您的提供者，以判斷其是否支援的文件**IRowsetScroll**。  
  
 使用**AbsolutePosition**移至資料的屬性會根據其序數位置中**資料錄集**物件，或要判定目前記錄的序數位置。 提供者必須支援這個屬性才能使用適當的功能。  
  
 像[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)屬性， **AbsolutePosition**是以 1 為基礎，並且等於 1，目前的記錄時的第一個記錄**資料錄集**。 您可以取得中的記錄總數**資料錄集**物件從[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)屬性。  
  
 當您將**AbsolutePosition**屬性，即使它是目前的快取中的記錄 ADO 重新載入快取以一組新的記錄從您指定的記錄。 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)屬性會決定此群組的大小。  
  
> [!NOTE]
>  您不應該使用**AbsolutePosition**屬性設為代理的記錄數目。 刪除先前的記錄時，就會變更特定記錄的位置。 另外還有任何指定的資料錄將會具有相同的保證**AbsolutePosition**如果**資料錄集**物件是重新查詢，或重新開啟。 書籤仍會保留並傳回指定位置的建議的方式，和是唯一的方法，在所有類型的定位**資料錄集**物件。  
  
## <a name="applies-to"></a>適用於  
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [AbsolutePosition 和 CursorLocation 屬性範例 (VB)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [AbsolutePosition 和 CursorLocation 屬性範例 （VC + +）](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [AbsolutePage 屬性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [RecordCount 屬性 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)

