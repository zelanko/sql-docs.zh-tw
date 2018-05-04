---
title: 步驟 4： 彈性地連接到 SQL 搭配 ADO.NET |Microsoft 文件
ms.custom: ''
ms.date: 08/08/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado-net
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9b608b0b-6b38-42da-bb83-79df8c170cd7
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 525ff62998cd18afbed8f6732d9d474cce47d69a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>步驟 4： 彈性地連接到使用 ADO.NET 的 SQL

- 前一篇文章：&nbsp;&nbsp;&nbsp;[步驟 3： 使用 ADO.NET 的 sql 連接的概念證明](step-3-proof-of-concept-connecting-to-sql-using-ado-net.md)  

  
本主題提供的 C# 程式碼範例示範自訂重試邏輯。 重試邏輯提供可靠性。 重試邏輯的設計為正常處理暫時錯誤或*暫時性錯誤*這通常會在程式等待數秒並重會消失。  
  
暫時性錯誤的來源包括：  
  
- 支援網際網路的網路功能的簡短失敗。  
- 雲端系統可能會是負載平衡其資源，此時您查詢傳送。  
  
  
連接到本機 Microsoft SQL Server 的 ADO.NET 類別也可以連接到 Azure SQL Database。 不過，單獨 ADO.NET 類別不能提供所有穩定性和可靠性需要在實際執行環境中。 用戶端程式可能會遇到從中應該以無訊息模式和依正常程序復原並繼續其本身的暫時性錯誤。  
  
## <a name="step-1-identify-transient-errors"></a>步驟 1： 識別暫時性錯誤  
  
您的程式必須區分暫時性錯誤與持續性錯誤。 暫時性錯誤是在一段時間，例如暫時性網路問題可能會清除錯誤狀況。  如果您的程式具有目標資料庫名稱的拼字錯誤-在此情況下，「 沒有這類資料庫找到 」 錯誤會持續存在，且不可能在短時間內清除，可能會持續性錯誤的範例。  
  
分類為暫時性錯誤的錯誤號碼清單是可從[SQL 資料庫用戶端應用程式的錯誤訊息](http://docs.microsoft.com/azure/sql-database/sql-database-develop-error-messages/)  
  
## <a name="step-2-create-and-run-sample-application"></a>步驟 2： 建立及執行範例應用程式  
  
這個範例假設 .NET Framework 4.5.1 或更新版本安裝。  C# 程式碼範例是由一個名為 Program.cs 的檔案所組成。 下一節中，會提供其程式碼。  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>步驟 2.a： 擷取和編譯程式碼範例  
  
您可以編譯此範例使用下列步驟：  
  
1. 在[免費的 Visual Studio Community edition](https://www.visualstudio.com/products/visual-studio-community-vs)，從 C# 主控台應用程式範本建立新的專案。  
    - 檔案 > 新 > 專案 > 安裝 > 範本 > Visual C# > Windows > 傳統桌面 > 主控台應用程式  
    - 將專案命名**RetryAdo2**。  
2. 開啟 [方案總管] 窗格。  
    - 請參閱您的專案名稱。  
    - 請參閱 Program.cs 檔案的名稱。  
3. 開啟 Program.cs 檔案。  
4. 完全在下列程式碼區塊的程式碼取代 Program.cs 檔案的內容。  
5. 按一下 [建置] 功能表 > 建置方案。  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>步驟 2.b： 複製和貼上的範例程式碼  
  
貼上此程式碼到您**Program.cs**檔案。  
  
然後，您必須編輯伺服器名稱、 密碼和等等的字串。 您可以找到這些字串的方法中**GetSqlConnectionStringBuilder**。  
  
注意： 伺服器名稱的連接字串專為 Azure SQL Database，因為它包含的四個字元前置詞**tcp:**。 但是，您可以調整的伺服器字串來連接到 Microsoft SQL Server。  
  
  
```CSharp  
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
  
  
**RetryAdo2.exe**可執行檔中輸入任何參數。 若要執行.exe:  
  
1. 開啟的主控台視窗，以編譯 RetryAdo2.exe 二進位檔的位置。  
2. 執行 RetryAdo2.exe，與任何輸入參數。  
  
  
  
```  
    database_firewall_rules_table   245575913  
    filestream_tombstone_2073058421 2073058421  
    filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>步驟 3： 測試重試邏輯的方式  
  
有許多種方式可讓您模擬測試重試邏輯的暫時性錯誤。  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>步驟 3.a： 將測試例外狀況  
  
此程式碼範例包含：  
  
- 小型的第二個類別，名為**TestSqlException**，屬性名為**數目**。  
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
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>步驟 3.b： 重新測試與持續性錯誤  
  
若要證明程式碼控制代碼的持續性錯誤正確地重新執行先前的測試，但請勿 4060 像真正的暫時性錯誤的數目。 改為使用任何意義數目 7654321。 程式應該將此視為持續性錯誤，且應該略過任何重試。  
  
###  <a name="step-3c-disconnect-from-the-network"></a>步驟 3.c： 中斷網路連線  
  
1. 中斷與網路的用戶端電腦。  
    - 桌面，請拔除網路纜線。  
    - 膝上型電腦，請按函式的組合索引鍵，若要關閉 網路介面卡。  
2. 啟動 RetryAdo2.exe，並等候要顯示的第一個暫時性錯誤，可能 11001 主控台。  
3. 當 RetryAdo2.exe 繼續執行到網路，重新連接。  
4. 監看後續的重試主控台執行報告成功。  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>步驟 2.d： 暫時拼錯的伺服器名稱  
  
1. 暫時將 40615 新增至另一個錯誤號碼為**TransientErrorNumbers**，並重新編譯。  
2. 行上設定中斷點： `new QC.SqlConnectionStringBuilder()`。  
3. 使用*編輯後繼續*刻意伺服器名稱拼錯，下列幾行的功能。  
    - 讓程式執行，並返回您的中斷點。  
    - 發生此錯誤 40615。  
4. 修正拼字錯誤。  
5. 讓程式執行，並已成功完成。  
6. 移除 40615，並重新編譯。  
  
## <a name="next-steps"></a>後續步驟  
  
若要瀏覽其他最佳 practicies 和設計指導方針，請造訪[連接到 SQL Database： 連結、 最佳作法和設計指導方針](http://azure.microsoft.com/documentation/articles/sql-database-connect-central-recommendations/)  
