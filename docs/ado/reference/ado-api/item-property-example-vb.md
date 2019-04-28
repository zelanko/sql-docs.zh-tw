---
title: 項目屬性範例 (VB) |Microsoft Docs
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
- Item property [ADO], Visual Basic example
ms.assetid: b4476603-691b-4081-8797-a3d0b331dce5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 941c6a8cf6c7ed57e0a28d5cb288d92ab8e231c1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864502"
---
# <a name="item-property-example-vb"></a>Item 屬性範例 (VB)
此範例示範如何[項目](../../../ado/reference/ado-api/item-property-ado.md)屬性存取集合的成員。 此範例會開啟***作者***一覽表***Pubs***使用參數化命令的資料庫。  
  
 從存取中針對資料庫發出命令的參數[命令](../../../ado/reference/ado-api/command-object-ado.md)物件的[參數](../../../ado/reference/ado-api/parameters-collection-ado.md)集合索引及名稱。 傳回的欄位[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)再從該物件的存取[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合索引及名稱。  
  
```  
'BeginItemVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn As ADODB.Connection  
    Dim rstAuthors As ADODB.Recordset  
    Dim cmd As ADODB.Command  
    Dim prm As ADODB.Parameter  
    Dim fld As ADODB.Field  
    Dim strCnxn As String  
  
    Dim ix As Integer  
    Dim limit As Long  
    Dim Column(0 To 8) As Variant  
  
    Set Cnxn = New ADODB.Connection  
    Set rstAuthors = New ADODB.Recordset  
    Set cmd = New ADODB.Command  
  
    'Set the array with the Authors table field (column) names  
    Column(0) = "au_id"  
    Column(1) = "au_lname"  
    Column(2) = "au_fname"  
    Column(3) = "phone"  
    Column(4) = "address"  
    Column(5) = "city"  
    Column(6) = "state"  
    Column(7) = "zip"  
    Column(8) = "contract"  
  
    cmd.CommandText = "SELECT * FROM Authors WHERE state = ?"  
    Set prm = cmd.CreateParameter("ItemXparm", adChar, adParamInput, 2, "CA")  
    cmd.Parameters.Append prm  
     ' set connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
    cmd.ActiveConnection = Cnxn  
     ' open recordset  
    rstAuthors.Open cmd, , adOpenStatic, adLockReadOnly  
    'Connection and CommandType are omitted because  
    'a Command object is provided  
  
    Debug.Print "The Parameters collection accessed by index..."  
    Set prm = cmd.Parameters.Item(0)  
    Debug.Print "Parameter name = '"; prm.Name; "', value = '"; prm.Value; "'"  
    Debug.Print  
  
    Debug.Print "The Parameters collection accessed by name..."  
    Set prm = cmd.Parameters.Item("ItemXparm")  
    Debug.Print "Parameter name = '"; prm.Name; "', value = '"; prm.Value; "'"  
    Debug.Print  
  
    Debug.Print "The Fields collection accessed by index..."  
  
    rstAuthors.MoveFirst  
    limit = rstAuthors.Fields.Count - 1  
    For ix = 0 To limit  
       Set fld = rstAuthors.Fields.Item(ix)  
       Debug.Print "Field "; ix; ": Name = '"; fld.Name; _  
                   "', Value = '"; fld.Value; "'"  
    Next ix  
  
    Debug.Print  
  
    Debug.Print "The Fields collection accessed by name..."  
  
    rstAuthors.MoveFirst  
    For ix = 0 To 8  
       Set fld = rstAuthors.Fields.Item(Column(ix))  
       Debug.Print "Field name = '"; fld.Name; "', Value = '"; fld.Value; "'"  
    Next ix  
  
    ' clean up  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    Set cmd = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
'EndItemVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [Fields 集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [項目屬性 (ADO)](../../../ado/reference/ado-api/item-property-ado.md)   
 [參數集合 (ADO)](../../../ado/reference/ado-api/parameters-collection-ado.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
