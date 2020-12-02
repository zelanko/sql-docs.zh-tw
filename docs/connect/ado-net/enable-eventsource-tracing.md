---
title: 在 SqlClient 中啟用事件追蹤
description: 描述如何透過實作事件接聽程式來在 SqlClient 中啟用事件追蹤，以及如何存取事件資料。
ms.date: 11/23/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: b45f6146f8b5e2f367281720b0fa1c3395d94256
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123954"
---
# <a name="enable-event-tracing-in-sqlclient"></a>在 SqlClient 中啟用事件追蹤

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

[Windows (ETW) 的事件追蹤](/windows/win32/etw/event-tracing-portal)是一種有效率的核心程序層級追蹤設施，其可供記錄驅動程式定義的事件以進行偵錯和測試。 SqlClient 支援在不同資訊層級上擷取 ETW 事件。 若要開始擷取事件追蹤，用戶端應用程式應接聽 SqlClient EventSource 實作的事件：

```
Microsoft.Data.SqlClient.EventSource
```

目前的實作支援下列事件關鍵字：

| 關鍵字名稱 | 值 | 描述 |
| ------------ | ----- | ----------- |
| ExecutionTrace | 1 | 開啟/停止擷取命令執行前後的事件。 |
| 追蹤 | 2 | 開啟擷取基本應用程式流程追蹤事件。 |
| 影響範圍 | 4 | 開啟擷取輸入和結束事件 |
| NotificationTrace | 8 | 開啟擷取 `SqlNotification` 追蹤事件 |
| NotificationTrace | 16 | 開啟擷取 `SqlNotification` 範圍輸入和結束事件 |
| PoolerTrace | 32 | 開啟擷取連線集區流程追蹤事件。 |
| PoolerScope | 64 | 開啟擷取連線集區範圍追蹤事件。 |
| AdvancedTrace | 128 | 開啟擷取進階流程追蹤事件。 |
| AdvancedTraceBin  | 256 | 開啟擷取包含其他資訊的進階流程追蹤事件。 |
| CorrelationTrace | 512 | 開啟擷取相互關聯流程追蹤事件。 |
| StateDump | 1024 | 開啟擷取 `SqlConnection` 的完整狀態傾印 |
| SNITrace | 2048 | 開啟擷取來自受控網路實作的流程追蹤事件 (僅適用於 .NET Core) |
| SNIScope | 4096 | 開啟擷取來自受控網路實作的範圍事件 (僅適用於 .NET Core) |
|||

## <a name="example"></a>範例
下列範例會啟用 **AdventureWorks** 範例資料庫上資料作業的事件追蹤，並在主控台視窗中顯示事件。

[!code-csharp [SqlClientEventSource#1](~/../sqlclient/doc/samples/SqlClientEventSource.cs#1)]

## <a name="event-tracing-support-in-native-sni"></a>原生 SNI 中的事件追蹤支援

**Microsoft.Data.SqlClient** v2.1.0 擴充了 **Microsoft.Data.SqlClient.SNI** 與 **Microsoft.Data.SqlClient.SNI.runtime** 中的事件追蹤支援。 透過將 EventCommand 傳送至 `SqlClientEventSource`，即可使用 [Xperf](https://docs.microsoft.com/windows-hardware/test/wpt/) 與 [PerfView](https://github.com/microsoft/perfview) 工具來收集原生 SNI.dll 中的事件。 有效的 EventCommand 值如下所示：

```cs
// Enables trace events:
EventSource.SendCommand(eventSource, (EventCommand)8192, null);

// Enables flow events:
EventSource.SendCommand(eventSource, (EventCommand)16384, null);

// Enables both trace and flow events:
EventSource.SendCommand(eventSource, (EventCommand)(8192 | 16384), null);
```

下列範例會在應用程式以 .NET Framework 為目標時，啟用原生 SNI.dll 中的事件追蹤。 

```cs
// Native SNI tracing example
// .NET Framework application
using System;
using System.Diagnostics.Tracing;
using Microsoft.Data.SqlClient;

public class SqlClientListener : EventListener
{
    protected override void OnEventSourceCreated(EventSource eventSource)
    {
        if (eventSource.Name.Equals("Microsoft.Data.SqlClient.EventSource"))
        {
            // Enables both trace and flow events
            EventSource.SendCommand(eventSource, (EventCommand)(8192 | 16384), null);
        }
    }
}

class Program
{
    static string connectionString = @"Data Source = localhost; Initial Catalog = AdventureWorks;Integrated Security=true;";

    static void Main(string[] args)
    {
        using (SqlClientListener listener = new SqlClientListener())
        using (SqlConnection connection = new SqlConnection(connectionString))
        {
            connection.Open();
        }        
    }
}
```

### <a name="use-xperf-to-collect-trace-log"></a>使用 Xperf 來收集追蹤記錄

1. 使用下列命令列來啟動追蹤。

   ```
   xperf -start trace -f myTrace.etl -on *Microsoft.Data.SqlClient.EventSource
   ```
   
2. 執行原生 SNI 追蹤範例，以連線到 SQL Server。

3. 使用下列命令列來停止追蹤。

   ```
   xperf -stop trace
   ```
   
4. 使用 PerfView 來開啟步驟 1 中所指定的 myTrace.etl 檔案。 您可以使用 `Microsoft.Data.SqlClient.EventSource/SNIScope` 與 `Microsoft.Data.SqlClient.EventSource/SNITrace` 的事件名稱來找到 SNI 追蹤記錄。 

   ![使用 PerfView 來檢視 SNI 追蹤檔案](media/view-event-trace-native-sni.png)


### <a name="use-perfview-to-collect-trace-log"></a>使用 PerfView 來收集追蹤記錄

1. 從功能表列啟動 PerfView 並執行 `Collect > Collect`。

2. 設定追蹤檔案名稱、輸出路徑與提供者名稱。

   ![收集之前先設定 Prefview](media/collect-event-trace-native-sni.png)
   
3. 開始收集。

4. 執行原生 SNI 追蹤範例，以連線到 SQL Server。

5. 從 PerfView 停止收集。 根據步驟 2 中的設定產生 PerfViewData.etl 檔案，將需要一些時間。

6. 在 PerfView 中開啟 etl 檔案。 您可以使用 `Microsoft.Data.SqlClient.EventSource/SNIScope` 與 `Microsoft.Data.SqlClient.EventSource/SNITrace` 的事件名稱來找到 SNI 追蹤記錄。 


## <a name="external-resources"></a>外部資源  
如需詳細資訊，請參閱下列資源。  
  
|資源|說明|  
|--------------|-----------------|  
|[EventSource 類別](/dotnet/api/system.diagnostics.tracing.eventsource)|提供建立 ETW 事件的能力。| 
|[EventListener 類別](/dotnet/api/system.diagnostics.tracing.eventlistener)|提供啟用和停用事件來源事件的方法。|
