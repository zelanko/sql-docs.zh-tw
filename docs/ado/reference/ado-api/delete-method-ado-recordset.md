---
title: Delete 方法（ADO Recordset） |Microsoft Docs
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
ms.openlocfilehash: b978e3d885e3ff06dda18859384f88eb4c564254
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919127"
---
# <a name="delete-method-ado-recordset"></a>Delete 方法 (ADO Recordset)
刪除目前的記錄或一組記錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>參數  
 *AffectRecords*  
 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，決定**Delete**方法會影響多少記錄。 預設值為**adAffectCurrent**。  
  
> [!NOTE]
>  **adAffectAll**和**adAffectAllChapters**不是要**刪除**的有效引數。  
  
## <a name="remarks"></a>備註  
 使用**Delete**方法會將目前的記錄或記錄[集](../../../ado/reference/ado-api/recordset-object-ado.md)物件中的一組記錄標記為要刪除。 如果**記錄集**物件不允許刪除記錄，就會發生錯誤。 如果您處於立即更新模式，則會立即在資料庫中進行刪除。 如果無法成功刪除記錄（例如，由於資料庫完整性違規），記錄將會在呼叫[更新](../../../ado/reference/ado-api/update-method.md)之後維持在編輯模式。 這表示您必須先取消具有[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)的更新，再移出目前的記錄（例如，使用[Close](../../../ado/reference/ado-api/close-method-ado.md)、 [Move](../../../ado/reference/ado-api/move-method-ado.md)或[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)）。  
  
 如果您是在批次更新模式中，則會將記錄標示為從快取中刪除，而實際的刪除作業會在您呼叫[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法時進行。 使用 [[篩選](../../../ado/reference/ado-api/filter-property.md)] 屬性來查看已刪除的記錄。  
  
 從已刪除的記錄中抓取域值會產生錯誤。 刪除目前的記錄之後，已刪除的記錄會保持為最新狀態，直到您移至不同的記錄為止。 當您離開已刪除的記錄之後，就無法再存取它。  
  
 如果您在交易中嵌套刪除，您可以使用[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法來復原已刪除的記錄。 如果您是在批次更新模式中，您可以使用[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法來取消暫止的刪除或暫止刪除群組。  
  
 如果嘗試刪除記錄因為與基礎資料衝突而失敗（例如，另一位使用者已刪除記錄），則提供者會將警告傳回給[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合，但不會停止程式執行。 只有在所有要求的記錄有衝突時，才會發生執行階段錯誤。  
  
 如果已[設定唯一的資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)動態屬性，而且**記錄集**是在多個資料表上執行聯結作業的結果，則**Delete**方法只會從[唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)屬性中名為的資料表中刪除資料列。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Delete 方法範例（VB）](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [Delete 方法範例（VBScript）](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [Delete 方法範例（VC + +）](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [Delete 方法（ADO Fields 集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法（ADO Parameters 集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)
