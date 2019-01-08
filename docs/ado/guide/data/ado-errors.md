---
title: ADO 錯誤 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO]
ms.assetid: 9bb84114-a1df-4122-a1b8-ad98dcd85cc3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5b2d3f43067750d2fc70a86c6a23bc74dd3bbc4
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52509114"
---
# <a name="ado-run-time-errors"></a>執行階段錯誤
ADO 錯誤會回報到您的程式中，為執行階段錯誤。 您可以使用您的程式語言的錯誤捕捉機制來攔截並處理它們。 例如，在 Visual Basic 中使用**On Error**陳述式。 Visual c + + 中，這取決於您用來存取 ADO 程式庫的方法。 有了 #import，使用**try / catch**區塊。 否則，c + + 程式設計人員必須明確地呼叫以擷取物件時發生錯誤**GetErrorInfo**。 下列 Visual Basic sub 程序示範如何捕捉 ADO 錯誤：

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

 這**Form_Load**事件程序刻意建立錯誤嘗試開啟相同**連線**物件兩次。 第二次**開啟**呼叫方法，就會啟動錯誤處理常式。 在此情況下錯誤屬於類型**adErrObjectOpen**，因此錯誤處理常式繼續程式執行前顯示下列訊息：

```
Error #3705: Operation is not allowed when the object is open.
Error reported by: ADODB.Connection
Help File: E:\WINNT\HELP\ADO260.CHM Topic ID: 1003705
```

 錯誤訊息會包含每個 Visual Basic 所提供的資訊片段**Err**物件除了**LastDLLError**這裡不適用的值。 錯誤號碼會告訴您發生了什麼錯誤。 描述可用於在其中您不想自行處理錯誤的情況。 您只可以將它傳遞給使用者。 雖然您通常會想要使用您的應用程式的自訂訊息，您不能預期每項錯誤;描述會提供一些線索，所發生的錯誤。 範例程式碼中所報告的錯誤**連線**物件。 您會看到物件的型別或程式設計識別碼-不是變數的名稱。

> [!NOTE]
>  Visual Basic **Err**物件只會包含最常見的錯誤相關資訊。 ADO**錯誤**的集合**連線**物件包含一個**錯誤**最近的 ADO 作業所引發的每個錯誤的物件。 使用**錯誤**集合而非**Err**物件，以處理多個錯誤。 如需詳細資訊**錯誤**集合，請參閱[提供者錯誤](../../../ado/guide/data/provider-errors.md)。 不過，如果無法有效**連接**物件， **Err**物件是 ADO 錯誤的相關資訊的唯一來源。

 何種作業都有可能造成 ADO 錯誤？ 常見的 ADO 錯誤可能是開啟物件，例如**連接**或是**資料錄集**、 嘗試更新資料，或呼叫方法或您的提供者不支援的屬性。

 OLE DB 錯誤也可以傳遞至您的應用程式中的執行階段錯誤**錯誤**集合。

 下列主題提供有關 ADO 錯誤的詳細資訊。

-   [ADO 錯誤參考](../../../ado/guide/data/ado-error-reference.md)
