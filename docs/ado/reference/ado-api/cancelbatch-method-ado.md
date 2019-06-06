---
title: CancelBatch 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_CancelBatch
- Recordset15::CancelBatch
helpviewer_keywords:
- CancelBatch method [ADO]
ms.assetid: dbdc2574-e44e-4d95-b03d-4a5d9e9adf3c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 572738c966651e35f2980ea75c3770ddc4bd029d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66696175"
---
# <a name="cancelbatch-method-ado"></a>CancelBatch 方法 (ADO)
取消擱置中的批次更新。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>參數  
 *AffectRecords*  
 選擇性。 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，指出多少筆記錄**CancelBatch**方法將會影響。  
  
## <a name="remarks"></a>備註  
 使用**CancelBatch**方法來取消任何暫止更新[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)以批次更新模式。 如果**資料錄集**是立即更新模式中，呼叫**CancelBatch**而不需要**adAffectCurrent**會產生錯誤。  
  
 如果您正在編輯目前的記錄，或要新增新的記錄，當您呼叫**CancelBatch**，ADO 會先呼叫[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法來取消任何快取的變更。 在那之後，所有暫止的變更**資料錄集**已取消。  
  
 目前的記錄可能是未知之後**CancelBatch**呼叫，尤其是如果您正在新增新的記錄。 基於這個理由，最好將目前的記錄位置設定中的已知位置**Recordset**之後**CancelBatch**呼叫。 例如，呼叫[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法。  
  
 如果嘗試取消擱置中的更新失敗，因為基礎資料 （例如，如果記錄已刪除另一位使用者） 與發生衝突，提供者會傳回警告[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合，但不會不會中斷程式執行。 只有當所有要求的記錄上會發生衝突，就會發生執行階段錯誤。 使用[篩選條件](../../../ado/reference/ado-api/filter-property.md)屬性 (**adFilterAffectedRecords**) 和[狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性找出具有衝突的記錄。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [UpdateBatch 和 CancelBatch 方法範例 (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch 和 CancelBatch 方法範例 （VC + +）](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Cancel 方法 (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel 方法 (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelUpdate 方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate 方法 (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType 屬性 (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
