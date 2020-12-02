---
title: Microsoft.Data.SqlClient 命名空間簡介
description: 了解 Microsoft.Data.SqlClient 命名空間，以及其為何是連線至適用於 .NET 應用程式的 SQL 其慣用方式。
ms.date: 11/19/2020
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-jizho2
ms.openlocfilehash: f522b856e759ec9821b5cc549ce3f801951b7283
ms.sourcegitcommit: 4c3949f620d09529658a2172d00bfe37aeb1a387
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2020
ms.locfileid: "95011834"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Microsoft.Data.SqlClient 命名空間簡介

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

## <a name="release-notes-for-microsoftdatasqlclient-21"></a>Microsoft.Data.SqlClient 2.1 的版本資訊

您也可以在 GitHub 存放庫中取得版本資訊：[2.1 版本資訊](https://github.com/dotnet/SqlClient/tree/master/release-notes/2.1) \(英文\)。

### <a name="new-features"></a>新功能

### <a name="cross-platform-support-for-always-encrypted"></a>對 Always Encrypted 的跨平台支援
Microsoft.Data.SqlClient v2.1 在下列平台上擴充了對 Always Encrypted 的支援：

| 支援 Always Encrypted | 支援具有安全記憶體保護區的 Always Encrypted  | 目標 Framework | Microsoft.Data.SqlClient 版本 | 作業系統 |
|:--|:--|:--|:--:|:--:|
| 是 | 是 | .NET Framework 4.6+ | 1.1.0+ | Windows |
| 是 | 是 | .NET Core 2.1+ | 2.1.0+<sup>1</sup> | Windows、Linux、macOS |
| Yes | 否<sup>2</sup> | .NET Standard 2.0 | 2.1.0+ | Windows、Linux、macOS |
| 是 | 是 | .NET Standard 2.1+ | 2.1.0+ | Windows、Linux、macOS |

> [!NOTE]
> <sup>1</sup> 在 Microsoft.Data.SqlClient v2.1 版之前，只有 Windows 上支援 Always Encrypted。
> <sup>2</sup> .NET Standard 2.0 上不支援具有安全記憶體保護區的 Always Encrypted。

### <a name="azure-active-directory-device-code-flow-authentication"></a>Azure Active Directory 裝置程式碼流程驗證
Microsoft.Data.SqlClient v2.1 提供使用 MSAL.NET 進行「裝置程式碼流程」驗證的支援。
參考文件：[OAuth 2.0 裝置授權授與流程](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-device-code) \(部分機器翻譯\)

連接字串範例：

`Server=<server>.database.windows.net; Authentication=Active Directory Device Code Flow; Database=Northwind;`

下列 API 可讓您自訂裝置程式碼流程回呼機制：

```csharp
public class ActiveDirectoryAuthenticationProvider
{
    // For .NET Framework, .NET Core and .NET Standard targeted applications
    public void SetDeviceCodeFlowCallback(Func<DeviceCodeResult, Task> deviceCodeFlowCallbackMethod)
}
```

### <a name="azure-active-directory-managed-identity-authentication"></a>Azure Active Directory 受控識別驗證
Microsoft.Data.SqlClient v2.1 引進了使用[受控識別](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)進行 Azure Active Directory 驗證的支援。

目前支援下列驗證模式關鍵字：
- Active Directory 受控識別
- Active Directory MSI (適用於跨 MS SQL 驅動程式相容性)

連接字串範例：

```cs
// For System Assigned Managed Identity
"Server={serverURL}; Authentication=Active Directory MSI; Initial Catalog={db};"

// For System Assigned Managed Identity
"Server={serverURL}; Authentication=Active Directory Managed Identity; Initial Catalog={db};"

// For User Assigned Managed Identity
"Server={serverURL}; Authentication=Active Directory MSI; User Id={ObjectIdOfManagedIdentity}; Initial Catalog={db};"

// For User Assigned Managed Identity
"Server={serverURL}; Authentication=Active Directory Managed Identity; User Id={ObjectIdOfManagedIdentity}; Initial Catalog={db};"
```

### <a name="azure-active-directory-interactive-authentication-enhancements"></a>Azure Active Directory 互動式驗證增強功能
Microsoft.Data.SqlClient v2.1 新增了下列可自訂「Active Directory 互動式」驗證體驗的 API：

```csharp
public class ActiveDirectoryAuthenticationProvider
{
    // For .NET Framework targeted applications only
    public void SetIWin32WindowFunc(Func<IWin32Window> iWin32WindowFunc);

    // For .NET Standard targeted applications only
    public void SetParentActivityOrWindowFunc(Func<object> parentActivityOrWindowFunc);

    // For .NET Framework, .NET Core and .NET Standard targeted applications
    public void SetAcquireAuthorizationCodeAsyncCallback(Func<Uri, Uri, CancellationToken, Task<Uri>> acquireAuthorizationCodeAsyncCallback);

    // For .NET Framework, .NET Core and .NET Standard targeted applications
    public void ClearUserTokenCache();
}
```

### <a name="sqlclientauthenticationproviders-configuration-section"></a>`SqlClientAuthenticationProviders` 設定區段
Microsoft.Data.SqlClient v2.1 引進了新的設定區段 `SqlClientAuthenticationProviders` (現有 `SqlAuthenticationProviders` 的複製品)。 定義適當的類型時，仍支援現有的設定區段 `SqlAuthenticationProviders`，以提供回溯相容性。

新區段讓應用程式組態檔能夠同時包含適用於 System.Data.SqlClient 的 SqlAuthenticationProviders 區段，以及適用於 Microsoft.Data.SqlClient 的 SqlClientAuthenticationProviders 區段。


### <a name="azure-active-directory-authentication-using-an-application-client-id"></a>使用應用程式用戶端識別碼進行 Azure Active Directory 驗證
Microsoft.Data.SqlClient v2.1 引進了將使用者定義的應用程式用戶端識別碼傳遞至 Microsoft 驗證程式庫的支援。 使用 Azure Active Directory 進行驗證時，會使用應用程式用戶端識別碼。

已引進下列新的 API：

1. 已在 ActiveDirectoryAuthenticationProvider 中引進了新的建構函式：
[適用於所有 .NET 平台 (.NET Framework、.NET Core 與 .NET Standard)]

```csharp
public ActiveDirectoryAuthenticationProvider(string applicationClientId)
```

Usage :
```csharp
string APP_CLIENT_ID = "<GUID>";
SqlAuthenticationProvider customAuthProvider = new ActiveDirectoryAuthenticationProvider(APP_CLIENT_ID);
SqlAuthenticationProvider.SetProvider(SqlAuthenticationMethod.ActiveDirectoryInteractive, customAuthProvider);

using (SqlConnection sqlConnection = new SqlConnection("<connection_string>")
{
    sqlConnection.Open();
}
```

2. 已在 `SqlAuthenticationProviderConfigurationSection` 與 `SqlClientAuthenticationProviderConfigurationSection` 底下引進了新的設定屬性：
[適用於 .NET Framework 與 .NET Core]

```csharp
internal class SqlAuthenticationProviderConfigurationSection : ConfigurationSection
{
    ...
    [ConfigurationProperty("applicationClientId", IsRequired = false)]
    public string ApplicationClientId => this["applicationClientId"] as string;
}

// Inheritance
internal class SqlClientAuthenticationProviderConfigurationSection : SqlAuthenticationProviderConfigurationSection
{ ... }
```

Usage :
```xml
<configuration>
    <configSections>
        <section name="SqlClientAuthenticationProviders"
                         type="Microsoft.Data.SqlClient.SqlClientAuthenticationProviderConfigurationSection, Microsoft.Data.SqlClient" />
    </configSections>
    <SqlClientAuthenticationProviders applicationClientId ="<GUID>" />
</configuration>

<!--or-->

<configuration>
    <configSections>
        <section name="SqlAuthenticationProviders"
                         type="Microsoft.Data.SqlClient.SqlAuthenticationProviderConfigurationSection, Microsoft.Data.SqlClient" />
    </configSections>
    <SqlAuthenticationProviders applicationClientId ="<GUID>" />
</configuration>
```

### <a name="data-classification-v2-support"></a>資料分類 v2 支援
Microsoft.Data.SqlClient v2.1.0 引進了對資料分類「敏感度順位」資訊的支援。 現在有下列新的 API 可供使用：

```csharp
public class SensitivityClassification
{
    public SensitivityRank SensitivityRank;
}

public class SensitivityProperty
{
    public SensitivityRank SensitivityRank;
}

public enum SensitivityRank
{
    NOT_DEFINED = -1,
    NONE = 0,
    LOW = 10,
    MEDIUM = 20,
    HIGH = 30,
    CRITICAL = 40
}
```

### <a name="server-process-id-for-an-active-sqlconnection"></a>使用中 `SqlConnection` 的伺服器處理序識別碼
Microsoft.Data.SqlClient v2.1 在使用中的連線上引進了新的 `SqlConnection` 屬性 (`ServerProcessId`)。

```csharp
public class SqlConnection
{
    // Returns the server process Id (SPID) of the active connection.
    public int ServerProcessId;
}
```

### <a name="trace-logging-support-in-native-sni"></a>原生 SNI 中的追蹤記錄支援
Microsoft.Data.SqlClient v2.1 擴充了現有的 `SqlClientEventSource` 實作，以在 SNI.dll 中啟用事件追蹤。 您必須使用 Xperf 之類的工具來擷取事件。

您可以透過將命令傳送至 `SqlClientEventSource` 來啟用追蹤，如下所示：

```csharp
// Enables trace events:
EventSource.SendCommand(eventSource, (EventCommand)8192, null);

// Enables flow events:
EventSource.SendCommand(eventSource, (EventCommand)16384, null);

// Enables both trace and flow events:
EventSource.SendCommand(eventSource, (EventCommand)(8192 | 16384), null);
```


### <a name="command-timeout-connection-string-property"></a>「命令逾時」連接字串屬性
Microsoft.Data.SqlClient v2.1 引進了「命令逾時」連接字串屬性，以覆寫 30 秒的預設值。 您可以使用 SqlCommand 上的 `CommandTimeout` 屬性來覆寫個別命令的逾時。

連接字串範例：

`"Server={serverURL}; Initial Catalog={db}; Integrated Security=true; Command Timeout=60"`

### <a name="removal-of-symbols-from-native-sni"></a>從原生 SNI 移除符號
在 Microsoft.Data.SqlClient v2.1，我們已從 [v2.1.1](https://www.nuget.org/packages/Microsoft.Data.SqlClient.SNI.runtime/2.1.1) \(英文\) 開始，移除了從 [Microsoft.Data.SqlClient.SNI.runtime](https://www.nuget.org/packages/Microsoft.Data.SqlClient.SNI.runtime) \(英文\) NuGet 的 [v2.0.0](https://www.nuget.org/packages/Microsoft.Data.SqlClient.SNI/2.0.0) \(英文\) 中引進的符號。 現在已將公用符號發佈至 Microsoft 符號伺服器，以供需要存取公用符號的工具 (例如 BinSkim) 使用。

### <a name="source-linking-of-microsoftdatasqlclient-symbols"></a>Microsoft.Data.SqlClient 符號的來源連結
從 Microsoft.Data.SqlClient v2.1 開始，Microsoft.Data.SqlClient 符號會與來源連結並發佈至 Microsoft 符號伺服器，以提供增強的偵錯體驗，而不需要下載原始程式碼。


## <a name="release-notes-for-microsoftdatasqlclient-20"></a>Microsoft.Data.SqlClient 2.0 的版本資訊

您也可以在 GitHub 存放庫中取得版本資訊：[2.0 版本資訊](https://github.com/dotnet/SqlClient/tree/master/release-notes/2.0)。

### <a name="breaking-changes"></a>重大變更

- 記憶體保護區提供者介面 `SqlColumnEncryptionEnclaveProvider` 的存取修飾詞，已從 `public` 變更為 `internal`。

- `SqlClientMetaDataCollectionNames` 類別中的常數已更新，以反映 SQL Server 中的變更。

- 現在當目標 SQL Server 強制執行 TLS 加密 (此為 Azure 連線的預設值) 時，驅動程式會執行伺服器憑證驗證。

- `SqlDataReader.GetSchemaTable()` 現在會傳回空的 `DataTable`，而不是 `null`。

- 驅動程式現在會將十進位小數位數四捨五入，以符合 SQL Server 的行為。 如需回溯相容性，可使用 AppContext 參數來啟用先前的截斷行為。

- 對於使用 **Microsoft.Data.SqlClient** 的 .NET Framework 應用程式，先前下載至 `bin\x64` 與 `bin\x86` 資料夾的 SNI.dll 檔案現在會命名為 `Microsoft.Data.SqlClient.SNI.x64.dll` 及 ` Microsoft.Data.SqlClient.SNI.x86.dll`，並會下載至 `bin` 目錄。

- 從 `SqlConnectionStringBuilder` 擷取連接字串以取得一致性時，新的連接字串屬性同義字會取代舊屬性。 [閱讀更多資訊](#new-connection-string-property-synonyms)

### <a name="new-features"></a>新功能

#### <a name="dns-failure-resiliency"></a>DNS 失敗復原

驅動程式現在會將每個成功連線中 IP 位址快取至支援該功能的 SQL Server 端點。 如果在嘗試連線時 DNS 解析失敗，則驅動程式會嘗試使用該伺服器的快取 IP 位址 (如果有的話) 來建立連線。

#### <a name="eventsource-tracing"></a>EventSource 追蹤

此版本導入對偵錯工具其擷取事件追蹤記錄的支援。 若要擷取這些事件，用戶端應用程式必須接聽 SqlClient EventSource 實作的事件：

```
Microsoft.Data.SqlClient.EventSource
```

如需詳細資訊，請參閱如何[在 SqlClient 中啟用事件追蹤](enable-eventsource-tracing.md)。

#### <a name="enabling-managed-networking-on-windows"></a>在 Windows 上啟用受控網路

新 AppContext 切換， **"Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows"** ，可供啟用 Windows 上的受控 SNI 實作，以用於測試與偵錯。 此參數會切換驅動程式的行為，以在 Windows 的 .NET Core 2.1+ 與 .NET Standard 2.0+ 專案中使用受控 SNI，同時消除 Microsoft.Data.SqlClient 程式庫的原生程式庫上所有相依性。

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows", true);
```

如需驅動程式中可用參數的完整清單，請參閱 [SqlClient 中的 AppContext 參數](appcontext-switches.md)。

#### <a name="enabling-decimal-truncation-behavior"></a>啟用十進位截斷行為

根據預設，驅動程式會與 SQL Server 相同，將十進位資料小數位數四捨五入。 如需回溯相容性，則可將 AppCoNtext 參數 **"Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal"** 設定為 **true**。

```csharp
AppContext.SetSwitch("Switch.Microsoft.Data.SqlClient.TruncateScaledDecimal", true);
```

#### <a name="new-connection-string-property-synonyms"></a>全新連接字串屬性同義字

已為下列現有連接字串屬性新增新的同義字，以避免具有一個單字以上的屬性之間的間距混淆。 將繼續支援舊版屬性名稱，以獲得回溯相容性，但現在從 [SqlConnectionStringBuilder](/dotnet/api/microsoft.data.sqlclient.sqlconnectionstringbuilder) 連接字串時，會包含新的連接字串屬性。

|現有的連接字串屬性|全新同義字|
|-----------------------------------|-----------|
| ApplicationIntent | 應用程式的意圖 |
| ConnectRetryCount | 連線重試計數 |
| ConnectRetryInterval | 連線重試間隔 |
| PoolBlockingPeriod | 集區封鎖期間 |
| MultipleActiveResultSets | Multiple Active Result Set |
| MultiSubnetFailover | 多重子網容錯移轉 |
| TransparentNetworkIPResolution | 透明網路 IP 解析 |
| TrustServerCertificate | 信任伺服器憑證 |

#### <a name="sqlbulkcopy-rowscopied-property"></a>SqlBulkCopy RowsCopied 屬性

RowsCopied 屬性提供資料列數目的唯讀存取，該資料列已在進行中的大量複製作業中處理。 此值不一定等於新增至目的地資料表的最終資料列數目。

#### <a name="connection-open-overrides"></a>連線開啟覆寫

可覆寫 SqlConnection.Open () 的預設行為，以停用暫時性錯誤所觸發的 10 秒延遲及自動連線重試。

```csharp
using SqlConnection sqlConnection = new SqlConnection("Data Source=(local);Integrated Security=true;Initial Catalog=AdventureWorks;");
sqlConnection.Open(SqlConnectionOverrides.OpenWithoutRetry);
```

> [!NOTE]
> 請注意，此覆寫只能套用至 SqlConnection.Open()，無法套用至 SqlConnection.OpenAsync()。

#### <a name="username-support-for-active-directory-interactive-mode"></a>支援 Active Directory 互動模式的使用者名稱

使用 .NET Framework 及 .NET Core 的 Azure Active Directory 互動式驗證模式時，可在連接字串中指定使用者名稱

使用 **使用者識別碼** 或 **UID** 連接字串屬性來設定使用者名稱：

```
"Server=<server name>; Database=<db name>; Authentication=Active Directory Interactive; User Id=<username>;"
```

#### <a name="order-hints-for-sqlbulkcopy"></a>SqlBulkCopy 的順序提示

可提供順序提示以改善資料表 (具有叢集索引) 上的大量複製作業效能。 如需詳細資訊，請參閱[大量複製作業](sql/bulk-copy-order-hints.md)。

#### <a name="sni-dependency-changes"></a>SNI 相依性變更

Windows 上的 Microsoft.Data.SqlClient (.NET Core 及 .NET Standard) 現在相依於 **Microsoft.Data.SqlClient.SNI.runtime**，其取代先前對 **runtime.native.System.Data.SqlClient.SNI** 的相依性。 全新相依性新增對 ARM 平台的支援，並已支援 Windows 上的 ARM64、x64 與 x86 平台。

## <a name="release-notes-for-microsoftdatasqlclient-110"></a>Microsoft.Data.SqlClient 1.1.0 的版本資訊

您也可以在 GitHub 存放庫中取得版本資訊：[1.1 版本資訊](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.1) \(英文\)。

### <a name="new-features"></a>新功能

#### <a name="always-encrypted-with-secure-enclaves"></a>具有安全記憶體保護區的 Always Encrypted

Always Encrypted 從 Microsoft SQL Server 2016 開始提供。 安全記憶體保護區從 Microsoft SQL Server 2019 開始提供。 若要使用記憶體保護區功能，則連接字串應該包含必要的證明通訊協定與證明 URL。 例如：

```
Attestation Protocol=HGS;Enclave Attestation Url=<attestation_url_for_HGS>
```

如需詳細資訊，請參閱

- [SqlClient 對 Always Encrypted 的支援](sql/sqlclient-support-always-encrypted.md)
- [教學課程：使用具有安全記憶體保護區的 Always Encrypted 開發 .NET 應用程式](sql/tutorial-always-encrypted-enclaves-develop-net-apps.md)

## <a name="release-notes-for-microsoftdatasqlclient-10"></a>Microsoft.Data.SqlClient 1.0 的版本資訊

Microsoft.Data.SqlClient 命名空間的初始版本提供超越現有 Microsoft.Data.SqlClient 命名空間的其他功能。
您也可以在 GitHub 存放庫上取得版本資訊：[1.0 版本資訊](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.0) \(英文\)。

### <a name="new-features"></a>新功能

#### <a name="new-features-over-net-framework-472-systemdatasqlclient"></a>超越 .NET Framework 4.7.2 System.Data.SqlClient 的新功能

- **資料分類**：適用於 Azure SQL Database 和 Microsoft SQL Server 2019。

- **UTF-8 支援**：適用於 Microsoft SQL Server 2019。

#### <a name="new-features-over-net-core-22-systemdatasqlclient"></a>超越 .NET Core 2.2 System.Data.SqlClient 的新功能

- **資料分類**：適用於 Azure SQL Database 和 Microsoft SQL Server 2019。

- **UTF-8 支援**：適用於 Microsoft SQL Server 2019。

- **驗證**：Active Directory 密碼驗證模式。

### <a name="data-classification"></a>資料分類

當底層來源支援此功能，並包含有關[資料敏感度和分類](../../relational-databases/security/sql-data-discovery-and-classification.md)的中繼資料時，資料分類會帶來一組新的 API，公開有關透過 SqlDataReader 擷取之物件的唯讀資料敏感度和分類資訊。 請參閱 [SqlClient 中的資料探索及分類](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.1)的範例應用程式。

```csharp
public class SqlDataReader
{
    public Microsoft.Data.SqlClient.DataClassification.SensitivityClassification SensitivityClassification
}

namespace Microsoft.Data.SqlClient.DataClassification
{
    public class ColumnSensitivity
    {
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.SensitivityProperty> SensitivityProperties
    }
    public class InformationType
    {
        public string Id
        public string Name
    }
    public class Label
    {
        public string Id
        public string Name
    }
    public class SensitivityClassification
    {
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.ColumnSensitivity> ColumnSensitivities
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.InformationType> InformationTypes
        public System.Collections.ObjectModel.ReadOnlyCollection<Microsoft.Data.SqlClient.DataClassification.Label> Labels
    }
    public class SensitivityProperty
    {
        public Microsoft.Data.SqlClient.DataClassification.InformationType InformationType
        public Microsoft.Data.SqlClient.DataClassification.Label Label
    }
}
```

### <a name="utf-8-support"></a>UTF-8 支援

UTF-8 支援不需要進行任何應用程式程式碼變更。 這些 SqlClient 變更會在伺服器支援 UTF-8 且底層資料行定序為 UTF-8 時，將用戶端與伺服器之間的通訊最佳化。 請參閱 [SQL Server 2019 的新功能](../../sql-server/what-s-new-in-sql-server-ver15.md)下方的 UTF-8 一節。

### <a name="always-encrypted-with-enclaves"></a>具有記憶體保護區的 Always Encrypted

一般來說，在 .NET Framework **及內建資料行主要金鑰存放區提供者** 上使用 System.Data.SqlClient 的現有文件，現在也應該使用 .NET Core。

 [搭配使用 Always Encrypted 與 .NET Framework Data Provider 進行開發](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted：保護敏感性資料並將加密金鑰儲存在 Windows 憑證存放區中](/azure/sql-database/sql-database-always-encrypted) \(部分機器翻譯\)

### <a name="authentication"></a>驗證

您可以使用 _Authentication_ 連接字串選項來指定不同的驗證模式。 如需詳細資訊，請參閱 [SqlAuthenticationMethod 的文件](/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2&preserve-view=true) \(部分機器翻譯\)。

> [!NOTE]
> 自訂金鑰存放區提供者 (例如 Azure Key Vault 提供者) 將需要更新，才能支援 Microsoft.Data.SqlClient。 同樣地，記憶體保護區提供者也必須更新，才能支援 Microsoft.Data.SqlClient。
> 僅針對 .NET Framework 和 .NET Core 目標支援 Always Encrypted。 並未針對 .NET Standard 提供支援，因為 .NET Standard 遺漏了某些加密相依性。
