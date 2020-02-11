---
title: Error 物件屬性範例（VB） |Microsoft Docs
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
ms.openlocfilehash: 90673f82643ae24d242879fb19b748d5d1e3cc43
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919046"
---
# <a name="description-helpcontext-helpfile-nativeerror-number-source-and-sqlstate-properties-example-vb"></a>Description、HelpCoNtext、內容説明、NativeError、Number、Source 和 SQLState 屬性範例（VB）
這個範例會觸發錯誤、將其設為陷阱，並顯示所產生[錯誤](../../../ado/reference/ado-api/error-object.md)物件的[描述](../../../ado/reference/ado-api/description-property.md)、 [HelpCoNtext](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)、內容[説明](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)程式、 [NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md)、[數位](../../../ado/reference/ado-api/number-property-ado.md)、[來源](../../../ado/reference/ado-api/source-property-ado-error.md)和[SQLState](../../../ado/reference/ado-api/sqlstate-property.md)屬性。  
  
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
 [HelpCoNtext，內容説明的屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [HelpCoNtext，內容説明的屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [NativeError 屬性（ADO）](../../../ado/reference/ado-api/nativeerror-property-ado.md)   
 [Number 屬性（ADO）](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 屬性（ADO Error）](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [SQLState 屬性](../../../ado/reference/ado-api/sqlstate-property.md)
