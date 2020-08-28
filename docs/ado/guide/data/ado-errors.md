---
description: ADO 執行階段錯誤
title: ADO 錯誤 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO]
ms.assetid: 9bb84114-a1df-4122-a1b8-ad98dcd85cc3
author: rothja
ms.author: jroth
ms.openlocfilehash: 0b1da9cd8e7afd2b56921fa6b413b5d349d7027f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991729"
---
# <a name="ado-run-time-errors"></a>ADO 執行階段錯誤
當您的程式發生執行階段錯誤時，會將 ADO 錯誤回報給您的程式。 您可以使用程式設計語言的錯誤捕捉機制來將它們設為陷阱和處理。 例如，在 Visual Basic 中，請使用 **On Error** 語句。 在 Visual C++ 中，這取決於您用來存取 ADO 程式庫的方法。 使用 #import，請使用 **try-catch** 區塊。 否則，c + + 程式設計人員必須藉由呼叫 **GetErrorInfo**，明確地取出 error 物件。 下列 Visual Basic sub 程式示範如何捕捉 ADO 錯誤：

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

 此 **Form_Load** 事件程式會嘗試開啟相同的 **連接** 物件兩次，以刻意建立錯誤。 第二次呼叫 **Open** 方法時，就會啟動錯誤處理常式。 在此情況下，錯誤的類型為 **adErrObjectOpen**，因此錯誤處理常式會在繼續執行程式之前顯示下列訊息：

```
Error #3705: Operation is not allowed when the object is open.
Error reported by: ADODB.Connection
Help File: E:\WINNT\HELP\ADO260.CHM Topic ID: 1003705
```

 此錯誤訊息包含 Visual Basic **Err** 物件所提供的每一項資訊，但 **LastDLLError** 值除外，此值不適用於此處。 錯誤號碼會指出發生了哪些錯誤。 當您不想要自行處理錯誤時，描述會很有用。 您可以直接將它傳遞給使用者。 雖然您通常會想要使用針對應用程式自訂的訊息，但您無法預期每個錯誤;描述會針對發生錯誤的原因提供一些線索。 在範例程式碼中， **連接** 物件報告了錯誤。 您會在這裡看到物件的類型或程式設計識別碼-不是變數名稱。

> [!NOTE]
>  Visual Basic **Err** 物件只包含最新錯誤的相關資訊。 **連接**物件的 ADO **Errors**集合針對最近的 ADO 作業所引發的每個錯誤，各包含一個**錯誤**物件。 使用 **Errors** 集合而非 **Err** 物件來處理多個錯誤。 如需有關 **錯誤** 集合的詳細資訊，請參閱 [提供者錯誤](./provider-errors.md)。 但是，如果沒有有效的 **連接** 物件，則 **ERR** 物件是 ADO 錯誤相關資訊的唯一來源。

 哪些種類的作業可能會導致 ADO 錯誤？ 常見的 ADO 錯誤可能牽涉到開啟物件（例如 **連接** 或 **記錄集**）、嘗試更新資料，或呼叫您的提供者不支援的方法或屬性。

 您也可以將 OLE DB 錯誤傳遞至您的應用程式，做為 **錯誤** 集合中的執行階段錯誤。

 下列主題提供有關 ADO 錯誤的詳細資訊。

-   [ADO 錯誤參考](./ado-error-reference.md)