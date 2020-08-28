---
description: UpdateBatch 方法
title: UpdateBatch 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 648e6f8e64d4001851afb3838c901ab2b1172108
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987999"
---
# <a name="updatebatch-method"></a>UpdateBatch 方法
將所有暫止的批次更新寫入磁片。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>參數  
 *AffectRecords*  
 選擇性。 [AffectEnum](./affectenum.md)值，指出**UpdateBatch**方法將會影響的記錄數目。  
  
 *PreserveStatus*  
 選擇性。 **布林**值，指定是否應該認可本機變更（如[Status](./status-property-ado-recordset.md)屬性所指示）。 如果這個值設定為 **True**，則在更新完成之後，每個記錄的 **Status** 屬性都會保持不變。  
  
## <a name="remarks"></a>備註  
 修改批次更新模式中的**記錄集**物件時，請使用**UpdateBatch**方法，將**記錄集**物件中所做的所有變更傳送到基礎資料庫。  
  
 如果 **記錄集** 物件支援批次更新，您可以在本機快取一或多個記錄的多個變更，直到您呼叫 **UpdateBatch** 方法為止。 如果您要編輯目前的記錄，或在呼叫 **UpdateBatch** 方法時加入新的記錄，ADO 會自動呼叫 [Update](./update-method.md) 方法，在將批次變更傳送給提供者之前，先將任何暫止的變更儲存至目前的記錄。 您應該只使用索引鍵集或靜態資料指標來進行批次更新。  
  
> [!NOTE]
>  將 **adAffectGroup** 指定為此參數的值，會在目前的 **記錄集中** 沒有可見記錄時產生錯誤 (例如，沒有任何記錄符合) 的篩選準則。  
  
 如果嘗試傳送任何或所有記錄的變更失敗，因為與基礎資料發生衝突 (例如，其他使用者) 已刪除記錄，則提供者會將警告傳回至 [錯誤](./errors-collection-ado.md) 集合，併發生執行階段錯誤。 使用 [Filter](./filter-property.md) 屬性 (**AdFilterAffectedRecords**) 和 [Status](./status-property-ado-recordset.md) 屬性來尋找有衝突的記錄。  
  
 若要取消所有暫止的批次更新，請使用 [CancelBatch](./cancelbatch-method-ado.md) 方法。  
  
 如果已設定[Unique Table](./unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)和[Update Resync](./update-resync-property-dynamic-ado.md)動態屬性，而且**記錄集**是在多個資料表上執行聯結作業的結果，則根據[更新同步](./update-resync-property-dynamic-ado.md)處理屬性的設定，執行**UpdateBatch**方法時，會隱含地接著重新[同步](./resync-method.md)處理方法。  
  
 在資料來源上執行個別更新的順序，不一定會與在本機 **記錄集**上執行的順序相同。 更新順序視提供者而定。 在撰寫彼此相關的更新（例如插入或更新的外鍵條件約束）時，請將這一點列入考慮。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的 UpdateBatch 和 CancelBatch 方法範例 ](./updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch 和 CancelBatch 方法範例 (VC + +) ](./updatebatch-and-cancelbatch-methods-example-vc.md)   
 [ (ADO) 的 CancelBatch 方法 ](./cancelbatch-method-ado.md)   
 [ (ADO) 的 Clear 方法 ](./clear-method-ado.md)   
 [ (ADO) 的 LockType 屬性 ](./locktype-property-ado.md)   
 [Update 方法](./update-method.md)