---
description: Resync 方法
title: 重新同步方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::raw_Resync
- Fields::Resync
- Recordset20::Resync
- Fields::raw_Resync
helpviewer_keywords:
- Resync method [ADO]
ms.assetid: 73b355d4-a4c0-434b-bfc4-039b1c76b32e
author: rothja
ms.author: jroth
ms.openlocfilehash: 6e64c2f297e4628f04f99a7e97a6b9df00f6efa1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777647"
---
# <a name="resync-method"></a>Resync 方法
從基礎資料庫重新整理目前[記錄集](./recordset-object-ado.md)物件中的資料，或[記錄](./record-object-ado.md)物件的[欄位](./fields-collection-ado.md)集合中的資料。  
  
## <a name="syntax"></a>語法  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>參數  
 *AffectRecords*  
 選擇性。 [AffectEnum](./affectenum.md)值，可決定重新**同步**方法將會影響的記錄數目。 預設值為 **adAffectAll**。 **記錄**物件之**Fields**集合的**Resync**方法無法使用這個值。  
  
 *ResyncValues*  
 選擇性。 指定是否覆寫基礎值的 [ResyncEnum](./resyncenum.md) 值。 預設值為 **adResyncAllValues**。  
  
## <a name="remarks"></a>備註  
  
## <a name="recordset"></a>資料錄集  
 使用 **Resync** 方法可將目前 **記錄集** 內的記錄與基礎資料庫重新同步處理。 如果您使用靜態或順向資料指標，但您想要查看基礎資料庫中的任何變更，這會很有用。  
  
 如果您將 [CursorLocation](./cursorlocation-property-ado.md) 屬性設定為 **adUseClient**，則 [重新 **同步** 處理] 只適用于非唯讀的 **記錄集** 物件。  
  
 與 [Requery](./requery-method.md) 方法不同的是， **Resync** 方法不會重新執行 **記錄集** 物件的基礎命令。 基礎資料庫中的新記錄將不會顯示。  
  
 如果嘗試重新同步處理失敗，因為與基礎資料相衝突 (例如，其他使用者) 已刪除記錄，則提供者會將警告傳回至 [錯誤](./errors-collection-ado.md) 集合，併發生執行階段錯誤。 使用 [Filter](./filter-property.md) 屬性 (**AdFilterConflictingRecords**) 和 [Status](./status-property-ado-recordset.md) 屬性來尋找有衝突的記錄。  
  
 如果已設定[Unique table](./unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)和[Resync 命令](./resync-command-property-dynamic-ado.md)動態屬性，而且**記錄集**是在多個資料表上執行聯結作業的結果，則**resync**方法只會在**Unique Table**屬性中命名的資料表上，執行**resync 命令**屬性中提供的命令。  
  
## <a name="fields"></a>欄位  
 使用**Resync**方法，將**Record**物件的**Fields**集合值與基礎資料來源重新同步。 [Count](./count-property-ado.md)屬性不受此方法影響。  
  
 如果*ResyncValues*設定為**adResyncAllValues** (預設值) ，則會同步處理集合中[欄位](./field-object.md)物件的[UnderlyingValue](./underlyingvalue-property.md)、 [value](./value-property-ado.md)和[OriginalValue](./originalvalue-property-ado.md)屬性。 如果 *ResyncValues* 設定為 **adResyncUnderlyingValues**，則只會同步處理 **UnderlyingValue** 屬性。  
  
 在呼叫時，每個**欄位**物件的**Status**屬性值也會影響重新**同步**的行為。 對於具有**adFieldPendingUnknown**或 adFieldPendingInsert**狀態值**的**欄位**物件， **adFieldPendingInsert** **Resync**沒有任何作用。 針對**adFieldPendingChange**或**adFieldPendingDelete**的**狀態值**， **Resync**會同步處理仍存在於資料來源之欄位的資料值。  
  
 除非在呼叫重新**同步**時發生錯誤，否則重新**同步**處理不會修改**欄位**物件的**狀態值**。 例如，如果欄位已不存在，則提供者會為**field**物件傳回適當的**狀態值**，例如**adFieldDoesNotExist**。 傳回的 **狀態值** 可以邏輯方式結合在 **Status** 屬性的值內。  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [Fields 集合 (ADO)](./fields-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Recordset 物件 (ADO)](./recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另請參閱  
 [ (VB) 的 Resync 方法範例 ](./resync-method-example-vb.md)   
 [ (VC + +) 的 Resync 方法範例 ](./resync-method-example-vc.md)   
 [ (ADO) 的 Clear 方法 ](./clear-method-ado.md)   
 [UnderlyingValue 屬性](./underlyingvalue-property.md)