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
manager: jroth
ms.openlocfilehash: 11c930efdffe5eb685494843f2b0abe7b753ea3d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710412"
---
# <a name="updatebatch-method"></a>UpdateBatch 方法
寫入磁碟中的所有暫止的批次更新。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>參數  
 *AffectRecords*  
 選擇性。 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，指出多少筆記錄**UpdateBatch**方法將會影響。  
  
 *PreserveStatus*  
 選擇性。 A**布林**值，指定是否本機變更時，所示[狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性，都應該認可。 如果此值設為**真**，則**狀態**每一筆記錄的屬性在更新完成之後會維持不變。  
  
## <a name="remarks"></a>備註  
 使用**UpdateBatch**方法時修改**資料錄集**傳輸中的所有變更的批次更新模式中物件**資料錄集**基礎資料庫的物件。  
  
 如果**Recordset**物件支援的批次更新，直到您呼叫，在本機，您可以快取讓一或多個記錄的多個變更**UpdateBatch**方法。 如果您正在編輯目前的記錄，或加入新的記錄，當您呼叫**UpdateBatch**方法，ADO 會自動會呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法，將任何暫止的變更儲存至目前的記錄之前傳輸批次的變更提供者。 您應該使用批次使用 keyset 或 static 資料指標更新。  
  
> [!NOTE]
>  指定**adAffectGroup**中目前沒有任何可見的記錄時，此參數的值會造成錯誤**資料錄集**（例如，沒有記錄符合篩選條件）。  
  
 如果嘗試傳輸變更因為與基礎資料發生衝突而失敗的任何或所有的記錄 （例如，記錄已刪除另一位使用者），提供者會傳回警告[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合和會發生執行階段錯誤。 使用[篩選條件](../../../ado/reference/ado-api/filter-property.md)屬性 (**adFilterAffectedRecords**) 和[狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性找出具有衝突的記錄。  
  
 若要取消所有擱置中的批次更新，請使用[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)方法。  
  
 如果[唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)並[更新重新同步處理](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)設定的動態屬性，而**資料錄集**是執行在多個資料表，聯結作業的結果則執行**UpdateBatch**方法隱含後面[重新同步處理](../../../ado/reference/ado-api/resync-method.md)方法，視設定而定[重新同步處理更新](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md)屬性。  
  
 資料來源所執行之批次個別更新的順序不一定是在本機所執行的順序相同**資料錄集**。 更新順序是取決於提供者。 撰寫程式碼彼此相關，例如外部索引鍵條件約束的 insert 或 update 的更新時，請考慮這點。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [UpdateBatch 和 CancelBatch 方法範例 (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch 和 CancelBatch 方法範例 （VC + +）](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [CancelBatch 方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType 屬性 (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
