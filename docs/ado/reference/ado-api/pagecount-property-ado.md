---
description: PageCount 屬性 (ADO)
title: " (ADO) 的 PageCount 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 335f28c570ef240db6d65b66ef33f907d0202816
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990199"
---
# <a name="pagecount-property-ado"></a>PageCount 屬性 (ADO)
指出 [記錄集](./recordset-object-ado.md) 物件包含多少頁面的資料。  
  
## <a name="return-value"></a>傳回值  
 傳回 **Long** 值，指出 **記錄集中**的頁面數目。  
  
## <a name="remarks"></a>備註  
 您可以使用 **PageCount** 屬性來判斷 **記錄集** 物件中有多少頁面的資料。 *頁面* 是其大小等於 [PageSize](./pagesize-property-ado.md) 屬性設定的記錄群組。 即使最後一個頁面不完整，因為記錄比 **PageSize** 值少，因此它會計算為 **PageCount** 值中的額外頁面。 如果 **記錄集** 物件不支援這個屬性，則值會是-1，表示 **PageCount** 是未知。  
  
 如需頁面功能的詳細資訊，請參閱 **PageSize** 和 [AbsolutePage](./absolutepage-property-ado.md) 屬性。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [AbsolutePage、PageCount 和 PageSize 屬性範例 (VB) ](./absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage、PageCount 和 PageSize 屬性範例 (VC + +) ](./absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [ (ADO) 的 AbsolutePage 屬性 ](./absolutepage-property-ado.md)   
 [ (ADO) 的 PageSize 屬性 ](./pagesize-property-ado.md)   
 [RecordCount 屬性 (ADO)](./recordcount-property-ado.md)