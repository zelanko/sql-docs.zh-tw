---
description: Status 屬性 (ADO Recordset)
title: Status 屬性 (ADO 記錄集) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7869ff91269d033b14a7f77e014da70962a1c1d5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441930"
---
# <a name="status-property-ado-recordset"></a>Status 屬性 (ADO Recordset)
指出與批次更新或其他大量作業相關的目前記錄狀態。  
  
## <a name="return-value"></a>傳回值  
 傳回一或多個 [RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md) 值的總和。  
  
## <a name="remarks"></a>備註  
 您可以使用 [ **狀態** ] 屬性來查看批次更新期間修改的記錄有哪些變更暫止。 您也可以使用 [**狀態**] 屬性來查看在大量作業期間失敗的記錄狀態，例如當您在[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件上呼叫[Resync](../../../ado/reference/ado-api/resync-method.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法，或將**記錄集**物件上的[Filter](../../../ado/reference/ado-api/filter-property.md)屬性設定為書簽的陣列時。 您可以使用這個屬性來判斷指定的記錄如何失敗，並據此加以解決。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Status 屬性範例 (記錄集)  (VB) ](../../../ado/reference/ado-api/status-property-example-recordset-vb.md)   
 [Status 屬性範例 (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
