---
title: 錯誤物件屬性範例 (VB) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e7061c804393fe73e249636646c298c977002928
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="description-helpcontext-helpfile-nativeerror-number-source-and-sqlstate-properties-example-vb"></a>描述、 HelpContext、 說明檔案、 NativeError、 數字、 來源和 SQLState 屬性範例 (VB)
這個範例會觸發錯誤、 設陷，並顯示[描述](../../../ado/reference/ado-api/description-property.md)， [HelpContext](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)， [HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)， [NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md)， [數字](../../../ado/reference/ado-api/number-property-ado.md)，[來源](../../../ado/reference/ado-api/source-property-ado-error.md)，和[SQLState](../../../ado/reference/ado-api/sqlstate-property.md)屬性產生[錯誤](../../../ado/reference/ado-api/error-object.md)物件。  
  
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
 [HelpContext，HelpFile 屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [HelpContext，HelpFile 屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [NativeError 屬性 (ADO)](../../../ado/reference/ado-api/nativeerror-property-ado.md)   
 [Number 屬性 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [來源屬性 （ADO 錯誤）](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [SQLState 屬性](../../../ado/reference/ado-api/sqlstate-property.md)
