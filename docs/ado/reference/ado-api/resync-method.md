---
title: "重新同步處理方法 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset20::raw_Resync
- Fields::Resync
- Recordset20::Resync
- Fields::raw_Resync
helpviewer_keywords: Resync method [ADO]
ms.assetid: 73b355d4-a4c0-434b-bfc4-039b1c76b32e
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 101e2695a47b2c255aac94aedb6b613c1fca15c6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="resync-method"></a>重新同步處理方法
在目前的資料重新整理[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，或[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件，從基礎資料庫。  
  
## <a name="syntax"></a>語法  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>參數  
 *AffectRecords*  
 選擇性。 [AffectEnum](../../../ado/reference/ado-api/affectenum.md)值，決定多少記錄**重新同步處理**方法將會影響。 預設值是**adAffectAll**。 這個值不是適用於**重新同步處理**方法**欄位**集合**記錄**物件。  
  
 *ResyncValues*  
 選擇性。 A [ResyncEnum](../../../ado/reference/ado-api/resyncenum.md)值，指定是否會覆寫基礎的值。 預設值是**adResyncAllValues**。  
  
## <a name="remarks"></a>備註  
  
## <a name="recordset"></a>資料錄集  
 使用**重新同步處理**方法來重新同步處理在目前的記錄**資料錄集**與基礎資料庫。 如果您使用其中一個是靜態或順向資料指標，但您想要查看基礎資料庫中的任何變更，這非常有用。  
  
 如果您設定[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性**adUseClient**，**重新同步處理**只適用於非唯讀**資料錄集**物件。  
  
 不同於[Requery](../../../ado/reference/ado-api/requery-method.md)方法，**重新同步處理**方法不會重新執行**資料錄集**物件之基礎命令。 基礎資料庫中的新記錄不會顯示。  
  
 如果嘗試重新同步處理失敗因為與基礎資料衝突 （例如，某筆記錄被其他使用者已刪除），提供者所傳回的警告，[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合且執行階段發生錯誤。 使用[篩選](../../../ado/reference/ado-api/filter-property.md)屬性 (**adFilterConflictingRecords**) 和[狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性找出具有衝突的記錄。  
  
 如果[唯一資料表](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)和[重新同步處理命令](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)設定的動態屬性，而**資料錄集**是執行多個資料表，然後的聯結運算的結果**重新同步處理**方法會執行命令中指定**重新同步處理命令**屬性只在資料表中名為**唯一資料表**屬性。  
  
## <a name="fields"></a>欄位  
 使用**重新同步處理**方法來重新同步處理的值**欄位**集合**記錄**與基礎資料來源的物件。 [計數](../../../ado/reference/ado-api/count-property-ado.md)屬性不會受到這個方法。  
  
 如果*ResyncValues*設**adResyncAllValues** （預設值）， [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)，[值](../../../ado/reference/ado-api/value-property-ado.md)，和[OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md)屬性[欄位](../../../ado/reference/ado-api/field-object.md)同步處理集合中的物件。 如果*ResyncValues*設**adResyncUnderlyingValues**，則只**UnderlyingValue**屬性同步處理。  
  
 值**狀態**每個屬性**欄位**物件在呼叫時也會影響行為**重新同步處理**。 如**欄位**物件**狀態**值**adFieldPendingUnknown**或**adFieldPendingInsert**，**重新同步處理**沒有任何作用。 如**狀態**值**adFieldPendingChange**或**adFieldPendingDelete**，**重新同步處理**同步處理欄位的資料值，仍存在於資料來源。  
  
 **重新同步處理**也不會修改**狀態**值**欄位**物件，除非發生錯誤時**重新同步處理**呼叫。 例如，如果欄位不存在，提供者會傳回適當**狀態**值**欄位**物件，例如**adFieldDoesNotExist**。 傳回**狀態**值以邏輯方式組合的值內**狀態**屬性。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>請參閱  
 [重新同步處理方法的範例 (VB)](../../../ado/reference/ado-api/resync-method-example-vb.md)   
 [重新同步處理方法的範例 （VC + +）](../../../ado/reference/ado-api/resync-method-example-vc.md)   
 [Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [UnderlyingValue 屬性](../../../ado/reference/ado-api/underlyingvalue-property.md)
