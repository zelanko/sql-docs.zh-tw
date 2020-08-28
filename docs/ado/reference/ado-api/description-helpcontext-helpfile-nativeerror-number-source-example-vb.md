---
description: 'Description、HelpCoNtext、NativeError、Number、Source 和 SQLState 屬性範例 (VB) '
title: Error 物件屬性範例 (VB) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9cfb607ba02125856b07b447dd20378d93ed1f11
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973989"
---
# <a name="description-helpcontext-helpfile-nativeerror-number-source-and-sqlstate-properties-example-vb"></a>Description、HelpCoNtext、NativeError、Number、Source 和 SQLState 屬性範例 (VB) 
此範例會觸發錯誤、將其設為陷阱，並顯示所產生之[錯誤](../../../ado/reference/ado-api/error-object.md)物件的[描述](../../../ado/reference/ado-api/description-property.md)、 [HelpCoNtext](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)、[説明](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)、 [NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md)、[數位](../../../ado/reference/ado-api/number-property-ado.md)、[來源](../../../ado/reference/ado-api/source-property-ado-error.md)和[SQLState](../../../ado/reference/ado-api/sqlstate-property.md)屬性。  
  
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
 [HelpCoNtext，內容説明屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [HelpCoNtext，內容説明屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [ (ADO) 的 NativeError 屬性 ](../../../ado/reference/ado-api/nativeerror-property-ado.md)   
 [Number 屬性 (ADO) ](../../../ado/reference/ado-api/number-property-ado.md)   
 [ (ADO Error) 的 Source 屬性 ](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [SQLState 屬性](../../../ado/reference/ado-api/sqlstate-property.md)
