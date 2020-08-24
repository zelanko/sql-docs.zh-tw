---
description: AbsolutePage 屬性 (ADO)
title: " (ADO) 的 AbsolutePage 屬性 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3c5c9d802dd6ba373b7bf92f063125f0b656eab8
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759988"
---
# <a name="absolutepage-property-ado"></a>AbsolutePage 屬性 (ADO)
指出目前記錄所在的頁面。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 若為32位程式碼，則會將 **Long** 值從1設定或傳回至 [記錄集](./recordset-object-ado.md) 物件中的頁面數目 ([PageCount](./pagecount-property-ado.md)) ，或傳回其中一個 [PositionEnum](./positionenum.md) 值。  
  
 若為64位的程式碼，請使用提供的資料類型來儲存64位值。 例如，您可以使用 **Long** 或可能是64位長度的其他值，例如 DBORDINAL。 請勿使用 **PositionEnum** 值，因為它們受限於32位長度。  
  
## <a name="remarks"></a>備註  
 這個屬性可以用來識別目前記錄所在的頁碼。 它會使用 [PageSize](./pagesize-property-ado.md) 屬性，以邏輯方式將 **記錄集** 物件的總數據列集計數分割成一系列的頁面，其中每一個頁面都有等於 **PageSize** (的記錄數目，但最後一個頁面可能會有較少的記錄) 。 提供者必須支援適當的功能，才能使用此屬性。  
  
-   取得或設定 **AbsolutePage** 屬性時，ADO 會一起使用 [AbsolutePosition](./absoluteposition-property-ado.md) 屬性和 [PageSize](./pagesize-property-ado.md) 屬性，如下所示：  
  
-   為了取得 **AbsolutePage**，ADO 會先抓取 **AbsolutePosition**，然後再除以 **PageSize**。  
  
-   若要設定 **AbsolutePage**，ADO 會移動 **AbsolutePosition** ，如下所示：它會將 **PageSize** 乘以新的 **AbsolutePage** 值，然後將值加1。 如此一來，在成功設定**AbsolutePage**之後，**記錄集**內的目前位置就是該頁面中的第一筆記錄。  
  
 如同 **AbsolutePosition** 屬性， **AbsolutePage** 是以1為基礎，而當目前記錄是記錄 **集**內的第一筆記錄時，則等於1。 將此屬性設定為移至特定頁面的第一筆記錄。 取得 **PageCount** 屬性中的總頁數。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [AbsolutePage、PageCount 和 PageSize 屬性範例 (VB) ](./absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、PageCount 和 PageSize 屬性範例 (VC + +) ](./absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [ (ADO) 的 AbsolutePosition 屬性 ](./absoluteposition-property-ado.md)   
 [ (ADO) 的 PageCount 屬性 ](./pagecount-property-ado.md)   
 [PageSize 屬性 (ADO)](./pagesize-property-ado.md)