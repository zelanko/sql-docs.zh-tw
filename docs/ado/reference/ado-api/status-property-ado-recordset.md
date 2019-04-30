---
title: Status 屬性 (ADO Recordset) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetStatus
- Recordset15::Status
helpviewer_keywords:
- Status property [ADO Recordset]
ms.assetid: 41d70d89-880f-4850-9d17-19d9790cc8eb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5847300af48b39dc12ccb65f5e03f1fdc6f8e795
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63275884"
---
# <a name="status-property-ado-recordset"></a>Status 屬性 (ADO Recordset)
指出相對於批次更新目前的記錄或其他的大量作業的狀態。  
  
## <a name="return-value"></a>傳回值  
 傳回一或多個總和[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)值。  
  
## <a name="remarks"></a>備註  
 使用**狀態**屬性，以查看哪些變更被暫止的修改在批次更新的記錄。 您也可以使用**狀態**屬性，以檢視在大量作業，例如當您呼叫期間失敗的記錄狀態[重新同步處理](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)上的方法[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，或設定[篩選](../../../ado/reference/ado-api/filter-property.md)屬性**資料錄集**物件陣列的書籤。 這個屬性中，您可以決定如何指定的記錄失敗及解決它。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Status 屬性範例 (Recordset) (VB)](../../../ado/reference/ado-api/status-property-example-recordset-vb.md)   
 [Status 屬性範例 (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
