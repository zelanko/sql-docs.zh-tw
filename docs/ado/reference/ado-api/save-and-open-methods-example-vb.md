---
title: Save 和 Open 方法範例 (VB) |Microsoft Docs
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
- Save method [ADO], Visual Basic example
- Open method [ADO]
ms.assetid: ddccdf58-9c57-4c9b-8b7f-0cf193f955fb
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 32ed7e6240f5f9622bfcb80e2f05a633fcaf2fdc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711640"
---
# <a name="save-and-open-methods-example-vb"></a>Save 和 Open 方法範例 (VB)
這三個範例示範如何[儲存](../../../ado/reference/ado-api/save-method.md)並[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法可以一起使用。  
  
 假設您即將在出差，而且想要採取沿著從資料庫資料表。 您繼續之前，您存取資料，當做[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)並將它儲存在容易進行傳輸的表單。 當您抵達您的目的地時，存取**Recordset**為本機，中斷連接**資料錄集**。 若要變更**資料錄集**，然後重新儲存。 最後，當您重返首頁，再連接到資料庫並更新您所做的變更在路上。  
  
 首先，存取並儲存***作者***資料表。  
  
```  
'BeginSaveVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstAuthors As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    Set rstAuthors = New ADODB.Recordset  
    strSQLAuthors = "SELECT au_id, au_lname, au_fname, city, phone FROM Authors"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenDynamic, adLockOptimistic, adCmdText  
  
    'For sake of illustration, save the Recordset to a diskette in XML format  
    rstAuthors.Save "c:\Pubs.xml", adPersistXML  
  
    ' clean up  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    'clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndSaveVB  
```  
  
 此時，您已到達目的地。 您將會存取***作者***資料表中的做為本機、 中斷連線**資料錄集**。 您必須擁有**MSPersist**用來存取儲存的檔案，在電腦上的提供者 a:\Pubs.xml。  
  
```  
Attribute VB_Name = "Save"  
```  
  
 最後，將主資料夾。 現在您的變更更新資料庫。  
  
```  
Attribute VB_Name = "Save"  
```  
  
## <a name="see-also"></a>另請參閱  
 [Open 方法 (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [深入了解資料錄集的持續性](../../../ado/guide/data/more-about-recordset-persistence.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
