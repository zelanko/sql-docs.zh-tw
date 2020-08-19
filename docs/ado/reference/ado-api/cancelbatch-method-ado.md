---
description: CancelBatch 方法 (ADO)
title: " (ADO) 的 CancelBatch 方法 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f8fa4d02dd10325726c83a6b645ebdd5b94397f9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451030"
---
# <a name="cancelbatch-method-ado"></a>CancelBatch 方法 (ADO)
取消暫止的批次更新。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>參數  
 *AffectRecords*  
 選擇性。 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，指出**CancelBatch**方法將會影響的記錄數目。  
  
## <a name="remarks"></a>備註  
 您可以使用 **CancelBatch** 方法，以批次更新模式取消 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 內的任何暫止更新。 如果**記錄集**是在立即更新模式中，則在沒有**adAffectCurrent**的情況下呼叫**CancelBatch**會產生錯誤。  
  
 如果您要編輯目前的記錄，或在呼叫 **CancelBatch**時加入新的記錄，ADO 會先呼叫 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 方法來取消任何快取的變更。 之後，就會取消 **記錄集** 內的所有暫止變更。  
  
 目前的記錄可能會在 **CancelBatch** 呼叫之後未知，特別是當您正在新增記錄的過程中。 基於這個理由，在**CancelBatch**呼叫之後，將目前的記錄位置設定為**記錄集**內的已知位置是明智的。 例如，呼叫 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) 方法。  
  
 如果嘗試取消暫止的更新因為與基礎資料發生衝突而失敗 (例如，如果另一位使用者) 刪除了記錄，則提供者會將警告傳回至 [錯誤](../../../ado/reference/ado-api/errors-collection-ado.md) 集合，但不會終止程式執行。 只有在所有要求的記錄有衝突時，才會發生執行階段錯誤。 使用 [Filter](../../../ado/reference/ado-api/filter-property.md) 屬性 (**AdFilterAffectedRecords**) 和 [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) 屬性來尋找有衝突的記錄。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的 UpdateBatch 和 CancelBatch 方法範例 ](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch 和 CancelBatch 方法範例 (VC + +) ](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [ (ADO) 的 Cancel 方法 ](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [ (RDS) 的 Cancel 方法 ](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [ (ADO) 的 CancelUpdate 方法 ](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [RDS)  (CancelUpdate 方法 ](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [ (ADO) 的 Clear 方法 ](../../../ado/reference/ado-api/clear-method-ado.md)   
 [ (ADO) 的 LockType 屬性 ](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
