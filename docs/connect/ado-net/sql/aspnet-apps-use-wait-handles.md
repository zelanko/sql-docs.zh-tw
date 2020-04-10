---
title: 使用 Wait 控制代碼的 ASP.NET 應用程式
description: 提供範例來示範如何從 ASP.NET 網頁執行多個並行命令，並使用 Wait 控制代碼來管理完成所有命令的作業。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: f588597a-49de-4206-8463-4ef377e112ff
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: b96d0b862e034123d61bbce038ea81ce2b1a61bd
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928944"
---
# <a name="aspnet-applications-using-wait-handles"></a>使用 Wait 控制代碼的 ASP.NET 應用程式

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

當您的應用程式一次只處理一個非同步作業時，用於處理非同步作業的回呼和輪詢模型就很實用。 等候模型提供更有彈性的方式來處理多個非同步作業。 等候模型有兩種，這兩者都是針對用於實作它們的 <xref:System.Threading.WaitHandle> 方法而命名：等候 (任何) 模型和等候 (全部) 模型。  
  
若要使用任一種等候模型，您必須使用 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>、<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> 或 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> 方法所傳回之 <xref:System.IAsyncResult> 物件的 <xref:System.IAsyncResult.AsyncWaitHandle%2A> 屬性。 <xref:System.Threading.WaitHandle.WaitAny%2A> 和 <xref:System.Threading.WaitHandle.WaitAll%2A> 方法都會要求您傳送 <xref:System.Threading.WaitHandle> 物件作為引數，並於陣列中群組在一起。  
  
這兩種等候方法都會監視非同步作業，等待完成。 <xref:System.Threading.WaitHandle.WaitAny%2A> 方法會等候任意一項作業完成或逾時。一旦您知道某項特定作業已完成，就可處理其結果，然後繼續等候下一項作業完成或逾時。<xref:System.Threading.WaitHandle.WaitAll%2A> 方法會等候 <xref:System.Threading.WaitHandle> 執行個體陣列中的所有處理序完成或逾時後才繼續。  
  
當您需要在不同伺服器上執行某個長度的多個作業時，或者，當您伺服器的功能強大到足以同時處理所有查詢時，等候模型的優點最為顯著。 在這裡顯示的範例中，三個查詢會藉由將不同長度的 WAITFOR 命令新增到無關緊要的 SELECT 查詢來模擬較長的處理序。  
  
## <a name="example-wait-any-model"></a>範例：等候 (任何) 模型  
下列範例說明等候 (任何) 模型。 一旦啟動三個非同步處理序之後，即會呼叫 <xref:System.Threading.WaitHandle.WaitAny%2A> 方法，以等候其中任一個處理序完成。 當每個處理序完成時，即會呼叫 <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> 方法，並讀取產生的 <xref:Microsoft.Data.SqlClient.SqlDataReader> 物件。 此時，真實世界的應用程式可能會使用 <xref:Microsoft.Data.SqlClient.SqlDataReader> 來填入頁面的一部分。 在這個簡單範例中，會將處理序完成的時間新增至對應到該處理序的文字方塊。 總括來說，文字方塊中的時間可說明：每次處理序完成時，就會執行程式碼。  
  
若要設定此範例，請建立新的 ASP.NET 網站專案。 在頁面上放置一個 <xref:System.Web.UI.WebControls.Button> 控制項和四個 <xref:System.Web.UI.WebControls.TextBox> 控制項 (接受每個控制項的預設名稱)。  
  
將下列程式碼新增至表單的類別，並視您的環境需要修改連接字串。  
  
```csharp  
// Add the following using statements, if they are not already there.  
using System;  
using System.Data;  
using System.Configuration;  
using System.Web;  
using System.Web.Security;  
using System.Web.UI;  
using System.Web.UI.WebControls;  
using System.Web.UI.WebControls.WebParts;  
using System.Web.UI.HtmlControls;  
using System.Threading;  
using Microsoft.Data.SqlClient;  
  
// Add this code to the page's class  
string GetConnectionString()  
     //  To avoid storing the connection string in your code,              
     //  you can retrieve it from a configuration file.   
     //  If you have not included "Asynchronous Processing=true"   
     //  in the connection string, the command will not be able  
     //  to execute asynchronously.  
{  
     return "Data Source=(local);Integrated Security=SSPI;" +  
          "Initial Catalog=AdventureWorks;" +  
          "Asynchronous Processing=true";  
}  
void Button1_Click(object sender, System.EventArgs e)  
{  
     //  In a real-world application, you might be connecting to   
     //   three different servers or databases. For the example,  
     //   we connect to only one.  
  
     SqlConnection connection1 =   
          new SqlConnection(GetConnectionString());  
     SqlConnection connection2 =   
          new SqlConnection(GetConnectionString());  
     SqlConnection connection3 =   
          new SqlConnection(GetConnectionString());  
     //  To keep the example simple, all three asynchronous   
     //  processes select a row from the same table. WAITFOR  
     //  commands are used to emulate long-running processes  
     //  that complete after different periods of time.  
  
     string commandText1 = "WAITFOR DELAY '0:0:01';" +   
          "SELECT * FROM Production.Product " +   
          "WHERE ProductNumber = 'BL-2036'";  
     string commandText2 = "WAITFOR DELAY '0:0:05';" +   
          "SELECT * FROM Production.Product " +   
          "WHERE ProductNumber = 'BL-2036'";  
     string commandText3 = "WAITFOR DELAY '0:0:10';" +   
          "SELECT * FROM Production.Product " +   
          "WHERE ProductNumber = 'BL-2036'";  
     try  
          //  For each process, open a connection and begin   
          //  execution. Use the IAsyncResult object returned by   
          //  BeginExecuteReader to add a WaitHandle for the   
          //  process to the array.  
     {  
          connection1.Open();  
          SqlCommand command1 =  
               new SqlCommand(commandText1, connection1);  
          IAsyncResult result1 = command1.BeginExecuteReader();  
          WaitHandle waitHandle1 = result1.AsyncWaitHandle;  
  
          connection2.Open();  
          SqlCommand command2 =  
               new SqlCommand(commandText2, connection2);  
          IAsyncResult result2 = command2.BeginExecuteReader();  
          WaitHandle waitHandle2 = result2.AsyncWaitHandle;  
  
          connection3.Open();  
          SqlCommand command3 =  
               new SqlCommand(commandText3, connection3);  
          IAsyncResult result3 = command3.BeginExecuteReader();  
          WaitHandle waitHandle3 = result3.AsyncWaitHandle;  
  
          WaitHandle[] waitHandles = {  
               waitHandle1, waitHandle2, waitHandle3  
          };  
  
          int index;  
          for (int countWaits = 0; countWaits <= 2; countWaits++)  
          {  
               //  WaitAny waits for any of the processes to   
               //  complete. The return value is either the index   
               //  of the array element whose process just   
               //  completed, or the WaitTimeout value.  
  
               index = WaitHandle.WaitAny(waitHandles,   
                    60000, false);  
               //  This example doesn't actually do anything with   
               //  the data returned by the processes, but the   
               //  code opens readers for each just to demonstrate       
               //  the concept.  
               //  Instead of using the returned data to fill the   
               //  controls on the page, the example adds the time  
               //  the process was completed to the corresponding  
               //  text box.  
  
               switch (index)  
               {  
                    case 0:  
                         SqlDataReader reader1;  
                         reader1 =   
                              command1.EndExecuteReader(result1);  
                         if (reader1.Read())  
                         {  
                           TextBox1.Text =   
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader1.Close();  
                         break;  
                    case 1:  
                         SqlDataReader reader2;  
                         reader2 =   
                              command2.EndExecuteReader(result2);  
                         if (reader2.Read())  
                         {  
                           TextBox2.Text =   
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader2.Close();  
                         break;  
                    case 2:  
                         SqlDataReader reader3;  
                         reader3 =   
                              command3.EndExecuteReader(result3);  
                         if (reader3.Read())  
                         {  
                           TextBox3.Text =   
                           "Completed " +  
                           System.DateTime.Now.ToLongTimeString();  
                         }  
                         reader3.Close();  
                         break;  
                    case WaitHandle.WaitTimeout:  
                         throw new Exception("Timeout");  
                         break;  
               }  
          }  
     }  
     catch (Exception ex)  
     {  
          TextBox4.Text = ex.ToString();  
     }  
     connection1.Close();  
     connection2.Close();  
     connection3.Close();  
}  
```  
  
## <a name="example-wait-all-model"></a>範例：等候 (全部) 模型  
下列範例說明等候 (全部) 模型。 一旦啟動三個非同步處理序之後，即會呼叫 <xref:System.Threading.WaitHandle.WaitAll%2A> 方法，以等候處理序完成或逾時。  
  
如同等候 (任何) 模型的範例，會將處理序完成的時間新增至對應到該處理序的文字方塊。 同樣地，文字方塊中的時間可說明：只有當所有處理序都完成之後，才會執行 <xref:System.Threading.WaitHandle.WaitAny%2A> 方法後的程式碼。  
  
若要設定此範例，請建立新的 ASP.NET 網站專案。 在頁面上放置一個 <xref:System.Web.UI.WebControls.Button> 控制項和四個 <xref:System.Web.UI.WebControls.TextBox> 控制項 (接受每個控制項的預設名稱)。  
  
將下列程式碼新增至表單的類別，並視您的環境需要修改連接字串。  
  
```csharp  
// Add the following using statements, if they are not already there.  
using System;  
using System.Data;  
using System.Configuration;  
using System.Web;  
using System.Web.Security;  
using System.Web.UI;  
using System.Web.UI.WebControls;  
using System.Web.UI.WebControls.WebParts;  
using System.Web.UI.HtmlControls;  
using System.Threading;  
using Microsoft.Data.SqlClient;  
  
// Add this code to the page's class  
string GetConnectionString()  
    //  To avoid storing the connection string in your code,              
    //  you can retrieve it from a configuration file.   
    //  If you have not included "Asynchronous Processing=true"   
    //  in the connection string, the command will not be able  
    //  to execute asynchronously.  
{  
    return "Data Source=(local);Integrated Security=SSPI;" +  
        "Initial Catalog=AdventureWorks;" +  
        "Asynchronous Processing=true";  
}  
void Button1_Click(object sender, System.EventArgs e)  
{  
    //  In a real-world application, you might be connecting to   
    //   three different servers or databases. For the example,  
    //   we connect to only one.  
  
    SqlConnection connection1 =   
        new SqlConnection(GetConnectionString());  
    SqlConnection connection2 =   
        new SqlConnection(GetConnectionString());  
    SqlConnection connection3 =   
        new SqlConnection(GetConnectionString());  
    //  To keep the example simple, all three asynchronous   
    //  processes execute UPDATE queries that result in  
      //  no change to the data. WAITFOR  
    //  commands are used to emulate long-running processes  
    //  that complete after different periods of time.  
  
    string commandText1 =   
        "UPDATE Production.Product " +  
        "SET ReorderPoint = ReorderPoint + 1 " +  
        "WHERE ReorderPoint Is Not Null;" +  
        "WAITFOR DELAY '0:0:01';" +  
        "UPDATE Production.Product " +  
        "SET ReorderPoint = ReorderPoint - 1 " +  
        "WHERE ReorderPoint Is Not Null";  
  
    string commandText2 =   
      "UPDATE Production.Product " +  
      "SET ReorderPoint = ReorderPoint + 1 " +  
      "WHERE ReorderPoint Is Not Null;" +  
      "WAITFOR DELAY '0:0:05';" +  
      "UPDATE Production.Product " +  
      "SET ReorderPoint = ReorderPoint - 1 " +  
      "WHERE ReorderPoint Is Not Null";  
  
    string commandText3 =  
       "UPDATE Production.Product " +  
       "SET ReorderPoint = ReorderPoint + 1 " +  
       "WHERE ReorderPoint Is Not Null;" +  
       "WAITFOR DELAY '0:0:10';" +  
       "UPDATE Production.Product " +  
       "SET ReorderPoint = ReorderPoint - 1 " +  
       "WHERE ReorderPoint Is Not Null";  
    try  
        //  For each process, open a connection and begin   
        //  execution. Use the IAsyncResult object returned by   
        //  BeginExecuteReader to add a WaitHandle for the   
        //  process to the array.  
    {  
        connection1.Open();  
        SqlCommand command1 =  
            new SqlCommand(commandText1, connection1);  
        IAsyncResult result1 = command1.BeginExecuteNonQuery();  
        WaitHandle waitHandle1 = result1.AsyncWaitHandle;  
        connection2.Open();  
  
        SqlCommand command2 =  
            new SqlCommand(commandText2, connection2);  
        IAsyncResult result2 = command2.BeginExecuteNonQuery();  
        WaitHandle waitHandle2 = result2.AsyncWaitHandle;  
        connection3.Open();  
  
        SqlCommand command3 =  
            new SqlCommand(commandText3, connection3);  
        IAsyncResult result3 = command3.BeginExecuteNonQuery();  
        WaitHandle waitHandle3 = result3.AsyncWaitHandle;  
  
        WaitHandle[] waitHandles = {  
            waitHandle1, waitHandle2, waitHandle3  
        };  
  
        bool result;  
        //  WaitAll waits for all of the processes to   
        //  complete. The return value is True if the processes  
        //  all completed successfully, False if any process  
        //  timed out.  
  
        result = WaitHandle.WaitAll(waitHandles, 60000, false);  
        if(result)  
        {  
            long rowCount1 =   
                command1.EndExecuteNonQuery(result1);  
            TextBox1.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
            long rowCount2 =   
                command2.EndExecuteNonQuery(result2);  
            TextBox2.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
  
            long rowCount3 =   
                command3.EndExecuteNonQuery(result3);  
            TextBox3.Text = "Completed " +  
                System.DateTime.Now.ToLongTimeString();  
        }  
        else  
        {  
            throw new Exception("Timeout");  
        }  
    }  
  
    catch (Exception ex)  
    {  
        TextBox4.Text = ex.ToString();  
    }  
    connection1.Close();  
    connection2.Close();  
    connection3.Close();  
}  
```  
  
## <a name="next-steps"></a>後續步驟
- [非同步作業](asynchronous-operations.md)
