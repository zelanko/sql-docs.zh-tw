---
description: " (VB 的讀取、ReadText、寫入和 WriteText 方法範例) "
title: " (VB) 的讀取、ReadText、寫入和 WriteText 方法範例 |Microsoft Docs"
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
- ReadText method [ADO], Visual Basic example
- Write method [ADO], Visual Basic example
- Read method [ADO], Visual Basic example
- WriteText method [ADO], Visual Basic example
ms.assetid: 699b73f7-04f9-4d46-94b2-6cb12be6de56
author: rothja
ms.author: jroth
ms.openlocfilehash: de640c5348b43fa7da5ad7e10b2dfa404f9ff4b9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442540"
---
# <a name="read-readtext-write-and-writetext-methods-example-vb"></a> (VB 的讀取、ReadText、寫入和 WriteText 方法範例) 
此範例示範如何將文字方塊的內容讀取至文字 [資料流程](../../../ado/reference/ado-api/stream-object-ado.md) 和二進位 **資料流程**。 所顯示的其他屬性和方法包括 [位置](../../../ado/reference/ado-api/position-property-ado.md)、 [大小](../../../ado/reference/ado-api/size-property-ado-parameter.md)、 [字元集](../../../ado/reference/ado-api/charset-property-ado.md)和 [SetEOS](../../../ado/reference/ado-api/seteos-method.md)。  
  
```  
'BeginReadVB  
Private Sub cmdRead_Click()  
    On Error GoTo ErrorHandler  
  
    'Declare variables  
    Dim objStream As Stream  
    Dim varA As Variant  
    Dim bytA() As Byte  
    Dim i As Integer  
    Dim strBytes As String  
  
    'Instantiate and Open Stream  
    Set objStream = New Stream  
    objStream.Open  
  
    'Write the text content of a textbox to the stream  
    If Text1.Text = "" Then  
        Err.Raise 1, , "The text field is blank."  
    End If  
    objStream.WriteText Text1.Text  
  
    'Display the text contents and size of the stream  
    objStream.Position = 0  
    Debug.Print "Default text:"  
    Debug.Print objStream.ReadText  
    Debug.Print objStream.Size  
  
    'Switch character set and display  
    objStream.Position = 0  
    objStream.Charset = "Windows-1252"  
    Debug.Print "New Charset text:"  
    Debug.Print objStream.ReadText  
    Debug.Print objStream.Size  
  
    'Switch to a binary stream and display  
    objStream.Position = 0  
    objStream.Type = adTypeBinary  
    Debug.Print "Binary:"  
    Debug.Print objStream.Read  
    Debug.Print objStream.Size  
  
    'Load an array of bytes with the text box text  
    ReDim bytA(Len(Text1.Text))  
    For i = 1 To Len(Text1.Text)  
        bytA(i - 1) = CByte(Asc(Mid(Text1.Text, i, 1)))  
    Next  
  
    'Write the buffer to the binary stream and display  
    objStream.Position = 0  
    objStream.Write bytA()  
    objStream.SetEOS  
    objStream.Position = 0  
    Debug.Print "Binary after Write:"  
    Debug.Print objStream.Read  
    Debug.Print objStream.Size  
  
    'Switch back to a text stream and display  
    Debug.Print "Translated back:"  
    objStream.Position = 0  
    objStream.Type = adTypeText  
    Debug.Print objStream.ReadText  
    Debug.Print objStream.Size  
  
    ' clean up  
    objStream.Close  
    Set objStream = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not objStream Is Nothing Then  
        If objStream.State = adStateOpen Then objStream.Close  
    End If  
    Set objStream = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndReadVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的字元集屬性 ](../../../ado/reference/ado-api/charset-property-ado.md)   
 [Position 屬性 (ADO) ](../../../ado/reference/ado-api/position-property-ado.md)   
 [Read 方法](../../../ado/reference/ado-api/read-method.md)   
 [ReadText 方法](../../../ado/reference/ado-api/readtext-method.md)   
 [SetEOS 方法](../../../ado/reference/ado-api/seteos-method.md)   
 [ (ADO Stream) 的 Size 屬性 ](../../../ado/reference/ado-api/size-property-ado-stream.md)   
 [ (ADO) 的資料流程物件 ](../../../ado/reference/ado-api/stream-object-ado.md)   
 [Write 方法](../../../ado/reference/ado-api/write-method.md)   
 [WriteText 方法](../../../ado/reference/ado-api/writetext-method.md)
