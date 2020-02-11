---
title: UpdateBatch 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::UpdateBatch
- Recordset15::raw_UpdateBatch
helpviewer_keywords:
- UpdateBatch method [ADO]
ms.assetid: 23f9314c-b027-4a51-aeae-50caa2977740
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e9d74fe938ce486a4cd15573af8166dbed12ba6f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67937846"
---
# <a name="updatebatch-method"></a>UpdateBatch 方法
將所有暫止的批次更新寫入磁片。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>參數  
 *AffectRecords*  
 選擇性。 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，指出**UpdateBatch**方法會影響多少記錄。  
  
 *PreserveStatus*  
 選擇性。 **布林**值，指定是否應該認可本機變更（如[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性所表示）。 如果此值設定為**True**，則在更新完成之後，每筆記錄的**Status**屬性會維持不變。  
  
## <a name="remarks"></a>備註  
 在批次更新模式中修改**記錄集**物件時，請使用**UpdateBatch**方法，將**記錄集**物件中進行的所有變更傳送至基礎資料庫。  
  
 如果**記錄集**物件支援批次更新，您可以在本機快取一或多筆記錄的多個變更，直到您呼叫**UpdateBatch**方法為止。 如果您要在呼叫**UpdateBatch**方法時編輯目前的記錄或加入新的記錄，ADO 會自動呼叫[Update](../../../ado/reference/ado-api/update-method.md)方法，將任何暫止的變更儲存至目前的記錄，再將批次變更傳送給提供者。 您應該只使用索引鍵集或靜態資料指標來進行批次更新。  
  
> [!NOTE]
>  將**adAffectGroup**指定為此參數的值，將會在目前的**記錄集**內沒有任何可見記錄（例如沒有記錄符合的篩選）時產生錯誤。  
  
 如果因為基礎資料發生衝突而導致任何或所有記錄的傳輸變更失敗（例如，另一位使用者已刪除記錄），則提供者會將警告傳回給[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合，併發生執行階段錯誤。 使用[Filter](../../../ado/reference/ado-api/filter-property.md)屬性（**AdFilterAffectedRecords**）和[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性來找出具有衝突的記錄。  
  
 若要取消所有暫止的批次更新，請使用[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法。  
  
 如果設定[了唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)和[更新](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)的重新同步動態屬性，而**記錄集**是在多個資料表上執行聯結作業的結果，則根據[更新重新同步](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)處理屬性的設定，執行**UpdateBatch**方法時，會隱含地跟隨重新[同步](../../../ado/reference/ado-api/resync-method.md)處理方法。  
  
 在資料來源上執行批次之個別更新的順序，不一定會與在本機**記錄集**上執行的順序相同。 更新順序會視提供者而定。 在撰寫彼此相關的更新程式碼時，例如插入或更新的外鍵條件約束，請將此納入考慮。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [UpdateBatch 和 CancelBatch 方法範例（VB）](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch 和 CancelBatch 方法範例（VC + +）](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [CancelBatch 方法（ADO）](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Clear 方法（ADO）](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType 屬性（ADO）](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
