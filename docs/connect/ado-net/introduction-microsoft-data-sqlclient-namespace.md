---
title: Microsoft.Data.SqlClient 命名空間簡介
description: Microsoft.Data.SqlClient 命名空間的簡介頁面。
ms.date: 06/23/2019
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 3a4f0611d3708aba9557deb81ab702f29e7a7462
ms.sourcegitcommit: 22f687e9e8b4f37b877b2d19c5090dade8fa26d0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/24/2020
ms.locfileid: "85334580"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Microsoft.Data.SqlClient 命名空間簡介

[!INCLUDE [Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

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

新 AppContext 參數 **"Switch.Microsoft.Data.SqlClient.UseManagedNetworkingOnWindows"** 可供啟用 Windows 上的受控 SNI 實作，以用於測試與偵錯。 此參數會切換驅動程式的行為，以在 Windows 的 .NET Core 2.1+ 與 .NET Standard 2.0+ 專案中使用受控 SNI，同時消除 Microsoft.Data.SqlClient 程式庫的原生程式庫上所有相依性。

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

已為下列現有連接字串屬性新增新的同義字，以避免具有一個單字以上的屬性之間的間距混淆。 將繼續支援舊版屬性名稱，以獲得回溯相容性，但現在從 [SqlConnectionStringBuilder](https://docs.microsoft.com/dotnet/api/microsoft.data.sqlclient.sqlconnectionstringbuilder) 連接字串時，會包含新的連接字串屬性。

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

使用**使用者識別碼**或 **UID** 連接字串屬性來設定使用者名稱：

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

UTF-8 支援不需要進行任何應用程式程式碼變更。 這些 SqlClient 變更會在伺服器支援 UTF-8 且底層資料行定序為 UTF-8 時，將用戶端與伺服器之間的通訊最佳化。 請參閱 [SQL Server 2019 預覽版的新功能](../../sql-server/what-s-new-in-sql-server-ver15.md)底下的 UTF-8 小節。

### <a name="always-encrypted-with-enclaves"></a>具有記憶體保護區的 Always Encrypted

一般來說，在 .NET Framework **和內建資料行主要金鑰存放區提供者**上使用 System.Data.SqlClient 的現有文件現在也應該使用 .NET Core。

 [搭配使用 Always Encrypted 與 .NET Framework Data Provider 進行開發](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted：保護敏感性資料並將加密金鑰儲存在 Windows 憑證存放區中](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted) \(部分機器翻譯\)

### <a name="authentication"></a>驗證

您可以使用 _Authentication_ 連接字串選項來指定不同的驗證模式。 如需詳細資訊，請參閱 [SqlAuthenticationMethod 的文件](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2) \(部分機器翻譯\)。

> [!NOTE]
> 自訂金鑰存放區提供者 (例如 Azure Key Vault 提供者) 將需要更新，才能支援 Microsoft.Data.SqlClient。 同樣地，記憶體保護區提供者也必須更新，才能支援 Microsoft.Data.SqlClient。
> 僅針對 .NET Framework 和 .NET Core 目標支援 Always Encrypted。 並未針對 .NET Standard 提供支援，因為 .NET Standard 遺漏了某些加密相依性。
