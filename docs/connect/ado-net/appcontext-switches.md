---
title: SqlClient 中的 AppContext 參數
description: 描述如何使用 SqlClient 中提供的 AppContext 參數。
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
ms.openlocfilehash: 16d3ed6db478f12157333badf93682eb861c57f3
ms.sourcegitcommit: 8515bb2021cfbc7791318527b8554654203db4ad
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86091686"
---
# <a name="appcontext-switches-in-sqlclient"></a>SqlClient 中的 AppContext 參數

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

AppContext 類別允許 SqlClient 提供新功能，同時繼續支援相依於之前行為的呼叫端。 使用者可以透過設定特定的 AppContext 參數，選擇退出行為中的變更。

## <a name="enabling-decimal-truncation-behavior"></a>啟用十進位截斷行為

[!INCLUDE [appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

從 Microsoft.Data.SqlClient 2.0 開始，十進位資料預設會四捨五入，和 SQL Server 一樣。 若要啟用之前的截斷行為，您可以在應用程式啟動時將 AppContext 參數 **"Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal"** 設為 `true`：

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal", true);
```

## <a name="enabling-managed-networking-on-windows"></a>在 Windows 上啟用受控網路

[!INCLUDE [appliesto-xxxx-netcore-netst-md](../../includes/appliesto-xxxx-netcore-netst-md.md)]

在 Windows 上，SqlClient 預設使用 SNI 網路介面的原生實作。 若要使用受控的 SNI 實作，您可以在應用程式啟動時將 AppContext 參數 **"Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows"** 設為 `true`：

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows", true);
```

此參數會切換驅動程式的行為，以在 Windows 的 .NET Core 2.1+ 與 .NET Standard 2.0+ 專案中使用受控網路實作，同時消除 Microsoft.Data.SqlClient 程式庫之原生程式庫的所有相依性。 此僅用於測試與偵錯用途。

> [!NOTE]
> 與原生實作相比，有一些已知差異。 例如，受控實作不支援非網域 Windows 驗證。

## <a name="disabling-transparent-network-ip-resolution"></a>停用透明網路 IP 解析

[!INCLUDE [appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

透明網路 IP 解析 (TNIR) 為現有 MultiSubnetFailover 功能的修訂版本。 如果第一個解析的主機名稱 IP 未回應，且該主機名稱有多個相關聯的 IP 時，TNIR 會影響驅動程式的連線順序。 TNIR 會與 MultiSubnetFailover 互動，以提供下列三種連線順序：<br />
* 0：嘗試一個 IP，然後以並行方式嘗試所有 IP
* 1：以並行方式嘗試所有 IP
* 2：逐一嘗試所有 IP

|TransparentNetworkIPResolution|MultiSubnetFailover|行為|
|--------|--------|--------|
|True|True|1|
|True|否|0|
|False|True|1|
|False|False|2|

TransparentNetworkIPResolution 預設為啟用。 MultiSubnetFailover 預設為停用。 若要停用 TNIR，您可以在應用程式啟動時將 AppContext 參數 **"Switch.Microsoft.Data.SqlClient.DisableTNIRByDefaultInConnectionString"** 設為 `true`：

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.DisableTNIRByDefaultInConnectionString", true);
```

如需設定這些屬性的詳細資訊，請參閱 [SqlConnection.ConnectionString 屬性](https://docs.microsoft.com/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring) (英文) 文件。 

## <a name="enable-a-minimum-timeout-during-login"></a>在登入期間啟用逾時最小值

[!INCLUDE [appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

若要避免登入嘗試永遠等候，您可以在應用程式啟動時將 AppContext 參數 **Switch.Microsoft.Data.SqlClient.UseOneSecFloorInTimeoutCalculationDuringLogin** 設為 `true`：

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.UseOneSecFloorInTimeoutCalculationDuringLogin", false);
```

## <a name="disable-blocking-behavior-of-readasync"></a>停用 ReadAsync 的封鎖行為

[!INCLUDE [appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

ReadAsync 預設同步執行並禁止呼叫 .NET Framework 上的執行緒。 若要停用此封鎖行為，您可以在應用程式啟動時將 AppContext 參數 **Switch.Microsoft.Data.SqlClient.MakeReadAsyncBlocking** 設為 `false`：

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.MakeReadAsyncBlocking", false);
```

## <a name="see-also"></a>另請參閱

[AppContext 類別](https://docs.microsoft.com/dotnet/api/system.appcontext?view=netcore-3.1) (機器翻譯)
