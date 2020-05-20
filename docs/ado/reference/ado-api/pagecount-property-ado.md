---
title: PageCount 屬性（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ebb85eee8ea976f1ef078ebfe22eca195081bba
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762002"
---
# <a name="pagecount-property-ado"></a>PageCount 屬性 (ADO)
指出[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件包含多少頁的資料。  
  
## <a name="return-value"></a>傳回值  
 傳回**Long**值，指出**記錄集中**的頁面數目。  
  
## <a name="remarks"></a>備註  
 使用**PageCount**屬性來判斷**記錄集**物件中的資料頁數目。 *頁面*是一組記錄，其大小等於[PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md)屬性設定。 即使最後一頁不完整，因為記錄數目比**PageSize**值少，因此會計算為**PageCount**值中的額外頁面。 如果**記錄集**物件不支援此屬性，則值會是-1，表示**PageCount**是未知深度。  
  
 如需頁面功能的詳細資訊，請參閱**PageSize**和[AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)屬性。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [AbsolutePage、PageCount 和 PageSize 屬性範例（VB）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、PageCount 和 PageSize 屬性範例（VC + +）](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage 屬性（ADO）](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [PageSize 屬性（ADO）](../../../ado/reference/ado-api/pagesize-property-ado.md)   
 [RecordCount 屬性 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
