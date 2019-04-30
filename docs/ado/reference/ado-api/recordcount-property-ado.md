---
title: RecordCount 屬性 (ADO) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: fa6f29c480244919de71d06cf3d56e672f00c47f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240065"
---
# <a name="recordcount-property-ado"></a>RecordCount 屬性 (ADO)

表示中的記錄數目[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。
  
## <a name="return-value"></a>傳回值

傳回**長**值，指出中的記錄數目**資料錄集**。
  
## <a name="remarks"></a>備註

使用**RecordCount**屬性，找出多少筆記錄位於**資料錄集**物件。 屬性會傳回-1，當 ADO 無法判斷的記錄數目，或提供者或資料指標類型不支援**RecordCount**。 讀取**RecordCount**屬性已關閉**資料錄集**會造成錯誤。

#### <a name="bookmarks-or-approximate-positioning"></a>書籤或大約位置

如果資料錄集物件*沒有*支援任一個書籤或近似定位，這個屬性會傳回記錄的確切數目的資料錄集。 這個屬性會傳回確切的數字，不論是否已完全填入資料錄集。

相反地，如果資料錄集物件*不*支援書籤或大約定位，存取這個屬性可能是資源的大量消耗。 因為必須擷取所有記錄，以及計算在內，以傳回精確的 RecordCount 值，就會發生清空。

- **adBookmark**與書籤。
- **adApproxPosition**與約略位置。

> [!NOTE]
> 2.8 和更早版本的 ADO 版本，SQLOLEDB 提供者會擷取所有記錄使用伺服器端資料指標時，它會傳回儘管 **，則為 True**同時**支援 (adApproxPosition)** 和**支援 (adBookmark)**。
  
資料指標類型**資料錄集**物件會影響是否可判斷記錄數目。 **RecordCount**屬性會傳回-1 的順向資料指標; 靜態的實際計數或 keyset 資料指標，並可能是-1 或動態資料指標，根據資料來源的實際計數。
  
## <a name="applies-to"></a>適用於

[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱

[Filter 和 RecordCount 屬性範例 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[Filter 和 RecordCount 屬性範例 （VC + +）](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[AbsolutePosition 屬性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[PageCount 屬性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
