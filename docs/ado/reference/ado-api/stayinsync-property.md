---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18d17e0a761fe03053ba90b8ff1ef87f3067df76
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67930741"
---
# <a name="stayinsync-property"></a>StayInSync 屬性
指出階層式[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件中，當父資料列位置變更時，基礎子記錄（也就是*章節*）的參考是否會變更。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**布林**值。 預設值為 **True**。 若**為 True**，則當父**記錄集**物件變更資料列位置時，將會更新該章節;若**為 False**，即使父**記錄集**物件已變更資料列位置，本章仍會繼續參考上一章中的資料。  
  
## <a name="remarks"></a>備註  
 這個屬性會套用至階層式記錄集，例如適用[于 OLE DB 的 Microsoft 資料成形服務](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)所支援，而且必須在取得子**記錄集**之前于父**記錄集**上設定。 此屬性可簡化階層式記錄集的導覽。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [StayInSync 屬性範例（VB）](../../../ado/reference/ado-api/stayinsync-property-example-vb.md)   
 [適用于 OLE DB 的 Microsoft 資料成形服務（ADO 服務提供者）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)
