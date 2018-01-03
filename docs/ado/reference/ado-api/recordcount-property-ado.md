---
title: "RecordCount 屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::RecordCount
- Recordset15::GetRecordCount
- Recordset15::get_RecordCount
helpviewer_keywords: RecordCount property [ADO]
ms.assetid: 834f0121-394a-44d4-ad7d-999b43a6fe63
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f33a73aa4aa322d6eb0a00612789f4048a24e85d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="recordcount-property-ado"></a>RecordCount 屬性 (ADO)
表示中的記錄數目[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
## <a name="return-value"></a>傳回值  
 傳回**長**值，指出中的記錄數目**資料錄集**。  
  
## <a name="remarks"></a>備註  
 使用**RecordCount**屬性，找出多少記錄位於**資料錄集**物件。 屬性會傳回-1，當 ADO 無法判斷記錄數目，或提供者或資料指標類型不支援**RecordCount**。 讀取**RecordCount**上關閉屬性**資料錄集**會造成錯誤。  
  
 如果**資料錄集**物件支援大約定位或書籤。 也就是說，**支援 (adApproxPosition)**或**支援 (adBookmark)**，分別傳回**True**??? 這個值會記錄中的確切數目**資料錄集**，不論是否已經完全擴展。 如果**資料錄集**物件不支援大約定位，因為所有的記錄會擷取和計算以傳回正確的這個屬性可能是資源的大量消耗**RecordCount**值。  
  
> [!NOTE]
>  在 ADO 版本 2.8 及更早版本，SQLOLEDB 提供者擷取所有記錄使用伺服器端資料指標時，它會傳回儘管**True**兩者**支援 (adApproxPosition)**和**支援 (adBookmark)**。  
  
 資料指標類型的**資料錄集**物件會影響是否可判斷記錄數目。 **RecordCount**屬性會傳回-1 的順向資料指標; 實際計數靜態或索引鍵集資料指標; 和-1 或動態資料指標，根據資料來源的實際計數。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>請參閱  
 [篩選器和 RecordCount 屬性範例 (VB)](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vb.md)   
 [篩選器和 RecordCount 屬性範例 （VC + +）](../../../ado/reference/ado-api/filter-and-recordcount-properties-example-vc.md)   
 [AbsolutePosition 屬性 (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [PageCount 屬性 (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
