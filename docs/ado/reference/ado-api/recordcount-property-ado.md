---
title: RecordCount 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords:
- RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7304062298a95406a223ba58026379a3bebf392f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931476"
---
# <a name="recordcount-property-ado"></a>RecordCount 屬性 (ADO)

指出記錄[集](../../../ado/reference/ado-api/recordset-object-ado.md)物件中的記錄數目。
  
## <a name="return-value"></a>傳回值

傳回**Long**值，指出記錄**集中**的記錄數目。
  
## <a name="remarks"></a>備註

您可以使用**RecordCount**屬性來找出**記錄集**物件中有多少筆記錄。 當 ADO 無法判斷記錄的數目，或提供者或資料指標類型不支援**RecordCount**時，屬性會傳回-1。 讀取封閉**記錄集**上的**RecordCount**屬性會造成錯誤。

#### <a name="bookmarks-or-approximate-positioning"></a>書簽或近似定位

如果記錄集物件支援書簽或近似位置，此屬性*會*傳回記錄集內的確切記錄數目。 這個屬性會傳回確切的數位，而不論記錄集是否已完全填入。

相反地，如果記錄集物件不*支援書簽*或近似位置，存取此屬性可能會耗用大量資源。 清空會發生，因為所有記錄都必須取得並計算，才會傳回精確的 RecordCount 值。

- 與書簽相關的**adBookmark** 。
- **adApproxPosition**與大約的定位相關。

> [!NOTE]
> 在 ADO 版本2.8 和舊版中，當使用伺服器端資料指標時，SQLOLEDB 提供者會提取所有記錄，儘管它傳回**True**同時**支援（AdApproxPosition）** 和**支援（adBookmark）**。
  
**記錄集**物件的資料指標類型會影響是否可以判斷記錄的數目。 對於順向資料指標， **RecordCount**屬性會傳回-1;靜態或索引鍵集資料指標的實際計數;視資料來源而定，也可以是-1 或動態資料指標的實際計數。
  
## <a name="applies-to"></a>套用至

[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱

[Filter 和 RecordCount 屬性範例（VB）](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[Filter 和 RecordCount 屬性範例（VC + +）](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[AbsolutePosition 屬性（ADO）](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[PageCount 屬性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
