---
title: 偵測並解決衝突 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a27a8ff70a995ab24dcf762d0ada731e0de6fa92
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62472280"
---
# <a name="detecting-and-resolving-conflicts"></a>偵測並解決衝突
如果您在即時模式中處理資料錄集，會有較少機會發生的並行處理問題。 相反地，如果您的應用程式會使用批次模式更新，可能會有一個良好機會儲存編輯同一筆記錄的另一位使用者所做的變更之前，一位使用者將變更記錄。 在此情況下，您會想，正常處理衝突的應用程式。 它可能是您將更新傳送至伺服器的最後一個人中 「 獲勝。 」 的願望 或者，您可能想要讓最新的使用者決定哪些更新應該優先選擇兩個衝突的值，提供與他連絡。  
  
 無論如何，ADO 提供 UnderlyingValue OriginalValue 物件和屬性欄位來處理這些衝突類型。 使用重新同步處理方法和資料錄集的 [篩選] 屬性搭配使用這些屬性。  
  
## <a name="remarks"></a>備註  
 當 ADO 批次更新期間發生衝突時，警告會加入錯誤集合。 因此，您應該一律檢查錯誤呼叫 BatchUpdate，並找到它們，如果開始測試的假設，您已偵測到衝突之後，立即。 第一個步驟是資料錄集 equal to adFilterConflictingRecords 上設定篩選屬性。 這會限制只在有衝突的記錄資料錄集的檢視。 如果 RecordCount 屬性等於零，在此步驟之後，就會知道以外衝突的問題所引發的錯誤。  
  
 當您呼叫 BatchUpdate 時，ADO 和提供者會產生 SQL 陳述式來執行更新的資料來源。 請記住，特定資料來源已在其的資料行的類型可以使用 WHERE 子句中的限制。  
  
 接下來，呼叫資料錄集與 AffectRecords 引數設定為等於 adAffectGroup 和 ResyncValues 引數設定為等於 adResyncUnderlyingValues 重新同步處理方法。 重新同步處理方法會更新目前的資料錄集物件，從基礎資料庫中的資料。 您可以藉由使用 adAffectGroup，確保只顯示與目前的篩選條件設定，也就只有衝突的記錄，記錄會重新同步處理與資料庫。 如果您正在處理大量資料集，這可能造成顯著的效能差異。 藉由呼叫重新同步處理時，則您可以設 adResyncUnderlyingValues ResyncValues 引數，可確保 UnderlyingValue 屬性將包含 （衝突） 的值，從資料庫中，[值] 屬性會維護由使用者輸入的值和OriginalValue 屬性會保留原始的值欄位 （在進行最後一個成功的 UpdateBatch 呼叫之前，它所具有的值）。 您接著可以使用這些值，以程式設計的方式解決衝突，或要求使用者選取將使用的值。  
  
 這項技術是以下列程式碼範例所示。 以人為方式的範例會使用不同的資料錄集變更基礎資料表中的值，才能呼叫 UpdateBatch 以建立衝突。  
  
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
  
 您可以使用目前資料錄或特定欄位的 Status 屬性來判斷發生何種衝突。  
  
 如需錯誤處理的詳細資訊，請參閱[錯誤處理](../../../ado/guide/data/error-handling.md)。  
  
## <a name="see-also"></a>另請參閱  
 [批次模式](../../../ado/guide/data/batch-mode.md)
