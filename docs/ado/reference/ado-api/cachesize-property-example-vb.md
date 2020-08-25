---
description: CacheSize 屬性範例 (VB)
title: " (VB) 的 CacheSize 屬性範例 |Microsoft Docs"
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
- CacheSize property [ADO], Visual Basic example
ms.assetid: a237ffdb-6e5b-47c6-9901-d5cdbe8625f3
author: rothja
ms.author: jroth
ms.openlocfilehash: be5e96526cc68701615617991c774c7124f7cd09
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776377"
---
# <a name="cachesize-property-example-vb"></a>CacheSize 屬性範例 (VB)
這個範例會使用 [CacheSize](./cachesize-property-ado.md) 屬性來顯示以和沒有30個記錄快取執行之作業的效能差異。  
  
```  
'BeginCacheSizeVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstRoySched As ADODB.Recordset  
    Dim strSQLSched As String  
    Dim strCnxn As String  
     'record variables  
    Dim sngStart As Single  
    Dim sngEnd As Single  
    Dim sngNoCache As Single  
    Dim sngCache As Single  
    Dim intLoop As Integer  
    Dim strTemp As String  
  
    ' Open the connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
  
    ' Open the RoySched Table  
    Set rstRoySched = New ADODB.Recordset  
    strSQLSched = "roysched"  
    rstRoySched.Open strSQLSched, strCnxn, , , adCmdTable  
  
    ' Enumerate the Recordset object twice and  
    ' record the elapsed time  
    sngStart = Timer  
  
    For intLoop = 1 To 2  
        rstRoySched.MoveFirst  
  
        If Not rstRoySched.EOF Then  
            ' Execute a simple operation for the  
            ' performance test  
            Do  
                strTemp = rstRoySched!title_id  
                rstRoySched.MoveNext  
            Loop Until rstRoySched.EOF  
        End If  
    Next intLoop  
  
    sngEnd = Timer  
    sngNoCache = sngEnd - sngStart  
  
    ' Cache records in groups of 30 records.  
    rstRoySched.MoveFirst  
    rstRoySched.CacheSize = 30  
    sngStart = Timer  
  
    ' Enumerate the Recordset object twice and record  
    ' the elapsed time  
    For intLoop = 1 To 2  
        rstRoySched.MoveFirst  
        Do While Not rstRoySched.EOF  
            ' Execute a simple operation for the  
            ' performance test  
            strTemp = rstRoySched!title_id  
            rstRoySched.MoveNext  
        Loop  
    Next intLoop  
  
    sngEnd = Timer  
    sngCache = sngEnd - sngStart  
  
    ' Display performance results.  
    MsgBox "Caching Performance Results:" & vbCr & _  
        "   No cache: " & Format(sngNoCache, "##0.000") & " seconds" & vbCr & _  
        "   30-record cache: " & Format(sngCache, "##0.000") & " seconds"  
  
    ' clean up  
    rstRoySched.Close  
    Set rstRoySched = Nothing  
    Exit Sub  
  
ErrorHandler:  
   ' clean up  
    If Not rstRoySched Is Nothing Then  
        If rstRoySched.State = adStateOpen Then rstRoySched.Close  
    End If  
    Set rstRoySched = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndCacheSizeVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADO) 的 CacheSize 屬性 ](./cachesize-property-ado.md)   
 [Recordset 物件 (ADO)](./recordset-object-ado.md)