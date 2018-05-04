---
title: 尋找方法範例 (VB) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Find method [ADO], Visual Basic example
ms.assetid: bbf27dcc-9815-4e2f-8ea8-b8c9fe6dedd6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 19ac7451ddd8a405c9729c2a11409a660c48d07e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="find-method-example-vb"></a>尋找方法範例 (VB)
這個範例會使用[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件的[尋找](../../../ado/reference/ado-api/find-method-ado.md)方法找出和商務標題中的次數***Pubs***資料庫。 此範例假設基礎提供者不支援類似的功能。  
  
```  
'BeginFindVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
     ' connection and recordset variables  
    Dim Cnxn As New ADODB.Connection  
    Dim rstTitles As New ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLTitles As String  
  
     ' record variables  
    Dim mark As Variant  
    Dim count As Integer  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' open recordset with default parameters which are  
    ' sufficient to search forward through a Recordset  
    Set rstTitles = New ADODB.Recordset  
    strSQLTitles = "SELECT title_id FROM titles"  
    rstTitles.Open strSQLTitles, Cnxn, adOpenStatic, adLockReadOnly, adCmdText  
  
    count = 0  
    rstTitles.Find "title_id LIKE 'BU%'"  
  
    Do While Not rstTitles.EOF  
        'continue if last find succeeded  
        Debug.Print "Title ID: "; rstTitles!title_id  
        'count the last title found  
        count = count + 1  
        ' note current position  
        mark = rstTitles.Bookmark  
        rstTitles.Find "title_id LIKE 'BU%'", 1, adSearchForward, mark  
        ' above code skips current record to avoid finding the same row repeatedly;  
        ' last arg (bookmark) is redundant because Find searches from current position  
    Loop  
  
    Debug.Print "The number of business titles is " & count  
  
    ' clean up  
    rstTitles.Close  
    Cnxn.Close  
    Set rstTitles = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstTitles Is Nothing Then  
        If rstTitles.State = adStateOpen Then rstTitles.Close  
    End If  
    Set rstTitles = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndFindVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [Find 方法 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
