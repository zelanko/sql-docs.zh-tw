---
title: Save 和 Open 方法範例（VB） |Microsoft Docs
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
ms.openlocfilehash: 6d42488f8f167cc7c98f663478c742963d24253c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931199"
---
# <a name="save-and-open-methods-example-vb"></a>Save 和 Open 方法範例 (VB)
這三個範例會示範如何搭配使用[Save](../../../ado/reference/ado-api/save-method.md)和[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法。  
  
 假設您正在出差，而且想要從資料庫中取得資料表。 在您開始之前，您會以[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的形式存取資料，並將其儲存為可傳送的格式。 當您抵達目的地時，您會以本機、離線式**記錄集**的身分存取**記錄集**。 您對**記錄集**進行變更，然後重新儲存。 最後，當您返回 home 時，您會再次連接到資料庫，並以您在路上所做的變更來更新它。  
  
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
  
 到目前為止，您已到達目的地。 您將會存取***作者***資料表做為本機、中斷連接的**記錄集**。 您必須在用來存取已儲存檔案的電腦上擁有**MSPersist**提供者，a:\Pubs.xml。  
  
```  
Attribute VB_Name = "Save"  
```  
  
 最後，您會返回 home。 現在，請使用您的變更來更新資料庫。  
  
```  
Attribute VB_Name = "Save"  
```  
  
## <a name="see-also"></a>另請參閱  
 [Open 方法（ADO Recordset）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Recordset 物件（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [深入瞭解記錄集持續性](../../../ado/guide/data/more-about-recordset-persistence.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
