---
title: RecordCount 屬性 (ADO) |Microsoft 文件
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords:
- RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a6ee9d1ea1c4e996c9608bc1ce76ff3f1baa7c62
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
---
# <a name="recordcount-property-ado"></a>RecordCount 屬性 (ADO)

表示中的記錄數目[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。
  
## <a name="return-value"></a>傳回值

傳回**長**值，指出中的記錄數目**資料錄集**。
  
## <a name="remarks"></a>備註

使用**RecordCount**屬性，找出多少記錄位於**資料錄集**物件。 屬性會傳回-1，當 ADO 無法判斷記錄數目，或提供者或資料指標類型不支援**RecordCount**。 讀取**RecordCount**上關閉屬性**資料錄集**會造成錯誤。

#### <a name="bookmarks-or-approximate-positioning"></a>書籤或近似定位

如果資料錄集物件*沒有*支援任一個書籤或近似定位，這個屬性會傳回精確的記錄數目的資料錄集中。 這個屬性會傳回確切的數字，不論是否已經完全填入資料錄集。

相反地，如果資料錄集物件*不*支援書籤或大約位置，存取這個屬性可能會大量消耗資源。 所有記錄必須擷取和計算以傳回精確的 RecordCount 值，就會發生清空。

- **adBookmark**與書籤。
- **adApproxPosition**大約位置與相關。

> [!NOTE]
> 在 ADO 版本 2.8 及更早版本，SQLOLEDB 提供者擷取所有記錄使用伺服器端資料指標時，它會傳回儘管**True**兩者**支援 (adApproxPosition)**和**支援 (adBookmark)**。
  
資料指標類型的**資料錄集**物件會影響是否可判斷記錄數目。 **RecordCount**屬性會傳回-1 的順向資料指標; 實際計數靜態或索引鍵集資料指標; 和-1 或動態資料指標，根據資料來源的實際計數。
  
## <a name="applies-to"></a>適用於

[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱

[篩選器和 RecordCount 屬性範例 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
[篩選器和 RecordCount 屬性範例 （VC + +）](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
[AbsolutePosition 屬性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
[PageCount 屬性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
