---
title: "PageCount 屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::PageCount
helpviewer_keywords:
- PageCount property [ADO]
ms.assetid: b601b56c-0ac4-44ee-bc91-c3d2d104f00a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d0ce12f42693b58a57ecc4a08c186027a054bc80
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="pagecount-property-ado"></a>PageCount 屬性 (ADO)
表示網頁的資料數量[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)包含物件。  
  
## <a name="return-value"></a>傳回值  
 傳回**長**值，指出在頁數**資料錄集**。  
  
## <a name="remarks"></a>備註  
 使用**PageCount**屬性來判斷多少頁的資料是在**資料錄集**物件。 *頁面*是群組的記錄，其大小等於[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)屬性設定。 即使最後一頁不完整，因為有較少的記錄比**PageSize**值，它會計算為一個額外的頁面中**PageCount**值。 如果**資料錄集**物件不支援這個屬性，此值會是 – 1，表示**PageCount**不確定。  
  
 請參閱**PageSize**和[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)多個開啟的頁面功能的屬性。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [AbsolutePage、 PageCount 和 PageSize 屬性範例 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、 PageCount 和 PageSize 屬性範例 （VC + +）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage 屬性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [PageSize 屬性 (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)   
 [RecordCount 屬性 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
