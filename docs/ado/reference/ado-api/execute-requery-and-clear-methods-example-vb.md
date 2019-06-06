---
title: Execute、 Requery 和 Clear 方法範例 (VB) |Microsoft Docs
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
- Requery method [ADO], Visual Basic example
- Clear method [ADO], Visual Basic example
- Execute method [ADO], Visual Basic example
ms.assetid: ed5e1b60-3769-4b26-a253-1d721e37941d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: bda27b7941244ac77de08e81baeb1307c14c60cc
ms.sourcegitcommit: fc341b2e08937fdd07ea5f4d74a90677fcdac354
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719248"
---
# <a name="execute-requery-and-clear-methods-example-vb"></a>Execute、 Requery 和 Clear 方法範例 (VB)
此範例示範**Execute**方法時執行兩個[命令](../../../ado/reference/ado-api/command-object-ado.md)物件和[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件。 它也會使用[Requery](../../../ado/reference/ado-api/requery-method.md)方法來擷取目前的資料，在[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，而[清除](../../../ado/reference/ado-api/clear-method-ado.md)方法，以清除內容[錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合。 (**錯誤**收集透過存取**連線**物件[ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md)屬性[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。)ExecuteCommand 和 PrintOutput 程序不需要執行這個程序。  
  
```  
'BeginExecuteVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo Err_Execute  
  
    ' connection, command, and recordset variables  
    Dim Cnxn As ADODB.Connection  
    Dim cmdChange As ADODB.Command  
    Dim rstTitles As ADODB.Recordset  
    Dim Err As ADODB.Error  
    Dim strSQLChange As String  
    Dim strSQLRestore As String  
    Dim strSQLTitles  
    Dim strCnxn As String  
  
     ' Define two SQL statements to execute as command text  
    strSQLChange = "UPDATE Titles SET Type = 'self_help' WHERE Type = 'psychology'"  
    strSQLRestore = "UPDATE Titles SET Type = 'psychology' WHERE Type = 'self_help'"  
  
     ' Open connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Set Cnxn = New ADODB.Connection  
    Cnxn.Open strCnxn  
  
     ' Create command object  
    Set cmdChange = New ADODB.Command  
    Set cmdChange.ActiveConnection = Cnxn  
    cmdChange.CommandText = strSQLChange  
  
     ' Open titles table  
    Set rstTitles = New ADODB.Recordset  
    strSQLTitles = "titles"  
    rstTitles.Open strSQLTitles, Cnxn, , , adCmdTable  
  
    ' Print report of original data  
    Debug.Print _  
       "Data in Titles table before executing the query"  
    PrintOutput rstTitles  
  
    ' Call the ExecuteCommand subroutine below to execute cmdChange command  
    ExecuteCommand cmdChange, rstTitles  
  
    ' Print report of new data  
    Debug.Print _  
       "Data in Titles table after executing the query"  
    PrintOutput rstTitles  
  
    ' Use the Connection object's execute method to  
    ' execute SQL statement to restore data and trap for  
    ' errors, checking the Errors collection if necessary  
    Cnxn.Execute strSQLRestore, , adExecuteNoRecords  
  
    ' Retrieve the current data by requerying the recordset  
    rstTitles.Requery  
  
    ' Print report of restored data using sub from below  
    Debug.Print "Data after executing the query to restore the original information "  
    PrintOutput rstTitles  
  
    ' clean up  
    rstTitles.Close  
    Cnxn.Close  
    Set rstTitles = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
Err_Execute:  
    ' Notify user of any errors that result from  
    ' executing the query  
    If rstTitles.ActiveConnection.Errors.Count >= 0 Then  
       For Each Err In rstTitles.ActiveConnection.Errors  
          MsgBox "Error number: " & Err.Number & vbCr & _  
             Err.Description  
       Next Err  
    End If  
  
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
  
Public Sub ExecuteCommand(cmdTemp As ADODB.Command, rstTemp As ADODB.Recordset)  
  
   Dim Err As Error  
  
   ' Run the specified Command object and trap for  
   ' errors, checking the Errors collection  
   On Error GoTo Err_Execute  
   cmdTemp.Execute  
   On Error GoTo 0  
  
   ' Retrieve the current data by requerying the recordset  
   rstTemp.Requery  
  
   Exit Sub  
  
Err_Execute:  
  
   ' Notify user of any errors that result from  
   ' executing the query  
   If rstTemp.ActiveConnection.Errors.Count > 0 Then  
      For Each Err In rstTemp.ActiveConnection.Errors  
         MsgBox "Error number: " & Err.Number & vbCr & _  
            Err.Description  
      Next Err  
   End If  
  
   Resume Next  
  
End Sub  
  
Public Sub PrintOutput(rstTemp As ADODB.Recordset)  
  
   ' Enumerate Recordset  
   Do While Not rstTemp.EOF  
      Debug.Print "  " & rstTemp!Title & _  
         ", " & rstTemp!Type  
      rstTemp.MoveNext  
   Loop  
  
End Sub  
'EndExecuteVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [Clear 方法 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Command 物件 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [連接物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Error 物件](../../../ado/reference/ado-api/error-object.md)   
 [Execute 方法 (ADO Command)](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Execute 方法 (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Requery 方法](../../../ado/reference/ado-api/requery-method.md)
