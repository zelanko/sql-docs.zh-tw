---
title: 錯誤的物件屬性範例 (VB) |Microsoft Docs
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
- Number property [ADO], Visual Basic example
- Source property [ADO], Visual Basic example
- NativeError property [ADO], Visual Basic example
- Description property [ADO], Visual Basic example
- HelpFile property [ADO], Visual Basic example
- SQLState property [ADO], Visual Basic example
- HelpContext property [ADO], Visual Basic example
ms.assetid: 5c728458-d85c-497c-afcf-2cfa36c3342a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 139ffaee3210709dd82f328eca88bb3ae2973bbe
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727726"
---
# <a name="description-helpcontext-helpfile-nativeerror-number-source-and-sqlstate-properties-example-vb"></a>描述、 HelpContext、 HelpFile、 NativeError、 數目、 來源和 SQLState 屬性範例 (VB)
這個範例會觸發錯誤、 設陷，並顯示[描述](../../../ado/reference/ado-api/description-property.md)， [HelpContext](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)， [HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)， [NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md)， [數字](../../../ado/reference/ado-api/number-property-ado.md)，[來源](../../../ado/reference/ado-api/source-property-ado-error.md)，和[SQLState](../../../ado/reference/ado-api/sqlstate-property.md)內容產生[錯誤](../../../ado/reference/ado-api/error-object.md)物件。  
  
```  
'BeginDescriptionVB  
Public Sub Main()  
  
    Dim Cnxn As ADODB.Connection  
    Dim Err As ADODB.Error  
    Dim strError As String  
  
    On Error GoTo ErrorHandler  
  
    ' Intentionally trigger an error  
    Set Cnxn = New ADODB.Connection  
    Cnxn.Open "nothing"  
  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
  
    ' Enumerate Errors collection and display  
    ' properties of each Error object  
    For Each Err In Cnxn.Errors  
        strError = "Error #" & Err.Number & vbCr & _  
            "   " & Err.Description & vbCr & _  
            "   (Source: " & Err.Source & ")" & vbCr & _  
            "   (SQL State: " & Err.SQLState & ")" & vbCr & _  
            "   (NativeError: " & Err.NativeError & ")" & vbCr  
        If Err.HelpFile = "" Then  
            strError = strError & "   No Help file available"  
        Else  
            strError = strError & _  
               "   (HelpFile: " & Err.HelpFile & ")" & vbCr & _  
               "   (HelpContext: " & Err.HelpContext & ")" & _  
               vbCr & vbCr  
        End If  
  
        Debug.Print strError  
    Next  
  
    Resume Next  
End Sub  
'EndDescriptionVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [Description 屬性](../../../ado/reference/ado-api/description-property.md)   
 [Error 物件](../../../ado/reference/ado-api/error-object.md)   
 [HelpContext、 HelpFile 屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [HelpContext、 HelpFile 屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [NativeError 屬性 (ADO)](../../../ado/reference/ado-api/nativeerror-property-ado.md)   
 [Number 屬性 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [來源屬性 (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [SQLState 屬性](../../../ado/reference/ado-api/sqlstate-property.md)
