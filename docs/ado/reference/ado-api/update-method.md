---
title: Update 方法 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Update
helpviewer_keywords:
- Update method [ADO]
ms.assetid: 6b2a9c31-1a7e-40db-8a53-30720d0f6cc1
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0183e7e490a653efab4e4a7a3575d60491c28182
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="update-method"></a>Update 方法
儲存您對目前資料列的任何變更[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，或[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>參數  
 *欄位*  
 選擇性。 A **Variant**代表單一名稱，或**Variant**陣列，表示名稱或您想要修改的欄位或欄位的序數位置。  
  
 *值*  
 選擇性。 A **Variant** ，表示的單一值，或**Variant**代表新記錄中的欄位值的陣列。  
  
## <a name="remarks"></a>備註  
  
## <a name="recordset"></a>資料錄集  
 使用**更新**方法，即可儲存您對目前記錄的任何變更**資料錄集**物件後呼叫[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)方法，或自變更中的任何欄位值現有的記錄。 **資料錄集**物件必須支援更新。  
  
 若要設定欄位值，執行下列其中一項：  
  
-   將值指派給[欄位](../../../ado/reference/ado-api/field-object.md)物件的[值](../../../ado/reference/ado-api/value-property-ado.md)屬性並呼叫**更新**方法。  
  
-   將欄位名稱和值傳遞做為引數與**更新**呼叫。  
  
-   傳遞陣列的欄位名稱和值的陣列**更新**呼叫。  
  
 當您使用的欄位和值的陣列時，必須有相同數量的兩個陣列中的項目。 此外，欄位名稱的順序必須符合欄位值的順序。 如果不相符的數目與順序的欄位和值，就會發生錯誤。  
  
 如果**資料錄集**物件支援批次更新，您可以快取多對一或多個記錄的變更在本機直到您呼叫[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法。 如果您正在編輯目前的記錄或加入新的記錄，當您呼叫**UpdateBatch**自動呼叫方法時，ADO 會**更新**方法來儲存目前的記錄之前的任何暫止的變更傳送給提供者的批次的變更。  
  
 如果您將記錄從您要加入或編輯，然後再呼叫**更新**自動呼叫方法時，ADO 會**更新**儲存的變更。 您必須呼叫[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法，如果您想要取消目前的記錄所做的變更或捨棄新加入的記錄。  
  
 目前的記錄會保留目前之後呼叫**更新**方法。  
  
## <a name="record"></a>記錄  
 **更新**方法完成新增、 刪除與欄位中更新[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合**記錄**物件。  
  
 例如，欄位時刪除**刪除**方法會立即標示為刪除，但保留在集合中。 **更新**必須呼叫方法，以從提供者的集合中實際刪除這些欄位。  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>另請參閱  
 [更新和 CancelUpdate 方法範例 (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [更新和 CancelUpdate 方法範例 （VC + +）](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [AddNew 方法 (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [CancelUpdate 方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [EditMode 屬性](../../../ado/reference/ado-api/editmode-property.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
