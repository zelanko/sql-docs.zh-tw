---
title: 刪除資料錄使用 Delete 方法 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, deleting records
- deleting records [ADO]
- editing data [ADO], Delete method
- Delete method [ADO]
ms.assetid: bfed5cfa-7f57-463b-9da2-0c612a079d30
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a708b3ed5d709be7a05e50a0511f29e3f1430e89
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270337"
---
# <a name="deleting-records-using-the-delete-method"></a>使用 Delete 方法刪除記錄
使用**刪除**方法會標示為目前的記錄或群組中的記錄**資料錄集**為要刪除的物件。 如果**資料錄集**物件不允許刪除記錄，就會發生錯誤。 如果您是在立即更新模式中，刪除資料庫中會立即發生。 如果無法成功 （因為資料庫完整性違規，如範例） 刪除記錄，記錄之後，仍處於編輯模式下呼叫**更新。** 這表示您必須取消更新使用[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)再移離目前的記錄 (例如，使用[關閉](../../../ado/reference/ado-api/close-method-ado.md)，[移動](../../../ado/reference/ado-api/move-method-ado.md)，或[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md))。  
  
 如果您是在批次更新模式中，記錄標示為刪除從快取，當您呼叫時，會發生實際刪除**UpdateBatch**方法。 (若要檢視已刪除的記錄，設定**篩選**屬性**adFilterAffectedRecords**之後**刪除**稱為。)  
  
 嘗試從已刪除的記錄擷取欄位的值會產生錯誤。 刪除目前的記錄後, 已刪除的記錄會保留目前直到您移動到不同的記錄為止。 一次您離開刪除的記錄，就無法再存取。  
  
 如果您建立巢狀交易中的刪除，您可以使用復原已刪除的記錄**RollbackTrans**方法。 如果您是在批次更新模式中，您可以使用取消的暫止刪除或一組暫止的刪除**CancelBatch**方法。  
  
 如果嘗試刪除的記錄失敗，因為與基礎資料衝突 （例如，記錄已刪除另一位使用者），提供者所傳回的警告，**錯誤**集合，但未中止程式執行。 只有當要求的所有記錄中都有衝突，就會發生執行階段錯誤。  
  
 如果**唯一資料表**動態屬性設定和**資料錄集**是執行多個資料表中聯結作業的結果**刪除**方法將只刪除資料列從資料表中名為**唯一資料表**屬性。  
  
 **刪除**方法會採用選擇性引數，可讓您指定的記錄受到**刪除**作業。 唯一有效的值，這個引數不是屬於下列 ADO **AffectEnum**列舉常數：  
  
-   **adAffectCurrent**會影響目前的記錄。  
  
-   **adAffectGroup**會影響滿足目前的記錄**篩選**屬性設定。 **篩選**屬性必須設定為**FilterGroupEnum**值或陣列**書籤**才能使用此選項。  
  
 下列程式碼顯示範例指定**adAffectGroup**呼叫時**刪除**方法。 這個範例會將某些記錄範例**資料錄集**並更新資料庫。 然後它會篩選**資料錄集**使用**adFilterAffectedRecords**篩選列舉的常數，這會將新加入的記錄中看見**資料錄集。** 最後，它會呼叫**刪除**方法，並指定所有符合目前的記錄**篩選**應該刪除屬性設定 （新的記錄）。  
  
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
