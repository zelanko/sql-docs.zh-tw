---
title: CLR 表值函數 |微軟文件
description: 表值函數返回表。 在 SQL Server CLR 整合中,可以在託管代碼中編寫表值函數。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- Transact-SQL table-valued functions
- table-valued functions [CLR integration]
- TVFs [CLR integration]
ms.assetid: 9a6133ea-36e9-45bf-b572-1c0df3d6c194
author: rothja
ms.author: jroth
ms.openlocfilehash: 42391504a8c48248e47b5f09e8feb31b613bbfca
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488456"
---
# <a name="clr-table-valued-functions"></a>CLR 資料表值函式
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  資料表值函式是會傳回資料表的使用者定義函數。  
  
 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 開始，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可讓您以任何 Managed 語言定義資料表值函式，藉以擴充資料表值函式的功能。 數據通過**IE500 或** **IE 枚舉器**物件從表值函數返回。  
  
> [!NOTE]  
>  對於表值函數,傳回表類型的列不能包括時間戳列或非 Unicode 字串資料類型列(如**char、varchar**和**varchar****文字**)。 不支援 NOT NULL 條件約束。  
  
 有關 CLR 表值函數的詳細資訊,請查看 MSSQLTips[對 SQL Server CLR 表值函數的介紹!](https://www.mssqltips.com/sqlservertip/2582/introduction-to-sql-server-clr-table-valued-functions/)  
  
## <a name="differences-between-transact-sql-and-clr-table-valued-functions"></a>Transact-SQL 和 CLR 資料表值函式之間的差異  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料表值函式會將呼叫函數的結果具體化為中繼資料表。 由於 TVF 使用中繼資料表，因此可以透過結果支援條件約束和唯一的索引。 當傳回較大的結果時，這些功能會非常有用。  
  
 相反地，CLR 資料表值函式則是屬於以資料流模型進行處理的替代方案。 整組結果不需要在單一資料表中具體化。 託管函數返回的**IE55 物件**由調用表值函數的查詢的執行計劃直接調用,結果以增量方式使用。 此資料流模型能確保第一個資料列可供使用之後，就立即使用結果，而不會等待整個資料表填入完成。 如果傳回大量的資料列，這也是一個較好的替代方式，因為它們不必整體在記憶體中進行實體化。 例如，Managed 資料表值函式可用來剖析文字檔案，並將每一行以資料列的方式傳回。  
  
## <a name="implementing-table-valued-functions"></a>實作資料表數值函數  
 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 組件中，將資料表值函式當做類別上的方法實作。 表值函數代碼必須實現**IE500 介面**。 **IE500 介面**在 .NET 框架中定義。 表示 .NET 框架中的陣列和集合的類型已經實現了**IE500 介面**。 這樣您就可以輕易地撰寫出能將集合或陣列轉換為結果集的資料表值函式。  
  
## <a name="table-valued-parameters"></a>資料表值參數  
 資料表值參數是傳入到程序或函數中的使用者定義資料表類型，能提供有效的方式將資料的多個資料列傳遞到伺服器。 資料表值參數提供的功能與參數陣列相似，但是具備了更大的彈性並且和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 更緊密地整合。 它們也能夠協助您獲得更佳的效能。 資料表值參數也可以減少與伺服器之間的往返次數。 資料能以資料表值參數的形式傳送到伺服器，而不是傳送多個要求到伺服器，例如一併傳送純量參數的清單。 使用者定義資料表類型無法以資料表值參數的形式傳遞到 Managed 預存程序或在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序中執行的函數，也無法從該預存程序或函數傳回。 如需詳細資訊，請參閱[使用資料表值參數 &#40;Database Engine&#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)。  
  
## <a name="output-parameters-and-table-valued-functions"></a>輸出參數和資料表值函式  
 資訊可以使用輸出參數，從資料表值函式傳回。 實作程式碼資料表值函式中的對應參數應使用依參照傳遞的參數做為引數。 請注意，Visual Basic 不支援輸出參數的方式，與 Visual C# 所使用的方式不同。 您必須透過引用指定參數,並應用\<Out()> 屬性來表示輸出參數,如下所示:  
  
```vb  
Imports System.Runtime.InteropServices  
...  
Public Shared Sub FillRow ( <Out()> ByRef value As SqlInt32)  
```  
  
### <a name="defining-a-table-valued-function-in-transact-sql"></a>在 Transact-SQL 中定義資料表值函式  
 定義 CLR 表值函數的語法[!INCLUDE[tsql](../../includes/tsql-md.md)]類似於 表值函數的語法,並添加外部**NAME**子句。 例如：  
  
```  
CREATE FUNCTION GetEmpFirstLastNames()  
RETURNS TABLE (FirstName NVARCHAR(4000), LastName NVARCHAR(4000))  
EXTERNAL NAME MyDotNETAssembly.[MyNamespace.MyClassname]. GetEmpFirstLastNames;  
```  
  
 資料表值函式用於以關聯式形式表示資料，以便在查詢中進行進一步的處理，例如：  
  
```  
select * from function();  
select * from tbl join function() f on tbl.col = f.col;  
select * from table t cross apply function(t.column);  
```  
  
 當資料表值函式符合下列條件時，便會傳回資料表：  
  
-   當資料表值函式是從純量輸入引數建立時。 例如，採用逗號分隔數字字串，並將它們樞紐至資料表的資料表值函式。  
  
-   當資料表值函式是從外部資料產生時。 例如，讀取事件記錄檔並將其以資料表的方式公開的資料表值函式。  
  
 **注意**表值函數只能通過[!INCLUDE[tsql](../../includes/tsql-md.md)]**InitMethod 方法**中的查詢執行數據訪問,而不能在**FillRow**方法中執行數據訪問。 如果執行[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢,則應使用**SqlFunction.DataAccess.Read**屬性標記**InitMethod。**  
  
## <a name="a-sample-table-valued-function"></a>資料表值函式範例  
 下列資料表值函式會從系統事件記錄檔傳回資訊。 該函數使用包含要讀取之事件記錄檔名稱的單一字串引數。  
  
###### <a name="sample-code"></a>範例程式碼  
  
```csharp  
using System;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Collections;  
using System.Data.SqlTypes;  
using System.Diagnostics;  
  
public class TabularEventLog  
{  
    [SqlFunction(FillRowMethodName = "FillRow")]  
    public static IEnumerable InitMethod(String logname)  
    {  
        return new EventLog(logname).Entries;    }  
  
    public static void FillRow(Object obj, out SqlDateTime timeWritten, out SqlChars message, out SqlChars category, out long instanceId)  
    {  
        EventLogEntry eventLogEntry = (EventLogEntry)obj;  
        timeWritten = new SqlDateTime(eventLogEntry.TimeWritten);  
        message = new SqlChars(eventLogEntry.Message);  
        category = new SqlChars(eventLogEntry.Category);  
        instanceId = eventLogEntry.InstanceId;  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data.Sql  
Imports Microsoft.SqlServer.Server  
Imports System.Collections  
Imports System.Data.SqlTypes  
Imports System.Diagnostics  
Imports System.Runtime.InteropServices  
  
Public Class TabularEventLog  
    <SqlFunction(FillRowMethodName:="FillRow")> _  
    Public Shared Function InitMethod(ByVal logname As String) As IEnumerable  
        Return New EventLog(logname).Entries  
    End Function  
  
    Public Shared Sub FillRow(ByVal obj As Object, <Out()> ByRef timeWritten As SqlDateTime, <Out()> ByRef message As SqlChars, <Out()> ByRef category As SqlChars, <Out()> ByRef instanceId As Long)  
        Dim eventLogEnTry As EventLogEntry = CType(obj, EventLogEntry)  
        timeWritten = New SqlDateTime(eventLogEnTry.TimeWritten)  
        message = New SqlChars(eventLogEnTry.Message)  
        category = New SqlChars(eventLogEnTry.Category)  
        instanceId = eventLogEnTry.InstanceId  
    End Sub  
End Class  
```  
  
###### <a name="declaring-and-using-the-sample-table-valued-function"></a>宣告和使用範例資料表值函式  
 在範例資料表值函式經過編譯之後，就可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中以下列的方式宣告：  
  
```  
use master;  
-- Replace SQL_Server_logon with your SQL Server user credentials.  
GRANT EXTERNAL ACCESS ASSEMBLY TO [SQL_Server_logon];   
-- Modify the following line to specify a different database.  
ALTER DATABASE master SET TRUSTWORTHY ON;  
  
-- Modify the next line to use the appropriate database.  
CREATE ASSEMBLY tvfEventLog   
FROM 'D:\assemblies\tvfEventLog\tvfeventlog.dll'   
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
GO  
CREATE FUNCTION ReadEventLog(@logname nvarchar(100))  
RETURNS TABLE   
(logTime datetime,Message nvarchar(4000),Category nvarchar(4000),InstanceId bigint)  
AS   
EXTERNAL NAME tvfEventLog.TabularEventLog.InitMethod;  
GO  
```  
  
 不支援在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 上執行使用 /clr:pure 編譯的 Visual C++ 資料庫物件。 例如，這類資料庫物件包括資料表值函式。  
  
 若要測試範例，請嘗試下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼：  
  
```  
-- Select the top 100 events,  
SELECT TOP 100 *  
FROM dbo.ReadEventLog(N'Security') as T;  
go  
  
-- Select the last 10 login events.  
SELECT TOP 10 T.logTime, T.Message, T.InstanceId   
FROM dbo.ReadEventLog(N'Security') as T  
WHERE T.Category = N'Logon/Logoff';  
go  
```  
  
## <a name="sample-returning-the-results-of-a-sql-server-query"></a>範例：傳回 SQL Server 查詢的結果  
 下列範例示範查詢 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫的資料表值函式。 這個範例使用 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 的 AdventureWorks Light 資料庫。 有關[https://www.codeplex.com/sqlserversamples](https://go.microsoft.com/fwlink/?LinkId=87843)下載冒險作品的更多資訊,請參閱。  
  
 將原始程式碼檔命名為 FindInvalidEmails.cs 或 FindInvalidEmails.vb。  
  
```csharp  
using System;  
using System.Collections;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
  
using Microsoft.SqlServer.Server;  
  
public partial class UserDefinedFunctions {  
   private class EmailResult {  
      public SqlInt32 CustomerId;  
      public SqlString EmailAdress;  
  
      public EmailResult(SqlInt32 customerId, SqlString emailAdress) {  
         CustomerId = customerId;  
         EmailAdress = emailAdress;  
      }  
   }  
  
   public static bool ValidateEmail(SqlString emailAddress) {  
      if (emailAddress.IsNull)  
         return false;  
  
      if (!emailAddress.Value.EndsWith("@adventure-works.com"))  
         return false;  
  
      // Validate the address. Put any more rules here.  
      return true;  
   }  
  
   [SqlFunction(  
       DataAccess = DataAccessKind.Read,  
       FillRowMethodName = "FindInvalidEmails_FillRow",  
       TableDefinition="CustomerId int, EmailAddress nvarchar(4000)")]  
   public static IEnumerable FindInvalidEmails(SqlDateTime modifiedSince) {  
      ArrayList resultCollection = new ArrayList();  
  
      using (SqlConnection connection = new SqlConnection("context connection=true")) {  
         connection.Open();  
  
         using (SqlCommand selectEmails = new SqlCommand(  
             "SELECT " +  
             "[CustomerID], [EmailAddress] " +  
             "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " +  
             "WHERE [ModifiedDate] >= @modifiedSince",  
             connection)) {  
            SqlParameter modifiedSinceParam = selectEmails.Parameters.Add(  
                "@modifiedSince",  
                SqlDbType.DateTime);  
            modifiedSinceParam.Value = modifiedSince;  
  
            using (SqlDataReader emailsReader = selectEmails.ExecuteReader()) {  
               while (emailsReader.Read()) {  
                  SqlString emailAddress = emailsReader.GetSqlString(1);  
                  if (ValidateEmail(emailAddress)) {  
                     resultCollection.Add(new EmailResult(  
                         emailsReader.GetSqlInt32(0),  
                         emailAddress));  
                  }  
               }  
            }  
         }  
      }  
  
      return resultCollection;  
   }  
  
   public static void FindInvalidEmails_FillRow(  
       object emailResultObj,  
       out SqlInt32 customerId,  
       out SqlString emailAdress) {  
      EmailResult emailResult = (EmailResult)emailResultObj;  
  
      customerId = emailResult.CustomerId;  
      emailAdress = emailResult.EmailAdress;  
   }  
};  
```  
  
```vb  
Imports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Public Partial Class UserDefinedFunctions  
   Private Class EmailResult  
      Public CustomerId As SqlInt32  
      Public EmailAdress As SqlString  
  
      Public Sub New(customerId__1 As SqlInt32, emailAdress__2 As SqlString)  
         CustomerId = customerId__1  
         EmailAdress = emailAdress__2  
      End Sub  
   End Class  
  
   Public Shared Function ValidateEmail(emailAddress As SqlString) As Boolean  
      If emailAddress.IsNull Then  
         Return False  
      End If  
  
      If Not emailAddress.Value.EndsWith("@adventure-works.com") Then  
         Return False  
      End If  
  
      ' Validate the address. Put any more rules here.  
      Return True  
   End Function  
  
   <SqlFunction(DataAccess := DataAccessKind.Read, FillRowMethodName := "FindInvalidEmails_FillRow", TableDefinition := "CustomerId int, EmailAddress nvarchar(4000)")> _  
   Public Shared Function FindInvalidEmails(modifiedSince As SqlDateTime) As IEnumerable  
      Dim resultCollection As New ArrayList()  
  
      Using connection As New SqlConnection("context connection=true")  
         connection.Open()  
  
         Using selectEmails As New SqlCommand("SELECT " & "[CustomerID], [EmailAddress] " & "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " & "WHERE [ModifiedDate] >= @modifiedSince", connection)  
            Dim modifiedSinceParam As SqlParameter = selectEmails.Parameters.Add("@modifiedSince", SqlDbType.DateTime)  
            modifiedSinceParam.Value = modifiedSince  
  
            Using emailsReader As SqlDataReader = selectEmails.ExecuteReader()  
               While emailsReader.Read()  
                  Dim emailAddress As SqlString = emailsReader.GetSqlString(1)  
                  If ValidateEmail(emailAddress) Then  
                     resultCollection.Add(New EmailResult(emailsReader.GetSqlInt32(0), emailAddress))  
                  End If  
               End While  
            End Using  
         End Using  
      End Using  
  
      Return resultCollection  
   End Function  
  
   Public Shared Sub FindInvalidEmails_FillRow(emailResultObj As Object, ByRef customerId As SqlInt32, ByRef emailAdress As SqlString)  
      Dim emailResult As EmailResult = DirectCast(emailResultObj, EmailResult)  
  
      customerId = emailResult.CustomerId  
      emailAdress = emailResult.EmailAdress  
   End Sub  
End ClassImports System.Collections  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Public Partial Class UserDefinedFunctions  
   Private Class EmailResult  
      Public CustomerId As SqlInt32  
      Public EmailAdress As SqlString  
  
      Public Sub New(customerId__1 As SqlInt32, emailAdress__2 As SqlString)  
         CustomerId = customerId__1  
         EmailAdress = emailAdress__2  
      End Sub  
   End Class  
  
   Public Shared Function ValidateEmail(emailAddress As SqlString) As Boolean  
      If emailAddress.IsNull Then  
         Return False  
      End If  
  
      If Not emailAddress.Value.EndsWith("@adventure-works.com") Then  
         Return False  
      End If  
  
      ' Validate the address. Put any more rules here.  
      Return True  
   End Function  
  
   <SqlFunction(DataAccess := DataAccessKind.Read, FillRowMethodName := "FindInvalidEmails_FillRow", TableDefinition := "CustomerId int, EmailAddress nvarchar(4000)")> _  
   Public Shared Function FindInvalidEmails(modifiedSince As SqlDateTime) As IEnumerable  
      Dim resultCollection As New ArrayList()  
  
      Using connection As New SqlConnection("context connection=true")  
         connection.Open()  
  
         Using selectEmails As New SqlCommand("SELECT " & "[CustomerID], [EmailAddress] " & "FROM [AdventureWorksLT2008].[SalesLT].[Customer] " & "WHERE [ModifiedDate] >= @modifiedSince", connection)  
            Dim modifiedSinceParam As SqlParameter = selectEmails.Parameters.Add("@modifiedSince", SqlDbType.DateTime)  
            modifiedSinceParam.Value = modifiedSince  
  
            Using emailsReader As SqlDataReader = selectEmails.ExecuteReader()  
               While emailsReader.Read()  
                  Dim emailAddress As SqlString = emailsReader.GetSqlString(1)  
                  If ValidateEmail(emailAddress) Then  
                     resultCollection.Add(New EmailResult(emailsReader.GetSqlInt32(0), emailAddress))  
                  End If  
               End While  
            End Using  
         End Using  
      End Using  
  
      Return resultCollection  
   End Function  
  
   Public Shared Sub FindInvalidEmails_FillRow(emailResultObj As Object, customerId As SqlInt32, emailAdress As SqlString)  
      Dim emailResult As EmailResult = DirectCast(emailResultObj, EmailResult)  
  
      customerId = emailResult.CustomerId  
      emailAdress = emailResult.EmailAdress  
   End Sub  
End Class  
```  
  
 將原始程式碼編譯為 DLL，並且將這個 DLL 複製到 C 磁碟機的根目錄。  接著執行下列的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢。  
  
```  
use AdventureWorksLT2008;  
go  
  
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'FindInvalidEmails')  
   DROP FUNCTION FindInvalidEmails;  
go  
  
IF EXISTS (SELECT name FROM sys.assemblies WHERE name = 'MyClrCode')  
   DROP ASSEMBLY MyClrCode;  
go  
  
CREATE ASSEMBLY MyClrCode FROM 'C:\FindInvalidEmails.dll'  
WITH PERMISSION_SET = SAFE -- EXTERNAL_ACCESS;  
GO  
  
CREATE FUNCTION FindInvalidEmails(@ModifiedSince datetime)   
RETURNS TABLE (  
   CustomerId int,  
   EmailAddress nvarchar(4000)  
)  
AS EXTERNAL NAME MyClrCode.UserDefinedFunctions.[FindInvalidEmails];  
go  
  
SELECT * FROM FindInvalidEmails('2000-01-01');  
go  
```  
  
  
