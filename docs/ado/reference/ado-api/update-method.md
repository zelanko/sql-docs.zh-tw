---
title: 更新方法 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938846"
---
# <a name="update-method"></a>Update 方法
儲存您對目前資料列的任何變更[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)物件，或有[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)的集合[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>參數  
 *欄位*  
 選擇性。 A **Variant**表示單一的名稱，或有**Variant**陣列，表示名稱或您想要修改的欄位或欄位的序數位置。  
  
 *值*  
 選擇性。 A **Variant** ，表示單一的值，或有**Variant**陣列，表示新記錄中欄位的值。  
  
## <a name="remarks"></a>備註  
  
## <a name="recordset"></a>資料錄集  
 使用**更新**方法來儲存您對目前記錄的任何變更**資料錄集**物件，因為呼叫[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)方法，或自變更中的任何欄位值現有的記錄。 **資料錄集**物件必須支援更新。  
  
 若要設定欄位值，執行下列其中一項動作：  
  
-   將值指派給[欄位](../../../ado/reference/ado-api/field-object.md)物件的[值](../../../ado/reference/ado-api/value-property-ado.md)屬性並呼叫**Update**方法。  
  
-   傳遞做為引數使用的欄位名稱和值**更新**呼叫。  
  
-   傳遞陣列的欄位名稱和值的陣列**更新**呼叫。  
  
 當您使用的欄位和值的陣列時，必須有相同數量的兩個陣列中的項目。 此外，欄位名稱的順序必須符合欄位值的順序。 如果不相符的欄位和值的順序與數量，就會發生錯誤。  
  
 如果**Recordset**物件支援的批次更新，直到您呼叫，在本機，您可以快取讓一或多個記錄的多個變更[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法。 如果您正在編輯目前的記錄，或加入新的記錄，當您呼叫**UpdateBatch**方法，ADO 會自動會呼叫**更新**方法，將任何暫止的變更儲存至目前的記錄之前傳輸批次的變更提供者。  
  
 如果您將記錄從您要加入或編輯，然後再呼叫**更新**方法，ADO 會自動會呼叫**更新**以儲存變更。 您必須呼叫[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法，如果您想要取消目前的記錄所做的變更或捨棄新加入的記錄。  
  
 目前的記錄會保留目前之後呼叫**更新**方法。  
  
## <a name="record"></a>記錄  
 **更新**方法完成新增、 刪除及更新中的欄位[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合**記錄**物件。  
  
 例如，刪除使用的欄位**刪除**方法會立即標示為刪除，但保留在集合中。 **更新**必須呼叫方法，以從提供者的集合中實際刪除這些欄位。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [Update 和 CancelUpdate 方法範例 (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Update 和 CancelUpdate 方法範例 （VC + +）](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew 方法 (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [CancelUpdate 方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [EditMode 屬性](../../../ado/reference/ado-api/editmode-property.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
