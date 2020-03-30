---
title: SQL Server 的提供者統計資料
description: 描述對取得 SQL Server 執行階段統計資料的支援。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 429c9d09-92ac-46ec-829a-fbff0a9575a2
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 76fc14c112d47f04fc790df118eea77f1bec42cb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896600"
---
# <a name="provider-statistics-for-sql-server"></a>SQL Server 的提供者統計資料

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

從 .NET Framework 2.0 版與 .NET Core 1.0 版開始，適用於 SQL Server 的 Microsoft SqlClient Data Provider 就支援執行階段統計資料。 您必須在建立有效的連線物件之後，將 <xref:Microsoft.Data.SqlClient.SqlConnection.StatisticsEnabled%2A> 物件的 <xref:Microsoft.Data.SqlClient.SqlConnection> 屬性設定為 `True`，以啟用統計資料。 啟用統計資料之後，您可以透過 <xref:System.Collections.IDictionary> 物件的 <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> 方法來擷取 <xref:Microsoft.Data.SqlClient.SqlConnection> 參考，以「及時快照集」方式加以檢閱。 您可以將清單列舉為一組名稱/值對字典項目。 這些名稱/值對並未排序。 您隨時都可以呼叫 <xref:Microsoft.Data.SqlClient.SqlConnection.ResetStatistics%2A> 物件的 <xref:Microsoft.Data.SqlClient.SqlConnection> 方法來重設計數器。 如果尚未啟用統計資料收集功能，就不會產生例外狀況。 此外，如果在未先呼叫 <xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> 的情況下呼叫 <xref:Microsoft.Data.SqlClient.SqlConnection.StatisticsEnabled%2A>，擷取的值會是每個項目的初始值。 如果您啟用統計資料、執行應用程式一段時間，然後停用統計資料，擷取的值將會反映出直到停用統計資料那一刻為止，所收集到的值。 所有收集到的統計值都是以個別連線為基礎。  
  
## <a name="statistical-values-available"></a>可用的統計值  
Microsoft SQL Server 提供者目前提供了 18 個不同的項目。 可以透過 **傳回之** 介面參考的 <xref:System.Collections.IDictionary>Count<xref:Microsoft.Data.SqlClient.SqlConnection.RetrieveStatistics%2A> 屬性，存取可用的項目數目。 提供者統計資料的所有計數器均使用 Common Language Runtime <xref:System.Int64> 類型 (C# 及 Visual Basic 中的 **long**)，寬度為 64 位元。 如 **int64.MaxValue** 欄位所定義，**int64** 資料類型的最大值是 ((2^63)-1))。 當計數器的值達到此最大值時，應該就不會再被視為準確的值。 這表示 **int64.MaxValue**-1((2^63)-2) 實際上是任何統計資料的最大有效值。  
  
> [!NOTE]
>  字典是用來傳回提供者統計資料，因為未來所傳回統計資料的數目、名稱與順序可能會變更。 應用程式不應該依賴在字典中找到的特定值，而應該改為檢查值是否存在，並據以進行分支處理。  
  
下表說明目前可用的統計值。 請注意，個別值的機碼名稱不會在 Microsoft .NET Framework 與 .NET Core 的跨區域版本中當地語系化。  
  
|金鑰名稱|描述|  
|--------------|-----------------|  
|`BuffersReceived`|傳回應用程式開始使用提供者並啟用統計資料之後，提供者從 SQL Server 接收到的表格式資料流 (TDS) 封包數目。|  
|`BuffersSent`|傳回啟用統計資料之後，提供者傳送給 SQL Server 的 TDS 封包數目。 大型命令可能會需要多個緩衝區。 例如，如果將大型命令傳送至伺服器，而且該命令需要 6 個封包，`ServerRoundtrips` 就會遞增 1，`BuffersSent` 會遞增 6。|  
|`BytesReceived`|傳回應用程式開始使用提供者並啟用統計資料之後，提供者從 SQL Server 接收到的 TDS 封包中所包含資料的位元組數目。|  
|`BytesSent`|傳回應用程式開始使用提供者並啟用統計資料之後，TDS 封包中傳送給 SQL Server 之資料的位元組數目。|  
|`ConnectionTime`|在啟用統計資料後連線處於開啟的時間量 (如果統計資料是在開啟連線之前啟用的，則為總連線時間)。|  
|`CursorOpens`|傳回應用程式開始使用提供者並啟用統計資料之後，透過連線開啟的資料指標次數。<br /><br /> 請注意，SELECT 陳述式傳回的唯讀/順向結果不會被視為資料指標，因此不會影響此計數器。|  
|`ExecutionTime`|傳回啟用統計資料後，提供者在處理作業所耗用的累計時間量 (以毫秒為單位)，包括等待伺服器回覆的時間，以及提供者本身執行程式碼的時間。<br /><br /> 包含計時程式碼的類別如下：<br /><br /> SqlConnection<br /><br /> SqlCommand<br /><br /> SqlDataReader<br /><br /> SqlDataAdapter<br /><br /> SqlTransaction<br /><br /> SqlCommandBuilder<br /><br /> 為了盡可能減少需要高效能才能正常運作的成員數，不會針對下列成員計時：<br /><br /> SqlDataReader<br /><br /> this[] 運算子 (所有多載)<br /><br /> GetBoolean<br /><br /> GetChar<br /><br /> GetDateTime<br /><br /> GetDecimal<br /><br /> GetDouble<br /><br /> GetFloat<br /><br /> GetGuid<br /><br /> GetInt16<br /><br /> GetInt32<br /><br /> GetInt64<br /><br /> GetName<br /><br /> GetOrdinal<br /><br /> GetSqlBinary<br /><br /> GetSqlBoolean<br /><br /> GetSqlByte<br /><br /> GetSqlDateTime<br /><br /> GetSqlDecimal<br /><br /> GetSqlDouble<br /><br /> GetSqlGuid<br /><br /> GetSqlInt16<br /><br /> GetSqlInt32<br /><br /> GetSqlInt64<br /><br /> GetSqlMoney<br /><br /> GetSqlSingle<br /><br /> GetSqlString<br /><br /> GetString<br /><br /> IsDBNull|  
|`IduCount`|傳回應用程式開始使用提供者並啟用統計資料之後，透過連線執行的 INSERT、DELETE 與 UPDATE 陳述式總數。|  
|`IduRows`|傳回應用程式開始使用提供者並啟用統計資料之後，受透過連線執行的 INSERT、DELETE 與 UPDATE 陳述式所影響的資料列總數。|  
|`NetworkServerTime`|一旦應用程式已開始使用提供者並啟用統計資料後，傳回提供者等待伺服器回覆的累計時間量 (以毫秒為單位)。|  
|`PreparedExecs`|傳回應用程式開始使用提供者並啟用統計資料後，透過連線所執行的備妥命令數目。|  
|`Prepares`|傳回應用程式開始使用提供者並啟用統計資料之後，透過連線所備妥陳述式的數目。|  
|`SelectCount`|傳回應用程式已開始使用提供者並啟用統計資料之後，透過連線所執行的 SELECT 陳述式數目。 這包括用來從資料指標取出資料列的 FETCH 陳述式，而且在到達 <xref:Microsoft.Data.SqlClient.SqlDataReader> 的結尾時，會更新 SELECT 陳述式的計數。|  
|`SelectRows`|傳回應用程式開始使用提供者並啟用統計資料之後，已選取的資料列數目。 此計數器會反映 SQL 陳述式產生的所有資料列，即使呼叫者並未實際取用的資料列也算在內。 例如，在讀取整個結果集之前關閉資料讀取器並不會影響計數。 這包括透過 FETCH 陳述式從資料指標擷取的資料列。|  
|`ServerRoundtrips`|傳回應用程式開始使用提供者並啟用統計資料之後，連線傳送命令至伺服器並收到回覆的次數。|  
|`SumResultSets`|傳回應用程式開始使用提供者並啟用統計資料之後，已使用的結果集數目。 例如，這會包含傳回給用戶端的任何結果集。 針對資料指標，系統會將每個擷取或區塊擷取作業都視為獨立結果集。|  
|`Transactions`|傳回應用程式開始使用提供者並啟用統計資料 (包括復原) 之後，已啟動的使用者交易數目。 如果是使用自動認可來執行連線，系統會將每個命令都視為一個交易。<br /><br /> 只要 BEGIN TRAN 陳述式一執行，此計數器就會遞增交易計數，無論交易之後獲認可或遭復原。|  
|`UnpreparedExecs`|傳回應用程式已開始使用提供者並啟用統計資料之後，透過連線所執行的未備妥陳述式數目。|  
  
### <a name="retrieving-a-value"></a>擷取值  
下列主控台應用程式會顯示如何在連線上啟用統計資料、擷取四個獨立統計資料值，並將其寫到主控台視窗。  
  
> [!NOTE]
>  下列範例使用包含於 SQL Server 的 **AdventureWorks** 範例資料庫。 範例程式碼中提供的連接字串會假設資料庫安裝在本機電腦且可供使用。 請依據您的環境需求修改連接字串。  
  
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
  
### <a name="retrieving-all-values"></a>擷取所有值  
下列主控台應用程式會顯示如何在連線上啟用統計資料、使用列舉程式擷取所有可用的統計資料值，並將其寫到主控台視窗。  
  
> [!NOTE]
>  下列範例使用包含於 SQL Server 的 **AdventureWorks** 範例資料庫。 範例程式碼中提供的連接字串會假設資料庫安裝在本機電腦且可供使用。 請依據您的環境需求修改連接字串。  
  
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
