---
title: CopyRecord、 CopyTo 和 SaveToFile 方法範例 (VB) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- CopyRecord method [ADO], Visual Basic example
- SaveToFile method [ADO], Visual Basic example
- CopyTo method [ADO], Visual Basic example
ms.assetid: 61a51b74-93cd-439c-877f-f3055499d39f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7cc7a22d72e282bfe84d9a63dac8382a380eebe7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63309115"
---
# <a name="copyrecord-copyto-and-savetofile-methods-example-vb"></a>CopyRecord、 CopyTo 和 SaveToFile 方法範例 (VB)
此範例示範如何建立檔案，使用的複本[Stream](../../../ado/reference/ado-api/stream-object-ado.md)或是[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件。 一個複本進行，以適用於網際網路發佈的 Web 資料夾。 其他屬性和方法，顯示包含[Stream 型別](../../../ado/reference/ado-api/type-property-ado-stream.md)，**開啟**， [LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)，以及[記錄開啟](../../../ado/reference/ado-api/open-method-ado-record.md)。  
  
```  
'BeginCopyRecordVB  
  
'Note:  
' This sample requires that "C:\checkmrk.wmf" and  
' "https://MyServer/mywmf.wmf" exist.  
  
Option Explicit  
  
Private Sub Form_Load()  
    On Error GoTo ErrorHandler  
  
    ' Declare variables  
    Dim strPicturePath, strStreamPath, strStream2Path, _  
        strRecordPath, strStreamURL, strRecordURL As String  
    Dim objStream, objStream2 As Stream  
    Dim objRecord As Record  
    Dim objField As Field  
  
    ' Instantiate objects  
    Set objStream = New Stream  
    Set objStream2 = New Stream  
    Set objRecord = New Record  
  
    ' Initialize path and URL strings  
    strPicturePath = "C:\checkmrk.wmf"  
    strStreamPath = "C:\mywmf.wmf"  
    strStreamURL = "URL=https://MyServer/mywmf.wmf"  
    strStream2Path = "C:\checkmrk2.wmf"  
    strRecordPath = "C:\mywmf.wmf"  
    strRecordURL = "https://MyServer/mywmf2.wmf"  
  
    ' Load the file into the stream  
    objStream.Open  
    objStream.Type = adTypeBinary  
    objStream.LoadFromFile (strPicturePath)  
  
    ' Save the stream to a new path and filename  
    objStream.SaveToFile strStreamPath, adSaveCreateOverWrite  
  
    ' Copy the contents of the first stream to a second stream  
    objStream2.Open  
    objStream2.Type = adTypeBinary  
    objStream.CopyTo objStream2  
  
    ' Save the second stream to a different path  
    objStream2.SaveToFile strStream2Path, adSaveCreateOverWrite  
  
    ' Because strStreamPath is a Web Folder, open a Record on the URL  
    objRecord.Open "", strStreamURL  
  
    ' Display the Fields of the record  
    For Each objField In objRecord.Fields  
        Debug.Print objField.Name & ": " & objField.Value  
    Next  
  
    ' Copy the record to a new URL  
    objRecord.CopyRecord "", strRecordURL, , , adCopyOverWrite  
  
    ' Load each copy of the graphic into Image controls for viewing  
    Image1.Picture = LoadPicture(strPicturePath)  
    Image2.Picture = LoadPicture(strStreamPath)  
    Image3.Picture = LoadPicture(strStream2Path)  
    Image4.Picture = LoadPicture(strRecordPath)  
  
    ' clean up  
    objStream.Close  
    objStream2.Close  
    objRecord.Close  
    Set objStream = Nothing  
    Set objStream2 = Nothing  
    Set objRecord = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not objStream Is Nothing Then  
        If objStream.State = adStateOpen Then objStream.Close  
    End If  
    Set objStream = Nothing  
  
    If Not objStream2 Is Nothing Then  
        If objStream2.State = adStateOpen Then objStream2.Close  
    End If  
    Set objStream2 = Nothing  
  
    If Not objRecord Is Nothing Then  
        If objRecord.State = adStateOpen Then objRecord.Close  
    End If  
    Set objRecord = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndCopyRecordVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [CopyRecord 方法 (ADO)](../../../ado/reference/ado-api/copyrecord-method-ado.md)   
 [CopyTo 方法 (ADO)](../../../ado/reference/ado-api/copyto-method-ado.md)   
 [LoadFromFile 方法 (ADO)](../../../ado/reference/ado-api/loadfromfile-method-ado.md)   
 [Open 方法 （ADO 記錄）](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Open 方法 (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Record 物件 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [SaveToFile 方法](../../../ado/reference/ado-api/savetofile-method.md)   
 [Stream 物件 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [Type 屬性 (ADO Stream)](../../../ado/reference/ado-api/type-property-ado-stream.md)
