---
title: 使用命令呼叫預存程式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- calling stored procedures [ADO]
- stored procedures [ADO]
- commands [ADO]
ms.assetid: 685f7652-2271-4ede-b552-2eeb8c756b4c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 32f1013ef0aa9c8f02e19ec98234418480bc5f22
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925869"
---
# <a name="calling-a-stored-procedure-with-a-command"></a>使用命令呼叫預存程序
您可以使用命令來呼叫預存程式。 本主題結尾的程式碼範例會參考 Northwind 範例資料庫中的預存程式，稱為 CustOrdersOrders，其定義如下。  
  
```  
CREATE PROCEDURE CustOrdersOrders @CustomerID nchar(5) AS  
SELECT OrderID, OrderDate, RequiredDate, ShippedDate  
FROM Orders  
WHERE CustomerID = @CustomerID  
ORDER BY OrderID  
```  
  
 如需如何定義和呼叫預存程式的詳細資訊，請參閱您的 SQL Server 檔。  
  
 這個預存程式類似于[命令物件參數](../../../ado/guide/data/command-object-parameters.md)中使用的命令。 它會採用客戶識別碼參數，並傳回該客戶訂單的相關資訊。 下列程式碼範例會使用這個預存程式做為 ADO**記錄集**的來源。  
  
 使用預存程式可讓您存取 ADO 的另一項功能： **Parameters**集合**Refresh**方法。 藉由使用這個方法，ADO 就可以在執行時間自動填入命令所需參數的所有相關資訊。 使用這項技術會對效能造成負面影響，因為 ADO 必須查詢資料來源以取得參數的相關資訊。  
  
 下列程式碼範例與[命令物件參數](../../../ado/guide/data/command-object-parameters.md)中的程式碼之間有其他重要的差異，其中參數是以手動方式輸入。 首先，此程式碼不會將**備**妥的屬性設定為**True** ，因為它是一個 SQL Server 的預存程式，而且是由定義先行編譯。 其次，在第二個範例中，**命令**物件的**CommandType**屬性已變更為**adCmdStoredProc** ，以通知 ADO 該命令為預存程式。  
  
 最後，在第二個範例中，設定值時，參數必須參考索引，因為您在設計階段可能不知道參數的名稱。 如果您知道參數的名稱，您可以將**Command**物件的 new [NamedParameters](../../../ado/reference/ado-api/namedparameters-property-ado.md)屬性設為 True，並參考屬性的名稱。 您可能會想知道預存程式（@CustomerID）中所提及第一個參數的位置為何是1，而`objCmd(1) = "ALFKI"`不是0（）。 這是因為參數0包含來自 SQL Server 預存程式的傳回值。  
  
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
 [知識庫文章117500](https://go.microsoft.com/fwlink/?LinkId=117500)
