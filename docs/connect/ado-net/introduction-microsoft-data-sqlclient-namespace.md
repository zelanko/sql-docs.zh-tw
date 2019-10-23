---
title: Microsoft.Data.SqlClient 命名空間簡介
description: SqlClient 命名空間的簡介頁面。
ms.date: 09/30/2019
ms.assetid: c18b1fb1-2af1-4de7-80a4-95e56fd976cb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 4f4034c557c13054dcfb6ed425ca996b0c5363f6
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452388"
---
# <a name="introduction-to-microsoftdatasqlclient-namespace"></a>Microsoft.Data.SqlClient 命名空間簡介

![Download-DownArrow-Circled](../../ssdt/media/download.png)[下載 ADO.NET](../sql-connection-libraries.md#anchor-20-drivers-relational-access)

此頁面說明 SqlClient 命名空間如何透過現有的 SqlClient 命名空間提供額外的功能。
  
## <a name="release-notes"></a>版本資訊
所有版本資訊都可在[GitHub 存放庫](https://github.com/dotnet/SqlClient/tree/master/release-notes)中取得。

## <a name="new-features"></a>新增功能

### <a name="new-features-over-net-framework-472-systemdatasqlclient"></a>.NET Framework 4.7.2 的新功能 SqlClient。

資料分類-自 CTP 2.0 開始，Azure SQL Database 和 Microsoft SQL Server 2019 中提供。

UTF-8 支援-自 CTP 2.3 開始，Microsoft SQL Server SQL Server 2019 中提供。

### <a name="new-features-over-net-core-22-systemdatasqlclient"></a>.NET Core 2.2 SqlClient 的新功能。

資料分類-自 CTP 2.0 開始，Azure SQL Database 和 Microsoft SQL Server 2019 中提供。

UTF-8 支援-自 CTP 2.3 開始，Microsoft SQL Server SQL Server 2019 中提供。

具有記憶體保護區 Always Encrypted 的 Always Encrypted 可在 Microsoft SQL Server 2016 和更新版本中使用。 Microsoft Sql Server 2019 CTP 2.0 中引進了記憶體保護區支援。

驗證-Active Directory 密碼驗證模式。

### <a name="data-classification"></a>資料分類

資料分類會提供一組新的 Api，以公開唯讀資料敏感度，以及當基礎來源支援此功能時，透過 SqlDataReader 取得之物件的分類資訊，並包含有關[資料敏感度和的中繼資料。分類](../../relational-databases/security/sql-data-discovery-and-classification.md)。

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

UTF-8 支援不需要任何應用程式代碼變更。 這些 SqlClient 變更只會在伺服器支援 UTF-8 且基礎資料行定序為 UTF-8 時，將用戶端與伺服器之間的通訊優化。 如[SQL Server 2019 preview 的新功能](../../sql-server/what-s-new-in-sql-server-ver15.md)，請參閱 utf-8 一節。

### <a name="always-encrypted-with-enclaves"></a>一律使用記憶體保護區加密

一般來說，使用 SqlClient on .NET Framework**和內建資料行主要金鑰存放區提供者**的現有檔，現在也應該使用 .net Core。

 [搭配使用 Always Encrypted 與 .NET Framework Data Provider 進行開發](../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)

 [Always Encrypted：保護機密資料，並將加密金鑰儲存在 Windows 憑證存放區中](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

### <a name="authentication"></a>驗證

您可以使用 [_驗證_連接字串] 選項來指定不同的驗證模式。 如需詳細資訊，請參閱[SqlAuthenticationMethod 的檔](https://docs.microsoft.com/dotnet/api/system.data.sqlclient.sqlauthenticationmethod?view=netframework-4.7.2)。

> [!NOTE]
> 自訂金鑰存放區提供者（如 Azure Key Vault 提供者）將需要更新，以支援 SqlClient。 同樣地，記憶體保護區提供者也必須更新以支援 SqlClient。
> 只有 .NET Framework 和 .NET Core 目標支援 Always Encrypted。 不支援 .NET Standard，因為 .NET Standard 遺失某些加密相依性。
