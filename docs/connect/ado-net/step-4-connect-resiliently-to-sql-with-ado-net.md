---
title: '步驟 4: 使用 ADO.NET 將彈性地連接到 SQL |Microsoft Docs'
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9b608b0b-6b38-42da-bb83-79df8c170cd7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7a080f68497829657c60bbd96238b71123b70d87
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957590"
---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>步驟 4︰使用 ADO.NET 彈性地連線到 SQL

- 上一篇文章：&nbsp;&nbsp;&nbsp;[步驟 3︰使用 ADO.NET 連線到 SQL 的概念證明](step-3-proof-of-concept-connecting-to-sql-using-ado-net.md)  

  
本主題提供示範C#自訂重試邏輯的程式碼範例。 重試邏輯可提供可靠性。 重試邏輯的設計是為了正常處理暫時性錯誤或*暫時性*錯誤, 如果程式等待數秒後重試, 這通常會消失。  
  
暫時性錯誤的來源包括:  
  
- 支援網際網路的網路短暫失敗。  
- 雲端系統可能會在您的查詢傳送時, 對其資源進行負載平衡。  
  
  
用來連接到本機 Microsoft SQL Server 的 ADO.NET 類別也可以連接到 Azure SQL Database。 不過, ADO.NET 類別本身無法提供在生產環境中使用所需的所有穩定性和可靠性。 您的用戶端程式可能會遇到暫時性錯誤, 其應該以無訊息模式和適當的方式自行復原和繼續。  
  
## <a name="step-1-identify-transient-errors"></a>步驟 1: 識別暫時性錯誤  
  
您的程式必須區分暫時性錯誤與持續性錯誤。 暫時性錯誤是可能在短時間內清除的錯誤狀況, 例如暫時性網路問題。  持續性錯誤的範例是, 如果您的程式拼錯了目標資料庫名稱-在此情況下, 就會保存「找不到這類資料庫」錯誤, 而且不可能在短時間內清除。  
  
分類為暫時性錯誤的錯誤號碼清單可在[SQL Database 用戶端應用程式的錯誤訊息中取得](https://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/)  
  
## <a name="step-2-create-and-run-sample-application"></a>步驟 2: 建立並執行範例應用程式  
  
這個範例假設已安裝 .NET Framework 4.5.1 或更新版本。  此C#程式碼範例是由一個名為 Program.cs 的檔案所組成。 下一節會提供其程式碼。  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>步驟 2: 捕捉和編譯器代碼範例  
  
您可以使用下列步驟來編譯範例:  
  
1. 在[免費的 Visual Studio Community 版本](https://www.visualstudio.com/products/visual-studio-community-vs)中, 從 [ C#主控台應用程式] 範本建立新的專案。  
    - 檔案 > 新的 > 專案 > 安裝 > 範本 > C# Visual > Windows > 傳統桌面 > 主控台應用程式  
    - 將專案命名為**retryado2.exe**。  
2. 開啟 [方案總管] 窗格。  
    - 請參閱您專案的名稱。  
    - 請參閱 Program.cs 檔案的名稱。  
3. 開啟 Program.cs 檔案。  
4. 使用下列程式碼區塊中的程式碼, 將 Program.cs 檔案的內容完全取代。  
5. 按一下 [建立 > 組建方案] 功能表。  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>步驟 2. b: 複製並貼上範例程式碼  
  
將此程式碼貼到您的**Program.cs**檔案中。  
  
接著, 您必須編輯伺服器名稱、密碼等的字串。 您可以在名為**GetSqlConnectionStringBuilder**的方法中找到這些字串。  
  
注意: 伺服器名稱的連接字串是針對 Azure SQL Database 而提供, 因為它包含**tcp:** 的四個字元前置詞。 但是, 您可以調整伺服器字串來連接到您的 Microsoft SQL Server。  
  
  
```csharp
    using System;  // C#  
    using CG = System.Collections.Generic;  
    using QC = System.Data.SqlClient;  
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
  
###  <a name="step-2c-run-the-program"></a>步驟 2. c: 執行程式  
  
  
**Retryado2.exe**可執行檔不會輸入任何參數。 若要執行 .exe:  
  
1. 開啟您已在其中編譯 Retryado2.exe 二進位檔的主控台視窗。  
2. 執行 Retryado2.exe, 不含任何輸入參數。  
  
  
  
```  
    database_firewall_rules_table   245575913  
    filestream_tombstone_2073058421 2073058421  
    filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>步驟 3: 測試重試邏輯的方式  
  
有各種方式可以模擬暫時性錯誤, 以測試您的重試邏輯。  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>步驟 3. 答: 擲回測試例外狀況  
  
此程式碼範例包含:  
  
- 名為**TestSqlException**的小型第二個類別, 具有名為**Number**的屬性。  
- `//throw new TestSqlException(4060);`, 您可以將它取消批註。  
  
如果您取消批註 throw 語句並重新編譯, 則下一次執行**retryado2.exe**時, 會輸出類似下面的內容。  
  
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
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>步驟 3. b: 使用持續性錯誤重新測試  
  
若要證明程式碼正確地處理持續性錯誤, 請重新執行上述測試, 但不使用實際暫時性錯誤的數目, 例如4060。 請改用沒有意義的數位7654321。 程式應將此視為持續性錯誤, 而且應該略過任何重試。  
  
###  <a name="step-3c-disconnect-from-the-network"></a>步驟 3. c: 中斷與網路的連線  
  
1. 中斷用戶端電腦與網路的連線。  
    - 若為桌上型電腦, 請拔下網路線。  
    - 若為膝上型電腦, 請按下按鍵的功能組合, 以關閉網路介面卡。  
2. 啟動 Retryado2.exe, 並等候主控台顯示第一個暫時性錯誤, 可能是11001。  
3. 重新連線到網路, 而 Retryado2.exe 則會繼續執行。  
4. 在後續的重試時, 監看主控台報告成功。  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>步驟 2. d: 暫時拼錯伺服器名稱  
  
1. 暫時新增40615做為要**TransientErrorNumbers**的另一個錯誤號碼, 然後重新編譯。  
2. 在行上設定中斷點: `new QC.SqlConnectionStringBuilder()`。  
3. 使用 [*編輯後繼續*] 功能, 刻意拼錯伺服器名稱, 這是以下幾行。  
    - 讓程式執行, 然後回到您的中斷點。  
    - 發生錯誤40615。  
4. 修正拼錯的問題。  
5. 讓程式執行並順利完成。  
6. 移除 40615, 然後重新編譯。  
  
## <a name="next-steps"></a>Next Steps  
  
若要探索其他最佳 practicies 和設計指導方針, 請造訪[連接到 SQL Database: 連結、最佳作法和設計指導方針](https://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/)  
