---
title: CancelBatch 方法（ADO） |Microsoft Docs
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
ms.openlocfilehash: f1c6a9f57d30b47641b9280e25a97336c28b0496
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920165"
---
# <a name="cancelbatch-method-ado"></a>CancelBatch 方法 (ADO)
取消暫止的批次更新。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>參數  
 *AffectRecords*  
 選擇性。 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，指出**CancelBatch**方法將會影響多少筆記錄。  
  
## <a name="remarks"></a>備註  
 使用**CancelBatch**方法，在批次更新模式中取消[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)內任何暫止的更新。 如果**記錄集**處於立即更新模式，在沒有**adAffectCurrent**的情況下呼叫**CancelBatch**會產生錯誤。  
  
 如果您要編輯目前的記錄，或在呼叫**CancelBatch**時加入新的記錄，ADO 會先呼叫[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法來取消任何快取的變更。 之後，就會取消**記錄集中**所有暫止的變更。  
  
 目前的記錄可能會在**CancelBatch**呼叫之後未知深度，特別是在您加入新記錄的過程中。 基於這個理由，在**CancelBatch**呼叫之後，將目前的記錄位置設定為**記錄集**內的已知位置是很謹慎的。 例如，呼叫[MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法。  
  
 如果嘗試取消暫止的更新會因為基礎資料衝突而失敗（例如，如果另一位使用者已刪除記錄），則提供者會將警告傳回給[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合，但不會停止程式執行。 只有在所有要求的記錄有衝突時，才會發生執行階段錯誤。 使用[Filter](../../../ado/reference/ado-api/filter-property.md)屬性（**AdFilterAffectedRecords**）和[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性來找出具有衝突的記錄。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [UpdateBatch 和 CancelBatch 方法範例（VB）](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch 和 CancelBatch 方法範例（VC + +）](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Cancel 方法（ADO）](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel 方法（RDS）](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelUpdate 方法（ADO）](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate 方法（RDS）](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Clear 方法（ADO）](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType 屬性（ADO）](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
