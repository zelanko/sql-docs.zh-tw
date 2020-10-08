---
title: 在 SqlClient 中啟用事件追蹤
description: 描述如何透過實作事件接聽程式來在 SqlClient 中啟用事件追蹤，以及如何存取事件資料。
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: 4eac1ab519549ccace092cfc175c735dd4537269
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725739"
---
# <a name="enabling-event-tracing-in-sqlclient"></a>在 SqlClient 中啟用事件追蹤

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

## <a name="external-resources"></a>外部資源  
如需詳細資訊，請參閱下列資源。  
  
|資源|說明|  
|--------------|-----------------|  
|[EventSource 類別](/dotnet/api/system.diagnostics.tracing.eventsource)|提供建立 ETW 事件的能力。| 
|[EventListener 類別](/dotnet/api/system.diagnostics.tracing.eventlistener)|提供啟用和停用事件來源事件的方法。|