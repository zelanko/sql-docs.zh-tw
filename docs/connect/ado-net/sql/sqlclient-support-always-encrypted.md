---
title: 搭配使用 Always Encrypted 與 SqlClient
description: 了解如何使用 Microsoft.Data.SqlClient 和 Always Encrypted 開發應用程式，以確保資料安全。
ms.date: 07/09/2020
ms.assetid: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: cheenamalhotra
ms.author: v-chmalh
ms.reviewer: v-kaywon
ms.openlocfilehash: a15c888abefba554bb4170039eea23988a6615fd
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725659"
---
# <a name="using-always-encrypted-with-the-microsoft-net-data-provider-for-sql-server"></a>搭配 Microsoft .NET Data Provider for SQL Server 使用 Always Encrypted

[!INCLUDE[appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-xxxx-md.md)]

此文章提供如何使用 [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) 或[具有安全記憶體保護區的 Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-enclaves.md) 與 [**Microsoft .NET Data Provider for SQL Server**](../microsoft-ado-net-sql-server.md) 來開發 .NET 應用程式的相關資訊。

[永遠加密] 可讓用戶端應用程式加密敏感性資料，且永遠不會顯示資料或 SQL Server 或 Azure SQL Database 的加密金鑰。 已啟用 Always Encrypted 的驅動程式 (例如 **Microsoft .NET Data Provider for SQL Server**) 會在用戶端應用程式中明確地加密及解密敏感性資料，以達成此目的。 驅動程式會自動判斷哪一個查詢參數對應至敏感性資料庫資料行 (使用 [永遠加密] 保護)，然後加密這些參數值後再將資料傳遞至 SQL Server 或 Azure SQL Database。 同樣地，驅動程式會以清晰簡明的方式，將擷取自查詢結果的加密資料庫資料行資料進行解密。 如需詳細資訊，請參閱[使用 Always Encrypted 開發應用程式](../../../relational-databases/security/encryption/always-encrypted-client-development.md)和[使用 Always Encrypted 搭配安全記憶體保護區開發應用程式](../../../relational-databases/security/encryption/always-encrypted-enclaves-client-development.md)。

## <a name="prerequisites"></a>Prerequisites

- 在資料庫中設定永遠加密。 這牽涉到佈建永遠加密金鑰，以及設定加密所選資料庫資料行。 如果您的資料庫尚未設定 Always Encrypted，請遵循 [Always Encrypted 入門](../../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)中的指示。
- 確定已在您的開發電腦上安裝必要的 .NET 平台。 透過 [Microsoft.Data.SqlClient](../microsoft-ado-net-sql-server.md)，.NET Framework 和 .NET Core 都支援 Always Encrypted 功能。 您需要確定已將 [.NET Framework 4.6](/dotnet/framework/) \(部分機器翻譯\) 或更新版本或是 [.NET Core 2.1](/dotnet/core/) \(部分機器翻譯\) 或更新版本設定為開發環境中的目標 .NET 平台版本。 如果您使用的是 Visual Studio，請參閱 [Framework 目標概觀](/visualstudio/ide/visual-studio-multi-targeting-overview) \(部分機器翻譯\)。

## <a name="enabling-always-encrypted-for-application-queries"></a>為應用程式查詢啟用 [永遠加密]

若要對以加密資料行為目標的參數進行加密，以及對查詢結果進行解密，最簡單的方式是將 `Column Encryption Setting` 連接字串關鍵字的值設定為 **enabled**。

可啟用永遠加密的連接字串範例如下：

```cs
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true; Column Encryption Setting=enabled";
SqlConnection connection = new SqlConnection(connectionString);
```

下列則為使用 SqlConnectionStringBuilder.ColumnEncryptionSetting 屬性的對等範例。

```cs
SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
builder.DataSource = "server63";
builder.InitialCatalog = "Clinic";
builder.IntegratedSecurity = true;
builder.ColumnEncryptionSetting = SqlConnectionColumnEncryptionSetting.Enabled;
SqlConnection connection = new SqlConnection(builder.ConnectionString);
connection.Open();
```

個別查詢也可以啟用 [永遠加密]。 請參閱以下的**控制 Always Encrypted 的效能影響**一節。
啟用 Always Encrypted 並不足以保證加密或解密成功。 您還需要確定︰

- 應用程式要有 [檢視任何資料行的主要金鑰定義]  和 [檢視任何資料行的加密金鑰定義]  資料庫權限，才能存取資料庫中永遠加密金鑰的相關中繼資料。 如需詳細資料，請參閱 [Always Encrypted (資料庫引擎) 中的「資料庫權限」一節](../../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)。
- 應用程式可以存取保護資料行加密金鑰的資料行主要金鑰，這些加密金鑰會加密查詢的資料庫資料行。

## <a name="enabling-always-encrypted-with-secure-enclaves"></a>啟用具有安全記憶體保護區的 Always Encrypted

從 Microsoft.Data.SqlClient 1.1.0 版開始，驅動程式支援[具有安全記憶體保護區的 Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-enclaves.md)。

若要在連線至 [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] 或更新版本時使用記憶體保護區，您需要設定應用程式，以啟用記憶體保護區計算和記憶體保護區證明。

如需記憶體保護區計算和記憶體保護區證明中用戶端驅動程式角色的一般資訊，請參閱[使用安全記憶體保護區的 Always Encrypted 開發應用程式](../../../relational-databases/security/encryption/always-encrypted-enclaves-client-development.md)。

設定您的應用程式：

1. 確定已將您的 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 執行個體設定為記憶體保護區類型 (請參閱[設定 Always Encrypted 伺服器設定選項的記憶體保護區類型](../../../database-engine/configure-windows/configure-column-encryption-enclave-type.md))。 [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] 支援 VBS 記憶體保護區類型和[主機守護者服務](/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-setting-up-the-host-guardian-service-hgs) \(部分機器翻譯\) 以進行證明。
2. 將連接字串中的 `Enclave Attestation URL` 關鍵字設定為證明端點，以針對應用程式到資料庫的連線啟用記憶體保護區計算。 關鍵字的值應設定為您環境中所設定的 HGS 伺服器證明端點。
3. 藉由在連接字串中設定 `Attestation Protocol` 關鍵字，來提供要使用的證明通訊協定。 此關鍵字的值應設定為 "HGS"。

如需逐步教學課程，請參閱[教學課程：使用具有安全記憶體保護區的 Always Encrypted 開發 .NET 應用程式](tutorial-always-encrypted-enclaves-develop-net-apps.md)。

> [!NOTE]
> 只有 Windows 支援具有安全記憶體保護區的 Always Encrypted。

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>擷取和修改加密資料行中的資料

一旦針對應用程式查詢啟用 Always Encrypted 之後，您就可以使用標準的 SqlClient API (請參閱[在 ADO.NET 中擷取和修改資料](/dotnet/framework/data/adonet/retrieving-and-modifying-data) \(部分機器翻譯\)) 或 [Microsoft.Data.SqlClient 命名空間](/dotnet/api/microsoft.data.sqlclient) \(英文\) 中定義的 [**Microsoft .NET Data Provider for SQL Server**](index.md) API，來擷取或修改加密資料庫資料行中的資料。 假設您的應用程式具有必要的資料庫權限，而且可以存取資料行主要金鑰，則 **Microsoft .NET Data Provider for SQL Server** 將加密所有以加密資料行為目標的查詢參數，並將解密擷取自加密資料行的資料，以傳回 .NET 類型的純文字值，其對應到為資料庫結構描述中之資料行所設定的 SQL Server 資料類型。
若未啟用 Always Encrypted，使用目標加密資料行參數的查詢就會失敗。 只要查詢沒有以加密資料行為目標的參數，查詢就仍然可以從加密資料行擷取資料。 不過，**Microsoft .NET Data Provider for SQL Server** 將不會嘗試解密所有擷取自加密資料行的值，而應用程式將會接收二進位的加密資料 (作為位元組陣列)。

下表摘要說明查詢的行為，視 Always Encrypted 是否啟用而定：

|查詢特性 | Always Encrypted 已啟用，且應用程式可以存取金鑰和金鑰中繼資料|Always Encrypted 已啟用，且應用程式可以存取金鑰或金鑰中繼資料 | [永遠加密] 已停用|
|:---|:---|:---|:---|
| 有以加密資料行為目標之參數的查詢。 | 以清晰簡明的方式加密參數值。 | 錯誤 | 錯誤 |
| 查詢從加密的資料行擷取資料，沒有任何以加密資料行為目標的參數。 | 以清晰簡明的方式解密來自加密資料行的結果。 應用程式會接收 .NET 資料類型的純文字值，其對應到為加密資料行所設定的 SQL Server 類型。 | 錯誤 | 不會解密來自加密資料行的結果。 應用程式收到位元組陣列 (byte[]) 形態的加密值。 |

以下範例將說明擷取和修改加密資料行中的資料。 這些範例假設目標資料表具有下列結構描述。 SSN 和 BirthDate 資料行均已加密。

```sql
CREATE TABLE [dbo].[Patients]([PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

### <a name="inserting-data-example"></a>插入資料範例

本例會將資料列插入病患資料表。 請注意：

- 範例程式碼中沒有任何需要加密的特定項目。 **Microsoft .NET Data Provider for SQL Server** 會自動偵測並加密以加密資料行為目標的 `paramSSN` 和 `paramBirthdate` 參數。 這讓加密對應用程式變得透明化。
- 插入至資料庫資料行的值，包括加密的資料行，會傳遞為 [SqlParameter](/dotnet/api/microsoft.data.sqlclient.sqlparameter) 物件。 雖然將值傳送到未加密的資料行時，使用 **SqlParameter** 為選擇性 (但強烈建議使用，因有利於防止 SQL 插入式攻擊)，但對以加密資料行為目標的值為必要。 如果將插入 SSN 或 BirthDate 資料行的值當作內嵌於查詢陳述式中的常值來傳遞，查詢就會失敗，因為 **Microsoft .NET Data Provider for SQL Server** 無法判斷目標加密資料行的值，所以不會加密值。 結果，伺服器會因與加密資料行不相容而拒絕它們。
- 設定為 ANSI (非 Unicode) 字串，以 SSN 資料行為目標的參數資料類型，會對應到 char/varchar SQL Server 資料類型。 如果參數類型先前設為 Unicode 字串 (String)，並對應至 nchar/nvarchar，則查詢會失敗，因為 Always Encrypted 不支援從已加密 nchar/nvarchar 值轉換成已加密 char/varchar 值。 如需資料類型對應的相關資訊，請參閱 [SQL Server 資料型別對應](/dotnet/framework/data/adonet/sql-server-data-type-mappings) 。
- 使用 [SqlParameter.SqlDbType 屬性](/dotnet/api/microsoft.data.sqlclient.sqlparameter.sqldbtype) \(英文\)，明確地將插入 BirthDate 資料行的參數資料類型設定為目標 SQL Server 資料類型，而不依賴隱含地將 .NET 類型對應到使用 [SqlParameter.DbType 屬性](/dotnet/api/microsoft.data.sqlclient.sqlparameter.dbtype) \(英文\) 時所套用的 SQL Server 資料類型。 [DateTime 結構](/dotnet/api/system.datetime) \(部分機器翻譯\) 預設會對應到日期時間 SQL Server 資料類型。 因為 BirthDate 資料行的資料類型是日期，且 [永遠加密] 不支援將加密的日期時間值轉換成加密的日期值，所以使用預設的對應會造成錯誤。

```cs
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true; Column Encryption Setting=enabled";

using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
using (SqlCommand cmd = connection.CreateCommand())
{
    connection.Open();
    cmd.CommandText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

    SqlParameter paramSSN = cmd.CreateParameter();
    paramSSN.ParameterName = @"@SSN";
    paramSSN.DbType = DbType.AnsiStringFixedLength;
    paramSSN.Direction = ParameterDirection.Input;
    paramSSN.Value = "795-73-9838";
    paramSSN.Size = 11;
    cmd.Parameters.Add(paramSSN);

    SqlParameter paramFirstName = cmd.CreateParameter();
    paramFirstName.ParameterName = @"@FirstName";
    paramFirstName.DbType = DbType.String;
    paramFirstName.Direction = ParameterDirection.Input;
    paramFirstName.Value = "Catherine";
    paramFirstName.Size = 50;
    cmd.Parameters.Add(paramFirstName);

    SqlParameter paramLastName = cmd.CreateParameter();
    paramLastName.ParameterName = @"@LastName";
    paramLastName.DbType = DbType.String;
    paramLastName.Direction = ParameterDirection.Input;
    paramLastName.Value = "Abel";
    paramLastName.Size = 50;
    cmd.Parameters.Add(paramLastName);

    SqlParameter paramBirthdate = cmd.CreateParameter();
    paramBirthdate.ParameterName = @"@BirthDate";
    paramBirthdate.SqlDbType = SqlDbType.Date;
    paramBirthdate.Direction = ParameterDirection.Input;
    paramBirthdate.Value = new DateTime(1996, 09, 10);
    cmd.Parameters.Add(paramBirthdate);

    cmd.ExecuteNonQuery();
}
```

### <a name="retrieving-plaintext-data-example"></a>擷取純文字資料範例

下列範例會示範根據加密值篩選資料，以及從加密資料行擷取純文字資料。 請注意：

- WHERE 子句中用來篩選 SSN 資料行的值需要使用 SqlParameter 來傳遞，如此一來，**Microsoft .NET Data Provider for SQL Server** 就能明確地加密它，然後再將它傳送到資料庫。
- 此程式將以純文字形式列印所有值，因為 **Microsoft .NET Data Provider for SQL Server** 會明確地解密擷取自 SSN 和 BirthDate 資料行的資料。

> [!NOTE]
> 如果使用具確定性的加密來進行加密，則查詢可執行資料行的相等比較。 如需詳細資訊，請參閱[選取確定性或隨機化加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)。

```cs
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true; Column Encryption Setting=enabled";
using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
using (SqlCommand cmd = connection.CreateCommand())
{
    connection.Open();
    cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN=@SSN";

    SqlParameter paramSSN = cmd.CreateParameter();
    paramSSN.ParameterName = @"@SSN";
    paramSSN.DbType = DbType.AnsiStringFixedLength;
    paramSSN.Direction = ParameterDirection.Input;
    paramSSN.Value = "795-73-9838";
    paramSSN.Size = 11;
    cmd.Parameters.Add(paramSSN);
    using (SqlDataReader reader = cmd.ExecuteReader())
    {
        if (reader.HasRows)
        {
            while (reader.Read())
            {
                Console.WriteLine(@"{0}, {1}, {2}, {3}", reader[0], reader[1], reader[2], ((DateTime)reader[3]).ToShortDateString());
            }
        }
    }
}
```

### <a name="retrieving-encrypted-data-example"></a>擷取加密的資料範例

如未啟用 [永遠加密]，只要查詢沒有以加密資料行為目標的參數，查詢就仍然可以從加密資料行擷取資料。

下例會示範如何從加密資料行擷取二進位的加密資料。 請注意：

- 因為連接字串未啟用 [永遠加密]，所以查詢會以位元組陣列 (程式會將值轉換為字串) 傳回加密的 SSN 和 BirthDate 值。
- 從加密資料行擷取資料但停用 [永遠加密] 的查詢可以有參數，只要沒有任何參數以加密資料行為目標。 上述依 LastName 篩選的查詢，在資料庫中未加密。 如果依 SSN 或 BirthDate 篩選查詢，查詢會失敗。

```cs
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true";

using (SqlConnection connection = new SqlConnection(connectionString))
using (SqlCommand cmd = connection.CreateCommand())
{
    connection.Open();
    cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName]=@LastName";

    SqlParameter paramLastName = cmd.CreateParameter();
    paramLastName.ParameterName = @"@LastName";
    paramLastName.DbType = DbType.String;
    paramLastName.Direction = ParameterDirection.Input;
    paramLastName.Value = "Abel";
    paramLastName.Size = 50;
    cmd.Parameters.Add(paramLastName);
    using (SqlDataReader reader = cmd.ExecuteReader())
    {
        if (reader.HasRows)
        {
            while (reader.Read())
            {
                Console.WriteLine(@"{0}, {1}, {2}, {3}", BitConverter.ToString((byte[])reader[0]), reader[1], reader[2], BitConverter.ToString((byte[])reader[3]));
            }
        }
    }
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>避免常見的加密資料行查詢問題

本節說明從 .NET 應用程式查詢加密資料行時常見的錯誤類別，以及如何避免的一些指導方針。

### <a name="unsupported-data-type-conversion-errors"></a>不支援的資料類型轉換錯誤

[永遠加密] 支援極少數的加密資料類型轉換。 如需支援的類型轉換詳細清單，請參閱 [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)。 請執行下列作業以免發生資料型別轉換錯誤︰

- 設定以加密資料行為目標的參數類型，如此一來，參數的 SQL Server 資料類型就會與目標資料行的類型完全相同，或是支援將參數的 SQL Server 資料類型轉換成資料行的目標類型。 您可以使用 SqlParameter.SqlDbType 屬性，強制執行 .NET 資料類型到特定 SQL Server 資料類型的必要對應。
- 確認小數和數值 SQL Server 資料類型資料行為目標之參數的有效位數和小數位數，和為目標資料行設定的有效位數和小數位數相同。  
- 確認在修改目標資料行值的查詢中，以 datetime2、datetimeoffset 或時間 SQL Server 資料類型資料行為目標之參數的有效位數，不大於目標資料行的有效位數。  

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>因為傳送純文字，而不是傳送加密值所造成的錯誤。

任何以加密資料行為目標的值都需要在應用程式內加密。 嘗試對加密資料行插入/修改或以純文字值篩選，會造成類似下面的錯誤︰

```log
Microsoft.Data.SqlClient.SqlException (0x80131904): Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'CEK_Auto1', column_encryption_key_database_name = 'Clinic') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

若要避免這類錯誤，請確定︰

- (針對連接字串或特定查詢的 [SqlCommand](/dotnet/api/microsoft.data.sqlclient.sqlcommand) 物件) 以加密資料行為目標的應用程式查詢已啟用 [永遠加密]。
- 您可以使用 SqlParameter 傳送以加密資料行為目標的資料。 下列範例示範以常值/常數錯誤篩選加密資料行 (SSN) 的查詢 (而不是在 SqlParameter 物件內傳遞常值)。

```cs
using (SqlCommand cmd = connection.CreateCommand())
{
    cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = '795-73-9838'";
    cmd.ExecuteNonQuery();
}
```

## <a name="working-with-column-master-key-stores"></a>使用資料行主要金鑰存放區

若要加密參數值或解密查詢結果的資料，**Microsoft .NET Data Provider for SQL Server** 需要取得為目標資料行設定的資料行加密金鑰。 資料行加密金鑰是以加密形式存放在資料庫中繼資料。 每個資料行加密金鑰都有對應的資料行主要金鑰，主要金鑰是用於加密資料行加密金鑰。 資料庫中繼資料不儲存資料行主要金鑰，它只包含金鑰存放區的相關資訊，金鑰存放區包含特定的資料行主要金鑰以及金鑰在金鑰存放區中的位置。

為了取得資料行加密金鑰的純文字值，**Microsoft .NET Data Provider for SQL Server** 會先取得有關資料行加密金鑰及其對應資料行主要金鑰的中繼資料，然後使用中繼資料的資訊來連絡包含資料行主要金鑰的金鑰存放區，並將加密的資料行加密金鑰解密。 **Microsoft .NET Data Provider for SQL Server** 會使用資料行主要金鑰存放區提供者來與金鑰存放區通訊，這是衍生自 [SqlColumnEncryptionKeyStoreProvider 類別](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptionkeystoreprovider) \(英文\) 的類別執行個體。

取得資料行加密金鑰的程序︰

1. 若已針對查詢啟用 Always Encrypted，則當查詢具有參數時，**Microsoft .NET Data Provider for SQL Server** 就會明確呼叫 **sys.sp_describe_parameter_encryption**，來擷取以加密資料行為目標之參數的加密中繼資料。 針對查詢結果所包含的加密資料，SQL Server 會自動附加加密中繼資料。 資料行主要金鑰的資訊包括：
    - 套件金鑰存放區的金鑰存放區提供者名稱，而該存放區包含資料行主要金鑰。
    - 金鑰路徑，其指定金鑰存放區中資料行主要金鑰的位置。

    資料行加密金鑰的資訊包括：

    - 資料行加密金鑰的加密值。
    - 用來將資料行加密金鑰加密的演算法名稱。
2. **Microsoft .NET Data Provider for SQL Server** 會使用資料行主要金鑰存放區提供者的名稱，在內部資料結構中查閱提供者物件 (衍生自 SqlColumnEncryptionKeyStoreProvider 類別的類別執行個體)。
3. 若要將資料行加密金鑰解密，**Microsoft .NET Data Provider for SQL Server** 會呼叫 `SqlColumnEncryptionKeyStoreProvider.DecryptColumnEncryptionKey()` 方法，來傳遞資料行主要金鑰路徑、資料行加密金鑰的加密值及加密演算法的名稱，用以產生加密的資料行加密金鑰。

### <a name="using-built-in-column-master-key-store-providers"></a>使用內建資料行主要金鑰存放區提供者

**Microsoft .NET Data Provider for SQL Server** 隨附於下列內建資料行主要金鑰存放區提供者，它們都會以特定提供者名稱 (用以查閱提供者) 預先註冊。 只有 Windows 支援這些內建的金鑰存放區提供者。

| 類別 | 描述 | 提供者 (查閱) 名稱 | 平台 |
|:---|:---|:---|:---|
|[SqlColumnEncryptionCertificateStoreProvider 類別](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptioncertificatestoreprovider) | Windows 憑證存放區的提供者。 | MSSQL_CERTIFICATE_STORE | Windows |
|[SqlColumnEncryptionCngProvider 類別](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptioncngprovider) | 支援以下功能的金鑰存放區提供者：[Microsoft Cryptography API：新一代 (CNG) API](/windows/win32/seccng/cng-portal)。 一般而言，這類型的存放區是硬體安全性模組，可保護和管理數位金鑰，並提供密碼編譯處理的實體裝置。 | MSSQL_CNG_STORE | Windows |
| [SqlColumnEncryptionCspProvider 類別](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptioncspprovider) | 支援 [Microsoft Cryptography API (CAPI)](/windows/win32/seccrypto/cryptographic-service-providers)的金鑰存放區提供者。 一般而言，這類型的存放區是硬體安全性模組，可保護和管理數位金鑰，並提供密碼編譯處理的實體裝置。 | MSSQL_CSP_PROVIDER | Windows |

您不需進行任何應用程式程式碼變更，即可使用這些提供者，但請注意下列事項：

- 您 (或您的 DBA) 需要確認設定在資料行主要金鑰中繼資料的提供者名稱是否正確，且資料行主要金鑰路徑符合指定提供者有效的金鑰路徑格式。 建議您使用 SQL Server Management Studio 等工具設定金鑰，這樣在發出 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 陳述式時，會自動產生有效的提供者名稱和金鑰路徑。 如需詳細資訊，請參閱 [使用 SQL Server Management Studio 設定永遠加密](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md) 和 [使用 PowerShell 設定永遠加密](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)。
- 確定應用程式可以存取金鑰存放區中的金鑰。 這可能牽涉到授與應用程式金鑰和/或金鑰存放區的存取權 (視金鑰存放區而定)，或執行其他的金鑰存放區特定組態步驟。 例如，若要存取實作 CNG 或 CAPI 的金鑰存放區 (例如硬體安全性模組)，您需要確定應用程式電腦上已安裝存放區實作 CNG 或 CAPI 的程式庫。 如需詳細資料，請參閱[建立及儲存 Always Encrypted 的資料行主要金鑰](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

### <a name="using-the-azure-key-vault-provider"></a>使用 Azure Key Vault 提供者

Azure 金鑰保存庫是存放和管理永遠加密資料行主要金鑰的方便選項 (尤其是當應用程式裝載在 Azure 時)。 **Microsoft .NET Data Provider for SQL Server** 不包含適用於 Azure Key Vault 的內建資料行主要金鑰存放區提供者，但可以 NuGet 套件形式提供 ([Microsoft.Data.SqLClient.AlwaysEncrypted.AzureKeyVaultProvider](https://www.nuget.org/packages/Microsoft.Data.SqlClient.AlwaysEncrypted.AzureKeyVaultProvider))，讓您輕鬆整合應用程式。 如需詳細資訊，請參閱 [一律加密 - 透過資料加密並將您的加密金鑰儲存在 Azure 金鑰保存庫，來保護 SQL Database 中的機密資料](/azure/azure-sql/database/always-encrypted-azure-key-vault-configure)。

| 類別 | 描述 | 提供者 (查閱) 名稱 | 平台 |
|:---|:---|:---|:---|
|[SqlColumnEncryptionAzureKeyVaultProvider 類別](/dotnet/api/microsoft.data.sqlclient.alwaysencrypted.azurekeyvaultprovider.sqlcolumnencryptionazurekeyvaultprovider) (英文) | Azure Key Vault 的提供者。 | AZURE_KEY_VAULT | Windows、Linux、macOS |

如需示範如何使用 Azure Key Vault 執行加密/解密的範例，請參閱[使用 Always Encrypted 的 Azure Key Vault](azure-key-vault-example.md) 和[使用具有安全記憶體保護區的 Always Encrypted 的 Azure Key Vault](azure-key-vault-enclave-example.md)。

### <a name="implementing-a-custom-column-master-key-store-provider"></a>實作自訂資料行主要金鑰存放區提供者

如果您想要將資料行主要金鑰儲存於現有提供者不支援的金鑰存放區，您可以擴充 [SqlColumnEncryptionCngProvider 類別](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptioncngprovider) \(英文\)，並使用 [SqlConnection.RegisterColumnEncryptionKeyStoreProviders](/dotnet/api/microsoft.data.sqlclient.sqlconnection.registercolumnencryptionkeystoreproviders) \(英文\) 方法來註冊提供者，以實作自訂提供者。

```cs
public class MyCustomKeyStoreProvider : SqlColumnEncryptionKeyStoreProvider
{
    public override byte[] EncryptColumnEncryptionKey(string masterKeyPath, string encryptionAlgorithm, byte[] columnEncryptionKey)
    {
        // Logic for encrypting a column encrypted key.
    }
    public override byte[] DecryptColumnEncryptionKey(string masterKeyPath, string encryptionAlgorithm, byte[] EncryptedColumnEncryptionKey)
    {
        // Logic for decrypting a column encrypted key.
    }
}  
class Program
{
    static void Main(string[] args)
    {
        Dictionary\<string, SqlColumnEncryptionKeyStoreProvider> providers =
            new Dictionary\<string, SqlColumnEncryptionKeyStoreProvider>();
        providers.Add("MY_CUSTOM_STORE", customProvider);
        SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        providers.Add(SqlColumnEncryptionCertificateStoreProvider.ProviderName, customProvider);
        SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        // ...
    }
}
```

### <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>使用資料行主要金鑰存放區提供者以程式設計方式佈建金鑰

存取加密的資料行時，**Microsoft .NET Data Provider for SQL Server** 會明確地尋找並呼叫正確的資料行主要金鑰存放區提供者，來解密資料行加密金鑰。 一般來說，一般應用程式程式碼不會直接呼叫資料行主要金鑰存放區提供者。 但是您可以明確具現化和呼叫提供者，以程式設計方式佈建和管理永遠加密金鑰︰產生加密的資料行加密金鑰和解密資料行加密金鑰 (例如作為部分資料行主要金鑰輪替)。 如需詳細資訊，請參閱 [Always Encrypted 的金鑰管理概觀](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。
只有使用自訂的金鑰存放區提供者時，才可能需要實作您自己的金鑰管理工具。 使用存放在金鑰存放區的金鑰時，凡是有內建提供者或位在 Azure 金鑰保存庫者，皆可使用 SQL Server Management Studio 或 PowerShell 等現有的工具，來管理和佈建金鑰。
下列範例示範如何產生資料行加密金鑰，以及使用 [SqlColumnEncryptionCertificateStoreProvider 類別](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptioncertificatestoreprovider) \(英文\)，利用憑證來加密金鑰。

```cs
using System.Security.Cryptography;
static void Main(string[] args)
{
    byte[] EncryptedColumnEncryptionKey = GetEncryptedColumnEncryptonKey();
    Console.WriteLine("0x" + BitConverter.ToString(EncryptedColumnEncryptionKey).Replace("-", ""));
    Console.ReadKey();
}

static byte[]  GetEncryptedColumnEncryptonKey()
{
    int cekLength = 32;
    String certificateStoreLocation = "CurrentUser";
    String certificateThumbprint = "698C7F8E21B2158E9AED4978ADB147CF66574180";
    // Generate the plaintext column encryption key.
    byte[] columnEncryptionKey = new byte[cekLength];
    RNGCryptoServiceProvider rngCsp = new RNGCryptoServiceProvider();
    rngCsp.GetBytes(columnEncryptionKey);

    // Encrypt the column encryption key with a certificate.
    string keyPath = String.Format(@"{0}/My/{1}", certificateStoreLocation, certificateThumbprint);
    SqlColumnEncryptionCertificateStoreProvider provider = new SqlColumnEncryptionCertificateStoreProvider();
    return provider.EncryptColumnEncryptionKey(keyPath, @"RSA_OAEP", columnEncryptionKey);
}
```

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>控制 Always Encrypted 的效能影響

由於 Always Encrypted 是一項用戶端加密技術，因此，所觀察到的效能額外負荷大部分都是在用戶端，而非資料庫中。 除了加密和解密作業成本之外，用戶端上效能額外負荷的其他來源如下：

- 額外反覆存取資料庫以擷取查詢參數的中繼資料。
- 呼叫資料行主要金鑰存放區以存取資料行主要金鑰。

此節描述 **Microsoft .NET Data Provider for SQL Server** 的內建效能最佳化，以及如何控制上述兩個因素對效能的影響。

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>控制反覆存取以擷取查詢參數的中繼資料

如果已針對連線啟用 Always Encrypted，**Microsoft .NET Data Provider for SQL Server** 預設將針對每個參數化查詢呼叫 [sys.sp_describe_parameter_encryption](../../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)，以將查詢陳述式 (不含任何參數值) 傳遞至 SQL Server。 **sys.sp_describe_parameter_encryption** 會分析查詢陳述式，以找出是否有任何參數需要加密；如果有，則會對每個需要加密的參數傳回加密相關資訊，讓 **Microsoft .NET Data Provider for SQL Server** 能夠加密參數值。 上述行為可對用戶端應用程式確保高透明度。 只要在 SqlParameter 物件中將以加密資料行為目標的值傳遞至 **Microsoft .NET Data Provider for SQL Server**，應用程式 (及應用程式開發人員) 就不需要留意哪些查詢會存取加密資料行。

### <a name="query-metadata-caching"></a>查詢中繼資料快取

**Microsoft .NET Data Provider for SQL Server** 會快取每個查詢陳述式的 **sys.sp_describe_parameter_encryption** 結果。 因此，如果執行多次相同的查詢陳述式，驅動程式就只會呼叫一次 **sys.sp_describe_parameter_encryption** 。 查詢陳述式的加密中繼資料快取大幅減少了從資料庫擷取中繼資料的效能成本。 預設啟用快取。 您可以透過將 [SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled 屬性](/dotnet/api/microsoft.data.sqlclient.sqlconnection.columnencryptionquerymetadatacacheenabled) \(英文\) 設定為 false，以停用參數中繼資料快取，但除非是諸如以下所述的罕見情況，否則不建議這樣做：

請考慮有後列兩個不同結構描述的資料庫︰s1 和 s2。 每個結構描述都有一份同名的資料表︰t。 s1.t 和 s2.t 資料表的定義是相同的，除了與加密相關的屬性：名為 c 的資料行在 s1.t 中並未加密，但在 s2.t 中則會加密。 資料庫有兩位使用者︰u1 和 u2。 u1 使用者的預設結構描述是 s1。 u2 的預設結構描述是 s2。 .NET 應用程式會開啟兩個資料庫連線，模擬 u1 使用者在一個連線，而 u2 使用者在另一個連線。 應用程式在使用者 u1 的連線上傳送具有以 c 資料行為目標之參數的查詢 (此查詢並未指定結構描述，因此假設使用預設的使用者結構描述)。 接下來，應用程式在 u2 使用者的連線上傳送相同的查詢。 如果已啟用查詢中繼資料快取，則在第一次查詢後，將會在快取中填入指出 c 資料行 (查詢參數的目標) 並未加密的中繼資料。 當第二次查詢有相同的查詢陳述式時，就會使用儲存在快取中的資訊。 結果，驅動程式傳送查詢時不會加密參數 (這是不正確的，因為目標資料行 s2.t.c 有加密)，將參數的純文字值洩漏給伺服器。 伺服器會偵測到不相容，並強制驅動程式重新整理快取，因此應用程式會明確重新傳送具有正確加密參數值的查詢。 這種情況應該停用快取，以免向伺服器洩漏機密值。

### <a name="setting-always-encrypted-at-the-query-level"></a>在查詢層級設定 [永遠加密]

若要控制擷取加密中繼資料對參數化查詢的效能影響，您可以針對個別查詢啟用 Always Encrypted，而不是針對連線來設定它。 如此一來，您可以確保只有您知道有以加密資料行為目標之參數的查詢可以叫用 **sys.sp_describe_parameter_encryption** 。 不過請注意，如此一來就會降低加密的透明度︰如果您變更資料庫資料行的加密屬性，可能就需要變更應用程式的程式碼，以配合結構描述變更。

> [!NOTE]
> 在查詢層級設定 Always Encrypted，會限制參數加密中繼資料快取的效能優勢。

若要控制個別查詢的 [永遠加密] 行為，您需要使用 [SqlCommand](/dotnet/api/microsoft.data.sqlclient.sqlcommand) 和 [SqlCommandColumnEncryptionSetting](/dotnet/api/microsoft.data.sqlclient.sqlcommandcolumnencryptionsetting)的這個建構函式。 以下是一些實用的方針：

- 如果用戶端應用程式透過資料庫連接傳送的大多數查詢都會存取加密資料行：
  - 將**資料行加密設定**連接字串關鍵字設為 [啟用]  。
  - 對不會存取任何加密資料行的個別查詢設定 **SqlCommandColumnEncryptionSetting.Disabled** 。 這會停用呼叫 sys.sp_describe_parameter_encryption 以及嘗試解密結果集內的任何值。
  - 對沒有任何參數要求加密，但會從加密資料行擷取資料的個別查詢設定 **SqlCommandColumnEncryptionSetting.ResultSet** 。 這會停用呼叫 sys.sp_describe_parameter_encryption 和參數加密。 查詢將能夠解密來自加密資料行的結果。
- 如果用戶端應用程式透過資料庫連接傳送的大多數查詢都不會存取加密資料行：
  - 將**資料行加密設定**連接字串關鍵字設為 [停用]  。
  - 對有任何參數需要加密的個別查詢設定 **SqlCommandColumnEncryptionSetting.Enabled** 。 這可以呼叫 sys.sp_describe_parameter_encryption 以及解密擷取自加密資料行的任何查詢結果。
  - 對沒有任何參數要求加密，但會從加密資料行擷取資料的查詢設定 **SqlCommandColumnEncryptionSetting.ResultSet** 。 這會停用呼叫 sys.sp_describe_parameter_encryption 和參數加密。 查詢將能夠解密來自加密資料行的結果。

下例中，資料庫連接已停用 [永遠加密]。 應用程式發出的查詢具有以 LastName 資料行為目標的參數，而此資料行未加密。 查詢會從加密的 SSN 和 BirthDate 資料行擷取資料。 在這種情況下，不需要呼叫 sys.sp_describe_parameter_encryption 以擷取加密中繼資料。 不過，需要啟用查詢結果的解密，以使應用程式從兩個加密資料行接收純文字值。 SqlCommandColumnEncryptionSetting.ResultSet 設定就是用於確認此項。

```cs
string connectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true";
using (SqlConnection connection = new SqlConnection(connectionString))
using (SqlCommand cmd = new SqlCommand(@"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName]=@LastName",
connection, null, SqlCommandColumnEncryptionSetting.ResultSetOnly))
{
    connection.Open();
    SqlParameter paramLastName = cmd.CreateParameter();
    paramLastName.ParameterName = @"@LastName";
    paramLastName.DbType = DbType.String;
    paramLastName.Direction = ParameterDirection.Input;
    paramLastName.Value = "Abel";
    paramLastName.Size = 50;
    cmd.Parameters.Add(paramLastName);
    using (SqlDataReader reader = cmd.ExecuteReader())
    {
        if (reader.HasRows)
        {
            while (reader.Read())
            {
                Console.WriteLine(@"{0}, {1}, {2}, {3}", reader[0], reader[1], reader[2], ((DateTime)reader[3]).ToShortDateString());
            }
        }
    }
}
```

### <a name="column-encryption-key-caching"></a>資料行加密金鑰快取

為了減少呼叫資料行主要金鑰存放區來解密資料行加密金鑰的次數，**Microsoft .NET Data Provider for SQL Server** 會將純文字資料行加密金鑰快取於記憶體中。 從資料庫中繼資料中接收加密的資料行加密金鑰值之後，驅動程式會先嘗試尋找對應加密金鑰值的純文字資料行加密金鑰。 只有在快取中找不到加密的資料行加密金鑰值時，驅動程式才會呼叫包含資料行主要金鑰的金鑰存放區。

基於安全性考量，會在可設定的存留時間間隔之後收回快取項目。 預設的存留時間值是 2 小時。 如果您對於應用程式中以純文字快取的資料行加密金鑰存留時間有更嚴格的安全性需求，則可使用 [SqlConnection.ColumnEncryptionKeyCacheTtl 屬性](/dotnet/api/microsoft.data.sqlclient.sqlconnection.columnencryptionkeycachettl) \(英文\) 來變更它。 

## <a name="enabling-additional-protection-for-a-compromised-sql-server"></a>對遭入侵的 SQL Server 啟用額外保護

根據預設，***Microsoft .NET Data Provider for SQL Server*** 依賴資料庫系統 (SQL Server 或 Azure SQL Database) 提供有關資料庫中哪些資料行已加密及加密方法的中繼資料。 加密中繼資料可讓 **Microsoft .NET Data Provider for SQL Server** 加密查詢參數及解密查詢結果，而不需任何應用程式輸入，這可大幅降低需要在應用程式中進行變更的次數。 不過，如果 SQL Server 處理序遭到入侵，且攻擊者竄改了 SQL Server 傳送到 **Microsoft .NET Data Provider for SQL Server** 的中繼資料，該攻擊者或許就能竊取敏感性資訊。 本節描述針對此類攻擊提供多一層防護的 API，代價是降低透明度。

### <a name="forcing-parameter-encryption"></a>強制參數加密

**Microsoft .NET Data Provider for SQL Server** 在將參數化查詢傳送到 SQL Server 之前，會先要求 SQL Server (藉由呼叫 [sys.sp_describe_parameter_encryption](../../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)) 分析查詢陳述式，並提供查詢中哪些參數應該加密的相關資訊。 儘管資料庫的資料行已加密，但遭入侵的 SQL Server 執行個體可能會傳送指出參數並未以加密資料行為目標的中繼資料，而誤導了 **Microsoft .NET Data Provider for SQL Server**。 因此，**Microsoft .NET Data Provider for SQL Server** 可能不會加密參數值，並將其以純文字形式字傳送到遭入侵的 SQL Server 執行個體。

為避免這類的攻擊，應用程式可將參數的 [SqlParameter.ForceColumnEncryption 屬性](/dotnet/api/microsoft.data.sqlclient.sqlparameter.forcecolumnencryption) 設為 true。 如果 **Microsoft .NET Data Provider for SQL Server** 從伺服器接收到的中繼資料指出參數不需要加密，則這將導致它擲回例外狀況。

雖然使用 **SqlParameter.ForceColumnEncryption 屬性**有助於改善安全性，但也會降低對用戶端應用程式加密的透明度。 如果更新資料庫結構描述來變更加密的資料行集合，您可能也需要變更應用程式。

下列程式碼範例示範如何使用 **SqlParameter.ForceColumnEncryption 屬性**，來防止將社會安全號碼以純文字形式傳送到資料庫。

```cs
using (SqlCommand cmd = _sqlconn.CreateCommand())
{
    // Use parameterized queries to access Always Encrypted data.

    cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = @SSN;";

    SqlParameter paramSSN = cmd.CreateParameter();
    paramSSN.ParameterName = @"@SSN";
    paramSSN.DbType = DbType.AnsiStringFixedLength;
    paramSSN.Direction = ParameterDirection.Input;
    paramSSN.Value = ssn;
    paramSSN.Size = 11;
    paramSSN.ForceColumnEncryption = true;
    cmd.Parameters.Add(paramSSN);

    using (SqlDataReader reader = cmd.ExecuteReader())
    {
        // Do something.
    }
}
```

### <a name="configuring-trusted-column-master-key-paths"></a>設定受信任的資料行主要金鑰路徑

SQL Server 針對以加密資料行為目標的查詢參數及擷取自加密資料行的結果所傳回的加密中繼資料，包括識別金鑰存放區之資料行主要金鑰的金鑰路徑，以及金鑰存放區的金鑰位置。 如果 SQL Server 執行個體遭到入侵，它可能會傳送金鑰路徑，以將 **Microsoft .NET Data Provider for SQL Server** 導向到受攻擊者控制的位置。 如果金鑰存放區需要驗證應用程式，這可能會導致金鑰存放區認證洩漏。

為了避免此類攻擊，應用程式可以使用 [SqlConnection.ColumnEncryptionTrustedMasterKeyPaths 屬性](/dotnet/api/microsoft.data.sqlclient.sqlconnection.columnencryptiontrustedmasterkeypaths) \(英文\)，為指定的伺服器指定受信任的金鑰路徑清單。 如果 **Microsoft .NET Data Provider for SQL Server** 接收到受信任金鑰路徑清單以外的金鑰路徑，就會擲回例外狀況。

雖然設定受信任的金鑰路徑可改善應用程式安全性，但您每次變換資料行主要金鑰 (每次資料行主要金鑰路徑變更時) 時，都必須變更應用程式的程式碼和/或設定。

下例示範如何設定受信任的資料行主要金鑰路徑︰

```cs
// Configure trusted key paths to protect against fake key paths sent by a compromised SQL Server instance
// First, create a list of trusted key paths for your server
List<string> trustedKeyPathList = new List<string>();
trustedKeyPathList.Add("CurrentUser/my/425CFBB9DDDD081BB0061534CE6AB06CB5283F5Ea");

// Register the trusted key path list for your server
SqlConnection.ColumnEncryptionTrustedMasterKeyPaths.Add(serverName, trustedKeyPathList);

```

## <a name="copying-encrypted-data-using-sqlbulkcopy"></a>使用 SqlBulkCopy 複製加密的資料

使用 SqlBulkCopy，您可以將已加密並儲存在某份資料表的資料，複製到另一份資料表，而不需要解密資料。 若要這樣做：

- 請確定目標資料表的加密組態與來源資料表的組態完全一致。 特別是，這兩份資料表都必須加密相同的資料行，且這些資料行必須使用相同的加密類型和相同的加密金鑰來加密。 注意︰如果任一目標資料行的加密方式不同於其對應的來源資料行，您將無法在複製作業後，解密目標資料表中的資料。 資料會損毀。
- 設定這兩個資料庫對來源資料表和目標資料表的連線，但不啟用 Always Encrypted。
- 設定 `AllowEncryptedValueModifications` 選項 (請參閱 [SqlBulkCopyOptions](/dotnet/api/microsoft.data.sqlclient.sqlbulkcopyoptions) \(英文\))。

> [!NOTE]
> 指定 `AllowEncryptedValueModifications` 時請小心，這可能會導致資料庫損毀，因為 **Microsoft .NET Data Provider for SQL Server** 不會檢查資料是否確實加密，或者是否使用與目標資料行相同的加密類型、演算法和金鑰正確加密。

以下是將資料從某份資料表複製到另一份資料表的範例。 請注意，SSN 和 BirthDate 資料行預設均已加密。

```cs
static public void CopyTablesUsingBulk(string sourceTable, string targetTable)
{
    string sourceConnectionString = "Data Source=server63; Initial Catalog=Clinic; Integrated Security=true";
    string targetConnectionString = "Data Source= server64; Initial Catalog=Clinic; Integrated Security=true";
    using (SqlConnection connSource = new SqlConnection(sourceConnectionString))
    {
        connSource.Open();
        using (SqlCommand cmd = new SqlCommand(string.Format("SELECT [PatientID], [SSN], [FirstName], [LastName], [BirthDate] FROM {0}", sourceTable), connSource))
        {
            using (SqlDataReader reader = cmd.ExecuteReader())
            using (SqlBulkCopy copy = new SqlBulkCopy(targetConnectionString, SqlBulkCopyOptions.KeepIdentity | SqlBulkCopyOptions.AllowEncryptedValueModifications))
            {
                copy.EnableStreaming = true;
                copy.DestinationTableName = targetTable;
                copy.WriteToServer(reader);
            }
        }
    }
}
```

## <a name="always-encrypted-api-reference"></a>一律加密 API 參考

**命名空間：** [Microsoft.Data.SqlClient](/dotnet/api/microsoft.data.sqlclient)

**組件：** Microsoft.Data.SqlClient.dll

|名稱|描述|
|:---|:---|
|[SqlColumnEncryptionCertificateStoreProvider 類別](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptioncertificatestoreprovider)|Windows 憑證存放區的金鑰存放區提供者。|
|[SqlColumnEncryptionCngProvider 類別](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptioncngprovider)|Microsoft 密碼編譯 API 的金鑰存放區提供者：新一代 (CNG)。|
|[SqlColumnEncryptionCspProvider 類別](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptioncspprovider)|Microsoft CAPI 型密碼編譯服務提供者 (CSP) 的金鑰存放區提供者。|
|[SqlColumnEncryptionKeyStoreProvider 類別](/dotnet/api/microsoft.data.sqlclient.sqlcolumnencryptionkeystoreprovider)|金鑰存放區提供者的基底類別。|
|[SqlCommandColumnEncryptionSetting 列舉](/dotnet/api/microsoft.data.sqlclient.sqlcommandcolumnencryptionsetting)|讓資料庫連接得以加密和解密的設定。|
|[SqlConnectionColumnEncryptionSetting 列舉](/dotnet/api/microsoft.data.sqlclient.sqlconnectioncolumnencryptionsetting)|可對個別查詢控制永遠加密行為的設定。|
|[SqlConnectionStringBuilder.ColumnEncryptionSetting 屬性](/dotnet/api/microsoft.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting)|在連接字串中取得及設定 [永遠加密]。|
|[SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled 屬性](/dotnet/api/microsoft.data.sqlclient.sqlconnection.columnencryptionquerymetadatacacheenabled)|啟用和停用加密查詢中繼資料快取。|
|[SqlConnection.ColumnEncryptionKeyCacheTtl 屬性](/dotnet/api/microsoft.data.sqlclient.sqlconnection.columnencryptionkeycachettl)|取得及設定資料行加密金鑰快取項目的存留時間。|
|[SqlConnection.ColumnEncryptionTrustedMasterKeyPaths 屬性](/dotnet/api/microsoft.data.sqlclient.sqlconnection.columnencryptiontrustedmasterkeypaths)|可讓您為資料庫伺服器設定受信任的金鑰路徑清單。 如果驅動程式在處理應用程式查詢時，接收到不在清單上的金鑰路徑，則查詢會失敗。 此屬性會針對受到安全性攻擊危害的 SQL Server 提供額外的保護，此類 SQL Server 會提供假的金鑰路徑，而可能會導致遺漏金鑰存放區認證。|
|[SqlConnection.RegisterColumnEncryptionKeyStoreProviders 方法](/dotnet/api/microsoft.data.sqlclient.sqlconnection.registercolumnencryptionkeystoreproviders)|可讓您註冊自訂金鑰存放區提供者。 它是一個字典，會將金鑰存放區提供者名稱對應至金鑰存放區提供者實作。|
|[SqlCommand 建構函式 (String、SqlConnection、SqlTransaction、SqlCommandColumnEncryptionSetting)](/dotnet/api/microsoft.data.sqlclient.sqlcommand.-ctor?view=sqlclient-dotnet-core-1.0#Microsoft_Data_SqlClient_SqlCommand__ctor_System_String_Microsoft_Data_SqlClient_SqlConnection_Microsoft_Data_SqlClient_SqlTransaction_Microsoft_Data_SqlClient_SqlCommandColumnEncryptionSetting_)|可讓您對個別查詢控制永遠加密的行為。|
|[SqlParameter.ForceColumnEncryption 屬性](/dotnet/api/microsoft.data.sqlclient.sqlparameter.forcecolumnencryption)|強制將參數加密。 如果 SQL Server 向驅動程式告知參數不需要加密，使用該參數的查詢就會失敗。 此屬性會針對受到安全性攻擊危害的 SQL Server 提供額外的保護，此類 SQL Server 會將不正確的加密中繼資料提供給用戶端，而可能導致資料洩露。|
|[連接字串](/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring) \(英文\) 關鍵字：`Column Encryption Setting=enabled`|啟用或停用連線的永遠加密功能。|

## <a name="see-also"></a>另請參閱

- [一律加密](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [SQL Database 教學課程：透過 Always Encrypted 來保護敏感性資料](/azure/azure-sql/database/always-encrypted-certificate-store-configure)
- [教學課程：使用具有安全記憶體保護區的 Always Encrypted 開發 .NET 應用程式](tutorial-always-encrypted-enclaves-develop-net-apps.md)
- [範例：使用 Always Encrypted 的 Azure Key Vault](azure-key-vault-example.md)
- [範例：使用具有安全記憶體保護區的 Always Encrypted 的 Azure Key Vault](azure-key-vault-enclave-example.md)。