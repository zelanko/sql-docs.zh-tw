---
description: AbsolutePosition 屬性 (ADO)
title: " (ADO) 的 AbsolutePosition 屬性 |Microsoft Docs"
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
ms.openlocfilehash: f8660c2b5fecaeb99c0e0f3b4bcc57b1b2fc222a
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759968"
---
# <a name="absoluteposition-property-ado"></a>AbsolutePosition 屬性 (ADO)
表示 [記錄集](./recordset-object-ado.md) 物件的目前記錄的序數位置。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 若為32位程式碼，則會將 **Long** 值從1設定或傳回 **記錄集** 物件中的記錄數目 ([RecordCount](./recordcount-property-ado.md)) ，或傳回其中一個 [PositionEnum](./positionenum.md) 值。  
  
 若為64位的程式碼，請使用提供的資料類型來儲存64位值。 例如，您可能會使用 Long 或另一個64位長度的值，例如 DBORDINAL。 請勿使用 **PositionEnum** 值，因為它們受限於32位長度。  
  
## <a name="remarks"></a>備註  
 為了設定 **AbsolutePosition** 屬性，ADO 要求您使用的 OLE DB 提供者必須執行 [IRowsetLocate： IRowset](/previous-versions/windows/desktop/ms721190(v=vs.85)) 介面。  
  
 存取以順向或動態資料指標開啟之**記錄集**的**AbsolutePosition**屬性，會引發錯誤**adErrFeatureNotAvailable**。 若使用其他資料指標類型，只要 OLE DB 提供者支援 **IRowsetScroll： IRowsetLocate** 介面，就會傳回正確的位置。 如果提供者不支援 **IRowsetScroll** 介面，則會將屬性設定為 **adPosUnknown**。 請參閱提供者的檔，以判斷它是否支援 **IRowsetScroll**。  
  
 您可以使用 **AbsolutePosition** 屬性，根據記錄 **集** 物件中的序數位置移至記錄，或決定目前記錄的序數位置。 提供者必須支援適當的功能，才能使用此屬性。  
  
 如同 [AbsolutePage](./absolutepage-property-ado.md) 屬性， **AbsolutePosition** 是以1為基礎，而當目前記錄是記錄 **集**內的第一筆記錄時，則等於1。 您可以從[RecordCount](./recordcount-property-ado.md)屬性取得**記錄集**物件中的總記錄數。  
  
 當您設定 **AbsolutePosition** 屬性時，即使它是目前快取中的記錄，ADO 仍會以您指定的記錄開頭的新記錄組重載快取。 [CacheSize](./cachesize-property-ado.md)屬性會決定這個群組的大小。  
  
> [!NOTE]
>  您不應該使用 **AbsolutePosition** 屬性做為代理記錄號碼。 當您刪除先前的記錄時，指定記錄的位置會變更。 如果重新查詢或重新開啟**記錄集**物件，則也不保證指定的記錄會有相同的**AbsolutePosition** 。 書簽仍是保留並返回指定位置的建議方式，而且是在所有 **記錄集** 物件類型之間唯一定位的方法。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [AbsolutePosition 和 CursorLocation 屬性範例 (VB) ](./absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [AbsolutePosition 和 CursorLocation 屬性範例 (VC + +) ](./absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [ (ADO) 的 AbsolutePage 屬性 ](./absolutepage-property-ado.md)   
 [RecordCount 屬性 (ADO)](./recordcount-property-ado.md)