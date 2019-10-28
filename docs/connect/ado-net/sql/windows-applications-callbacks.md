---
title: 使用回撥的 Windows 應用程式
description: 提供範例，示範如何安全地執行非同步命令，並正確地處理與表單的互動，以及從不同的執行緒中的內容。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: ae2ea457-0764-4b06-8977-713c77e85bd2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 5c2d46e3f2b26a8106e75f2bb116907e2f27a7b9
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451908"
---
# <a name="windows-applications-using-callbacks"></a>使用回撥的 Windows 應用程式

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

在大部分的非同步處理案例中，您想要啟動資料庫作業，並繼續執行其他進程，而不等候資料庫作業完成。 不過，許多案例都需要在資料庫作業結束後執行某些動作。 例如，在 Windows 應用程式中，您可能會想要將長時間執行的作業委派給背景執行緒，同時允許使用者介面執行緒保持回應。 不過，當資料庫作業完成時，您會想要使用結果來填入表單。 這種類型的案例最適合使用回呼來執行。  
  
您可以藉由在 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>、<xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> 或 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A> 方法中指定 <xref:System.AsyncCallback> 委派來定義回呼。 當作業完成時，會呼叫委派。 您可以將 <xref:Microsoft.Data.SqlClient.SqlCommand> 本身的參考傳遞給委派，讓您輕鬆存取 <xref:Microsoft.Data.SqlClient.SqlCommand> 物件，並呼叫適當的 `End` 方法，而不需要使用全域變數。  
  
## <a name="example"></a>範例  
下列 Windows 應用程式示範如何使用 <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A> 方法，執行包含幾秒延遲的 Transact-sql 語句（模擬長時間執行的命令）。  
  
這個範例會示範一些重要的技巧，包括呼叫與表單不同執行緒互動的方法。 此外，這個範例還會示範如何封鎖使用者多次執行命令，以及如何確保在呼叫回呼程式之前，表單不會關閉。  
  
若要設定此範例，請建立新的 Windows 應用程式。 將 <xref:System.Windows.Forms.Button> 控制項和兩個 <xref:System.Windows.Forms.Label> 控制項放在表單上（接受每個控制項的預設名稱）。 將下列程式碼新增至表單的類別，並視您的環境需要修改連接字串。  
  
```csharp  
// Add these to the top of the class, if they're not already there:  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
// Hook up the form's Load event handler (you can double-click on   
// the form's design surface in Visual Studio), and then add   
// this code to the form's class:  
  
// You'll need this delegate in order to display text from a thread  
// other than the form's thread. See the HandleCallback  
// procedure for more information.  
// This same delegate matches both the DisplayStatus   
// and DisplayResults methods.  
private delegate void DisplayInfoDelegate(string Text);  
  
// This flag ensures that the user doesn't attempt  
// to restart the command or close the form while the   
// asynchronous command is executing.  
private bool isExecuting;  
  
// This example maintains the connection object   
// externally, so that it's available for closing.  
private SqlConnection connection;  
  
private static string GetConnectionString()  
{  
    // To avoid storing the connection string in your code,              
    // you can retrieve it from a configuration file.   
  
    // If you have not included "Asynchronous Processing=true" in the  
    // connection string, the command will not be able  
    // to execute asynchronously.  
    return "Data Source=(local);Integrated Security=SSPI;" +  
    "Initial Catalog=AdventureWorks; Asynchronous Processing=true";  
}  
  
private void DisplayStatus(string Text)  
{  
    this.label1.Text = Text;  
}  
  
private void DisplayResults(string Text)  
{  
    this.label1.Text = Text;  
    DisplayStatus("Ready");  
}  
  
private void Form1_FormClosing(object sender, System.Windows.Forms.FormClosingEventArgs e)  
{  
    if (isExecuting)  
    {  
        MessageBox.Show(this, "Can't close the form until " +  
        "the pending asynchronous command has completed. Please " +  
        "wait...");
        e.Cancel = true;  
    }  
}  
  
private void button1_Click(object sender, System.EventArgs e)  
{  
    if (isExecuting)  
    {  
        MessageBox.Show(this, "Already executing. Please wait until " +  
        "the current query has completed.");  
    }  
    else  
    {  
        SqlCommand command = null;  
        try  
        {  
            DisplayResults("");  
            DisplayStatus("Connecting...");  
            connection = new SqlConnection(GetConnectionString());  
            // To emulate a long-running query, wait for   
            // a few seconds before working with the data.  
            // This command doesn't do much, but that's the point--  
            // it doesn't change your data, in the long run.  
            string commandText =  
                "WAITFOR DELAY '0:0:05';" +  
                "UPDATE Production.Product " +  
                "SET ReorderPoint = ReorderPoint + 1 " +  
                "WHERE ReorderPoint Is Not Null;" +  
                "UPDATE Production.Product " +  
                "SET ReorderPoint = ReorderPoint - 1 " +  
                "WHERE ReorderPoint Is Not Null";  
  
            command = new SqlCommand(commandText, connection);  
            connection.Open();  
  
            DisplayStatus("Executing...");  
            isExecuting = true;  
            // Although it's not required that you pass the   
            // SqlCommand object as the second parameter in the   
            // BeginExecuteNonQuery call, doing so makes it easier  
            // to call EndExecuteNonQuery in the callback procedure.  
            AsyncCallback callback = new AsyncCallback(HandleCallback);  
  
            // Once the BeginExecuteNonQuery method is called,  
            // the code continues--and the user can interact with  
            // the form--while the server executes the query.  
            command.BeginExecuteNonQuery(callback, command);  
  
        }  
        catch (Exception ex)  
        {  
            isExecuting = false;  
            DisplayStatus($"Ready (last error: {ex.Message})");
            if (connection != null)  
            {  
                connection.Close();  
            }  
        }  
    }  
}  
  
private void HandleCallback(IAsyncResult result)  
{  
    try  
    {  
        // Retrieve the original command object, passed  
        // to this procedure in the AsyncState property  
        // of the IAsyncResult parameter.  
        SqlCommand command = (SqlCommand)result.AsyncState;  
        int rowCount = command.EndExecuteNonQuery(result);  
        string rowText = " rows affected.";  
        if (rowCount == 1)  
        {  
            rowText = " row affected.";  
        }  
        rowText = rowCount + rowText;  
  
        // You may not interact with the form and its contents  
        // from a different thread, and this callback procedure  
        // is all but guaranteed to be running from a different thread  
        // than the form. Therefore you cannot simply call code that   
        // displays the results, like this:  
        // DisplayResults(rowText)  
  
        // Instead, you must call the procedure from the form's thread.  
        // One simple way to accomplish this is to call the Invoke  
        // method of the form, which calls the delegate you supply  
        // from the form's thread.   
        DisplayInfoDelegate del =   
         new DisplayInfoDelegate(DisplayResults);  
        this.Invoke(del, rowText);  
    }  
    catch (Exception ex)  
    {  
        // Because you're now running code in a separate thread,   
        // if you don't handle the exception here, none of your other  
        // code will catch the exception. Because none of your  
        // code is on the call stack in this thread, there's nothing  
        // higher up the stack to catch the exception if you don't   
        // handle it here. You can either log the exception or   
        // invoke a delegate (as in the non-error case in this   
        // example) to display the error on the form. In no case  
        // can you simply display the error without executing a   
        // delegate as in the try block here.   
  
        // You can create the delegate instance as you   
        // invoke it, like this:  
        this.Invoke(new DisplayInfoDelegate(DisplayStatus),  
            $"Ready (last error: {ex.Message}");
    }  
    finally  
    {  
        isExecuting = false;  
        if (connection != null)  
        {  
            connection.Close();  
        }  
    }  
}  
  
private void Form1_Load(object sender, System.EventArgs e)  
{  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    this.FormClosing += new System.Windows.Forms.  
        FormClosingEventHandler(this.Form1_FormClosing);  
}  
```  
  
## <a name="next-steps"></a>後續步驟
- [非同步作業](asynchronous-operations.md)
