---
title: AbsolutePosition 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePosition
helpviewer_keywords:
- AbsolutePosition property [ADO]
ms.assetid: 79f8ee5e-fc70-46d8-8c29-ebf943c66592
author: rothja
ms.author: jroth
ms.openlocfilehash: 56b21fe8cddf4d855ec1655a83cea306c0a3000c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747516"
---
# <a name="absoluteposition-property-ado"></a>AbsolutePosition 屬性 (ADO)
指出[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件目前記錄的序數位置。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 若是32位程式碼，則會設定或傳回從1到記錄**集**物件（[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)）中的記錄數目的**長**數值，或傳回其中一個[PositionEnum](../../../ado/reference/ado-api/positionenum.md)值。  
  
 若是64位程式碼，請使用提供給64位值儲存的資料類型。 例如，您可以使用 Long 或64位長度的另一個值，例如 DBORDINAL。 請勿使用**PositionEnum**值，因為它們的長度限制為32位。  
  
## <a name="remarks"></a>備註  
 若要設定**AbsolutePosition**屬性，ADO 會要求您使用的 OLE DB 提供者必須執行[IRowsetLocate： IRowset](https://msdn.microsoft.com/library/windows/desktop/ms721190.aspx)介面。  
  
 存取以順向或動態資料指標開啟之**記錄集**的**AbsolutePosition**屬性，會引發錯誤**adErrFeatureNotAvailable**。 使用其他資料指標類型時，只要 OLE DB 提供者支援**IRowsetScroll： IRowsetLocate**介面，就會傳回正確的位置。 如果提供者不支援**IRowsetScroll**介面，則屬性會設定為**adPosUnknown**。 請參閱提供者的檔，以判斷它是否支援**IRowsetScroll**。  
  
 您可以使用**AbsolutePosition**屬性，根據記錄**集**物件中的序數位置，或判斷目前記錄的序數位置。 提供者必須支援適當的功能，才能使用此屬性。  
  
 如同[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)屬性， **AbsolutePosition**是以1為基礎，而當目前記錄是**記錄集**內的第一筆記錄時，等於1。 您可以從[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)屬性取得記錄**集**物件中的記錄總數。  
  
 當您設定**AbsolutePosition**屬性時，即使它是目前快取中的記錄，ADO 還是會以您指定的記錄開頭的一組新記錄來重載快取。 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)屬性會決定此群組的大小。  
  
> [!NOTE]
>  您不應該使用**AbsolutePosition**屬性做為代理記錄號碼。 當您刪除先前的記錄時，指定記錄的位置會變更。 如果重新查詢或重新開啟**記錄集**物件，也不保證給定的記錄會有相同的**AbsolutePosition** 。 書簽仍然是保留並返回指定位置的建議方式，而且是在所有類型的**記錄集**物件上定位的唯一方法。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [AbsolutePosition 和 CursorLocation 屬性範例（VB）](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [AbsolutePosition 和 CursorLocation 屬性範例（VC + +）](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [AbsolutePage 屬性（ADO）](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [RecordCount 屬性 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
