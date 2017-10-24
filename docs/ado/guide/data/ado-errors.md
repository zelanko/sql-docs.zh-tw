---
title: "ADO 錯誤 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: H1Hack27Feb2017
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- errors [ADO]
ms.assetid: 9bb84114-a1df-4122-a1b8-ad98dcd85cc3
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 54a44c69afd01647c5dca1cab97993f890d81c21
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="ado-run-time-errors"></a>ADO 執行階段錯誤
ADO 錯誤會回報到您的程式，為執行階段錯誤。 您可以使用您的程式語言的錯誤截取機制來攔截和處理它們。 例如，在 Visual Basic 中使用**On Error**陳述式。 在 Visual c + + 中，它會取決於您用來存取 ADO 文件庫的方法。 使用 #import， **try catch**區塊。 否則，c + + 程式設計人員必須明確地擷取物件時發生錯誤，藉由呼叫**GetErrorInfo**。 下列 Visual Basic sub 程序示範設限 ADO 錯誤：

```
' BeginErrorHandlingVB01
Private Sub Form_Load()
' Turn on error handling
On Error GoTo FormLoadError

'Open the database and the recordset for processing.
'
Dim strCnn As String
strCnn = "Provider=sqloledb;" & _
    "Data Source=a-iresmi2000;" & _
    "Initial Catalog=Northwind;Integrated Security=SSPI"

' cnn is a Public Connection Object because
' it was defined WithEvents
Set cnn = New ADODB.Connection
cnn.Open strCnn

' The next line of code intentionally causes
' an error by trying to open a connection
' that has already been opened.
cnn.Open strCnn

' rst is a Public Recordset because it
' was defined WithEvents
Set rst = New ADODB.Recordset
rst.Open "Customers", cnn

Exit Sub

' Error handler
FormLoadError:
    Dim strErr As String
    Select Case Err
        Case adErrObjectOpen
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            strErr = strErr & "Error reported by: " & Err.Source & vbCrLf
            strErr = strErr & "Help File: " & Err.HelpFile & vbCrLf
            strErr = strErr & "Topic ID: " & Err.HelpContext
            MsgBox strErr
            Debug.Print strErr
            Err.Clear
            Resume Next
        ' If some other error occurs that
        ' has nothing to do with ADO, show
        ' the number and description and exit.
        Case Else
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            MsgBox strErr
            Debug.Print strErr
            Unload Me
    End Select
End Sub
' EndErrorHandlingVB01
```

 這**Form_Load**事件程序有意建立錯誤嘗試開啟相同**連接**物件兩次。 第二次**開啟**呼叫方法時，就會啟動錯誤處理常式。 在此情況下錯誤屬於型別**adErrObjectOpen**，因此錯誤處理常式之前繼續執行程式中顯示下列訊息：

```
Error #3705: Operation is not allowed when the object is open.
Error reported by: ADODB.Connection
Help File: E:\WINNT\HELP\ADO260.CHM Topic ID: 1003705
```

 此錯誤訊息包含每個 Visual Basic 所提供的資訊片段**Err**物件除了**LastDLLError**這裡不適用的值。 錯誤號碼會告訴您發生了什麼錯誤。 描述是在其在您不想自行處理錯誤的情況下很有用。 您只可以將它傳遞給使用者。 不過您通常會想要使用您的應用程式的自訂訊息，您不能預期每項錯誤。描述可提供一些線索何者發生錯誤。 範例程式碼中所報告的錯誤**連接**物件。 您會看到物件的型別或以下的程式設計識別碼，不是變數的名稱。

> [!NOTE]
>  Visual Basic **Err**物件只包含最近的錯誤相關資訊。 ADO**錯誤**集合**連接**物件包含一個**錯誤**最近 ADO 作業所產生的每個錯誤的物件。 使用**錯誤**集合而非**Err**物件，以便處理多個錯誤。 如需有關**錯誤**集合，請參閱[提供者錯誤](../../../ado/guide/data/provider-errors.md)。 不過，如果沒有不具有效**連接**物件**Err**物件是 ADO 錯誤的相關資訊的唯一來源。

 有可能造成 ADO 錯誤的作業種類？ 常見的 ADO 錯誤可能是開啟的物件，例如**連接**或**資料錄集**、 嘗試更新資料，或呼叫方法或您的提供者不支援的屬性。

 OLE DB 錯誤也可以傳遞至為應用程式中的執行階段錯誤**錯誤**集合。

 下列主題提供有關 ADO 錯誤的詳細資訊。

-   [ADO 錯誤參考](../../../ado/guide/data/ado-error-reference.md)

