---
title: Status 屬性（ADO Recordset） |Microsoft Docs
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
ms.openlocfilehash: 1d91c3e92be7679ad6fbbb4a4ee7bd1bb6a48422
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "67916832"
---
# <a name="status-property-ado-recordset"></a>Status 屬性 (ADO Recordset)
指出目前記錄有關批次更新或其他大量作業的狀態。  
  
## <a name="return-value"></a>傳回值  
 傳回一或多個[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)值的總和。  
  
## <a name="remarks"></a>備註  
 使用 [**狀態**] 屬性，查看在批次更新期間修改的記錄有哪些變更擱置中。 您也可以使用 [**狀態**] 屬性來查看在大量作業期間失敗的記錄狀態，例如當您在[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件上呼叫[Resync](../../../ado/reference/ado-api/resync-method.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)或[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法，或將**記錄集**物件上的[Filter](../../../ado/reference/ado-api/filter-property.md)屬性設定為書簽陣列時。 使用此屬性，您可以判斷指定的記錄如何失敗，並據此解決。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Status 屬性範例（Recordset）（VB）](../../../ado/reference/ado-api/status-property-example-recordset-vb.md)   
 [Status 屬性範例 (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
