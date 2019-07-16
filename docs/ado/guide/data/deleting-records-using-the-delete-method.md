---
title: 刪除使用 Delete 方法的資料錄 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5a862a244f06c64767f41529b4fff36881895a0b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925551"
---
# <a name="deleting-records-using-the-delete-method"></a>使用 Delete 方法刪除記錄
使用**刪除**群組中的記錄或目前的記錄方法會將標記**資料錄集**為要刪除的物件。 如果**資料錄集**物件不允許刪除記錄，則會發生錯誤。 如果您是在立即更新模式中，刪除資料庫中會立即發生。 記錄如果記錄無法成功地刪除 （因為資料庫完整性違規，例如），將會保留在編輯模式下呼叫之後**更新。** 這表示您必須取消更新使用[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)再移離目前的記錄 (例如，使用[關閉](../../../ado/reference/ado-api/close-method-ado.md)，[移動](../../../ado/reference/ado-api/move-method-ado.md)，或[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md))。  
  
 如果您是在批次更新模式中，記錄標示為刪除，從快取，而實際的刪除作業發生當您呼叫**UpdateBatch**方法。 (若要檢視已刪除的記錄，請設定**篩選條件**屬性設**adFilterAffectedRecords**之後**刪除**稱為。)  
  
 嘗試擷取已刪除的資料錄的欄位值，就會產生錯誤。 刪除目前的記錄之後, 已刪除的資料錄保持最新狀態直到您將移至不同的記錄。 一旦您離開已刪除的資料錄，就無法再存取。  
  
 如果您使用巢狀交易中的刪除，您可以使用來復原已刪除的記錄**RollbackTrans**方法。 如果您是在批次更新模式中，您可以使用取消的暫止刪除或暫止的刪除動作群組**CancelBatch**方法。  
  
 如果嘗試刪除記錄失敗，因為與基礎資料發生衝突 （例如，記錄已刪除另一位使用者），提供者會傳回警告**錯誤**集合，但不會不會中斷程式執行。 只有當所有要求的記錄上會發生衝突，就會發生執行階段錯誤。  
  
 如果**唯一資料表**動態屬性會設定並**資料錄集**是執行在多個資料表，聯結作業的結果**刪除**方法會只刪除資料列從資料表中名為**唯一資料表**屬性。  
  
 **刪除**方法會採用選擇性引數，可讓您指定哪些記錄會受到**刪除**作業。 唯一有效的值，這個引數不是屬於下列 ADO **AffectEnum**列舉常數：  
  
-   **adAffectCurrent**會影響目前的記錄。  
  
-   **adAffectGroup**影響只符合目前的記錄**篩選**屬性設定。 **篩選條件**屬性必須設為**FilterGroupEnum**值或陣列**書籤**才能使用此選項。  
  
 下列程式碼會顯示指定的範例**adAffectGroup**呼叫時**刪除**方法。 本範例會加入此範例中的某些記錄**資料錄集**並更新資料庫。 然後它會篩選**Recordset**使用**adFilterAffectedRecords**篩選列舉的常數，但只會新加入的記錄顯示在**資料錄集。** 最後，它會呼叫**刪除**方法，並指定所有符合目前的記錄**篩選**應該刪除屬性的設定 （新的記錄）。  
  
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
