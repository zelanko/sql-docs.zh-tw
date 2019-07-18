---
title: DefinedSize 屬性範例 (VB) |Microsoft Docs
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
- DefinedSize property [ADOX], Visual Basic example
ms.assetid: 4dda2239-7ab5-4729-9c63-eb530803f7d9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d188ba801112a94d1ac09c6e1bae7fbbe5bccfee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966450"
---
# <a name="definedsize-property-example-vb"></a>DefinedSize 屬性範例 (VB)
此範例示範[DefinedSize](../../../ado/reference/adox-api/definedsize-property-adox.md)屬性[資料行](../../../ado/reference/adox-api/column-object-adox.md)。 程式碼會重新定義的 FirstName 資料行的大小**員工**一覽表*Northwind*資料庫。 然後，FirstName 的值的變更[欄位](../../../ado/reference/ado-api/field-object.md)的[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)根據**員工**資料表會顯示。 請注意，根據預設，[FirstName] 欄位會變成填補空格之後您重新定義**DefinedSize**屬性。  
  
```  
' BeginDefinedSizeVB  
Public Sub Main()  
    On Error GoTo DefinedSizeXError  
  
    Dim rstEmployees As ADODB.Recordset  
    Dim catNorthwind As New ADOX.Catalog  
    Dim colFirstName As ADOX.Column  
    Dim colNewFirstName As New ADOX.Column  
    Dim aryFirstName() As String  
    Dim i As Integer  
    Dim strCnn As String  
  
    strCnn = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
             "Data Source='Northwind.mdb';"  
  
    ' Open a Recordset for the Employees table.  
    Set rstEmployees = New ADODB.Recordset  
    rstEmployees.Open "Employees", strCnn, adOpenKeyset, , adCmdTable  
    ReDim aryFirstName(rstEmployees.RecordCount)  
  
    ' Open a Catalog for the Northwind database,  
    ' using same connection as rstEmployees  
    Set catNorthwind.ActiveConnection = rstEmployees.ActiveConnection  
  
    ' Loop through the recordset displaying the contents  
    ' of the FirstName field, the field's defined size,  
    ' and its actual size.  
    ' Also store FirstName values in aryFirstName array.  
    rstEmployees.MoveFirst  
    Debug.Print " "  
    Debug.Print "Original Defined Size and Actual Size"  
    i = 0  
    Do Until rstEmployees.EOF  
        Debug.Print "Employee name: " & rstEmployees!FirstName & _  
            " " & rstEmployees!LastName  
        Debug.Print "    FirstName Defined size: " _  
            & rstEmployees!FirstName.DefinedSize  
        Debug.Print "    FirstName Actual size: " & _  
            rstEmployees!FirstName.ActualSize  
            If Not rstEmployees!FirstName = Null Then  
                aryFirstName(i) = rstEmployees!FirstName  
            End If  
        rstEmployees.MoveNext  
        i = i + 1  
    Loop  
    rstEmployees.Close  
  
    ' Redefine the DefinedSize of FirstName in the catalog  
    Set colFirstName = catNorthwind.Tables("Employees").Columns("FirstName")  
    colNewFirstName.Name = colFirstName.Name  
    colNewFirstName.Type = colFirstName.Type  
    colNewFirstName.DefinedSize = colFirstName.DefinedSize + 1  
  
    ' Append new FirstName column to catalog  
    catNorthwind.Tables("Employees").Columns.Delete colFirstName.Name  
    catNorthwind.Tables("Employees").Columns.Append colNewFirstName  
  
    ' Open Employee table in Recordset for updating  
    rstEmployees.Open "Employees", catNorthwind.ActiveConnection, _  
        adOpenKeyset, adLockOptimistic, adCmdTable  
  
    ' Loop through the recordset displaying the contents  
    ' of the FirstName field, the field's defined size,  
    ' and its actual size.  
    ' Also restore FirstName values from aryFirstName.  
    rstEmployees.MoveFirst  
    Debug.Print " "  
    Debug.Print "New Defined Size and Actual Size"  
    i = 0  
    Do Until rstEmployees.EOF  
        rstEmployees!FirstName = aryFirstName(i)  
        Debug.Print "Employee name: " & rstEmployees!FirstName & _  
            " " & rstEmployees!LastName  
        Debug.Print "    FirstName Defined size: " _  
            & rstEmployees!FirstName.DefinedSize  
        Debug.Print "    FirstName Actual size: " & _  
            rstEmployees!FirstName.ActualSize  
        rstEmployees.MoveNext  
        i = i + 1  
    Loop  
    rstEmployees.Close  
  
    ' Restore original FirstName column to catalog  
    catNorthwind.Tables("Employees").Columns.Delete colNewFirstName.Name  
    catNorthwind.Tables("Employees").Columns.Append colFirstName  
  
    ' Restore original FirstName values to Employees table  
    rstEmployees.Open "Employees", catNorthwind.ActiveConnection, _  
        adOpenKeyset, adLockOptimistic, adCmdTable  
  
    rstEmployees.MoveFirst  
    i = 0  
    Do Until rstEmployees.EOF  
        rstEmployees!FirstName = aryFirstName(i)  
        rstEmployees.MoveNext  
        i = i + 1  
    Loop  
    rstEmployees.Close  
  
    'Clean up  
    Set catNorthwind = Nothing  
    Set colNewFirstName = Nothing  
    Set colFirstName = Nothing  
    Set rstEmployees = Nothing  
    Exit Sub  
  
DefinedSizeXError:  
    Set catNorthwind = Nothing  
    Set colNewFirstName = Nothing  
    Set colFirstName = Nothing  
  
    If Not rstEmployees Is Nothing Then  
        If rstEmployees.State = adStateOpen Then rstEmployees.Close  
    End If  
    Set rstEmployees = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndDefinedSizeVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [資料行物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [DefinedSize 屬性 (ADOX)](../../../ado/reference/adox-api/definedsize-property-adox.md)
