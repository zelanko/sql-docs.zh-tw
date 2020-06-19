---
title: CLR 觸發程式 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- inserted tables
- database objects [CLR integration], triggers
- common language runtime [SQL Server], triggers
- updated columns
- building database objects [CLR integration], triggers
- triggers [CLR integration]
- deleted tables
- EventData property
- SqlTriggerContext class
- transactions [CLR integration]
ms.assetid: 302a4e4a-3172-42b6-9cc0-4a971ab49c1c
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 91f12b0d97d2e2065c5bb08d175253c22dffb032
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933690"
---
# <a name="clr-triggers"></a>CLR 觸發程序
  因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已與 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Common Language Runtime (CLR) 整合，所以您可以使用任何 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 語言建立 CLR 觸發程序。 本節涵蓋使用 CLR 整合實作之觸發程序的特定資訊。 如需觸發程式的完整討論，請參閱[DDL 觸發](../../relational-databases/triggers/ddl-triggers.md)程式。  
  
## <a name="what-are-triggers"></a>什麼是觸發程序？  
 觸發程序是一種特殊的預存程序，會在語言事件執行時自動執行。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 包含兩種一般的觸發程序：資料操作語言 (DML) 和資料定義語言 (DDL) 觸發程序。 當`INSERT`、`UPDATE` 或 `DELETE` 陳述式在指定的資料表或檢視中修改資料時，可以使用 DML 觸發程序。 DDL 觸發程序會引發預存程序來回應多種 DDL 陳述式，這些主要是以 `CREATE`、`ALTER` 和 `DROP` 開頭的陳述式。 DDL 觸發程序可用於稽核和控管資料庫作業等管理工作。  
  
## <a name="unique-capabilities-of-clr-triggers"></a>CLR 觸發程序的獨特功能  
 以 [!INCLUDE[tsql](../../includes/tsql-md.md)] 撰寫的觸發程序可以藉由使用 `UPDATE(column)` 和 `COLUMNS_UPDATED()` 函數，來判定檢視或資料表中哪些資料行已經更新。  
  
 以 CLR 語言撰寫的觸發程序與其他 CLR 整合物件有許多顯著的區別。 CLR 觸發程序可以：  
  
-   參考 `INSERTED` 及 `DELETED` 資料表中的資料  
  
-   判定 `UPDATE` 作業修改了哪些資料行。  
  
-   存取受 DDL 陳述式的執行所影響之資料庫物件的相關資訊。  
  
 這些功能可以在查詢語言中自動提供，或由 `SqlTriggerContext` 類別提供。 如需 CLR 整合的優點，以及在 managed 程式碼和之間選擇的詳細資訊 [!INCLUDE[tsql](../../includes/tsql-md.md)] ，請參閱[CLR 整合的總覽](../../relational-databases/clr-integration/clr-integration-overview.md)。  
  
## <a name="using-the-sqltriggercontext-class"></a>使用 SqlTriggerContext 類別  
 `SqlTriggerContext` 類別無法公開建構，而是僅可藉由存取 CLR 觸發程序主體內的 `SqlContext.TriggerContext` 屬性來取得。 藉由呼叫 `SqlTriggerContext` 屬性，可從作用中的 `SqlContext` 取得 `SqlContext.TriggerContext` 類別：  
  
 `SqlTriggerContext myTriggerContext = SqlContext.TriggerContext;`  
  
 `SqlTriggerContext` 類別會提供觸發程序的內容資訊。 此內容相關資訊包括會造成引發觸發程序的動作類型 (已使用 UPDATE 作業修改其資料行)，而且，若其為 DDL 觸發程序，則包括說明觸發作業的 XML `EventData` 結構。 如需詳細資訊，請參閱[EVENTDATA &#40;transact-sql&#41;](/sql/t-sql/functions/eventdata-transact-sql)。  
  
### <a name="determining-the-trigger-action"></a>決定觸發動作  
 一旦取得 `SqlTriggerContext`，您就可以用它來決定引發觸發程序的動作類型。 此資訊可以透過 `TriggerAction` 類別的 `SqlTriggerContext` 屬性來取得。  
  
 若為 DML 觸發程序，`TriggerAction` 屬性可以為下列其中一個值：  
  
-   TriggerAction.Update (0x1)  
  
-   TriggerAction.Insert (0x2)  
  
-   TriggerAction.Delete(0x3)  
  
-   若為 DDL 觸發程序，可能的 TriggerAction 值清單會相當長。 如需詳細資訊，請參閱 .NET Framework SDK 中的＜TriggerAction 列舉＞。  
  
### <a name="using-the-inserted-and-deleted-tables"></a>使用插入和刪除的資料表  
 DML 觸發程式語句中會使用兩個特殊資料表：**插入**的資料表和**已刪除**的資料表。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會自動建立及管理這些資料表。 您可以使用這些暫存資料表測試某些資料修改的影響，並設定會執行 DML 觸發程序動作的條件，但是您無法直接改變資料表中的資料。  
  
 CLR 觸發程式可以透過 CLR 同進程提供者存取已**插入**和**已刪除**的資料表。 這是透過從 SqlContext 物件取得 `SqlCommand` 物件而完成。 例如：  
  
 C#  
  
```  
SqlConnection connection = new SqlConnection ("context connection = true");  
connection.Open();  
SqlCommand command = connection.CreateCommand();  
command.CommandText = "SELECT * from " + "inserted";  
```  
  
 Visual Basic  
  
```  
Dim connection As New SqlConnection("context connection=true")  
Dim command As SqlCommand  
connection.Open()  
command = connection.CreateCommand()  
command.CommandText = "SELECT * FROM " + "inserted"  
```  
  
### <a name="determining-updated-columns"></a>判定更新的資料行  
 您可以透過使用 `ColumnCount` 物件的 `SqlTriggerContext` 屬性，判定 UPDATE 作業所修改的資料行數。 您可以使用會將資料行序數做為輸入參數的 `IsUpdatedColumn` 方法，判定資料行是否已更新。 `True` 值表示資料行已更新。  
  
 例如，此程式碼片段 (本主題中稍後的 EmailAudit 觸發程序) 會列出所有已更新的資料行：  
  
 C#  
  
```  
reader = command.ExecuteReader();  
reader.Read();  
for (int columnNumber = 0; columnNumber < triggContext.ColumnCount; columnNumber++)  
{  
   pipe.Send("Updated column "  
      + reader.GetName(columnNumber) + "? "  
   + triggContext.IsUpdatedColumn(columnNumber).ToString());  
 }  
  
 reader.Close();  
```  
  
 Visual Basic  
  
```  
reader = command.ExecuteReader()  
reader.Read()  
Dim columnNumber As Integer  
  
For columnNumber=0 To triggContext.ColumnCount-1  
  
   pipe.Send("Updated column " & reader.GetName(columnNumber) & _  
   "? " & triggContext.IsUpdatedColumn(columnNumber).ToString() )  
  
Next  
  
reader.Close()  
```  
  
### <a name="accessing-eventdata-for-clr-ddl-triggers"></a>存取 CLR DDL 觸發程序的 EventData  
 DDL 觸發程序和一般觸發程序一樣，會引發預存程序以回應事件。 但和 DML 觸發程序不同的是，DDL 觸發程序不會引發預存程序以回應資料表或檢視上的 UPDATE、INSERT 或 DELETE 陳述式， 相反地，它們會引發以回應各種 DDL 陳述式 (主要是以 CREATE、ALTER 和 DROP 開頭的陳述式)。 DDL 觸發程序可用於管理工作，如稽核及監視資料庫作業與結構描述變更。  
  
 引發 DDL 觸發程序之事件的相關資訊可以在 `EventData` 類別的 `SqlTriggerContext` 屬性中取得。 此屬性包含一個 `xml` 值。 XML 結構描述包含下列項目的相關資訊：  
  
-   事件的時間。  
  
-   執行觸發程序期間所連接的系統處理序 ID (SPID)。  
  
-   引發觸發程序的事件類型。  
  
 接著，視事件類型而定，結構描述會包括其他資訊，例如發生事件的資料庫、發生事件的物件以及事件的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令。  
  
 在下面的範例中，下列 DDL 觸發程序會傳回未經處理的 `EventData` 屬性。  
  
> [!NOTE]  
>  此處顯示透過 `SqlPipe` 物件傳遞的結果及訊息僅做為說明之用，一般不提倡用來做為程式設計 CLR 觸發程序時要實際執行的程式碼。 傳回的其他資料可能不是預期的結果，並且會導致應用程式錯誤。  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Xml;  
using System.Text.RegularExpressions;  
  
public class CLRTriggers  
{  
   public static void DropTableTrigger()  
   {  
       SqlTriggerContext triggContext = SqlContext.TriggerContext;             
  
       switch(triggContext.TriggerAction)  
       {  
           case TriggerAction.DropTable:  
           SqlContext.Pipe.Send("Table dropped! Here's the EventData:");  
           SqlContext.Pipe.Send(triggContext.EventData.Value);  
           break;  
  
           default:  
           SqlContext.Pipe.Send("Something happened! Here's the EventData:");  
           SqlContext.Pipe.Send(triggContext.EventData.Value);  
           break;  
       }  
   }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class CLRTriggers   
  
    Public Shared Sub DropTableTrigger()  
        Dim triggContext As SqlTriggerContext  
        triggContext = SqlContext.TriggerContext  
  
        Select Case triggContext.TriggerAction  
           Case TriggerAction.DropTable  
              SqlContext.Pipe.Send("Table dropped! Here's the EventData:")  
              SqlContext.Pipe.Send(triggContext.EventData.Value)  
  
           Case Else  
              SqlContext.Pipe.Send("Something else happened! Here's the EventData:")  
              SqlContext.Pipe.Send(triggContext.EventData.Value)  
  
        End Select  
    End Sub  
End Class     
```  
  
 下列範例輸出為 `EventData` 事件引發 DDL 觸發程序後的 `CREATE TABLE` 屬性值。  
  
 `<EVENT_INSTANCE><PostTime>2004-04-16T21:17:16.160</PostTime><SPID>58</SPID><EventType>CREATE_TABLE</EventType><ServerName>MACHINENAME</ServerName><LoginName>MYDOMAIN\myname</LoginName><UserName>MYDOMAIN\myname</UserName><DatabaseName>AdventureWorks</DatabaseName><SchemaName>dbo</SchemaName><ObjectName>UserName</ObjectName><ObjectType>TABLE</ObjectType><TSQLCommand><SetOptions ANSI_NULLS="ON" ANSI_NULL_DEFAULT="ON" ANSI_PADDING="ON" QUOTED_IDENTIFIER="ON" ENCRYPTED="FALSE" /><CommandText>create table dbo.UserName  
(  
 UserName varchar(50),  
 RealName varchar(50)  
)  
</CommandText></TSQLCommand></EVENT_INSTANCE>`  
  
 除了可透過 `SqlTriggerContext` 類別存取的資訊外，查詢也可以參考同處理序 (In-Process) 中所執行命令文字內的 `COLUMNS_UPDATED` 和插入/刪除的資料行。  
  
## <a name="sample-clr-trigger"></a>範例 CLR 觸發程序  
 此範例中，將假設您要讓使用者選擇想要的 ID，但您想要知道輸入電子郵件地址做為其 ID 之特定使用者的案例。 下列觸發程序將會偵測到該項資訊，並將它記錄到稽核表中。  
  
> [!NOTE]  
>  此處顯示透過 `SqlPipe` 物件傳遞的結果及訊息僅做為說明之用，一般不提倡用於實際執行的程式碼。 傳回的其他資料可能不是預期的結果，並且會導致應用程式錯誤  
  
```csharp  
using System;  
using System.Data;  
using System.Data.Sql;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Xml;  
using System.Text.RegularExpressions;  
  
public class CLRTriggers  
{  
   [SqlTrigger(Name = @"EmailAudit", Target = "[dbo].[Users]", Event = "FOR INSERT, UPDATE, DELETE")]  
   public static void EmailAudit()  
   {  
      string userName;  
      string realName;  
      SqlCommand command;  
      SqlTriggerContext triggContext = SqlContext.TriggerContext;  
      SqlPipe pipe = SqlContext.Pipe;  
      SqlDataReader reader;  
  
      switch (triggContext.TriggerAction)  
      {  
         case TriggerAction.Insert:  
         // Retrieve the connection that the trigger is using  
         using (SqlConnection connection  
            = new SqlConnection(@"context connection=true"))  
         {  
            connection.Open();  
            command = new SqlCommand(@"SELECT * FROM INSERTED;",  
               connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
            userName = (string)reader[0];  
            realName = (string)reader[1];  
            reader.Close();  
  
            if (IsValidEMailAddress(userName))  
            {  
               command = new SqlCommand(  
                  @"INSERT [dbo].[UserNameAudit] VALUES ('"  
                  + userName + @"', '" + realName + @"');",  
                  connection);  
               pipe.Send(command.CommandText);  
               command.ExecuteNonQuery();  
               pipe.Send("You inserted: " + userName);  
            }  
         }  
  
         break;  
  
         case TriggerAction.Update:  
         // Retrieve the connection that the trigger is using  
         using (SqlConnection connection  
            = new SqlConnection(@"context connection=true"))  
         {  
            connection.Open();  
            command = new SqlCommand(@"SELECT * FROM INSERTED;",  
               connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
  
            userName = (string)reader[0];  
            realName = (string)reader[1];  
  
            pipe.Send(@"You updated: '" + userName + @"' - '"  
               + realName + @"'");  
  
            for (int columnNumber = 0; columnNumber < triggContext.ColumnCount; columnNumber++)  
            {  
               pipe.Send("Updated column "  
                  + reader.GetName(columnNumber) + "? "  
                  + triggContext.IsUpdatedColumn(columnNumber).ToString());  
            }  
  
            reader.Close();  
         }  
  
         break;  
  
         case TriggerAction.Delete:  
            using (SqlConnection connection  
               = new SqlConnection(@"context connection=true"))  
               {  
                  connection.Open();  
                  command = new SqlCommand(@"SELECT * FROM DELETED;",  
                     connection);  
                  reader = command.ExecuteReader();  
  
                  if (reader.HasRows)  
                  {  
                     pipe.Send(@"You deleted the following rows:");  
                     while (reader.Read())  
                     {  
                        pipe.Send(@"'" + reader.GetString(0)  
                        + @"', '" + reader.GetString(1) + @"'");  
                     }  
  
                     reader.Close();  
  
                     //alternately, to just send a tabular resultset back:  
                     //pipe.ExecuteAndSend(command);  
                  }  
                  else  
                  {  
                     pipe.Send("No rows affected.");  
                  }  
               }  
  
               break;  
            }  
        }  
  
     public static bool IsValidEMailAddress(string email)  
     {  
         return Regex.IsMatch(email, @"^([\w-]+\.)*?[\w-]+@[\w-]+\.([\w-]+\.)*?[\w]+$");  
     }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
Imports System.Text.RegularExpressions  
  
'The Partial modifier is only required on one class definition per project.  
Partial Public Class CLRTriggers   
  
    <SqlTrigger(Name:="EmailAudit", Target:="[dbo].[Users]", Event:="FOR INSERT, UPDATE, DELETE")> _  
    Public Shared Sub EmailAudit()  
        Dim userName As String  
        Dim realName As String  
        Dim command As SqlCommand  
        Dim triggContext As SqlTriggerContext  
        Dim pipe As SqlPipe  
        Dim reader As SqlDataReader    
  
        triggContext = SqlContext.TriggerContext      
        pipe = SqlContext.Pipe    
  
        Select Case triggContext.TriggerAction  
           Case TriggerAction.Insert  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM INSERTED;", connection)  
  
                 reader = command.ExecuteReader()  
                 reader.Read()  
  
                 userName = CType(reader(0), String)  
                 realName = CType(reader(1), String)  
  
                 reader.Close()  
  
                 If IsValidEmailAddress(userName) Then  
                     command = New SqlCommand("INSERT [dbo].[UserNameAudit] VALUES ('" & _  
                       userName & "', '" & realName & "');", connection)  
  
                    pipe.Send(command.CommandText)  
                    command.ExecuteNonQuery()  
                    pipe.Send("You inserted: " & userName)  
  
                 End If  
              End Using  
  
           Case TriggerAction.Update  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM INSERTED;", connection)  
  
                 reader = command.ExecuteReader()  
                 reader.Read()  
  
                 userName = CType(reader(0), String)  
                 realName = CType(reader(1), String)  
  
                 pipe.Send("You updated: " & userName & " - " & realName)  
  
                 Dim columnNumber As Integer  
  
                 For columnNumber=0 To triggContext.ColumnCount-1  
  
                    pipe.Send("Updated column " & reader.GetName(columnNumber) & _  
                      "? " & triggContext.IsUpdatedColumn(columnNumber).ToString() )  
  
                 Next  
  
                 reader.Close()  
              End Using  
  
           Case TriggerAction.Delete  
              Using connection As New SqlConnection("context connection=true")  
                 connection.Open()  
                 command = new SqlCommand("SELECT * FROM DELETED;", connection)  
  
                 reader = command.ExecuteReader()  
  
                 If reader.HasRows Then  
                    pipe.Send("You deleted the following rows:")  
  
                    While reader.Read()  
  
                       pipe.Send( reader.GetString(0) & ", " & reader.GetString(1) )  
  
                    End While   
  
                    reader.Close()  
  
                    ' Alternately, just send a tabular resultset back:  
                    ' pipe.ExecuteAndSend(command)  
  
                 Else  
                   pipe.Send("No rows affected.")  
                 End If  
  
              End Using   
        End Select  
    End Sub  
  
    Public Shared Function IsValidEMailAddress(emailAddress As String) As Boolean  
  
       return Regex.IsMatch(emailAddress, "^([\w-]+\.)*?[\w-]+@[\w-]+\.([\w-]+\.)*?[\w]+$")  
    End Function      
End Class  
```  
  
 假設存在兩個資料表，其定義如下：  
  
```  
CREATE TABLE Users  
(  
    UserName nvarchar(200) NOT NULL,  
    RealName nvarchar(200) NOT NULL  
);  
GO CREATE TABLE UserNameAudit  
(  
    UserName nvarchar(200) NOT NULL,  
    RealName nvarchar(200) NOT NULL  
)  
```  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]在中建立觸發程式的語句 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 如下所示，並假設元件**SQLCLRTest**已經在目前的資料庫中註冊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
```  
CREATE TRIGGER EmailAudit  
ON Users  
FOR INSERT, UPDATE, DELETE  
AS  
EXTERNAL NAME SQLCLRTest.CLRTriggers.EmailAudit  
```  
  
## <a name="validating-and-canceling-invalid-transactions"></a>驗證和取消無效的交易  
 使用觸發程序來驗證 INSERT、UPDATE 或 DELETE 交易並取消無效的交易，或避免對資料庫結構描述進行變更是很常見的。 這項作業可藉由在觸發程序中整合驗證邏輯，然後在動作不符合驗證準則時回復目前的交易來完成。  
  
 在觸發程序內呼叫時，`Transaction.Rollback` 方法或具有 "TRANSACTION ROLLBACK" 命令文字的 SqlCommand 會擲回例外狀況並顯示模稜兩可的錯誤訊息，且必須包裝在 try/catch 區塊中。 您看到的錯誤訊息類似下列各項：  
  
```  
Msg 6549, Level 16, State 1, Procedure trig_InsertValidator, Line 0  
A .NET Framework error occurred during execution of user defined routine or aggregate 'trig_InsertValidator':   
System.Data.SqlClient.SqlException: Transaction is not allowed to roll back inside a user defined routine, trigger or aggregate because the transaction is not started in that CLR level. Change application logic to enforce strict transaction nesting... User transaction, if any, will be rolled back.  
```  
  
 這項例外狀況是在預期中，而必須有 try/catch 區塊，程式碼才能繼續執行。 當觸發程序程式碼完成執行時，會引發另一項例外狀況  
  
```  
Msg 3991, Level 16, State 1, Procedure trig_InsertValidator, Line 1   
The context transaction which was active before entering user defined routine, trigger or aggregate "trig_InsertValidator" has been ended inside of it, which is not allowed. Change application logic to enforce strict transaction nesting.  
The statement has been terminated.  
```  
  
 這項例外狀況也在預期中，而 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式周圍必須有執行引發觸發程序之動作的 try/catch 區塊，才能繼續執行。 儘管會擲回兩項例外狀況，交易仍會回復，而且不會將變更認可到資料表中。 CLR 觸發程序和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 觸發程序之間的主要差異在於 [!INCLUDE[tsql](../../includes/tsql-md.md)] 觸發程序在交易回復之後，仍可繼續執行其他作業。  
  
### <a name="example"></a>範例  
 下列觸發程序會在資料表上執行 INSERT 陳述式的簡單驗證。 如果插入的整數值等於 1，則交易會回復，而且值不會插入至資料表。 所有其他的整數值都會插入至資料表。 請注意 `Transaction.Rollback` 方法周圍的 try/catch 區塊。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼會建立測試資料表、組件和 Managed 預存程序。 請注意，這兩個 INSERT 陳述式會包裝在 try/catch 區塊中，如此才能捕捉觸發程序完成執行時所擲回的例外狀況。  
  
 C#  
  
```  
using System;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;  
using System.Transactions;  
  
public partial class Triggers  
{  
    // Enter existing table or view for the target and uncomment the attribute line  
    // [Microsoft.SqlServer.Server.SqlTrigger (Name="trig_InsertValidator", Target="Table1", Event="FOR INSERT")]  
    public static void trig_InsertValidator()  
    {  
        using (SqlConnection connection = new SqlConnection(@"context connection=true"))  
        {  
            SqlCommand command;  
            SqlDataReader reader;  
            int value;  
  
            // Open the connection.  
            connection.Open();  
  
            // Get the inserted value.  
            command = new SqlCommand(@"SELECT * FROM INSERTED", connection);  
            reader = command.ExecuteReader();  
            reader.Read();  
            value = (int)reader[0];  
            reader.Close();  
  
            // Rollback the transaction if a value of 1 was inserted.  
            if (1 == value)  
            {  
                try  
                {  
                    // Get the current transaction and roll it back.  
                    Transaction trans = Transaction.Current;  
                    trans.Rollback();                      
                }  
                catch (SqlException ex)  
                {  
                    // Catch the expected exception.                      
                }  
            }  
            else  
            {  
                // Perform other actions here.  
            }  
  
            // Close the connection.  
            connection.Close();              
        }  
    }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Transactions  
  
Partial Public Class Triggers  
' Enter existing table or view for the target and uncomment the attribute line  
' <Microsoft.SqlServer.Server.SqlTrigger(Name:="trig_InsertValidator", Target:="Table1", Event:="FOR INSERT")> _  
Public Shared Sub  trig_InsertValidator ()  
    Using connection As New SqlConnection("context connection=true")  
  
        Dim command As SqlCommand  
        Dim reader As SqlDataReader  
        Dim value As Integer  
  
        ' Open the connection.  
        connection.Open()  
  
        ' Get the inserted value.  
        command = New SqlCommand("SELECT * FROM INSERTED", connection)  
        reader = command.ExecuteReader()  
        reader.Read()  
        value = CType(reader(0), Integer)  
        reader.Close()  
  
        ' Rollback the transaction if a value of 1 was inserted.  
        If value = 1 Then  
  
            Try  
                ' Get the current transaction and roll it back.  
                Dim trans As Transaction  
                trans = Transaction.Current  
                trans.Rollback()  
  
            Catch ex As SqlException  
  
                ' Catch the exception.                      
            End Try  
        Else  
  
            ' Perform other actions here.  
        End If  
  
        ' Close the connection.  
        connection.Close()  
    End Using  
End Sub  
End Class  
```  
  
 Transact-SQL  
  
```  
-- Create the test table, assembly, and trigger.  
CREATE TABLE Table1(c1 int);  
go  
  
CREATE ASSEMBLY ValidationTriggers from 'E:\programming\ ValidationTriggers.dll';  
go  
  
CREATE TRIGGER trig_InsertValidator  
ON Table1  
FOR INSERT  
AS EXTERNAL NAME ValidationTriggers.Triggers.trig_InsertValidator;  
go  
  
-- Use a Try/Catch block to catch the expected exception  
BEGIN TRY  
   INSERT INTO Table1 VALUES(42)  
   INSERT INTO Table1 VALUES(1)  
END TRY  
BEGIN CATCH  
  SELECT ERROR_NUMBER() AS ErrorNum, ERROR_MESSAGE() AS ErrorMessage  
END CATCH;  
  
-- Clean up.  
DROP TRIGGER trig_InsertValidator;  
DROP ASSEMBLY ValidationTriggers;  
DROP TABLE Table1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [DML 觸發程式](../../relational-databases/triggers/dml-triggers.md)   
 [DDL 觸發程式](../../relational-databases/triggers/ddl-triggers.md)   
 [嘗試 .。。CATCH &#40;Transact-sql&#41;](/sql/t-sql/language-elements/try-catch-transact-sql)   
 [使用 Common Language Runtime 建立資料庫物件 &#40;CLR&#41; 整合](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
