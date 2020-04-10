---
title: 步驟 4：使用 ADO.NET 復原連線到 SQL | Microsoft Docs
description: 描述如何復原連線到 SQL
ms.custom: ''
ms.date: 08/15/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9b608b0b-6b38-42da-bb83-79df8c170cd7
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 23b87d6774fb4020b5c7eca3d3f776bbb95fc7fe
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80918038"
---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>步驟 4：使用 ADO.NET 彈性地連線到 SQL

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

- 上一篇文章：&nbsp;&nbsp;&nbsp;[步驟 3：使用 ADO.NET 連線到 SQL 的概念證明](step-3-connect-sql-ado-net.md)  

  
本主題提供的 C# 程式碼範例示範自訂的重試邏輯。 重試邏輯會提供可靠性。 重試邏輯的設計目的在於妥善處理暫時錯誤或「暫時性錯誤」  ，此類錯誤通常會在程式等候數秒並重試之後消失。  
  
暫時性錯誤的來源包括：  
  
- 支援網際網路的網路短暫失敗。  
- 傳送您的查詢時，雲端系統可能正在對其資源進行負載平衡。  
  
  
用於連接到本機 Microsoft SQL Server 的 ADO.NET 類別也可以連接到 Azure SQL Database。 不過，ADO.NET 類別本身無法提供在生產環境使用所需的所有穩定性和可靠性。 用戶端程式可能會遇到暫時性錯誤，用戶端程式應該會從失敗中無訊息且正常自行復原並繼續。  
  
## <a name="step-1-identify-transient-errors"></a>步驟 1:識別暫時性錯誤  
  
您的程式必須區分暫時性錯誤與持續性錯誤。 暫時性錯誤是可能在短時間內清除的錯誤狀況，例如暫時性網路問題。  假設您的程式拼錯了目標資料庫名稱，就是一個持續性錯誤的範例：在此情況下，「找不到這類資料庫」錯誤就會持續存在，而且沒有機會在短時間內清除。  
  
您可以在 [SQL Database 用戶端應用程式的錯誤訊息](https://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/) \(部分機器翻譯\) 上取得已分類為暫時性錯誤的錯誤號碼清單。  
  
## <a name="step-2-create-and-run-sample-application"></a>步驟 2:建立並執行範例應用程式  
  
此範例假設已安裝 .NET Framework 4.5.1 或更新版本。  C# 程式碼範例包含一個名為 Program.cs 的檔案。 下一節會提供它的程式碼。  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>步驟 2.a：擷取並編譯程式碼範例  
  
您可以使用下列步驟編譯此範例：  
  
1. 在 [免費的 Visual Studio Community 版本](https://www.visualstudio.com/products/visual-studio-community-vs)中，透過 C# 主控台應用程式範本建立新的專案。  
    - [檔案] > [新增] > [專案] > [已安裝] > [範本] > [Visual C#] > [Windows] > [傳統桌面] > [主控台應用程式]  
    - 將專案命名為 **RetryAdo2**。  
2. 開啟 [方案總管] 窗格。  
    - 查看專案的名稱。  
    - 查看 Program.cs 檔案的名稱。  
3. 開啟 Program.cs 檔案。  
4. 使用下列程式碼區塊中的程式碼，取代 Program.cs 檔案的所有內容。  
5. 按一下 [建置] 功能表 > [建置解決方案]。  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>步驟 2.b：複製並貼上範例程式碼  
  
將此程式碼到貼到您的 **Program.cs** 檔案中。  
  
接著，您必須編輯伺服器名稱、密碼等項目的字串。 您可以在名為 **GetSqlConnectionStringBuilder**的方法中找到這些字串。  
  
注意：伺服器名稱的連接字串適用於 Azure SQL Database，因其包含 **tcp:** 這四個字元前置詞。 但是，您可以調整伺服器字串，以連線到您的 Microsoft SQL Server。  
  
  
```csharp
using System;  // C#  
using CG = System.Collections.Generic;  
using QC = Microsoft.Data.SqlClient;  
using TD = System.Threading;  
    
namespace RetryAdo2  
{  
  public class Program  
  {  
    static public int Main(string[] args)  
    {  
      bool succeeded = false;  
      int totalNumberOfTimesToTry = 4;  
      int retryIntervalSeconds = 10;  
    
      for (int tries = 1;  
        tries <= totalNumberOfTimesToTry;  
        tries++)  
      {  
        try  
        {  
          if (tries > 1)  
          {  
            Console.WriteLine  
              ("Transient error encountered. Will begin attempt number {0} of {1} max...",  
              tries, totalNumberOfTimesToTry  
              );  
            TD.Thread.Sleep(1000 * retryIntervalSeconds);  
            retryIntervalSeconds = Convert.ToInt32  
              (retryIntervalSeconds * 1.5);  
          }  
          AccessDatabase();  
          succeeded = true;  
          break;  
        }  
    
        catch (QC.SqlException sqlExc)  
        {  
          if (TransientErrorNumbers.Contains  
            (sqlExc.Number) == true)  
          {  
            Console.WriteLine("{0}: transient occurred.", sqlExc.Number);  
            continue;  
          }  
          else  
          {  
            Console.WriteLine(sqlExc);  
            succeeded = false;  
            break;  
          }  
        }  
    
        catch (TestSqlException sqlExc)  
        {  
          if (TransientErrorNumbers.Contains  
            (sqlExc.Number) == true)  
          {  
            Console.WriteLine("{0}: transient occurred. (TESTING.)", sqlExc.Number);  
            continue;  
          }  
          else  
          {  
            Console.WriteLine(sqlExc);  
            succeeded = false;  
            break;  
          }  
        }  
    
        catch (Exception Exc)  
        {  
          Console.WriteLine(Exc);  
          succeeded = false;  
          break;  
        }  
      }  
    
      if (succeeded == true)  
      {  
        return 0;  
      }  
      else  
      {  
        Console.WriteLine("ERROR: Unable to access the database!");  
        return 1;  
      }  
    }  
    
    /// <summary>  
    /// Connects to the database, reads,  
    /// prints results to the console.  
    /// </summary>  
    static public void AccessDatabase()  
    {  
      //throw new TestSqlException(4060); //(7654321);  // Uncomment for testing.  
    
      using (var sqlConnection = new QC.SqlConnection  
          (GetSqlConnectionString()))  
      {  
        using (var dbCommand = sqlConnection.CreateCommand())  
        {  
          dbCommand.CommandText = @"  
SELECT TOP 3  
    ob.name,  
    CAST(ob.object_id as nvarchar(32)) as [object_id]  
  FROM sys.objects as ob  
  WHERE ob.type='IT'  
  ORDER BY ob.name;";  
    
          sqlConnection.Open();  
          var dataReader = dbCommand.ExecuteReader();  
    
          while (dataReader.Read())  
          {  
            Console.WriteLine("{0}\t{1}",  
              dataReader.GetString(0),  
              dataReader.GetString(1));  
          }  
        }  
      }  
    }  
    
    /// <summary>  
    /// You must edit the four 'my' string values.  
    /// </summary>  
    /// <returns>An ADO.NET connection string.</returns>  
    static private string GetSqlConnectionString()  
    {  
      // Prepare the connection string to Azure SQL Database.  
      var sqlConnectionSB = new QC.SqlConnectionStringBuilder();  
    
      // Change these values to your values.  
      sqlConnectionSB.DataSource = "tcp:myazuresqldbserver.database.windows.net,1433"; //["Server"]  
      sqlConnectionSB.InitialCatalog = "MyDatabase"; //["Database"]  
    
      sqlConnectionSB.UserID = "MyLogin";  // "@yourservername"  as suffix sometimes.  
      sqlConnectionSB.Password = "MyPassword";  
      sqlConnectionSB.IntegratedSecurity = false;  
    
      // Adjust these values if you like. (ADO.NET 4.5.1 or later.)  
      sqlConnectionSB.ConnectRetryCount = 3;  
      sqlConnectionSB.ConnectRetryInterval = 10;  // Seconds.  
    
      // Leave these values as they are.  
      sqlConnectionSB.IntegratedSecurity = false;  
      sqlConnectionSB.Encrypt = true;  
      sqlConnectionSB.ConnectTimeout = 30;  
    
      return sqlConnectionSB.ToString();  
    }  
    
    static public CG.List<int> TransientErrorNumbers =  
      new CG.List<int> { 4060, 40197, 40501, 40613,  
      49918, 49919, 49920, 11001 };  
  }  
    
  /// <summary>  
  /// For testing retry logic, you can have method  
  /// AccessDatabase start by throwing a new  
  /// TestSqlException with a Number that does  
  /// or does not match a transient error number  
  /// present in TransientErrorNumbers.  
  /// </summary>  
  internal class TestSqlException : ApplicationException  
  {  
    internal TestSqlException(int testErrorNumber)  
    { this.Number = testErrorNumber; }  
    
    internal int Number  
    { get; set; }  
  }  
}  
```  
  
###  <a name="step-2c-run-the-program"></a>步驟 2.c：執行程式  
  
  
**RetryAdo2.exe** 可執行檔不會輸入任何參數。 執行 .exe：  
  
1. 開啟主控台視窗至您編譯 RetryAdo2.exe 二進位檔的位置。  
2. 執行 RetryAdo2.exe，不含輸入參數。  
  
  
  
```  
database_firewall_rules_table   245575913  
filestream_tombstone_2073058421 2073058421  
filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>步驟 3：測試重試邏輯的方式  
  
有許多種方式可讓您模擬暫時性錯誤，以便測試您的重試邏輯。  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>步驟 3.a：擲回測試例外狀況  
  
程式碼範例包含：  
  
- 第二個名為 **TestSqlException** 的小型類別，其中含有名為 **Number** 的屬性。  
- `//throw new TestSqlException(4060);` ，您可以將它取消註解。  
  
如果您將 throw 陳述式取消註解，並重新編譯，那麼下次執行的 **RetryAdo2.exe** 輸出會類似下列內容。  
  
```  
[C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
>> RetryAdo2.exe  
4060: transient occurred. (TESTING.)  
Transient error encountered. Will begin attempt number 2 of 4 max...  
4060: transient occurred. (TESTING.)  
Transient error encountered. Will begin attempt number 3 of 4 max...  
4060: transient occurred. (TESTING.)  
Transient error encountered. Will begin attempt number 4 of 4 max...  
4060: transient occurred. (TESTING.)  
ERROR: Unable to access the database!  
  
[C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
>>  
```  
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>步驟 3.b：使用持續性錯誤重新測試  
  
若要證明程式碼正確地處理持續性錯誤，請重新執行先前的測試，但不要使用類似 4060 的真正暫時性錯誤的數字。 請改為使用無意義的數字 7654321。 此程式應該將這視為持續性錯誤，並且應該略過任何重試。  
  
###  <a name="step-3c-disconnect-from-the-network"></a>步驟 3.c：中斷網路連線  
  
1. 中斷用戶端電腦的網路連線。  
    - 若為桌上型電腦，請拔除網路線。  
    - 若為膝上型電腦，請按功能鍵組合來關閉網路介面卡。  
2. 啟動 RetryAdo2.exe，並等候主控台顯示第一個暫時性錯誤，可能是 11001。  
3. 在 RetryAdo2.exe 繼續執行時，重新連接網路。  
4. 觀看主控台報告後續的重試成功。  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>步驟 2.d：暫時拼錯伺服器名稱  
  
1. 暫時將 40615 當作另一個錯誤號碼加入 **TransientErrorNumbers**中，並重新編譯。  
2. 在 `new QC.SqlConnectionStringBuilder()`這行設定中斷點。  
3. 使用「編輯後繼續」  功能，在以下幾行中刻意拼錯伺服器名稱。  
    - 讓程式執行，並返回您的中斷點。  
    - 會發生錯誤 40615。  
4. 修正拼字錯誤。  
5. 讓程式執行並成功完成。  
6. 移除 40615，然後重新編譯。  
  
## <a name="next-steps"></a>後續步驟  
  
若要探索其他最佳做法和設計指導方針，請造訪[連線至 SQL Database：連結、最佳做法和設計指導方針](https://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/) \(部分機器翻譯\)  
