---
title: Delete 方法 (ADO Recordset) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 272b953a39a9ccbb01d94acc59d374304bda3ad0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47770338"
---
# <a name="delete-method-ado-recordset"></a>Delete 方法 (ADO Recordset)
刪除目前的記錄或一組記錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>參數  
 *AffectRecords*  
 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，決定多少筆記錄**刪除**方法將會影響。 預設值是**adAffectCurrent**。  
  
> [!NOTE]
>  **adAffectAll**並**adAffectAllChapters**不是有效的引數**刪除**。  
  
## <a name="remarks"></a>備註  
 使用**刪除**群組中的記錄或目前的記錄方法會將標記[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)為要刪除的物件。 如果**資料錄集**物件不允許刪除記錄，則會發生錯誤。 如果您是在立即更新模式中，刪除資料庫中會立即發生。 記錄如果記錄無法成功地刪除 （因為資料庫完整性違規，例如），將會保留在編輯模式中呼叫後面[更新](../../../ado/reference/ado-api/update-method.md)。 這表示您必須取消與更新[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)再移離目前的記錄 (例如，使用[關閉](../../../ado/reference/ado-api/close-method-ado.md)，[移動](../../../ado/reference/ado-api/move-method-ado.md)，或[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md))。  
  
 如果您是在批次更新模式中，記錄標示為刪除，從快取，而實際的刪除作業發生當您呼叫[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法。 使用[篩選](../../../ado/reference/ado-api/filter-property.md)屬性可檢視已刪除的記錄。  
  
 擷取已刪除的資料錄的欄位值會產生錯誤。 刪除目前的記錄之後, 已刪除的資料錄保持最新狀態直到您將移至不同的記錄。 一旦您離開已刪除的資料錄，就無法再存取。  
  
 如果您使用巢狀交易中的刪除，您可以復原已刪除的記錄，與[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法。 如果您是在批次更新模式中，您可以取消暫止刪除或暫止的刪除與群[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法。  
  
 如果嘗試刪除記錄失敗，因為與基礎資料發生衝突 （例如，記錄已刪除另一位使用者），提供者會傳回警告[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合，但不會不會中斷程式執行。 只有當所有要求的記錄上會發生衝突，就會發生執行階段錯誤。  
  
 如果[唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)動態屬性設定，而**資料錄集**是執行在多個資料表，聯結作業的結果則**刪除**方法只會刪除從資料表中所命名的資料列[唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)屬性。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Delete 方法範例 (VB)](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [Delete 方法範例 (VBScript)](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [Delete 方法範例 （VC + +）](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [Delete 方法 (ADO Fields 集合)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO Parameters 集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
