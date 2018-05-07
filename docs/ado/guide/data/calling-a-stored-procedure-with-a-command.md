---
title: 呼叫預存程序使用的命令 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- calling stored procedures [ADO]
- stored procedures [ADO]
- commands [ADO]
ms.assetid: 685f7652-2271-4ede-b552-2eeb8c756b4c
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbb9edb3744f1cc2483cfbe4d0d08a06868998d8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="calling-a-stored-procedure-with-a-command"></a>呼叫預存程序使用的命令
您可以使用命令來呼叫預存程序。 本主題結尾的程式碼範例是指在稱為 CustOrdersOrders，如下所示定義 Northwind 範例資料庫中的預存程序。  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 請參閱您的 SQL Server 文件，如需有關如何定義和呼叫預存程序。  
  
 這個預存程序是類似命令中使用[命令物件參數](../../../ado/guide/data/command-object-parameters.md)。 它接受客戶 ID 參數，並傳回該客戶的訂單的相關資訊。 下列程式碼範例使用此預存程序做為來源 ADO**資料錄集**。  
  
 使用預存程序可讓您存取其他功能的 ADO:**參數**集合**重新整理**方法。 使用此方法，ADO 可以自動填滿命令在執行階段所需的參數的所有資訊。 因為 ADO 必須查詢參數的相關資訊的資料來源中使用這項技巧，沒有對效能帶來負面影響。  
  
 下列程式碼範例和中的程式碼之間，有其他重要的差異[命令物件參數](../../../ado/guide/data/command-object-parameters.md)、 參數以手動方式輸入。 首先，此程式碼並不會設定**已準備**屬性**True**因為它是 SQL Server 預存程序，並根據定義先行編譯。 第二個， **CommandType**屬性**命令**物件變更為**adCmdStoredProc**在第二個範例中，通知 ADO 命令是預存程序。  
  
 最後，在第二個範例參數必須是由索引參考時設定值，因為您可能不在執行階段知道參數的名稱。 如果您知道參數的名稱，您可以設定新[NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md)屬性**命令**物件設為 True，並參考屬性的名稱。 您可能想知道的位置，第一個參數的預存程序中所述的原因 (@CustomerID) 為 1，而不是 0 (`objCmd(1) = "ALFKI"`)。 這是因為參數 0 包含從 SQL Server 預存程序的傳回值。  
  
```  
'BeginAutoParamCmd  
    On Error GoTo ErrHandler:  
  
    Dim objConn As New ADODB.Connection  
    Dim objCmd As New ADODB.Command  
    Dim objParm1 As New ADODB.Parameter  
    Dim objRs As New ADODB.Recordset  
  
    ' Set CommandText equal to the stored procedure name.  
    objCmd.CommandText = "CustOrdersOrders"  
    objCmd.CommandType = adCmdStoredProc  
  
    ' Connect to the data source.  
    Set objConn = GetNewConnection  
    objCmd.ActiveConnection = objConn  
  
    ' Automatically fill in parameter info from stored procedure.  
    objCmd.Parameters.Refresh  
  
    ' Set the param value.  
    objCmd(1) = "ALFKI"  
  
    ' Execute once and display...  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    ' ...then set new param value, re-execute command, and display.  
    objCmd(1) = "CACTU"  
    Set objRs = objCmd.Execute  
  
    Debug.Print objParm1.Value  
    Do While Not objRs.EOF  
        Debug.Print vbTab & objRs(0) & vbTab & objRs(1) & vbTab & _  
                    objRs(2) & vbTab & objRs(3)  
        objRs.MoveNext  
    Loop  
  
    'clean up  
    objRs.Close  
    objConn.Close  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
    Exit Sub  
  
ErrHandler:  
    'clean up  
    If objRs.State = adStateOpen Then  
        objRs.Close  
    End If  
  
    If objConn.State = adStateOpen Then  
        objConn.Close  
    End If  
  
    Set objRs = Nothing  
    Set objConn = Nothing  
    Set objCmd = Nothing  
    Set objParm1 = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
'EndAutoParamCmd  
  
'BeginNewConnection  
Private Function GetNewConnection() As ADODB.Connection  
    Dim oCn As New ADODB.Connection  
    Dim sCnStr As String  
  
    sCnStr = "Provider='SQLOLEDB';Data Source='MySqlServer';" & _  
             "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    oCn.Open sCnStr  
  
    If oCn.State = adStateOpen Then  
        Set GetNewConnection = oCn  
    End If  
  
End Function  
'EndNewConnection  
```  
  
## <a name="see-also"></a>另請參閱  
 [知識庫文章 117500](http://go.microsoft.com/fwlink/?LinkId=117500)
