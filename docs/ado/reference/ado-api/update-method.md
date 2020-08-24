---
description: Update 方法
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 819e6ebaa3932f19a693cb3d50651f7c451200e6
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776997"
---
# <a name="update-method"></a>Update 方法
儲存您對[記錄集](./recordset-object-ado.md)物件的目前資料列所做的任何變更，或[記錄](./record-object-ado.md)物件的[Fields](./fields-collection-ado.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>參數  
 *欄位*  
 選擇性。 代表單一名稱的 **variant** 或 **variant** 陣列，代表欄位或您想要修改之欄位的名稱或序數位置。  
  
 *值*  
 選擇性。 表示單一值的 **variant** 或 **variant** 陣列，表示新記錄中欄位或欄位的值。  
  
## <a name="remarks"></a>備註  
  
## <a name="recordset"></a>資料錄集  
 您可以使用 **Update** 方法，將您對 **記錄集** 物件的目前記錄所做的任何變更，從呼叫 [AddNew](./addnew-method-ado.md) 方法或變更現有記錄中的任何域值起。 **記錄集**物件必須支援更新。  
  
 若要設定域值，請執行下列其中一項：  
  
-   指派值給 [Field](./field-object.md) 物件的 [Value](./value-property-ado.md) 屬性，並呼叫 **Update** 方法。  
  
-   以 **更新** 呼叫傳遞功能變數名稱和值做為引數。  
  
-   使用 **Update** 呼叫傳遞功能變數名稱陣列和值陣列。  
  
 當您使用欄位和值的陣列時，這兩個數組中的元素數目必須相同。 此外，功能變數名稱的順序必須符合域值的順序。 如果欄位和值的數目和順序不符，就會發生錯誤。  
  
 如果 **記錄集** 物件支援批次更新，您可以在本機快取一或多個記錄的多個變更，直到您呼叫 [UpdateBatch](./updatebatch-method.md) 方法為止。 如果您要編輯目前的記錄，或在呼叫 **UpdateBatch** 方法時加入新的記錄，ADO 會自動呼叫 **Update** 方法，在將批次變更傳送給提供者之前，先將任何暫止的變更儲存至目前的記錄。  
  
 如果您在呼叫 **update** 方法之前從要新增或編輯的記錄中移動，ADO 會自動呼叫 **update** 來儲存變更。 如果您想要取消對目前記錄所做的任何變更或捨棄新加入的記錄，則必須呼叫 [CancelUpdate](./cancelupdate-method-ado.md) 方法。  
  
 當您呼叫 **Update** 方法之後，目前的記錄仍保持為最新狀態。  
  
## <a name="record"></a>Record  
 **Update**方法會完成**記錄**物件之[fields](./fields-collection-ado.md)集合中欄位的新增、刪除和更新。  
  
 例如，使用 **Delete** 方法刪除的欄位會被標示為立即刪除，但會保留在集合中。 必須呼叫 **Update** 方法，才能實際從提供者的集合中刪除這些欄位。  
  
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
 [Update 和 CancelUpdate 方法範例 (VB) ](./update-and-cancelupdate-methods-example-vb.md)   
 [Update 和 CancelUpdate 方法範例 (VC + +) ](./update-and-cancelupdate-methods-example-vc.md)   
 [ (ADO) 的 AddNew 方法 ](./addnew-method-ado.md)   
 [ (ADO) 的 CancelUpdate 方法 ](./cancelupdate-method-ado.md)   
 [EditMode 屬性](./editmode-property.md)   
 [UpdateBatch 方法](./updatebatch-method.md)