---
title: SqlPipe 物件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- custom result sets [CLR integration]
- SqlPipe object
- tabular results
ms.assetid: 3e090faf-085f-4c01-a565-79e3f1c36e3b
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bcf462f82d7455f83bb0bee8a3b0af991ec2e7db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62920059"
---
# <a name="sqlpipe-object"></a>SqlPipe 物件
  在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，通常會撰寫將結果或輸出參數傳送至呼叫用戶端的預存程序 (或擴充的預存程序)。  
  
 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序中，傳回零或多個資料列的任何 `SELECT` 陳述式都會將結果傳送至已連接之呼叫端的「管道」。  
  
 如果是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中執行的 Common Language Runtime (CLR) 資料庫物件，您可以使用 `Send` 物件的 `SqlPipe` 方法，將結果傳送至已連接的管道。 請存取 `Pipe` 物件的 `SqlContext` 屬性來取得 `SqlPipe` 物件。 
  `SqlPipe` 類別在概念上類似於在 ASP.NET 中找到的 `Response` 類別。 如需詳細資訊，請參閱 .NET Framework 軟體開發套件中的 SqlPipe 類別參考文件集。  
  
## <a name="returning-tabular-results-and-messages"></a>傳回表格式結果和訊息  
 
  `SqlPipe` 有一個 `Send` 方法，這個方法具有三個多載。 如下：  
  
-   `void Send(string message)`  
  
-   `void Send(SqlDataReader reader)`  
  
-   `void Send(SqlDataRecord record)`  
  
 
  `Send` 方法會將資料直接傳送至用戶端或呼叫端。 取用 `SqlPipe` 輸出的通常是用戶端，但在巢狀 CLR 預存程序的情況下，輸出取用者也可能是預存程序。 例如，Procedure1 會使用命令文字 "EXEC Procedure2" 呼叫 SqlCommand.ExecuteReader()。 而 Procedure2 也是 Managed 預存程序。 如果 Procedure2 此時呼叫 SqlPipe.Send( SqlDataRecord )，資料列便會傳送至 Procedure1 的讀取器 (Reader)，而非用戶端。  
  
 
  `Send` 方法會傳送字串訊息，此訊息會以資訊訊息顯示在用戶端上，與 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中的 PRINT 相等。 它也可以使用 `SqlDataRecord` 傳送單一資料列的結果集，或使用 `SqlDataReader` 傳送多重資料列的結果集。  
  
 
  `SqlPipe` 物件還擁有 `ExecuteAndSend` 方法。 此方法可用來執行命令 (做為 `SqlCommand` 物件傳遞)，並將結果直接傳送回呼叫端。 如果已提交的命令中出現錯誤，便會將例外狀況 (Exception) 傳送至管道，但也會傳送複本給呼叫的 Managed 程式碼。 如果呼叫程式碼未攔截到例外狀況，它會將堆疊向上傳播至 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，並在輸出中出現兩次。 如果呼叫程式碼攔截到例外狀況，管道取用者還是會看到錯誤，但是不會有重複的錯誤。  
  
 它只能使用與內容連接相關聯的 `SqlCommand`；而無法使用與非內容連接相關聯的命令。  
  
## <a name="returning-custom-result-sets"></a>傳回自訂結果集  
 Managed 預存程序可以傳送並非來自 `SqlDataReader` 的結果集。 
  `SendResultsStart` 方法及 `SendResultsRow` 與 `SendResultsEnd` 允許預存程序將自訂結果集傳送至用戶端。  
  
 
  `SendResultsStart` 會將 `SqlDataRecord` 做為輸入。 它會標示結果集的開頭，並使用記錄中繼資料來建構說明結果集的中繼資料。 它不使用 `SendResultsStart` 傳送記錄的值。 所有使用 `SendResultsRow` 傳送的後續資料列，都必須符合該中繼資料定義。  
  
> [!NOTE]  
>  呼叫 `SendResultsStart` 方法之後，只能呼叫 `SendResultsRow` 及 `SendResultsEnd`。 在相同的 `SqlPipe` 執行個體中呼叫任何其他方法會導致 `InvalidOperationException`。 
  `SendResultsEnd` 會將 `SqlPipe` 設定為可以呼叫其他方法的初始狀態。  
  
### <a name="example"></a>範例  
 
  `uspGetProductLine` 預存程序會傳回指定產品線內所有產品的名稱、產品編號、色彩和標價。 這個預存程式會接受與*prodLine*完全相符的專案。  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
  
public partial class StoredProcedures  
{  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void uspGetProductLine(SqlString prodLine)  
{  
    // Connect through the context connection.  
    using (SqlConnection connection = new SqlConnection("context connection=true"))  
    {  
        connection.Open();  
  
        SqlCommand command = new SqlCommand(  
            "SELECT Name, ProductNumber, Color, ListPrice " +  
            "FROM Production.Product " +   
            "WHERE ProductLine = @prodLine;", connection);  
  
        command.Parameters.AddWithValue("@prodLine", prodLine);  
  
        try  
        {  
            // Execute the command and send the results to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command);  
        }  
        catch (System.Data.SqlClient.SqlException ex)  
        {  
            // An error occurred executing the SQL command.  
        }  
     }  
}  
};  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Partial Public Class StoredProcedures  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub uspGetProductLine(ByVal prodLine As SqlString)  
    Dim command As SqlCommand  
  
    ' Connect through the context connection.  
    Using connection As New SqlConnection("context connection=true")  
        connection.Open()  
  
        command = New SqlCommand( _  
        "SELECT Name, ProductNumber, Color, ListPrice " & _  
        "FROM Production.Product " & _  
        "WHERE ProductLine = @prodLine;", connection)  
        command.Parameters.AddWithValue("@prodLine", prodLine)  
  
        Try  
            ' Execute the command and send the results   
            ' directly to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command)  
        Catch ex As System.Data.SqlClient.SqlException  
            ' An error occurred executing the SQL command.  
        End Try  
    End Using  
End Sub  
End Class  
```  
  
 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式會執行 `uspGetProduct` 程序，以傳回休閒車產品的清單。  
  
```  
EXEC uspGetProductLineVB 'T';  
```  
  
## <a name="see-also"></a>另請參閱  
 [SqlDataRecord 物件](sqldatarecord-object.md)   
 [CLR 預存程式](../../database-engine/dev-guide/clr-stored-procedures.md)   
 [ADO.NET 的 SQL Server 同處理序特定擴充](sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
