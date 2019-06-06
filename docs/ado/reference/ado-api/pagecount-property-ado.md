---
title: PageCount 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::PageCount
helpviewer_keywords:
- PageCount property [ADO]
ms.assetid: b601b56c-0ac4-44ee-bc91-c3d2d104f00a
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5187c73d4dde95a5ddd9396da95b2d4381c868c8
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706935"
---
# <a name="pagecount-property-ado"></a>PageCount 屬性 (ADO)
表示網頁的資料數量[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件包含。  
  
## <a name="return-value"></a>傳回值  
 傳回**長**值，指出頁面數**資料錄集**。  
  
## <a name="remarks"></a>備註  
 使用**PageCount**屬性來判斷多少頁的資料是在**資料錄集**物件。 *頁面*是一組的記錄，其大小等於[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)屬性設定。 即使最後一頁是不完整，因為有較少的記錄，比**PageSize**的值，它會計算為中的其他頁面**PageCount**值。 如果**Recordset**物件不支援這個屬性，此值會是-1 表示**PageCount**不確定。  
  
 請參閱**PageSize**並[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)屬性多個開啟的頁面功能。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [AbsolutePage、 PageCount、 和 PageSize 屬性範例 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、 PageCount、 和 PageSize 屬性範例 （VC + +）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage 屬性 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [PageSize 屬性 (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)   
 [RecordCount 屬性 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
