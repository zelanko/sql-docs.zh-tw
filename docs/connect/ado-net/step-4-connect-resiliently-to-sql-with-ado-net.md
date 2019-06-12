---
title: 步驟 4： 彈性連接到使用 ADO.NET 的 SQL |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: b3f7fc6d2d7ab6872bd7100fa51f05a9d9b957c8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 06/07/2019
ms.locfileid: "66770594"
---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>步驟 4︰使用 ADO.NET 彈性地連線到 SQL

- 上一篇文章：&nbsp;&nbsp;&nbsp;[步驟 3︰使用 ADO.NET 連線到 SQL 的概念證明](step-3-proof-of-concept-connecting-to-sql-using-ado-net.md)  

  
本主題提供的 C# 程式碼範例示範自訂重試邏輯。 重試邏輯提供可靠性。 重試邏輯可順暢處理暫時錯誤或*暫時性錯誤*這通常會消失，如果程式等候幾秒並重試。  
  
暫時性錯誤的來源包括：  
  
- 支援網際網路的網路功能的簡短失敗。  
- 雲端系統可能會是負載平衡傳送您查詢目前的資源。  
  
  
連接到您本機 Microsoft SQL Server 的 ADO.NET 類別也可以連接到 Azure SQL Database。 不過，本身的 ADO.NET 類別不能提供的所有穩定性和可靠性所需在生產環境使用。 用戶端程式可能會遇到暫時性錯誤從中它應該以無訊息模式和依正常程序中復原並繼續在它自己。  
  
## <a name="step-1-identify-transient-errors"></a>步驟 1︰ 識別暫時性錯誤  
  
您的程式必須區分暫時性錯誤與持續性錯誤。 暫時性錯誤是在一段時間，例如暫時性網路問題可能會清除的錯誤狀況。  持續性錯誤的範例是時間的，如果您的程式具有目標資料庫名稱的拼字錯誤-在此情況下，「 沒有這類資料庫找到 」 錯誤會保存，並清除在短時間內沒機會。  
  
分類為暫時性錯誤的錯誤號碼清單位於[SQL Database 用戶端應用程式的錯誤訊息](https://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/)  
  
## <a name="step-2-create-and-run-sample-application"></a>步驟 2： 建立和執行範例應用程式  
  
此範例假設 .NET Framework 4.5.1 或更新版本已經安裝。  C# 程式碼範例包含一個名為 Program.cs 的檔案。 下一節會提供其程式碼。  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>步驟 2.a： 擷取與編譯程式碼範例  
  
您可以編譯此範例使用下列步驟：  
  
1. 在 [免費的 Visual Studio Community edition](https://www.visualstudio.com/products/visual-studio-community-vs)，從 C# 主控台應用程式範本建立新的專案。  
    - 檔案 > 新增 > 專案 > 安裝 > 範本 > Visual C# > Windows > 傳統桌面 > 主控台應用程式  
    - 將專案命名為**RetryAdo2**。  
2. 開啟 [方案總管] 窗格。  
    - 請參閱您的專案名稱。  
    - 請參閱 Program.cs 檔案的名稱。  
3. 開啟 Program.cs 檔案。  
4. 下列程式碼區塊中的程式碼，完全取代 Program.cs 檔案的內容。  
5. 按一下 [建置] 功能表 > 建置方案。  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>步驟 2.b： 複製和貼上範例程式碼  
  
貼上此程式碼插入您**Program.cs**檔案。  
  
然後，您必須編輯伺服器名稱、 密碼和等等的字串。 您可以找到這些字串在方法中名為**GetSqlConnectionStringBuilder**。  
  
注意： 伺服器名稱的連接字串專為 Azure SQL Database，因為它包含的四個字元前置詞**tcp:** 。 但您可以調整伺服器字串以連線到 Microsoft SQL Server。  
  
  
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
  
###  <a name="step-2c-run-the-program"></a>步驟 2.c： 執行程式  
  
  
**RetryAdo2.exe**可執行檔會輸入任何參數。 若要執行.exe:  
  
1. 開啟主控台視窗，您編譯 RetryAdo2.exe 二進位檔的位置。  
2. 執行 RetryAdo2.exe，不含輸入參數。  
  
  
  
```  
    database_firewall_rules_table   245575913  
    filestream_tombstone_2073058421 2073058421  
    filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>步驟 3： 測試您的重試邏輯的方式  
  
有許多種方式可讓您模擬暫時性錯誤，以便測試您的重試邏輯。  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>步驟 3.a： 擲回測試例外狀況  
  
此程式碼範例包含：  
  
- 小型的第二個類別，名為**TestSqlException**，與屬性，名為**數目**。  
- `//throw new TestSqlException(4060);` 其中您可以取消註解。  
  
如果您取消註解 throw 陳述式，並重新編譯，在下次執行的**RetryAdo2.exe**會輸出類似下列的項目。  
  
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
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>步驟 3.b： 使用持續性錯誤重新測試  
  
若要證明程式碼處理持續性錯誤正確，請重新執行先前的測試，但不要使用類似 4060 的真正暫時性錯誤的數目。 改為使用無意義的數字 7654321。 此程式應該將這視為持續性錯誤，並應略過任何重試。  
  
###  <a name="step-3c-disconnect-from-the-network"></a>步驟 3.c： 中斷網路連線  
  
1. 中斷與網路的用戶端電腦。  
    - 為桌上型電腦，請拔除網路纜線。  
    - 為膝上型電腦，請按函式組合鍵來關閉網路介面卡。  
2. 啟動 RetryAdo2.exe，並等候主控台顯示的第一個暫時性錯誤，可能是 11001。  
3. 當手寫筆 RetryAdo2.exe 繼續執行時，重新連接到網路。  
4. 觀看主控台報告成功，後續的重試。  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>步驟 2.d： 暫時拼錯伺服器名稱  
  
1. 暫時將 40615 當作另一個錯誤號碼來**TransientErrorNumbers**，並重新編譯。  
2. 在該行設定中斷點： `new QC.SqlConnectionStringBuilder()`。  
3. 使用*編輯後繼續*功能刻意拼錯伺服器名稱，下列程式行數。  
    - 可讓程式執行，並返回您的中斷點。  
    - 發生錯誤 40615。  
4. 修正拼字錯誤。  
5. 讓程式執行並順利完成。  
6. 移除 40615，然後重新編譯。  
  
## <a name="next-steps"></a>Next Steps  
  
若要探索其他最佳 practicies 及設計指導方針，請瀏覽[連接到 SQL Database： 連結、 最佳作法和設計指導方針](https://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/)  
