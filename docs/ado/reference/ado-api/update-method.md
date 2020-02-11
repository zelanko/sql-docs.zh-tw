---
title: Update 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Update
helpviewer_keywords:
- Update method [ADO]
ms.assetid: 6b2a9c31-1a7e-40db-8a53-30720d0f6cc1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ce247905afd6ed34366424f5f905d57b42d988f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938846"
---
# <a name="update-method"></a>Update 方法
儲存您對[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件的目前資料列或[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件的[Fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合所做的任何變更。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>參數  
 *欄位*  
 選擇性。 表示單一名稱的**variant**或**variant**陣列，表示您想要修改之欄位或欄位的名稱或序數位置。  
  
 *值*  
 選擇性。 表示單一值的**variant**或**variant**陣列，表示新記錄中的欄位或欄位的值。  
  
## <a name="remarks"></a>備註  
  
## <a name="recordset"></a>資料錄集  
 使用**Update**方法來儲存您對**記錄集**物件的目前記錄所做的任何變更，因為呼叫[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)方法或變更現有記錄中的任何域值。 **記錄集**物件必須支援更新。  
  
 若要設定域值，請執行下列其中一項動作：  
  
-   將值指派給[欄位](../../../ado/reference/ado-api/field-object.md)物件的[Value](../../../ado/reference/ado-api/value-property-ado.md)屬性，並呼叫**Update**方法。  
  
-   使用**Update**呼叫傳遞功能變數名稱和值做為引數。  
  
-   使用**Update**呼叫傳遞功能變數名稱陣列和值陣列。  
  
 當您使用欄位和值的陣列時，兩個數組中的元素數目必須相同。 此外，功能變數名稱的順序必須符合域值的順序。 如果欄位和值的數目和順序不相符，就會發生錯誤。  
  
 如果**記錄集**物件支援批次更新，您可以在本機快取一或多筆記錄的多個變更，直到您呼叫[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法為止。 如果您要在呼叫**UpdateBatch**方法時編輯目前的記錄或加入新的記錄，ADO 會自動呼叫**Update**方法，將任何暫止的變更儲存至目前的記錄，再將批次變更傳送給提供者。  
  
 如果您在呼叫**update**方法之前，從您要新增或編輯的記錄中移動，ADO 會自動呼叫**update**來儲存變更。 如果您想要取消對目前記錄所做的任何變更，或捨棄新加入的記錄，則必須呼叫[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法。  
  
 呼叫**Update**方法之後，目前的記錄仍維持最新。  
  
## <a name="record"></a>Record  
 **Update**方法會針對**Record**物件的[fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合中的欄位，完成新增、刪除和更新。  
  
 例如，使用**Delete**方法刪除的欄位會立即標示為要刪除，但會保留在集合中。 必須呼叫**Update**方法，才能從提供者的集合中實際刪除這些欄位。  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Update 和 CancelUpdate 方法範例（VB）](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Update 和 CancelUpdate 方法範例（VC + +）](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew 方法（ADO）](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [CancelUpdate 方法（ADO）](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [EditMode 屬性](../../../ado/reference/ado-api/editmode-property.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
