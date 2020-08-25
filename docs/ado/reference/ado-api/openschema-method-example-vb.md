---
description: OpenSchema 方法範例 (VB)
title: " (VB) 的 OpenSchema 方法範例 |Microsoft Docs"
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
- OpenSchema method [ADO], Visual Basic example
ms.assetid: 455a02f0-8143-4562-8648-8fb45ffd334c
author: rothja
ms.author: jroth
ms.openlocfilehash: e3c576f5cd06b5fe075ca60a06ad1cc8877c49b4
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773747"
---
# <a name="openschema-method-example-vb"></a>OpenSchema 方法範例 (VB)
這個範例會使用 [OpenSchema](./openschema-method.md) 方法來顯示 ***Pubs*** 資料庫中每個資料表的名稱和類型。  
  
```  
'BeginOpenSchemaVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    Dim Cnxn As ADODB.Connection  
    Dim rstSchema As ADODB.Recordset  
    Dim strCnxn As String  
  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    Set rstSchema = Cnxn.OpenSchema(adSchemaTables)  
  
    Do Until rstSchema.EOF  
        Debug.Print "Table name: " & _  
            rstSchema!TABLE_NAME & vbCr & _  
            "Table type: " & rstSchema!TABLE_TYPE & vbCr  
        rstSchema.MoveNext  
    Loop  
  
    ' clean up  
    rstSchema.Close  
    Cnxn.Close  
    Set rstSchema = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstSchema Is Nothing Then  
        If rstSchema.State = adStateOpen Then rstSchema.Close  
    End If  
    Set rstSchema = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndOpenSchemaVB  
```  
  
 這個範例會在 **OpenSchema** 方法 ***準則*** 引數中指定 TABLE_TYPE 查詢準則約束。 如此一來，就只會傳回 ***Pubs*** 資料庫中所指定之視圖的架構資訊。 然後，此範例會顯示每個資料表 () 的名稱 () 和類型 (s) 。  
  
```  
Attribute VB_Name = "OpenSchema"  
```  
  
## <a name="see-also"></a>另請參閱  
 [OpenSchema 方法](./openschema-method.md)   
 [Recordset 物件 (ADO)](./recordset-object-ado.md)