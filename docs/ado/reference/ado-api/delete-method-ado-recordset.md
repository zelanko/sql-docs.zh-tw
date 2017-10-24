---
title: "Delete 方法 （ADO 資料錄集） |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::raw_Delete
- Recordset15::Delete
helpviewer_keywords:
- Delete method [ADO]
ms.assetid: 1eb9209c-602c-4507-b0c2-6527a599b67d
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7555de66879f0caa75c72196c30c5a7ec3611249
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="delete-method-ado-recordset"></a>Delete 方法 （ADO 資料錄集）
刪除目前的記錄或一組記錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Delete AffectRecords  
```  
  
#### <a name="parameters"></a>參數  
 *AffectRecords*  
 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，決定多少記錄**刪除**方法將會影響。 預設值是**adAffectCurrent**。  
  
> [!NOTE]
>  **adAffectAll**和**adAffectAllChapters**不是有效的引數**刪除**。  
  
## <a name="remarks"></a>備註  
 使用**刪除**方法會標示為目前的記錄或群組中的記錄[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)為要刪除的物件。 如果**資料錄集**物件不允許刪除記錄，就會發生錯誤。 如果您是在立即更新模式中，刪除資料庫中會立即發生。 如果無法成功 （因為資料庫完整性違規，如範例） 刪除記錄，記錄之後，仍處於編輯模式下呼叫[更新](../../../ado/reference/ado-api/update-method.md)。 這表示您必須取消搭配 update [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)再移離目前的記錄 (例如，與[關閉](../../../ado/reference/ado-api/close-method-ado.md)，[移動](../../../ado/reference/ado-api/move-method-ado.md)，或[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md))。  
  
 如果您是在批次更新模式中，記錄標示為刪除從快取，當您呼叫時，會發生實際刪除[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法。 使用[篩選](../../../ado/reference/ado-api/filter-property.md)屬性可檢視已刪除的記錄。  
  
 從刪除的記錄擷取欄位的值會產生錯誤。 刪除目前的記錄後, 已刪除的記錄會保留目前直到您移動到不同的記錄為止。 一次您離開刪除的記錄，就無法再存取。  
  
 如果您建立巢狀交易中的刪除，您可以復原已刪除的記錄[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法。 如果您是在批次更新模式中，您可以取消的暫止刪除或一組暫止的刪除與[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法。  
  
 如果嘗試刪除的記錄失敗，因為與基礎資料衝突 （例如，記錄已刪除另一位使用者），提供者所傳回的警告，[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合，但未中止程式執行。 只有當要求的所有記錄中都有衝突，就會發生執行階段錯誤。  
  
 如果[唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)動態屬性設定，而**資料錄集**是執行多個資料表中聯結作業的結果則**刪除**方法只會刪除從資料表中的資料列[唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)屬性。  
  
## <a name="applies-to"></a>適用於  
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [刪除方法的範例 (VB)](../../../ado/reference/ado-api/delete-method-example-vb.md)   
 [刪除方法的範例 (VBScript)](../../../ado/reference/ado-api/delete-method-example-vbscript.md)   
 [刪除方法的範例 （VC + +）](../../../ado/reference/ado-api/delete-method-example-vc.md)   
 [Delete 方法 （ADO 欄位集合）](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Delete 方法 （ADO 參數集合）](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [DeleteRecord 方法 (ADO)](../../../ado/reference/ado-api/deleterecord-method-ado.md)

