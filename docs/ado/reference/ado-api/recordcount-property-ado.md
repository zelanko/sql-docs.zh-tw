---
description: RecordCount 屬性 (ADO)
title: " (ADO) 的 RecordCount 屬性 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: b307a4116731016858ce4cc74f37bdcfbd258f3a
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88772477"
---
# <a name="recordcount-property-ado"></a>RecordCount 屬性 (ADO)

指出記錄 [集](./recordset-object-ado.md) 物件中的記錄數目。
  
## <a name="return-value"></a>傳回值

傳回 **Long** 值，指出記錄 **集中**的記錄數目。
  
## <a name="remarks"></a>備註

您可以使用 **RecordCount** 屬性來找出 **記錄集** 物件中有多少筆記錄。 當 ADO 無法判斷記錄的數目或提供者或資料指標類型不支援 **RecordCount**時，屬性會傳回-1。 讀取已關閉**記錄集**上的**RecordCount**屬性會導致錯誤。

#### <a name="bookmarks-or-approximate-positioning"></a>書簽或近似位置

如果記錄集物件支援書簽或近似位置，這個屬性 *會* 傳回記錄集內的確切記錄數目。 不論是否已完整填入記錄集，這個屬性都會傳回確切的數位。

相反地，如果記錄集物件不 *支援書簽* 或大約的位置，則存取這個屬性可能會耗用大量資源。 因為所有記錄都必須取出並計算，以傳回精確的 RecordCount 值，所以會發生清空。

- 與書簽相關的**adBookmark** 。
- **adApproxPosition** 與大約的定位有關。

> [!NOTE]
> 在 ADO 2.8 及更早版本中，當使用伺服器端資料指標時，SQLOLEDB 提供者會提取所有記錄，儘管 **它針對兩者** 都 **支援 (AdApproxPosition) ** 並 **支援 (adBookmark) **。
  
**記錄集**物件的資料指標類型會影響是否可判斷記錄的數目。 針對順向資料指標， **RecordCount** 屬性會傳回-1;靜態或索引鍵集資料指標的實際計數;以及-1 或動態資料指標的實際計數（視資料來源而定）。
  
## <a name="applies-to"></a>套用至

[Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱

[ (VB) 的 Filter 和 RecordCount 屬性範例 ](./filter-and-recordcount-properties-example-vb.md)   
[ (VC + +) 的 Filter 和 RecordCount 屬性範例 ](./filter-and-recordcount-properties-example-vc.md)   
[ (ADO) 的 AbsolutePosition 屬性 ](./absoluteposition-property-ado.md)   
[PageCount 屬性 (ADO)](./pagecount-property-ado.md)