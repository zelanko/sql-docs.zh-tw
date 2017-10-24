---
title: "StayInSync 屬性範例 (VB) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- StayInSync property [ADO], Visual Basic example
ms.assetid: b682bcc3-04b3-42b0-86f4-c17e0cd29baf
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5a8b2cfb058ab8e815f4a9320df5853a61f8e4a9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="stayinsync-property-example-vb"></a>StayInSync 屬性範例 (VB)
這個範例會示範如何[StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)屬性有助於進行存取的資料列，以階層[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
 外部迴圈會顯示每位作者的名字和姓氏、 狀態和識別。 附加**資料錄集**的每個資料列擷取自[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)集合並自動指派到**rstTitleAuthor**由**StayInSync**屬性每當父**資料錄集**移到新的資料列。 內部迴圈中附加資料錄集，顯示每個資料列的四個欄位。  
  
```  
'BeginStayInSyncVB  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn As ADODB.Connection  
    Dim rst As ADODB.Recordset  
    Dim rstTitleAuthor As New ADODB.Recordset  
    Dim strCnxn As String  
  
    ' Open the connection with Data Shape attributes  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider=MSDataShape;Data Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' Create a recordset  
    Set rst = New ADODB.Recordset  
    rst.StayInSync = True  
    rst.Open "SHAPE {select * from Authors} " & _  
                   "APPEND ( { select * from titleauthor} AS chapTitleAuthor " & _  
                   "RELATE au_id TO au_id) ", Cnxn, , , adCmdText  
  
    Set rstTitleAuthor = rst("chapTitleAuthor").Value  
    Do Until rst.EOF  
        Debug.Print rst!au_fname & " " & rst!au_lname & " " & _  
                   rst!State & " " & rst!au_id  
  
        Do Until rstTitleAuthor.EOF  
            Debug.Print rstTitleAuthor(0) & " " & rstTitleAuthor(1) & " " & _  
                   rstTitleAuthor(2) & " " & rstTitleAuthor(3)  
            rstTitleAuthor.MoveNext  
        Loop  
  
        rst.MoveNext  
    Loop  
  
    ' Clean up  
    rst.Close  
    Cnxn.Close  
    Set rst = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' Clean up  
    If Not rst Is Nothing Then  
        If rst.State = adStateOpen Then rst.Close  
    End If  
    Set rst = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndStayInSyncVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [欄位集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [StayInSync 屬性](../../../ado/reference/ado-api/stayinsync-property.md)

