---
title: SQL Server 的提供者統計資料
description: 描述取得 SQL Server 執行時間統計資料的支援。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 429c9d09-92ac-46ec-829a-fbff0a9575a2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 092cf63e62bce01e2a771ce4e5f7f46e1073e91a
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452060"
---
# <a name="provider-statistics-for-sql-server"></a>SQL Server 的提供者統計資料

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

從 .NET Framework 版本2.0 和 .NET Core 1.0 版開始，適用于 SQL Server 的 Microsoft SqlClient Data Provider 支援執行時間統計資料。 您必須在建立有效的連線物件之後，將 <xref:Microsoft.Data.SqlClient.SqlConnection> 物件的 <xref:Microsoft.Data.SqlClient.SqlConnection.StatisticsEnabled%2A> 屬性設定為 `True`，以啟用統計資料。 啟用統計資料之後，您可以透過 <xref:Microsoft.Data.SqlClient.SqlConnection> 物件的 <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> 方法來抓取 <xref:System.Collections.IDictionary> 參考，以「時間快照」的形式來檢查它們。 您會將清單列舉為一組名稱/值配對字典專案。 這些名稱/值組未排序。 您隨時都可以呼叫 <xref:Microsoft.Data.SqlClient.SqlConnection> 物件的 <xref:Microsoft.Data.SqlClient.SqlConnection.ResetStatistics%2A> 方法，以重設計數器。 如果尚未啟用統計資料收集，則不會產生例外狀況。 此外，如果在未先呼叫 <xref:Microsoft.Data.SqlClient.SqlConnection.StatisticsEnabled%2A> 的情況下呼叫 <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A>，則抓取的值是每個專案的初始值。 如果您啟用統計資料、執行您的應用程式一段時間，然後停用統計資料，則抓取的值將會反映到已停用統計資料的時間點所收集的值。 所有收集的統計值都是以每個連接為基礎。  
  
## <a name="statistical-values-available"></a>可用的統計值  
Microsoft SQL Server 提供者目前有18個不同的專案可供使用。 可以透過 <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> 傳回之 <xref:System.Collections.IDictionary> 介面參考的 **Count** 屬性，存取可用的項目數目。 提供者統計資料的所有計數器均使用 Common Language Runtime <xref:System.Int64> 類型 (C# 及 Visual Basic 中的 **long**)，寬度為 64 位元。 如 **int64.MaxValue** 欄位所定義，**int64** 資料類型的最大值是 ((2^63)-1))。 當計數器的值達到此最大值時，應該不會再將它們視為正確。 這表示 **int64.MaxValue**-1((2^63)-2) 實際上是任何統計資料的最大有效值。  
  
> [!NOTE]
>  字典是用來傳回提供者統計資料，因為傳回的統計資料的數目、名稱和順序可能會在未來變更。 應用程式不應該依賴在字典中找到的特定值，而應該改為檢查值是否存在，並據以分支。  
  
下表說明目前可用的統計值。 請注意，個別值的金鑰名稱不會在 Microsoft .NET Framework 和 .NET Core 的區域版本中當地語系化。  
  
|金鑰名稱|Description|  
|--------------|-----------------|  
|`BuffersReceived`|傳回提供者在應用程式開始使用提供者並啟用統計資料後，從 SQL Server 接收的表格式資料流程（TDS）封包數目。|  
|`BuffersSent`|傳回提供者在啟用統計資料之後，傳送給 SQL Server 的 TDS 封包數目。 大型命令可能需要多個緩衝區。 例如，如果將大型命令傳送至伺服器，而且它需要六個封包，`ServerRoundtrips` 會遞增一個，`BuffersSent` 會遞增6。|  
|`BytesReceived`|當應用程式已開始使用提供者並啟用統計資料後，傳回提供者從 SQL Server 接收之 TDS 封包中的資料位元組數目。|  
|`BytesSent`|傳回在應用程式已開始使用提供者並啟用統計資料之後，傳送至 TDS 封包中 SQL Server 的資料位元組數目。|  
|`ConnectionTime`|在啟用統計資料後連線處於開啟的時間量 (如果統計資料是在開啟連線之前啟用的，則為總連線時間)。|  
|`CursorOpens`|當應用程式已開始使用提供者並啟用統計資料後，傳回透過連接開啟資料指標的次數。<br /><br /> 請注意，SELECT 語句所傳回的唯讀/順向結果不會視為資料指標，因此不會影響此計數器。|  
|`ExecutionTime`|傳回啟用統計資料後，提供者在處理作業所耗用的累計時間量 (以毫秒為單位)，包括等待伺服器回覆的時間，以及提供者本身執行程式碼的時間。<br /><br /> 包含計時程式碼的類別如下：<br /><br /> SqlConnection<br /><br /> SqlCommand<br /><br /> SqlDataReader<br /><br /> SqlDataAdapter<br /><br /> SqlTransaction<br /><br /> SqlCommandBuilder<br /><br /> 為了盡可能減少效能關鍵成員，下列成員不會被計時：<br /><br /> SqlDataReader<br /><br /> 這個 [] 運算子（所有多載）<br /><br /> GetBoolean<br /><br /> GetChar<br /><br /> GetDateTime<br /><br /> GetDecimal<br /><br /> GetDouble<br /><br /> GetFloat<br /><br /> GetGuid<br /><br /> GetInt16<br /><br /> GetInt32<br /><br /> GetInt64<br /><br /> GetName<br /><br /> GetOrdinal<br /><br /> GetSqlBinary<br /><br /> GetSqlBoolean<br /><br /> GetSqlByte<br /><br /> GetSqlDateTime<br /><br /> GetSqlDecimal<br /><br /> GetSqlDouble<br /><br /> GetSqlGuid<br /><br /> GetSqlInt16<br /><br /> GetSqlInt32<br /><br /> GetSqlInt64<br /><br /> GetSqlMoney<br /><br /> GetSqlSingle<br /><br /> GetSqlString<br /><br /> GetString<br /><br /> IsDBNull|  
|`IduCount`|當應用程式已開始使用提供者並啟用統計資料後，傳回透過連接執行的 INSERT、DELETE 和 UPDATE 語句總數。|  
|`IduRows`|當應用程式已開始使用提供者並啟用統計資料後，傳回透過連接執行的 INSERT、DELETE 和 UPDATE 語句所影響的總數據列數。|  
|`NetworkServerTime`|一旦應用程式已開始使用提供者並啟用統計資料後，傳回提供者等待伺服器回覆的累計時間量 (以毫秒為單位)。|  
|`PreparedExecs`|當應用程式已開始使用提供者並啟用統計資料後，傳回透過連接執行的備妥命令數目。|  
|`Prepares`|當應用程式已開始使用提供者並啟用統計資料後，傳回透過連接準備的語句數目。|  
|`SelectCount`|當應用程式已開始使用提供者並啟用統計資料後，傳回透過連接執行的 SELECT 語句數目。 這包括用來從資料指標抓取資料列的 FETCH 語句，而當到達 <xref:Microsoft.Data.SqlClient.SqlDataReader> 的結尾時，會更新 SELECT 語句的計數。|  
|`SelectRows`|當應用程式已開始使用提供者並啟用統計資料後，傳回選取的資料列數目。 此計數器會反映 SQL 語句所產生的所有資料列，甚至是呼叫端實際未使用的資料列。 例如，在讀取整個結果集之前關閉資料讀取器並不會影響計數。 這包括透過 FETCH 語句從資料指標抓取的資料列。|  
|`ServerRoundtrips`|傳回當應用程式已開始使用提供者並啟用統計資料後，連接傳送命令至伺服器並收到回復的次數。|  
|`SumResultSets`|傳回應用程式已開始使用提供者並啟用統計資料後，已使用的結果集數目。 例如，這會包含傳回給用戶端的任何結果集。 針對資料指標，每個提取或區塊提取作業都會被視為獨立的結果集。|  
|`Transactions`|傳回應用程式開始使用提供者並啟用統計資料（包括回復）之後，啟動的使用者交易數目。 如果在上使用自動認可來執行連接，則會將每個命令視為一項交易。<br /><br /> 一旦執行 BEGIN transaction 語句時，此計數器就會遞增交易計數，而不論稍後是否認可或回復交易。|  
|`UnpreparedExecs`|當應用程式已開始使用提供者並啟用統計資料後，傳回透過連接執行的未準備語句數目。|  
  
### <a name="retrieving-a-value"></a>正在抓取值  
下列主控台應用程式會示範如何在連接上啟用統計資料、抓取四個個別的統計資料值，以及將它們寫入至主控台視窗。  
  
> [!NOTE]
>  下列範例使用包含於 SQL Server 的 **AdventureWorks** 範例資料庫。 範例程式碼中提供的連接字串假設本機電腦上已安裝並可使用資料庫。 視環境需要修改連接字串。  
  
```csharp  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
namespace CS_Stats_Console_GetValue  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =   
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the   
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =   
          new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
          awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
          currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        // Retrieve a few individual values  
        // related to the previous command.  
        long bytesReceived =  
            (long) currentStatistics["BytesReceived"];  
        long bytesSent =  
            (long) currentStatistics["BytesSent"];  
        long selectCount =  
            (long) currentStatistics["SelectCount"];  
        long selectRows =  
            (long) currentStatistics["SelectRows"];  
  
        Console.WriteLine("BytesReceived: " +  
            bytesReceived.ToString());  
        Console.WriteLine("BytesSent: " +  
            bytesSent.ToString());  
        Console.WriteLine("SelectCount: " +  
            selectCount.ToString());  
        Console.WriteLine("SelectRows: " +  
            selectRows.ToString());  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrieve it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +   
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
### <a name="retrieving-all-values"></a>正在抓取所有值  
下列主控台應用程式會顯示如何在連接上啟用統計資料、使用列舉值抓取所有可用的統計資料值，並將它們寫入主控台視窗。  
  
> [!NOTE]
>  下列範例使用包含於 SQL Server 的 **AdventureWorks** 範例資料庫。 範例程式碼中提供的連接字串假設本機電腦上已安裝並可使用資料庫。 視環境需要修改連接字串。  
  
```csharp  
using System;  
using System.Collections;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
namespace CS_Stats_Console_GetAll  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string connectionString = GetConnectionString();  
  
      using (SqlConnection awConnection =   
        new SqlConnection(connectionString))  
      {  
        // StatisticsEnabled is False by default.  
        // It must be set to True to start the   
        // statistic collection process.  
        awConnection.StatisticsEnabled = true;  
  
        string productSQL = "SELECT * FROM Production.Product";  
        SqlDataAdapter productAdapter =  
            new SqlDataAdapter(productSQL, awConnection);  
  
        DataSet awDataSet = new DataSet();  
  
        awConnection.Open();  
  
        productAdapter.Fill(awDataSet, "ProductTable");  
  
        // Retrieve the current statistics as  
        // a collection of values at this point  
        // and time.  
        IDictionary currentStatistics =  
            awConnection.RetrieveStatistics();  
  
        Console.WriteLine("Total Counters: " +  
            currentStatistics.Count.ToString());  
        Console.WriteLine();  
  
        Console.WriteLine("Key Name and Value");  
  
        // Note the entries are unsorted.  
        foreach (DictionaryEntry entry in currentStatistics)  
        {  
          Console.WriteLine(entry.Key.ToString() +  
              ": " + entry.Value.ToString());  
        }  
  
        Console.WriteLine();  
        Console.WriteLine("Press any key to continue");  
        Console.ReadLine();  
      }  
  
    }  
    private static string GetConnectionString()  
    {  
      // To avoid storing the connection string in your code,  
      // you can retrieve it from a configuration file.  
      return "Data Source=localhost;Integrated Security=SSPI;" +   
        "Initial Catalog=AdventureWorks";  
    }  
  }  
}  
```  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server and ADO.NET](index.md) (SQL Server 和 ADO.NET)
