---
title: 偵測和解決衝突 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- conflicts [ADO], detecting and resolving
- ADO, detecting and resolving conflicts
ms.assetid: b28fdd26-c1a4-40ce-a700-2b0c9d201514
author: rothja
ms.author: jroth
ms.openlocfilehash: d3b3a9f4c5482d0171c59a734aa6139bc2239c55
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761084"
---
# <a name="detecting-and-resolving-conflicts"></a>偵測並解決衝突
如果您是以即時模式處理記錄集，則會有更少的機率發生並行問題。 另一方面，如果您的應用程式使用批次模式更新，則在儲存另一位使用者編輯相同記錄所做的變更之前，可能會有一位使用者變更記錄的可能性很好。 在這種情況下，您會想要讓應用程式正常地處理衝突。 您可能想要讓最後一個人將更新傳送至伺服器「獲勝」。 或者，您可能會想要讓使用者可以選擇兩個衝突的值，以決定應優先進行哪些更新。  
  
 不論是哪種情況，ADO 都會提供 Field 物件的 UnderlyingValue 和 OriginalValue 屬性來處理這些類型的衝突。 將這些屬性與記錄集的 Resync 方法和 Filter 屬性搭配使用。  
  
## <a name="remarks"></a>備註  
 當 ADO 在批次更新期間發生衝突時，會將警告加入錯誤集合。 因此，在呼叫 BatchUpdate 之後，您應該一律檢查是否有錯誤，如果找到它們，請開始測試您遇到衝突的假設。 第一個步驟是將記錄集上的 Filter 屬性設定為等於 adFilterConflictingRecords。 這會將記錄集的視圖限制為只有衝突的記錄。 如果 RecordCount 屬性在此步驟之後等於零，您就知道錯誤是由衝突以外的專案引發。  
  
 當您呼叫 BatchUpdate 時，ADO 和提供者會產生 SQL 語句，以便在資料來源上執行更新。 請記住，某些資料來源對於 WHERE 子句中可使用的資料行類型有一些限制。  
  
 接下來，通話記錄集上的 Resync 方法，並將 AffectRecords 引數設定為等於 adAffectGroup，並將 ResyncValues 引數設定為等於 adResyncUnderlyingValues。 Resync 方法會從基礎資料庫更新目前記錄集物件中的資料。 藉由使用 adAffectGroup，您可以確保只有目前篩選設定可見的記錄（也就是只有衝突的記錄）會與資料庫重新同步處理。 如果您處理的是大型記錄集，這可能會造成顯著的效能差異。 藉由在呼叫重新同步時，將 ResyncValues 引數設定為 adResyncUnderlyingValues，您可以確保 UnderlyingValue 屬性會包含資料庫中的（衝突）值，而 Value 屬性會維護使用者輸入的值，而 OriginalValue 屬性會保留字段的原始值（最後一個成功的 UpdateBatch 呼叫之前的值）。 接著，您可以使用這些值來以程式設計方式解決衝突，或要求使用者選取將使用的值。  
  
 下列程式碼範例會顯示這項技術。 這個範例會在呼叫 UpdateBatch 之前，使用個別的記錄集來變更基礎資料表中的值，以建立衝突。  
  
```  
'BeginConflicts  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT * FROM Shippers WHERE ShipperID = 2"  
  
    'Open Rs and change a value  
    Set objRs1 = New ADODB.Recordset  
    Set objRs2 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Introduce a conflict at the db...  
    objRs2.Open strSQL, strConn, adOpenKeyset, adLockOptimistic, adCmdText  
    objRs2("Phone") = "(999) 555-9999"  
    objRs2.Update  
    objRs2.Close  
    Set objRs2 = Nothing  
  
    On Error Resume Next  
    objRs1.UpdateBatch  
  
    If objRs1.ActiveConnection.Errors.Count <> 0 Then  
        Dim intConflicts As Integer  
  
        intConflicts = 0  
  
        objRs1.Filter = adFilterConflictingRecords  
  
        intConflicts = objRs1.RecordCount  
  
        'Resync so we can see the UnderlyingValue and offer user a choice.  
        'This sample only displays all three values and resets to original.  
        objRs1.Resync adAffectGroup, adResyncUnderlyingValues  
  
        If intConflicts > 0 Then  
            strMsg = "A conflict occurred with updates for " & intConflicts & _  
                     " record(s)." & vbCrLf & "The values will be restored" & _  
                     " to their original values." & vbCrLf & vbCrLf  
  
            objRs1.MoveFirst  
            While Not objRs1.EOF  
              strMsg = strMsg & "SHIPPER = " & objRs1("CompanyName") & vbCrLf  
              strMsg = strMsg & "Value = " & objRs1("Phone").Value & vbCrLf  
              strMsg = strMsg & "UnderlyingValue = " & _  
                                 objRs1("Phone").UnderlyingValue & vbCrLf  
              strMsg = strMsg & "OriginalValue = " & _  
                                 objRs1("Phone").OriginalValue & vbCrLf  
              strMsg = strMsg & vbCrLf & "Original value has been restored."  
  
              MsgBox strMsg, vbOKOnly, _  
                    "Conflict " & objRs1.AbsolutePosition & _  
                    " of " & intConflicts  
  
              objRs1("Phone").Value = objRs1("Phone").OriginalValue  
              objRs1.MoveNext  
            Wend  
  
            objRs1.UpdateBatch adAffectGroup  
        Else  
            'Other error occurred. Minimal handling in this example.  
             strMsg = "Errors occurred during the update. " & _  
                        objRs1.ActiveConnection.Errors(0).Number & " " & _  
                        objRs1.ActiveConnection.Errors(0).Description  
        End If  
  
        On Error GoTo 0  
    End If  
  
    objRs1.MoveFirst  
    objRs1.Close  
    Set objRs1 = Nothing  
'EndConflicts  
```  
  
 您可以使用目前記錄或特定欄位的 Status 屬性，來判斷發生了哪種類型的衝突。  
  
 如需錯誤處理的詳細資訊，請參閱[錯誤處理](../../../ado/guide/data/error-handling.md)。  
  
## <a name="see-also"></a>另請參閱  
 [批次模式](../../../ado/guide/data/batch-mode.md)
