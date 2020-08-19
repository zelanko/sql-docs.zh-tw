---
description: StayInSync 屬性
title: StayInSync 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::StayInSync
- Recordset20::put_StayInSync
- Recordset20::PutStayInSync
- Recordset20::get_StayInSync
- Recordset20::GetStayInSync
helpviewer_keywords:
- StayInSync property
ms.assetid: 502d69b5-dc9a-455d-b115-a03bd39a552b
author: rothja
ms.author: jroth
ms.openlocfilehash: 7bd35cbd24dadef9d6a9468f65bc85f95169d0cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441880"
---
# <a name="stayinsync-property"></a>StayInSync 屬性
指出階層式 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件中的基礎子記錄參考是否 (也就是，在父資料列位置變更時 *，) 變更* 。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **布林** 值。 預設值是 **True**。 若 **為 True**，則會在父 **記錄集** 物件變更資料列位置時更新章節;如果 **為 False**，則表示章節將繼續參考上一章中的資料，即使父 **記錄集** 物件已變更資料列位置也一樣。  
  
## <a name="remarks"></a>備註  
 這個屬性會套用至階層式記錄集（例如 [Microsoft 資料成形服務針對 OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)所支援的記錄集），而且必須先在父 **記錄** 集上設定，才能抓取子 **記錄集** 。 這個屬性可簡化流覽階層式記錄集的流程。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的 StayInSync 屬性範例 ](../../../ado/reference/ado-api/stayinsync-property-example-vb.md)   
 [適用于 OLE DB (ADO 服務提供者的 Microsoft 資料成形服務) ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)
