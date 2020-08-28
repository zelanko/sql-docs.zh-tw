---
description: ConvertToString 方法範例 (VB)
title: " (VB) 的 ConvertToString 方法範例 |Microsoft Docs"
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
- ConvertToString method [ADO], Visual Basic example
ms.assetid: 31731e4f-3c0c-451e-8cbc-c9df28fabf6c
author: rothja
ms.author: jroth
ms.openlocfilehash: 2998027f3c32da89f97124671a6c30385d79c64b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974669"
---
# <a name="converttostring-method-example-vb"></a>ConvertToString 方法範例 (VB)
```  
'BeginConvertToStringVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
     ' to integrate this code replace the server name  
     ' in the CreateObject call  
  
     ' RDS variables  
    Dim rdsDS As RDS.DataSpace  
    Dim rdsDC As RDS.DataControl  
    Dim rdsDF As Object  
     ' recordset and connection variables  
    Dim rsAuthors As ADODB.Recordset  
    Dim strSQLAuthors As String  
    Dim strCnxn As String  
    Dim varString As Variant  
  
     ' Create a DataSpace object  
    Set rdsDS = New RDS.DataSpace  
     ' Create a DataFactory object  
    Set rdsDF = rdsDS.CreateObject("RDSServer.DataFactory", "https://MyServer") 'MyServer  
  
     ' Get all of the Author records  
  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    strSQLAuthors = "SELECT * FROM Authors"  
    Set rsAuthors = rdsDF.Query(strCnxn, strSQLAuthors)  
     ' Show results  
    Debug.Print "Old RDS recordset count:" & rsAuthors.RecordCount  
  
     ' Convert the recordset into a MIME formatted string  
    varString = rdsDF.ConvertToString(rsAuthors)  
    Debug.Print "Recordset as MIME format string:"  
    Debug.Print varString  
  
     ' Convert string value back into an ADO Recordset  
    Set rdsDC = New RDS.DataControl  
    rdsDC.SQL = varString  
    rdsDC.ExecuteOptions = adcExecSync  
    rdsDC.FetchOptions = adcFetchUpFront  
    rdsDC.Refresh  
     ' Show results  
    Debug.Print "New ADO recordset count:" & rdsDC.Recordset.RecordCount  
  
     ' clean up  
    rsAuthors.Close  
    Set rsAuthors = Nothing  
    Set rdsDC = Nothing  
    Set rdsDS = Nothing  
    Set rdsDC = Nothing  
  
ErrorHandler:  
  
    If Not rsAuthors Is Nothing Then  
        If rsAuthors.State = adStateOpen Then rsAuthors.Close  
    End If  
    Set rsAuthors = Nothing  
    Set rdsDC = Nothing  
    Set rdsDS = Nothing  
    Set rdsDC = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
'EndConvertToStringVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [RDS)  (ConvertToString 方法 ](../rds-api/converttostring-method-rds.md)   
 [Recordset 物件 (ADO)](./recordset-object-ado.md)