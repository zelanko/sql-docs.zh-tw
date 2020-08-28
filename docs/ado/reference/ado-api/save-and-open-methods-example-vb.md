---
description: Save 和 Open 方法範例 (VB)
title: " (VB) 的儲存和開啟方法範例 |Microsoft Docs"
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
- Save method [ADO], Visual Basic example
- Open method [ADO]
ms.assetid: ddccdf58-9c57-4c9b-8b7f-0cf193f955fb
author: rothja
ms.author: jroth
ms.openlocfilehash: 14668aba6cbc6817b951820bbdee4d5c69a51bc5
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989359"
---
# <a name="save-and-open-methods-example-vb"></a>Save 和 Open 方法範例 (VB)
這三個範例會示範如何搭配使用 [Save](./save-method.md) 和 [Open](./open-method-ado-recordset.md) 方法。  
  
 假設您正在進行商務旅程，並想要從資料庫中取出資料表。 在您開始之前，請先以 [記錄集](./recordset-object-ado.md) 的形式存取資料，並以可傳送的形式儲存。 當您抵達目的地時，您會存取 **記錄集** 作為本機、中斷連線的 **記錄集**。 您會對 **記錄集**進行變更，然後再次儲存。 最後，當您返回 home 時，請再次連接到資料庫，並使用您在道路上所做的變更來更新它。  
  
 首先，存取並儲存 ***作者*** 資料表。  
  
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
  
 到目前為止，您已經抵達目的地。 您將以本機、中斷連線的**記錄集**存取***作者***資料表。 您必須在用來存取已儲存之檔案的電腦上具有 **MSPersist** 提供者，a:\Pubs.xml。  
  
```  
Attribute VB_Name = "Save"  
```  
  
 最後，您會返回 home。 現在以您的變更更新資料庫。  
  
```  
Attribute VB_Name = "Save"  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO 記錄集的 Open 方法) ](./open-method-ado-recordset.md)   
 [ (ADO) 的記錄集物件 ](./recordset-object-ado.md)   
 [深入瞭解記錄集持續性](../../guide/data/more-about-recordset-persistence.md)   
 [Save 方法](./save-method.md)