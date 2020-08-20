---
description: 使用 Delete 方法刪除記錄
title: 使用 Delete 方法刪除記錄 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, deleting records
- deleting records [ADO]
- editing data [ADO], Delete method
- Delete method [ADO]
ms.assetid: bfed5cfa-7f57-463b-9da2-0c612a079d30
author: rothja
ms.author: jroth
ms.openlocfilehash: 3d8a29f2e1f35ddddc28e4aa3fb3c52c649e3056
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453530"
---
# <a name="deleting-records-using-the-delete-method"></a>使用 Delete 方法刪除記錄
使用 **Delete** 方法會將目前的記錄或記錄 **集** 物件中的一組記錄標記為刪除。 如果 **記錄集** 物件不允許刪除記錄，則會發生錯誤。 如果您是在立即更新模式中，則會立即在資料庫中進行刪除。 如果無法成功刪除記錄 (由於資料庫完整性違規（例如) ），記錄在呼叫 Update 之後仍會維持在編輯模式中 **。** 這表示您必須先使用 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 來取消更新，才能移出目前的記錄 (例如，使用 [Close](../../../ado/reference/ado-api/close-method-ado.md)、 [Move](../../../ado/reference/ado-api/move-method-ado.md)或 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)) 。  
  
 如果您是在批次更新模式中，則會將記錄標示為從快取中刪除，而且當您呼叫 **UpdateBatch** 方法時，就會實際刪除。  (若要查看已刪除的記錄，請在呼叫**Delete**之後，將**Filter**屬性設定為**adFilterAffectedRecords** 。 )   
  
 嘗試從已刪除的記錄中取出域值會產生錯誤。 刪除目前的記錄之後，已刪除的記錄會維持在最新狀態，直到您移至不同的記錄為止。 當您離開已刪除的記錄之後，就無法再存取。  
  
 如果您在交易中嵌套刪除，您可以使用 **RollbackTrans** 方法來復原已刪除的記錄。 如果您是在批次更新模式中，可以使用 **CancelBatch** 方法來取消暫止的刪除或暫止刪除群組。  
  
 如果嘗試刪除記錄失敗，因為與基礎資料發生衝突 (例如，其他使用者) 已刪除記錄，則提供者會將警告傳回至 **錯誤** 集合，但不會停止程式執行。 只有在所有要求的記錄有衝突時，才會發生執行階段錯誤。  
  
 如果已設定 **Unique table** 動態屬性，而且 **記錄集** 是在多個資料表上執行聯結作業的結果，則 **Delete** 方法只會從 **Unique table** 屬性中所指定的資料表刪除資料列。  
  
 **Delete**方法會採用選擇性引數，可讓您指定**刪除**作業會影響哪些記錄。 此引數唯一有效的值是下列其中一個 ADO **AffectEnum** 列舉常數：  
  
-   **adAffectCurrent** 只會影響目前的記錄。  
  
-   **adAffectGroup** 只會影響符合目前 **篩選** 屬性設定的記錄。 **篩選**屬性必須設定為**FilterGroupEnum**值或**書簽**陣列，才能使用此選項。  
  
 下列程式碼顯示呼叫**Delete**方法時指定**adAffectGroup**的範例。 此範例會將一些記錄新增至範例 **記錄集** ，並更新資料庫。 然後，它會使用**adFilterAffectedRecords** filter 列舉常數來篩選**記錄集**，這只會將新加入的記錄保留在**記錄集中。** 最後，它會呼叫 **Delete** 方法，並指定符合目前 **篩選** 屬性設定的所有記錄， (新的記錄) 應該刪除。  
  
```  
'BeginDeleteGroup  
    'add some bogus records  
    With objRs  
        For i = 0 To 8  
            .AddNew  
            .Fields("CompanyName") = "Shipper Number " & i + 1  
            .Fields("Phone") = "(425) 555-000" & (i + 1)  
            .Update  
        Next i  
  
        ' update  
        .UpdateBatch  
  
        'filter on newly added records  
        .Filter = adFilterAffectedRecords  
        Debug.Print "Deleting the " & .RecordCount & _  
                    " records you just added."  
  
        'delete the newly added bogus records  
        .Delete adAffectGroup  
        .Filter = adFilterNone  
        Debug.Print .RecordCount & " records remain."  
    End With  
'EndDeleteGroup  
```
