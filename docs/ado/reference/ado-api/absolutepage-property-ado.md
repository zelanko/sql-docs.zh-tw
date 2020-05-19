---
title: AbsolutePage 屬性（ADO） |Microsoft Docs
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
ms.openlocfilehash: 0da08a0c51c8d4d89329bbe9c36cacd7979c1e71
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747542"
---
# <a name="absolutepage-property-ado"></a>AbsolutePage 屬性 (ADO)
指出目前記錄所在的頁面。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 若是32位程式碼，會設定或傳回從1到[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件（[PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)）中的頁數，或傳回其中一個[PositionEnum](../../../ado/reference/ado-api/positionenum.md)值的**Long**值。  
  
 若是64位程式碼，請使用提供給64位值儲存的資料類型。 例如，您可以使用**Long**或其他可以是64位長度的值，例如 DBORDINAL。 請勿使用**PositionEnum**值，因為它們的長度限制為32位。  
  
## <a name="remarks"></a>備註  
 這個屬性可以用來識別目前記錄所在的頁碼。 它會使用[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)屬性，以邏輯方式將**記錄集**物件的總數據列集計數分割成一系列的頁面，其中每個都有等於**PageSize**的記錄數目（最後一頁可能會有較少的記錄）。 提供者必須支援適當的功能，才能使用此屬性。  
  
-   取得或設定**AbsolutePage**屬性時，ADO 會同時使用[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)屬性和[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)屬性，如下所示：  
  
-   為了取得**AbsolutePage**，ADO 會先抓取**AbsolutePosition**，然後再將它除以**PageSize**。  
  
-   若要設定**AbsolutePage**，ADO 會移動**AbsolutePosition** ，如下所示：它會將**PageSize**乘以新的**AbsolutePage**值，然後將1加到值中。 因此，成功設定**AbsolutePage**之後，**記錄集**內的目前位置是該頁面中的第一筆記錄。  
  
 如同**AbsolutePosition**屬性， **AbsolutePage**是以1為基礎，而當目前記錄是**記錄集**內的第一筆記錄時，等於1。 設定此屬性，以移至特定頁面的第一筆記錄。 從**PageCount**屬性取得總頁數。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [AbsolutePage、PageCount 和 PageSize 屬性範例（VB）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、PageCount 和 PageSize 屬性範例（VC + +）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePosition 屬性（ADO）](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [PageCount 屬性（ADO）](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [PageSize 屬性 (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)
