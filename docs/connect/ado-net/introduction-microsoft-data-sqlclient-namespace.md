---
title: Microsoft.Data.SqlClient 命名空間簡介
description: Microsoft.Data.SqlClient 命名空間的簡介頁面。
ms.date: 09/30/2019
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: dbc76f1a2ee93faf642d923d3a543eee40d5348b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "78897122"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Microsoft.Data.SqlClient 命名空間簡介

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

## <a name="release-notes-for-microsoftdatasqlclient-110"></a>Microsoft.Data.SqlClient 1.1.0 的版本資訊

您也可以在 GitHub 存放庫中取得版本資訊：[1.1 版本資訊](https://github.com/dotnet/SqlClient/tree/master/release-notes/1.1) \(英文\)。

### <a name="new-features"></a>新功能

#### <a name="always-encrypted-with-secure-enclaves"></a>具有安全記憶體保護區的 Always Encrypted

Always Encrypted 從 Microsoft SQL Server 2016 開始提供。 安全記憶體保護區從 Microsoft SQL Server 2019 開始提供。 為了使用記憶體保護區功能，連接字串應該包含必要的證明通訊協定和證明 URL。 範例：

```
Attestation Protocol=HGS;Enclave Attestation Url=<attestation_url_for_HGS>
```

如需詳細資訊，請參閱：

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

當底層來源支援此功能，並包含有關[資料敏感度和分類](../../relational-databases/security/sql-data-discovery-and-classification.md)的中繼資料時，資料分類會帶來一組新的 API，公開有關透過 SqlDataReader 擷取之物件的唯讀資料敏感度和分類資訊。

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

UTF-8 支援不需要進行任何應用程式程式碼變更。 這些 SqlClient 變更只會在伺服器支援 UTF-8 且底層資料行定序為 UTF-8 時，將用戶端與伺服器之間的通訊最佳化。 請參閱 [SQL Server 2019 預覽版的新功能](../../sql-server/what-s-new-in-sql-server-ver15.md)底下的 UTF-8 小節。

### <a name="always-encrypted-with-enclaves"></a>具有記憶體保護區的 Always Encrypted

一般來說，在 .NET Framework **和內建資料行主要金鑰存放區提供者**上使用 System.Data.SqlClient 的現有文件現在也應該使用 .NET Core。

 [搭配使用 Always Encrypted 與 .NET Framework Data Provider 進行開發](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted：保護敏感性資料並將加密金鑰儲存在 Windows 憑證存放區中](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted) \(部分機器翻譯\)

### <a name="authentication"></a>驗證

您可以使用 _Authentication_ 連接字串選項來指定不同的驗證模式。 如需詳細資訊，請參閱 [SqlAuthenticationMethod 的文件](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2) \(部分機器翻譯\)。

> [!NOTE]
> 自訂金鑰存放區提供者 (例如 Azure Key Vault 提供者) 將需要更新，才能支援 Microsoft.Data.SqlClient。 同樣地，記憶體保護區提供者也必須更新，才能支援 Microsoft.Data.SqlClient。
> 僅針對 .NET Framework 和 .NET Core 目標支援 Always Encrypted。 並未針對 .NET Standard 提供支援，因為 .NET Standard 遺漏了某些加密相依性。
