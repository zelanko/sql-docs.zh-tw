---
title: "偵測和解決衝突 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conflicts [ADO], detecting and resolving
- ADO, detecting and resolving conflicts
ms.assetid: b28fdd26-c1a4-40ce-a700-2b0c9d201514
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61f54b700be8ec03e56bf63999dc7f93b8d5fcdb
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="detecting-and-resolving-conflicts"></a>偵測並解決衝突
如果您正在處理您的資料錄集即時模式中，會有更少的並行存取問題發生的機率。 相反地，如果您的應用程式會使用批次模式更新，可能有更佳可能發生在儲存編輯同一筆記錄的另一位使用者所做的變更之前，一位使用者將變更的記錄。 在這種情況下，您將會正常處理衝突的應用程式。 它可能是您要將更新傳送至伺服器的最後一個人員中 「 獲勝。 」 的希望 或者，您可能想要讓最新的使用者決定哪些更新應該優先藉由向他提供兩個衝突的值之間的選擇。  
  
 無論如何，ADO 提供 UnderlyingValue OriginalValue 物件和屬性欄位來處理這些類型的衝突。 重新同步處理方法與資料錄集的篩選屬性搭配使用這些屬性。  
  
## <a name="remarks"></a>備註  
 當 ADO 批次更新期間發生衝突時，警告將會加入至錯誤集合。 因此，您應該一律檢查錯誤之後您可以呼叫 BatchUpdate，並找到它們，如果開始測試假設發生衝突。 第一個步驟是在資料錄集 equal to adFilterConflictingRecords 上設定篩選屬性。 這會限制只在有衝突的記錄資料錄集的檢視。 RecordCount 屬性等於零，在此步驟之後，如果您知道錯誤已由以外的衝突所造成。  
  
 當您呼叫 BatchUpdate 時，ADO 和提供者會產生 SQL 陳述式來執行更新的資料來源。 請記住特定資料來源有所在的資料行的類型可以用於 WHERE 子句的限制。  
  
 接下來，呼叫資料錄集與 AffectRecords 引數設為等於 adAffectGroup 和 ResyncValues 引數設為等於 adResyncUnderlyingValues 重新同步處理方法。 重新同步處理方法會更新目前的資料錄集物件，從基礎資料庫中的資料。 您可以藉由使用 adAffectGroup，確保只顯示與目前的篩選器設定，也就只衝突的記錄，記錄會重新同步處理資料庫。 如果您正在處理大量資料集，這可以讓顯著的效能差異。 藉由設定 adResyncUnderlyingValues ResyncValues 引數呼叫重新同步處理時，確保 UnderlyingValue 屬性將包含 （衝突） 的值來自資料庫、 「 值 」 屬性會維護由使用者所輸入的值和確認 OriginalValue 屬性會保留欄位 （最後一個成功 UpdateBatch 呼叫之前的值） 的原始值。 您接著可以使用這些值，以程式設計的方式解決衝突，或要求使用者選取將使用的值。  
  
 這項技術是以下列程式碼範例所示。 在可用手動方式建立衝突變更基礎資料表中的值，會在呼叫 UpdateBatch 之前使用個別的資料錄集。  
  
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
  
 您可以使用目前的記錄或特定欄位的 Status 屬性來判斷發生何種衝突。  
  
 如需錯誤處理的詳細資訊，請參閱[錯誤處理](../../../ado/guide/data/error-handling.md)。  
  
## <a name="see-also"></a>另請參閱  
 [批次模式](../../../ado/guide/data/batch-mode.md)
