---
title: CLR 預存程式 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- database objects [CLR integration], stored procedures
- stored procedures [CLR integration]
- common language runtime [SQL Server], stored procedures
- building database objects [CLR integration], stored procedures
- output parameters [CLR integration]
- tabular results
ms.assetid: bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 4998058d55cd49c0eecfdecce2edc609a4d62c1f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933709"
---
# <a name="clr-stored-procedures"></a>CLR 預存程序
  預存程序是無法在純量運算式中使用的常式。 不像純量函數，它們可以將表格式結果及訊息傳回到用戶端、叫用資料定義語言 (DDL) 及資料操作語言 (DML) 陳述式，並傳回輸出參數。 如需 CLR 整合的優點，以及在 managed 程式碼和之間選擇的詳細資訊 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，請參閱[CLR 整合的總覽](../../relational-databases/clr-integration/clr-integration-overview.md)。  
  
## <a name="requirements-for-clr-stored-procedures"></a>CLR 預存程序的需求  
 在 common language runtime （CLR）中，預存程式會實作為元件中類別的公用靜態方法 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 。 靜態方法可宣告為 Void，或傳回整數值。 如果它傳回整數值，則會將傳回的整數視為程序的傳回碼。 例如：  
  
 `EXECUTE @return_status = procedure_name`  
  
 @return_status變數會包含方法所傳回的值。 如果方法宣告為 Void，則傳回碼會是 0。  
  
 如果方法採用參數，則 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 實作中的參數數目應與預存程序之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 宣告中使用的參數數目相同。  
  
 傳遞至 CLR 預存程序的參數可以是在 Managed 程式碼中具有對等類型的任何原生 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型。 對於用以建立程序的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語法，應使用最適合的原生 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型對等類型來指定這些類型。 如需類型轉換的詳細資訊，請參閱[對應 CLR 參數資料](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。  
  
### <a name="table-valued-parameters"></a>資料表值參數  
 資料表值參數 (TVP) 是使用者定義資料表類型，會傳入到程序或函數中，提供有效的方式將資料的多個資料列傳遞到伺服器。 雖然 TVP 提供相似的功能給參數陣列，但是也提供更大的彈性和與 [!INCLUDE[tsql](../../includes/tsql-md.md)] 更緊密的整合。 它們也能夠協助您獲得更佳的效能。 TVP 也減少與伺服器之間的往返次數。 除了傳送多個要求到伺服器 (例如夾帶純量參數的清單)，資料能以 TVP 的形式傳送到伺服器。 使用者定義資料表類型無法以資料表值參數的形式傳遞到 Managed 預存程序或在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序中執行的函數，也無法從該預存程序或函數傳回。 如需 Tvp 的詳細資訊，請參閱[使用資料表值參數 &#40;資料庫引擎&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)。  
  
## <a name="returning-results-from-clr-stored-procedures"></a>傳回 CLR 預存程序的結果  
 有數種方式可從 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 預存程序傳回資訊。 這包括輸出參數、表格式結果及訊息。  
  
### <a name="output-parameters-and-clr-stored-procedures"></a>OUTPUT 參數與 CLR 預存程序  
 與 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序一樣，資訊可透過 OUTPUT 參數，從 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 預存程序傳回。 用於建立 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] DML 語法，與用於建立寫入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 之預存程序的語法相同。 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 類別內實作程式碼中的對應參數應使用依參照傳遞的參數做為引數。 請注意，Visual Basic 不支援與 c # 相同的輸出參數。 您必須依參考指定參數，並套用 \<Out()> 屬性來表示輸出參數，如下所示：  
  
```vb
Imports System.Runtime.InteropServices  
...  
Public Shared Sub PriceSum ( <Out()> ByRef value As SqlInt32)  
```  
  
 以下範例示範透過 OUT 參數傳回資訊的預存程序：  
  
```csharp  
using System;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void PriceSum(out SqlInt32 value)  
   {  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         value = 0;  
         connection.Open();  
         SqlCommand command = new SqlCommand("SELECT Price FROM Products", connection);  
         SqlDataReader reader = command.ExecuteReader();  
  
         using (reader)  
         {  
            while( reader.Read() )  
            {  
               value += reader.GetSqlInt32(0);  
            }  
         }           
      }  
   }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
Imports System.Runtime.InteropServices  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Executes a query and iterates over the results to perform a summation.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub PriceSum( <Out()> ByRef value As SqlInt32)  
  
        Using connection As New SqlConnection("context connection=true")  
           value = 0  
           Connection.Open()  
           Dim command As New SqlCommand("SELECT Price FROM Products", connection)  
           Dim reader As SqlDataReader  
           reader = command.ExecuteReader()  
  
           Using reader  
              While reader.Read()  
                 value += reader.GetSqlInt32(0)  
              End While  
           End Using  
        End Using          
    End Sub  
End Class  
```  
  
 一旦包含上述 CLR 預存程式的元件在伺服器上建立並建立之後， [!INCLUDE[tsql](../../includes/tsql-md.md)] 就會使用下列方法在資料庫中建立程式，並將*sum*指定為 OUTPUT 參數。  
  
```sql
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
-- if StoredProcedures class was inside a namespace, called MyNS,  
-- you would use:  
-- AS EXTERNAL NAME TestStoredProc.[MyNS.StoredProcedures].PriceSum  
```  
  
 請注意， *sum*會宣告為 `int` SQL Server 資料類型，並將 clr 預存程式中定義的*值*參數指定為 `SqlInt32` clr 資料類型。 當呼叫程式執行 CLR 預存程式時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動將 `SqlInt32` clr 資料類型轉換成 `int` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型。  如需哪些 CLR 資料類型可以和無法轉換的詳細資訊，請參閱[對應 Clr 參數資料](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。  
  
### <a name="returning-tabular-results-and-messages"></a>傳回表格式結果和訊息  
 將表格式結果及訊息傳回到用戶端可透過 `SqlPipe` 物件完成，該物件可藉由使用 `Pipe` 類別的 `SqlContext` 屬性來取得。 `SqlPipe` 物件具有 `Send` 方法。 藉由呼叫 `Send` 方法，您可透過管道將資料傳輸給呼叫應用程式。  
  
 這些是 `SqlPipe.Send` 方法的數個多載，包括傳送 `SqlDataReader` 多載及僅傳送文字字串的多載。  
  
###### <a name="returning-messages"></a>傳回訊息  
 使用 `SqlPipe.Send(string)` 將訊息傳送到用戶端應用程式。 訊息的文字限制在 8000 個字元以內。 如果訊息超過 8000 個字元，則會被截斷。  
  
###### <a name="returning-tabular-results"></a>傳回表格式結果  
 若要將查詢結果直接傳送至用戶端，請在 `Execute` 物件上使用 `SqlPipe` 方法的其中一個多載。 這是將結果傳回至用戶端的最有效方式，因為資料會傳輸到網域緩衝區，而不是複製到 Managed 記憶體中。 例如：  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Execute a command and send the results to the client directly.  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void ExecuteToClient()  
   {  
   using(SqlConnection connection = new SqlConnection("context connection=true"))   
   {  
      connection.Open();  
      SqlCommand command = new SqlCommand("select @@version", connection);  
      SqlContext.Pipe.ExecuteAndSend(command);  
      }  
   }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub ExecuteToClient()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            SqlContext.Pipe.ExecuteAndSend(command)  
        End Using  
    End Sub  
End Class  
```  
  
 若要傳送先前透過同處理序提供者執行的查詢結果 (或要使用 `SqlDataReader` 的自訂實作前置處理資料)，請使用採用 `Send` 之 `SqlDataReader` 方法的多載。 與先前描述的直接方法相比，此方法會稍微慢一點，但在將資料傳送到用戶端之前，它可以為操作資料提供更大彈性。  
  
```csharp  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Execute a command and send the resulting reader to the client  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void SendReaderToClient()  
   {  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         connection.Open();  
         SqlCommand command = new SqlCommand("select @@version", connection);  
         SqlDataReader r = command.ExecuteReader();  
         SqlContext.Pipe.Send(r);  
      }  
   }  
}  
```  
 
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub SendReaderToClient()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            Dim reader As SqlDataReader  
            reader = command.ExecuteReader()  
            SqlContext.Pipe.Send(reader)  
        End Using  
    End Sub  
End Class  
```  
  
 若要建立動態結果集、填入它並將它傳送至用戶端，您可建立目前連接的記錄，並使用 `SqlPipe.Send` 傳送該記錄。  
  
```csharp  
using System.Data;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
using System.Data.SqlTypes;  
  
public class StoredProcedures   
{  
   /// <summary>  
   /// Create a result set on the fly and send it to the client.  
   /// </summary>  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void SendTransientResultSet()  
   {  
      // Create a record object that represents an individual row, including it's metadata.  
      SqlDataRecord record = new SqlDataRecord(new SqlMetaData("stringcol", SqlDbType.NVarChar, 128));  
  
      // Populate the record.  
      record.SetSqlString(0, "Hello World!");  
  
      // Send the record to the client.  
      SqlContext.Pipe.Send(record);  
   }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Create a result set on the fly and send it to the client.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub SendTransientResultSet()  
        ' Create a record object that represents an individual row, including it's metadata.  
        Dim record As New SqlDataRecord(New SqlMetaData("stringcol", SqlDbType.NVarChar, 128) )  
  
        ' Populate the record.  
        record.SetSqlString(0, "Hello World!")  
  
        ' Send the record to the client.  
        SqlContext.Pipe.Send(record)          
    End Sub  
End Class   
```  
  
 此範例是透過 `SqlPipe` 傳送表格式結果及訊息。  
  
```csharp  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void HelloWorld()  
   {  
      SqlContext.Pipe.Send("Hello world! It's now " + System.DateTime.Now.ToString()+"\n");  
      using(SqlConnection connection = new SqlConnection("context connection=true"))   
      {  
         connection.Open();  
         SqlCommand command = new SqlCommand("SELECT ProductNumber FROM ProductMaster", connection);  
         SqlDataReader reader = command.ExecuteReader();  
         SqlContext.Pipe.Send(reader);  
      }  
   }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class StoredProcedures   
    ''' <summary>  
    ''' Execute a command and send the results to the client directly.  
    ''' </summary>  
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub HelloWorld()  
        SqlContext.Pipe.Send("Hello world! It's now " & System.DateTime.Now.ToString() & "\n")  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT ProductNumber FROM ProductMaster", connection)  
            Dim reader As SqlDataReader  
            reader = command.ExecuteReader()  
            SqlContext.Pipe.Send(reader)  
        End Using  
    End Sub  
End Class   
```  
  
 第一個 `Send` 會將訊息傳送至用戶端，而第二個則使用 `SqlDataReader` 傳送表格式結果。  
  
 請注意，這些範例僅做為說明之用。 對於需要大量計算的應用程式，CLR 函數比簡單的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式更為適合。 幾乎等同於先前範例的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序為：  
  
```sql
CREATE PROCEDURE HelloWorld() AS  
BEGIN  
PRINT('Hello world!')  
SELECT ProductNumber FROM ProductMaster  
END;  
```  
  
> [!NOTE]  
>  在用戶端應用程式中，擷取訊息及結果集的方式不同。 例如， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 結果集會出現在 [**結果**] 視圖中，而訊息則會出現在 [**訊息**] 窗格中。  
  
 如果上述的 Visual C# 程式碼儲存在 MyFirstUdp.cs 檔案中，而且使用下列方式編譯：  
  
```console
csc /t:library /out:MyFirstUdp.dll MyFirstUdp.cs   
```  
  
 或者，如果上述的 Visual Basic 程式碼儲存在 MyFirstUdp.vb 檔案中，而且使用下列方式編譯：  
  
```console
vbc /t:library /out:MyFirstUdp.dll MyFirstUdp.vb   
```  
  
> [!NOTE]  
>  從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，就不支援以 `/clr:pure` 編譯之 Visual C++ 資料庫物件 (如預存程序) 的執行。  
  
 利用下列 DDL，可以註冊所產生的組件，並叫用進入點：  
  
```sql
CREATE ASSEMBLY MyFirstUdp FROM 'C:\Programming\MyFirstUdp.dll';  
CREATE PROCEDURE HelloWorld  
AS EXTERNAL NAME MyFirstUdp.StoredProcedures.HelloWorld;  
EXEC HelloWorld;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CLR 使用者定義函數](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)   
 [CLR 使用者定義類型](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)   
 [CLR 觸發程序](../../../2014/database-engine/dev-guide/clr-triggers.md)  
  
  
