---
title: "StayInSync 屬性 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset20::StayInSync
- Recordset20::put_StayInSync
- Recordset20::PutStayInSync
- Recordset20::get_StayInSync
- Recordset20::GetStayInSync
helpviewer_keywords: StayInSync property
ms.assetid: 502d69b5-dc9a-455d-b115-a03bd39a552b
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 440cfbc89b1e5e1b221869880e061aad8711630f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="stayinsync-property"></a>StayInSync 屬性
表示以階層式[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件是否基礎的子記錄的參考 (也就是*章*) 變更，當父資料列變更時。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**布林**值。 預設值為 **True**。 如果**True**，章節，將會更新父系**資料錄集**物件變更資料列位置; 如果**False**，本章將繼續參考至前一章中的資料即使父**資料錄集**物件已變更的資料列位置。  
  
## <a name="remarks"></a>備註  
 這個屬性會套用至階層式資料錄集，例如支援的[Microsoft Data Shaping Service 的 OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)，和必須在父系上設定**資料錄集**子系之前**資料錄集**擷取。 這個屬性可簡化瀏覽階層式資料錄集。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>請參閱＜  
 [StayInSync 屬性範例 (VB)](../../../ado/reference/ado-api/stayinsync-property-example-vb.md)   
 [Microsoft 資料成形 OLE DB （ADO 服務提供者） 的服務](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)
