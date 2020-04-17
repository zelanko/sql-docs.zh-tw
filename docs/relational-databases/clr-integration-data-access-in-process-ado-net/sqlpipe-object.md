---
title: SqlPipe 物件 |微軟文件
description: 對於在 SQL Server 中執行的 CLR 資料庫物件,可以使用 SqlPipe 物件的「發送」方法將結果發送到連接的管道。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 7b95788d37fa8f8c2e57c2b20aa222938c65dc6c
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487508"
---
# <a name="sqlpipe-object"></a>SqlPipe 物件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，通常會撰寫將結果或輸出參數傳送至呼叫用戶端的預存程序 (或擴充的預存程序)。  
  
 在[!INCLUDE[tsql](../../includes/tsql-md.md)]存儲過程中,返回零行或更多行的任何**SELECT**語句都會將結果發送到連接的調用方的"管道"。  
  
 對於在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中 運行的常見語言運行時 (CLR) 資料庫物件,可以使用**SqlPipe**物件的**Send**方法將結果發送到連接的管道。 訪問**SqlContext**物件的**Pipe**屬性以獲取**SqlPipe**物件。 **SqlPipe**類在概念上類似於ASP.NET中的**回應**類。 如需詳細資訊，請參閱 .NET Framework 軟體開發套件中的 SqlPipe 類別參考文件集。  
  
## <a name="returning-tabular-results-and-messages"></a>傳回表格式結果和訊息  
 **SqlPipe**具有一個**Send**方法,該方法有三個重載。 其中包括：  
  
-   `void Send(string message)`  
  
-   `void Send(SqlDataReader reader)`  
  
-   `void Send(SqlDataRecord record)`  
  
 **Send**方法將數據直接發送到用戶端或調用方。 它通常是使用**SqlPipe**輸出的用戶端,但在嵌套 CLR 儲存過程中,輸出消費者也可以是一個儲存過程。 例如，Procedure1 會使用命令文字 "EXEC Procedure2" 呼叫 SqlCommand.ExecuteReader()。 而 Procedure2 也是 Managed 預存程序。 如果 Procedure2 此時呼叫 SqlPipe.Send( SqlDataRecord )，資料列便會傳送至 Procedure1 的讀取器 (Reader)，而非用戶端。  
  
 **Send**方法發送一個字串消息,該字串消息作為資訊消息顯示在用戶端上,等效於[!INCLUDE[tsql](../../includes/tsql-md.md)]中的 PRINT。 它還可以使用**SqlDataRecord**發送單行結果集,也可以使用**SqlDataReader**發送多行結果集。  
  
 **SqlPipe**物件還具有**Execute 和Send**方法。 此方法可用於執行命令(作為**SqlCommand**物件傳遞)並將結果直接發送回調用方。 如果已提交的命令中出現錯誤，便會將例外狀況 (Exception) 傳送至管道，但也會傳送複本給呼叫的 Managed 程式碼。 如果呼叫程式碼未攔截到例外狀況，它會將堆疊向上傳播至 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，並在輸出中出現兩次。 如果呼叫程式碼攔截到例外狀況，管道取用者還是會看到錯誤，但是不會有重複的錯誤。  
  
 它只能採用與上下文連接關聯的 SqlCommand;它只能使用與上下文連接關聯的**SqlCommand;** 它不能採用與非上下文連接關聯的命令。  
  
## <a name="returning-custom-result-sets"></a>傳回自訂結果集  
 託管儲存過程可以發送並非來自**SqlDataReader**的結果集。 **SendResultStart**方法以及**SendResultRow**和**SendResultEnd**允許儲存過程將自定義結果集發送到用戶端。  
  
 **發送結果開始**將**SqlDataRecord**作為輸入。 它會標示結果集的開頭，並使用記錄中繼資料來建構說明結果集的中繼資料。 它不發送具有**Send 結果開始**的記錄值。 使用**Send 結果行**發送的所有後續行必須與該元數據定義匹配。  
  
> [!NOTE]  
>  呼叫 **「發送結果開始」** 方法後,只能呼叫 **「發送結果行**」和 **「發送結果結束」。** 呼叫**SqlPipe**同一個實體中的任何其他方法會導致**不合法操作異常**。 **Send結果End**將**SqlPipe**設置回可以調用其他方法的初始狀態。  
  
### <a name="example"></a>範例  
 **uspGetProductLine**儲存過程返回指定產品線中所有產品的名稱、產品編號、顏色和標價。 此存儲過程接受*prodLine*的精確匹配。  
  
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
  
 以下[!INCLUDE[tsql](../../includes/tsql-md.md)]語句執行**uspGetProduct**過程,該過程返回旅遊自行車產品的清單。  
  
```  
EXEC uspGetProductLineVB 'T';  
```  
  
## <a name="see-also"></a>另請參閱  
 [SqlDataRecord 物件](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqldatarecord-object.md)   
 [CLR 預存程序](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)   
 [ADO.NET 的 SQL Server 同處理序特定擴充](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
  
