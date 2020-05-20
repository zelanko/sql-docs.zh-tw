---
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
ms.openlocfilehash: a8da01b9c92aeec9c01527370e19c8edfb751da9
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763619"
---
# <a name="deleting-records-using-the-delete-method"></a>使用 Delete 方法刪除記錄
使用**Delete**方法會將目前的記錄或記錄**集**物件中的一組記錄標記為要刪除。 如果**記錄集**物件不允許刪除記錄，就會發生錯誤。 如果您處於立即更新模式，則會立即在資料庫中進行刪除。 如果無法成功刪除記錄（例如，由於資料庫完整性違規），記錄將會在呼叫更新之後維持在編輯模式 **。** 這表示您必須先使用[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)取消更新，然後再移出目前的記錄（例如，使用[Close](../../../ado/reference/ado-api/close-method-ado.md)、 [Move](../../../ado/reference/ado-api/move-method-ado.md)或[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)）。  
  
 如果您是在批次更新模式中，則會將記錄標示為從快取中刪除，而實際的刪除作業會在您呼叫**UpdateBatch**方法時進行。 （若要查看已刪除的記錄，請在呼叫**Delete**之後，將**Filter**屬性設定為**adFilterAffectedRecords** 。）  
  
 嘗試從已刪除的記錄中取出域值會產生錯誤。 刪除目前的記錄之後，已刪除的記錄會保持為最新狀態，直到您移至不同的記錄為止。 當您離開已刪除的記錄之後，就無法再存取它。  
  
 如果您在交易中嵌套刪除，您可以使用**RollbackTrans**方法來復原已刪除的記錄。 如果您是在批次更新模式中，您可以使用**CancelBatch**方法來取消暫止的刪除或暫止刪除群組。  
  
 如果嘗試刪除記錄因為與基礎資料衝突而失敗（例如，另一位使用者已刪除記錄），則提供者會將警告傳回給**錯誤**集合，但不會停止程式執行。 只有在所有要求的記錄有衝突時，才會發生執行階段錯誤。  
  
 如果已**設定唯一的資料表**動態屬性，而**記錄集**是在多個資料表上執行聯結作業的結果，則**Delete**方法只會刪除**唯一資料表**屬性中所命名之資料表的資料列。  
  
 **Delete**方法會接受選擇性的引數，讓您指定哪些記錄會受到**刪除**作業的影響。 這個引數唯一的有效值是下列其中一個 ADO **AffectEnum**列舉常數：  
  
-   **adAffectCurrent**只會影響目前的記錄。  
  
-   **adAffectGroup**只會影響符合目前**篩選**屬性設定的記錄。 **篩選**屬性必須設定為**FilterGroupEnum**值或**書簽**陣列，才能使用此選項。  
  
 下列程式碼顯示呼叫**Delete**方法時，指定**adAffectGroup**的範例。 這個範例會將一些記錄新增至範例**記錄集**，並更新資料庫。 然後，它會使用**adFilterAffectedRecords**篩選列舉常數來篩選**記錄集**，而這只會使新加入的記錄只會顯示在**記錄集中。** 最後，它會呼叫**Delete**方法，並指定滿足目前**篩選**屬性設定（新記錄）的所有記錄都應該刪除。  
  
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
