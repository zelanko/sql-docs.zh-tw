---
description: Delete 方法 (ADO Recordset)
title: " (ADO 記錄集的 Delete 方法) |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Delete
- Recordset15::Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 1eb9209c-602c-4507-b0c2-6527a599b67d
author: rothja
ms.author: jroth
ms.openlocfilehash: a43aa64d970865b8de706fc4297bba9fd0d18786
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974089"
---
# <a name="delete-method-ado-recordset"></a>Delete 方法 (ADO Recordset)
刪除目前的記錄或一組記錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>參數  
 *AffectRecords*  
 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，決定**刪除**方法將會影響的記錄數目。 預設值為 **adAffectCurrent**。  
  
> [!NOTE]
>  **adAffectAll** 和 **adAffectAllChapters** 不是有效的引數，無法 **刪除**。  
  
## <a name="remarks"></a>備註  
 使用 **Delete** 方法會將目前的記錄或記錄 [集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件中的一組記錄標記為刪除。 如果 **記錄集** 物件不允許刪除記錄，則會發生錯誤。 如果您是在立即更新模式中，則會立即在資料庫中進行刪除。 如果無法成功刪除記錄 (由於資料庫完整性違規（例如) ），記錄在呼叫 [Update](../../../ado/reference/ado-api/update-method.md)之後仍會維持在編輯模式中。 這表示您必須先取消 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 的更新，再將目前的記錄移出 (例如，使用 [Close](../../../ado/reference/ado-api/close-method-ado.md)、 [Move](../../../ado/reference/ado-api/move-method-ado.md)或 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)) 。  
  
 如果您是在批次更新模式中，則會將記錄標示為從快取中刪除，而且當您呼叫 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 方法時，就會實際刪除。 使用 [Filter](../../../ado/reference/ado-api/filter-property.md) 屬性來查看已刪除的記錄。  
  
 從已刪除的記錄中取出域值會產生錯誤。 刪除目前的記錄之後，已刪除的記錄會維持在最新狀態，直到您移至不同的記錄為止。 當您離開已刪除的記錄之後，就無法再存取。  
  
 如果您在交易中嵌套刪除，您可以使用 [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) 方法來復原已刪除的記錄。 如果您是在批次更新模式中，可以使用 [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) 方法來取消暫止的刪除或暫止刪除群組。  
  
 如果嘗試刪除記錄失敗，因為與基礎資料發生衝突 (例如，其他使用者) 已刪除記錄，則提供者會將警告傳回至 [錯誤](../../../ado/reference/ado-api/errors-collection-ado.md) 集合，但不會停止程式執行。 只有在所有要求的記錄有衝突時，才會發生執行階段錯誤。  
  
 如果已設定 [Unique table](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 動態屬性，而且 **記錄集** 是在多個資料表上執行聯結作業的結果，則 **Delete** 方法只會從 [Unique table](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) 屬性中所指定的資料表中刪除資料列。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Delete 方法範例 (VB) ](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [Delete 方法範例 (VBScript) ](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [Delete 方法範例 (VC + +) ](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [ (ADO Fields 集合) 的 Delete 方法 ](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 (ADO Parameters 集合) ](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
