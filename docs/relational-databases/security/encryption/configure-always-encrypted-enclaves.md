---
title: 設定具有安全記憶體保護區的 Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 48580f2ca2e83a968f9599b98956c079f763bf71
ms.sourcegitcommit: 0acd84d0b22a264b3901fa968726f53ad7be815c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2018
ms.locfileid: "49307122"
---
# <a name="configure-always-encrypted-with-secure-enclaves"></a>設定具有安全記憶體保護區的 Always Encrypted
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves.md) 會擴充現有 [Always Encrypted](always-encrypted-database-engine.md) 功能，以啟用更豐富的敏感性資料功能，同時保持資料的機密性。

若要設定具有安全記憶體保護區的 Always Encrypted，請使用下列工作流程：

1. 設定主機守護者服務 (HGS) 證明。
2. 在 SQL Server 電腦上安裝 [!INCLUDE[sql-server-2019](..\..\..\includes\sssqlv15-md.md)]。
3. 在用戶端/開發電腦上安裝工具。
4. 在 SQL Server 執行個體中設定安全記憶體保護區類型。
5. 佈建已啟用記憶體保護區的金鑰。
6. 加密包含敏感性資料的資料行。

>[!NOTE]
>如需如何設定測試環境並在 SSMS 中嘗試具有安全記憶體保護區之 Always Encrypted 功能的逐步教學課程，請參閱[教學課程：使用 SSMS，開始使用具有安全記憶體保護區的 Always Encrypted](../tutorial-getting-started-with-always-encrypted-enclaves.md)。

## <a name="configure-your-environment"></a>設定環境

若要搭配使用安全記憶體保護區與 Always Encrypted，您的環境需要 Windows Server 2019 預覽、SQL Server Management Studio (SSMS) 18.0 (預覽)、.NET Framework 以及一些其他元件。 下列各節提供詳細資料和連結以取得必要元件。

### <a name="sql-server-computer-requirements"></a>SQL Server 電腦需求

執行 SQL Server 的電腦需要下列作業系統和 SQL Server 版本：

*SQL Server*：

- [!INCLUDE[sql-server-2019](..\..\..\includes\sssqlv15-md.md)] 或更新版本

*Windows*：

- Windows 10 企業版 1809 版
- Windows Server DataCenter (半年通道) 1809 版
- Windows Server 2019 DataCenter

> [!IMPORTANT]
> SQL Server 電腦必須設定為 HGS 所證明的受防護主機。 TPM 證明是生產環境的建議記憶體保護區證明方法，而且需要 SQL Server 在實體機器上執行，而不是在虛擬機器中執行。 虛擬機器僅適用於進入生產階段前環境。

### <a name="hgs-computer-requirements"></a>HGS 電腦需求

在測試和原型設計期間，單一 HGS 電腦就已經足夠。 在生產環境中，強烈建議具有 3 部電腦的 Windows 容錯移轉叢集。

Windows 主機守護者服務 (HGS) 必須安裝於不同的 HGS 電腦，而非與 SQL Server 相同的電腦。 如需 HGS 電腦需求和設定的詳細資料，請參閱[在 SQL Server 中設定 Always Encrypted 的主機守護者服務](https://docs.microsoft.com/windows-server/security/set-up-hgs-for-always-encrypted-in-sql-server)。


### <a name="determine-your-attestation-service-url"></a>判斷證明服務 URL

若要判斷證明服務 URL，您需要設定工具和應用程式：

1. 以系統管理員身分登入 SQL Server 電腦。
2. 以系統管理員身分執行 PowerShell。
3. 執行 [Get-HGSClientConfiguration](https://docs.microsoft.com/powershell/module/hgsclient/get-hgsclientconfiguration)。
4. 寫下並儲存 AttestationServerURL 屬性。 它看起來應該類似如下：`http://x.x.x.x/Attestation`。


### <a name="install-tools"></a>安裝工具

在用戶端/開發電腦上安裝下列工具：

1. [.NET Framework 4.7.2](https://www.microsoft.com/net/download/dotnet-framework-runtime)。
2. [SSMS 18.0 或更新版本](../../../ssms/download-sql-server-management-studio-ssms.md)。
3. [SQL Server PowerShell 模組](../../../powershell/download-sql-server-ps-module.md) 21.1 版或更新版本。
4. [Visual Studio (建議使用 2017 或更新版本)](https://visualstudio.microsoft.com/downloads/)。
5. [.NET Framework 4.7.2 開發人員套件](https://www.microsoft.com/net/download/visual-studio-sdks)。
6. [Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider NuGet 套件](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider) 2.2.0 版或更新版本。
7. [Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders NuGet 套件](https://www.nuget.org/packages?q=Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders)。

NuGet 套件要用於 Visual Studio 專案，以使用具有安全記憶體保護區的 Always Encrypted 來開發應用程式。 只有在您將資料行主要金鑰儲存至 Azure Key Vault 時，才需要第一個套件。 如需詳細資料，請參閱[開發應用程式](#develop-applications-issuing-rich-queries-in-visual-studio)。

### <a name="configure-a-secure-enclave"></a>設定安全記憶體保護區

在用戶端/開發電腦上：

1. 開啟 SSMS，並以 Active Directory (AD) 系統管理員身分連線至 SQL Server 執行個體。
2. 若要確認執行個體支援具有安全記憶體保護區的 Always Encrypted，請執行下列查詢：

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type'
   ```

    查詢應該會傳回一個資料列，它看起來如下所示：  

    | NAME                           | value | value_in_use |
    | ------------------------------ | ----- | -------------|
    | 資料行加密記憶體保護區類型 | 0     | 0            |

3. 將安全記憶體保護區類型設定為 VBS 記憶體保護區。

   ```sql
   EXEC sys.sp_configure 'column encryption enclave type', 1
   RECONFIGURE
   ```

4. 重新啟動您的 SQL Server 執行個體，先前的變更才會生效。 您可以在 SSMS 中重新啟動執行個體，方法是在 [物件總管] 中以滑鼠右鍵按一下它，然後選取 [重新啟動]。 執行個體重新啟動之後，請與它重新連線。

5. 執行下列查詢，確認現在已載入安全記憶體保護區：

   ```sql
   SELECT [name], [value], [value_in_use] FROM sys.configurations
   WHERE [name] = 'column encryption enclave type'
   ```   

    查詢應該會傳回一個資料列，它看起來如下所示：  

    | NAME                           | value | value_in_use |
    | ------------------------------ | ----- | -------------- |
    | 資料行加密記憶體保護區類型 | 1     | 1              |

6. 若要啟用對加密資料行的豐富計算，請執行下列查詢：

   ```sql
   DBCC traceon(127,-1)
   ```

    > [!NOTE]
    > 根據預設，會在 [!INCLUDE[sql-server-2019](..\..\..\includes\sssqlv15-md.md)] 中停用豐富計算。 每次重新啟動 SQL Server 執行個體之後，需要使用上述陳述式予以啟用。

## <a name="provision-enclave-enabled-keys"></a>佈建已啟用記憶體保護區的金鑰

引進已啟用記憶體保護區的金鑰基本上不會變更 [Always Encrypted 金鑰佈建和金鑰管理工作流程](overview-of-key-management-for-always-encrypted.md)。 唯一的變更是在資料行主要金鑰佈建工作流程中，即您現在可以將金鑰標示為已啟用記憶體保護區 (根據預設，資料行主要金鑰未啟用記憶體保護區)。 當您指定要已啟用記憶體保護區的新資料行主要金鑰 (使用 SSMS 或 PowerShell) 時，會發生下列情況：

- 設定資料庫資料行主要金鑰中繼資料中的 **ENCLAVE_COMPUTATIONS** 屬性。
- 資料行主要金鑰屬性值 (包含 **ENCLAVE_COMPUTATIONS** 設定) 經數位簽署。 此工具會將使用實際資料行主要金鑰所產生的簽章新增至中繼資料。 簽章的目的是要防止惡意 DBA 和電腦管理員竄改 **ENCLAVE_COMPUTATIONS** 設定。 SQL 用戶端驅動程式會先驗證簽章，才允許使用記憶體保護區。 這可讓安全性系統管理員控制在記憶體保護區內計算哪些資料行資料。

資料行主要金鑰的 **ENCLAVE_COMPUTATIONS** 屬性是不變的；金鑰在佈建之後就無法變更。 不過，您可以透過稱為[資料行主要金鑰輪替](#initiate-the-rotation-from-the-current-column-master-key-to-the-new-column-master-key)的程序，將資料行主要金鑰取代為其 **ENCLAVE_COMPUTATIONS** 屬性值與原始金鑰不同的新金鑰。 如需 **ENCLAVE_COMPUTATIONS** 屬性的詳細資訊，請參閱 [CREATE COLUMN MASTER KEY](../../../t-sql/statements/create-column-master-key-transact-sql.md)。

若要佈建已啟用記憶體保護區的資料行加密金鑰，您需要確定加密資料行加密金鑰的資料行主要金鑰已啟用記憶體保護區。

下列限制目前適用於佈建已啟用記憶體保護區的金鑰：

- 已啟用記憶體保護區的**資料行主要金鑰必須儲存至 Windows 憑證存放區或 Azure Key Vault**。 目前不支援將已啟用記憶體保護區的資料行主要金鑰儲存至其他類型金鑰存放區 (硬體安全性模組或自訂金鑰存放區)。

### <a name="provision-enclave-enabled-keys-using-sql-server-management-studio-ssms"></a>**使用 SQL Server Management Studio (SSMS) 佈建已啟用記憶體保護區的金鑰**

下列步驟會建立已啟用記憶體保護區的金鑰 (需要 SSMS 18.0 或更新版本)：

1. 使用 SSMS 連線至資料庫。
2. 在 [物件總管] 中，展開您的資料庫，然後巡覽至 [安全性] > [Always Encrypted 金鑰]。
3. 佈建已啟用記憶體保護區的新資料行主要金鑰：

    1. 以滑鼠右鍵按一下 [Always Encrypted 金鑰]，然後選取 [新增資料行主要金鑰]。
    2. 選取您的資料行主要金鑰名稱。
    3. 請確定您選取 [Windows 憑證存放區 (目前的使用者或本機電腦)] 或 [Azure Key Vault]。
    4. 選取 [允許記憶體保護區運算]。
    5. 如果您已選取 Azure Key Vault，請登入 Azure，然後選取您的金鑰保存庫。 如需如何建立 Always Encrypted 金鑰保存庫的詳細資訊，請參閱 [Manage your key vaults from Azure portal](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/) (從 Azure 入口網站管理金鑰保存庫)。
    6. 如果金鑰已存在，請選取它，或是遵循表單上的指示來建立新金鑰。
    7. 按一下 [確定] 。

        ![允許記憶體保護區運算](./media/always-encrypted-enclaves/allow-enclave-computations.png)

4. 建立已啟用記憶體保護區的新資料行加密金鑰：

    1. 以滑鼠右鍵按一下 [Always Encrypted 金鑰]，然後選取 [新增資料行加密金鑰]。
    2. 輸入新資料行加密金鑰的名稱。
    3. 在 [資料行主要金鑰] 下拉式清單中，選取您在先前步驟中建立的資料行主要金鑰。
    4. 按一下 [確定] 。

### <a name="provision-enclave-enabled-keys-using-powershell"></a>**使用 PowerShell 佈建已啟用記憶體保護區的金鑰**

下列各節提供範例 PowerShell 指令碼，以佈建已啟用記憶體保護區的金鑰。 會醒目提示具有安全記憶體保護區的 Always Encrypted 特定 (全新) 步驟。 如需使用 PowerShell 佈建金鑰的詳細資訊 (非具有安全記憶體保護區的 Always Encrypted 特定資訊)，請參閱[使用 PowerShell 設定 Always Encrypted 金鑰](https://docs.microsoft.com/sql/relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell)。

**佈建已啟用記憶體保護區的金鑰 - Windows 憑證存放區**

在用戶端/開發電腦上，開啟 Windows PowerShell ISE，並執行下列指令碼。

請務必注意在 [**New-SqlCertificateStoreColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings) Cmdlet 中使用 `-AllowEnclaveComputations` 參數。

```powershell
# Create a column master key in Windows Certificate Store.
$cert = New-SelfSignedCertificate -Subject "\<Subject Name\>" -CertStoreLocation Cert:CurrentUser\\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database. Provide the server/db name. Modify the connection string, if needed.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Data Source = " + $serverName + "; Initial Catalog = " + $databaseName + "; Integrated Security = true"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key
# using the -AllowEnclaveComputations parameter.
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "<column master key name in the database>"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database.
$cekName = "<column encryption key name in the database>"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```


### <a name="provisioning-enclave-enabled-keys--azure-key-vault"></a>佈建已啟用記憶體保護區的金鑰 - Azure Key Vault

在用戶端/開發電腦上，開啟 Windows PowerShell ISE，並執行下列指令碼。

**步驟 1：佈建 Azure Key Vault 中的資料行主要金鑰**

這也可以使用 Azure 入口網站完成。 如需詳細資料，請參閱[從 Azure 入口網站管理金鑰保存庫](https://blogs.technet.microsoft.com/kv/2016/09/12/manage-your-key-vaults-from-new-azure-portal/)。


```powershell
Import-Module AzureRM
Connect-AzureRmAccount

# User values
$SubscriptionId = "<Azure SubscriptionId>"
$resourceGroup = "<resource group name>"
$azureLocation = "<datacenter location>"
$akvName = "<key vault name>"
$akvKeyName = "<key name>"

# Set the context to the specified subscription.
$azureCtx = Set-AzureRMConteXt -SubscriptionId $SubscriptionId

# Create a new resource group - skip, if your desired group already exists.
New-AzureRmResourceGroup –Name $resourceGroup –Location $azureLocation

# Create a new key vault - skip if your vault already exists.
New-AzureRmKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation

# Grant yourself permissions needed to create and use the column master key.
Set-AzureRmKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, list, update, wrapKey,unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account

# Create a column master key in Azure Key Vault.
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination "Software"
```

**步驟 2：在資料庫中建立資料行主要金鑰中繼資料、建立資料行加密金鑰，以及在資料庫中建立資料行加密金鑰中繼資料**


```powershell
# Import the SqlServer module.
Import-Module "SqlServer" -Version

# Connect to your database. Provide the server and db name. If needed, modify the connection string.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Data Source = " + $serverName + "; Initial Catalog = " + $databaseName + "; Integrated Security = true"
$database = Get-SqlDatabase -ConnectionString $connStr

# Authenticate to Azure before calling New-SqlAzureKeyVaultColumnMasterKeySettings,
# because -AllowEnclaveComputations causes a call to Azure Key Vault
# to generate the signature of the column master key.
Add-SqlAzureAuthenticationContext -Interactive

# Create a SqlColumnMasterKeySettings object for your column master key.
$cmkSettings = New-SqlAzureKeyVaultColumnMasterKeySettings -KeyURL $akvKey.ID -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "<column master key name in the database>"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database.
$cekName = "<column encryption key name in the database>"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```


## <a name="identify-enclave-enabled-keys-and-columns"></a>識別已啟用記憶體保護區的金鑰和資料行

若要列出資料行主要金鑰 (設定於資料庫中)，您可以查詢 [sys.column_master_keys](../../system-catalog-views/sys-column-master-keys-transact-sql.md) 目錄檢視 (例如，在 SSMS 中)。 新的 **allow_enclave_computations** 資料行已新增至檢視。 它指出資料行主要金鑰是否已啟用記憶體保護區。

```sql
SELECT name, allow_enclave_computations
FROM sys.column_master_keys
```

若要判斷使用已啟用記憶體保護區的資料行加密金鑰加密哪些資料行加密金鑰 (因此已啟用記憶體保護區)，您需要聯結 [sys.column_master_keys](../../system-catalog-views/sys-column-master-keys-transact-sql.md)、[sys.column_encryption_key_values](../../system-catalog-views/sys-column-encryption-key-values-transact-sql.md) 和 [sys.column_encryption_keys](../../system-catalog-views/sys-column-encryption-keys-transact-sql.md)。


```sql
SELECT cek.name AS [cek_name]
, cmk.name AS [cmk_name]
, cmk.allow_enclave_computations
FROM sys.column_master_keys cmk
JOIN sys.column_encryption_key_values cekv
   ON cmk.column_master_key_id = cekv.column_master_key_id
JOIN sys.column_encryption_keys cek
   ON cekv.column_encryption_key_id = cek.column_encryption_key_id
```

若要判斷哪些資料行已啟用記憶體保護區 (使用已啟用記憶體保護區的資料行加密金鑰所加密資料行)，請使用下列查詢：

```sql
SELECT c.name AS column_name
, cek.name AS cek_name
, cmk.name AS [cmk_name]
, cmk.allow_enclave_computations
from sys.columns c
JOIN sys.column_encryption_keys cek 
ON c.column_encryption_key_id = cek.column_encryption_key_id 
JOIN sys.column_encryption_key_values cekv 
ON cekv.column_encryption_key_id = cek.column_encryption_key_id 
JOIN sys.column_master_keys cmk 
ON cmk.column_master_key_id = cekv.column_master_key_id
```


## <a name="manage-collations"></a>管理定序

自初始發行之後，Always Encrypted 具有定序使用限制：針對使用確定性加密所加密的字元字串資料行，不允許非 BIN2 定序。 這項限制也適用於已啟用記憶體保護區的字串資料行。

針對使用隨機化加密和已啟用記憶體保護區的資料行加密金鑰所加密字元字串資料行，允許使用非 BIN2 定序。 不過，針對這類資料行所啟用的唯一新功能就是就地加密。 若要啟用豐富計算 (模式比對、比較作業)，您必須確定資料行使用 BIN2 定序。

下表摘要說明已啟用記憶體保護區的字串資料行功能 (視加密類型和定序排序順序而定)。

| **定序排序次序** | **確定性加密** | **隨機化加密**                 |
| ------------------------ | ---------------------------- | ----------------------------------------- |
| **非 BIN2**             | 不支援                | 就地加密                       |
| **BIN2**                 | 相等比較          | 就地加密和豐富計算 |

### <a name="determining-and-changing-collations"></a>判斷和變更定序

在 SQL Server 中，可以在伺服器、資料庫或資料行層級設定定序。 如需如何判斷目前定序以及變更伺服器、資料庫或資料行層級定序的一般指示，請參閱[定序和 Unicode 支援](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support)。

**非 UNICODE 字串資料行的特殊考量**：

SQL 用戶端驅動程式中限制 (與 Always Encrypted 無關) 所強加的下列其他限制適用於非 UNICODE (ASCII) 字串資料行。 如果您覆寫非 UNICODE (char、varchar) 字串資料行的資料庫定序，則必須確定資料行定序使用與資料庫定序相同的字碼頁。
若要列出所有定序和其字碼頁識別碼，請使用下列查詢：

```sql
SELECT [Name]
   , [Description]
   , [CodePage] = COLLATIONPROPERTY([Name], 'CodePage')
FROM ::fn_helpcollations()
```

例如，Chinese_Traditional_Stroke_Order_100_CI_AI_WS 和 Chinese_Traditional_Stroke_Order_100_BIN2 具有相同的字碼頁 (950)，但 Chinese_Traditional_Stroke_Order_100_CI_AI_WS 和 Latin1_General_100_BIN2 具有不同的字碼頁 (分別是 950 和 1252)。 上述限制不適用於 UNICODE (nchar、nvarchar) 字串資料行。 因此，作為因應措施，您可以考慮設定所建立新加密資料行的 UNICODE 資料類型，或將類型變更為 UNICODE 類型，再加密現有資料行。


## <a name="create-a-new-table-with-enclave-enabled-columns"></a>使用已啟用記憶體保護區的資料行建立新資料表

您可以使用 [CREATE TABLE (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/create-table-transact-sql) 陳述式，建立具有加密資料行的新資料表。 具有安全記憶體保護區的 Always Encrypted 不會變更此陳述式語法。

1. 使用 SSMS，連線至您的資料庫，然後開啟查詢視窗。
   
     > [!NOTE]
     > 不需要在此工作的連接字串中啟用 Always Encrypted。

2. 在查詢視窗中，發出 CREATE TABLE 陳述式來建立新資料表，並在要加密之每個資料行的[資料行定義](https://docs.microsoft.com/sql/t-sql/statements/alter-table-column-definition-transact-sql)中指定 ENCRYPTED WITH 子句。 若要讓資料行啟用記憶體保護區，請確定您指定已啟用記憶體保護區的資料行加密金鑰。 如果您資料庫的預設定序不是 BIN2 定序，則您也可能需要指定字串資料行的 BIN2 定序。 如需詳細資料，請參閱＜定序設定＞一節。

### <a name="example"></a>範例

下列陳述式會建立具有兩個加密資料行 (SSN 和 Salary) 的新資料表。 假設 CEK1 是已啟用記憶體保護區的資料行加密金鑰，SQL Server Engine 同時支援就地加密以及這兩個資料行的豐富計算，因為資料行使用隨機化加密。 此陳述式設定 UNICODE SSN 資料行的 Latin1\_General\_BIN2 定序，其需要假設預設資料庫定序是非 BIN2 Latin1 定序。

```sql
CREATE TABLE [dbo].[Employees]
(
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [Salary] [int] ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    CONSTRAINT [PK_dbo.Employees] PRIMARY KEY CLUSTERED (
[EmployeeID] ASC
)
) ON [PRIMARY]
GO
```


## <a name="add-a-new-enclave-enabled-column-to-an-existing-table"></a>將已啟用記憶體保護區的新資料行新增至現有資料表

您可以使用 [ALTER TABLE (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/alter-table-transact-sql) / ADD 陳述式，將新的加密資料行新增至現有資料表。 具有安全記憶體保護區的 Always Encrypted 不會變更此陳述式語法。

1. 使用 SSMS，連線至您的資料庫，然後開啟查詢視窗。
    
   不需要在此工作的連接字串中啟用 Always Encrypted。

2. 在查詢視窗中，發出具有 ADD 子句的 ALTER TABLE 陳述式，並在[資料行定義](https://docs.microsoft.com/sql/t-sql/statements/alter-table-column-definition-transact-sql)中指定 ENCRYPTED WITH 子句，以及使用已啟用記憶體保護區的資料行加密金鑰。 如果您的新資料行是字串資料行，而且如果您資料庫的預設定序不是 BIN2 定序，則您也可能需要指定 BIN2 定序。 如需詳細資料，請參閱＜定序設定＞一節。

### <a name="example"></a>範例

假設 CEK1 是已啟用記憶體保護區的資料行加密金鑰，下列陳述式新增加密資料行 (名為 BirthDate)，同時支援豐富查詢和就地加密 (因為資料行使用隨機化加密)。

```sql
ALTER TABLE [dbo].[Employees]
ADD [BirthDate] [Date] ENCRYPTED WITH (
COLUMN_ENCRYPTION_KEY = [CEK1],
ENCRYPTION_TYPE = Randomized,
ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NULL
```


## <a name="prepare-an-ssms-query-window-with-always-encrypted-enabled"></a>準備已啟用 Always Encrypted 的 SSMS 查詢視窗

新增所需的連線參數以啟用記憶體保護區計算：

1. 開啟 SSMS。
2. 在 [連線到伺服器] 對話方塊中指定您的伺服器名稱和資料庫名稱之後，請按一下 [選項]。 巡覽至 [Always Encrypted] 索引標籤，並選取 [啟用 Always Encrypted]，然後指定您的記憶體保護區證明 URL。
    
    ![資料行加密設定](./media/always-encrypted-enclaves/column-encryption-setting.png)

3. 按一下 [連線]。
4. 開啟新的查詢視窗。

或者，如果您已經開啟查詢視窗，則以下是可更新其資料庫連線來啟用 Always Encrypted 的方法：

1. 以滑鼠右鍵按一下現有查詢視窗中的任何位置。
2. 選取 [連線] \> [變更連線]。
3. 按一下 [選項]。 巡覽至 [Always Encrypted] 索引標籤，並選取 [啟用 Always Encrypted]，然後指定您的記憶體保護區證明 URL。
4. 按一下 [連線]。


## <a name="work-with-encrypted-columns"></a>使用加密資料行

### <a name="encrypt-an-existing-plaintext-column-in-place"></a>就地加密現有純文字資料行

您可以使用 [ALTER TABLE (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/alter-table-transact-sql) / ALTER COLUMN 陳述式，就地加密現有純文字資料行，但前提是使用已啟用記憶體保護區的資料行加密金鑰。

若要使用未啟用記憶體保護區的金鑰來加密資料行，您需要使用用戶端工具，例如 SSMS 中的 Always Encrypted 精靈，或 SqlServer PowerShell 模組中的 Set-SqlColumnEncryption Cmdlet。 如需詳細資料，請參閱：

- [Always Encrypted 精靈](always-encrypted-wizard.md)
- [使用 PowerShell 設定資料行加密](configure-column-encryption-using-powershell.md)


### <a name="prerequisites"></a>Prerequisites

- 您現有的資料行不會予以加密。
- 您已佈建已啟用記憶體保護區的金鑰。
- 您可以存取資料行主要金鑰。

#### <a name="steps"></a>步驟

1. 使用 Always Encrypted 以及資料庫連線中所啟用的記憶體保護區計算，準備 SSMS 查詢視窗。 如需詳細資料，請參閱[準備已啟用 Always Encrypted 的 SSMS 查詢視窗](#prepare-an-ssms-query-window-with-always-encrypted-enabled)。
2. 在查詢視窗中，發出具有 ALTER COLUMN 子句的 ALTER TABLE 陳述式，並在 ENCRYPTED WITH 子句中指定已啟用記憶體保護區的資料行加密金鑰。 如果您的資料行是字串資料行 (例如，char、varchar、nchar、nvarchar)，則您也可能需要將定序變更為 BIN2 定序。 如需詳細資料，請參閱＜定序設定＞一節。
    
    > [!NOTE]
    > 如果您的資料行主要金鑰儲存至 Azure Key Vault，則系統可能會提示您登入 Azure。

3. (選擇性) 使用 [DBCC FREEPROCCACHE](../../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md) 清除計畫快取，確定在第一次執行查詢時重新建立任何對所加密資料行之查詢的計畫。
  
    > [!NOTE]
    > 如果您未從快取中移除受影響查詢的計畫，則加密後的第一次執行查詢可能會失敗。

    > [!NOTE]
    > 使用 DBCC FREEPROCCACHE 小心地清除計畫快取，因為它可能會導致暫時性的查詢效能降低。 若要將清除快取的負面影響降到最低，您可以選擇性地僅移除受影響查詢的計畫。

4.  (選擇性) 呼叫 [sp_refresh_parameter_encryption](../../system-stored-procedures/sp-refresh-parameter-encryption-transact-sql.md)，透過加密資料行以更新可能已失效之每個模組 (預存程序、函式、檢視、觸發程序) 的參數中繼資料。

#### <a name="example"></a>範例

下列範例假設：

  - CEK1 是已啟用記憶體保護區的資料行加密金鑰。

  - SSN 資料行是純文字，而且目前使用 Latin1、非 BIN2 定序 (例如，Latin1\_General\_CI\_AI\_KS\_WS)。

此陳述式會使用隨機化加密和已啟用記憶體保護區的資料行加密金鑰來加密 SSN 資料行。 它也會將預設資料庫定序覆寫為對應 (在相同的字碼頁中) BIN2 定序。

作業會在線上執行 (ONLINE = ON)。 另請注意，**DBCC FREEPROCCACHE** 呼叫可重新建立受資料表結構描述變更所影響的查詢計畫。

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char] COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
WITH
(ONLINE = ON)
GO
DBCC FREEPROCCACHE
GO
```


### <a name="make-an-existing-encrypted-column-enclave-enabled"></a>將現有加密資料行設為啟用記憶體保護區

針對未啟用記憶體保護區的現有資料行，有數種方式可以啟用記憶體保護區功能。 您選擇的方法取決於許多因素：

- **範圍/細微性：** 您要啟用一小部分資料行的記憶體保護區功能，還是啟用使用指定資料行主要金鑰保護之所有資料行的記憶體保護區功能？
- **資料大小：** 包含您要設為啟用記憶體保護區之資料行的資料表大小為何？
- 您也要變更資料行的加密類型嗎？ 請記住，唯一的隨機化加密支援豐富計算 (模式比對、比較運算子)。 如果您的資料行使用確定性加密所加密，則也需要使用隨機化加密來重新加密它，以解除鎖定記憶體保護區的完整功能。

下列三種方法可以啟用現有資料行的記憶體保護區：

#### <a name="option-1-rotate-the-column-master-key-to-replace-it-with-an-enclave-enabled-column-master-key"></a>選項 1：輪替資料行主要金鑰以將它取代為已啟用記憶體保護區的資料行主要金鑰。
  
- 優點：
  - 不包含重新加密資料，因此它通常是最快的方法。 這是用於包含大量資料之資料行的建議方法，但您需要啟用豐富計算的所有資料行都已使用確定性加密，因此不需要重新予以加密。
  - 可以啟用多個任意大小之資料行的記憶體保護區功能，因為它會將與原始資料行主要金鑰建立關聯的所有資料行加密金鑰和所有加密資料行設為啟用記憶體保護區。
  
- 缺點：
  - 不支援將加密類型從確定性變更為隨機化，因此在它解除鎖定確定性加密資料行的就地加密時，不會啟用豐富計算。
  - 不允許您選擇性地轉換與指定資料行主要金鑰建立關聯的一些資料行。
  - 引進金鑰管理額外負荷；您需要建立新的資料行主要金鑰，並讓它可供查詢受影響資料行的應用程式使用。  


#### <a name="option-2-this-approach-involves-two-steps-1-rotating-the-column-master-key-as-in-option-1-and-2-re-encrypting-a-subset-of-deterministically-encrypted-columns-using-randomized-encryption-to-enable-rich-computations-for-those-columns"></a>選項 2：此方法包含兩個步驟：1) 輪替資料行主要金鑰 (如選項 1) 以及 2) 使用隨機化加密來重新加密一小部分的確定性加密資料行，以啟用這些資料行的豐富計算。
  
- 優點：
  - 就地重新加密資料，因此建議啟用包含大量資料之確定性加密資料行的豐富查詢。 請注意，步驟 1 使用確定性加密來解除鎖定資料行的就地加密，因此可以就地執行步驟 2。
  - 可以啟用多個任意大小之資料行的記憶體保護區功能。
  
- 缺點：
  - 不允許您選擇性地轉換與指定資料行主要金鑰建立關聯的一些資料行。
  - 它引進金鑰管理額外負荷；您需要建立新的資料行主要金鑰，並讓它可供查詢受影響資料行的應用程式使用。

#### <a name="option-3-re-encrypting-selected-columns-with-a-new-enclave-enabled-column-encryption-key-and-randomized-encryption-if-needed-on-the-client-side"></a>選項 3：在用戶端使用已啟用記憶體保護區的新資料行加密金鑰和隨機化加密 (需要時) 重新加密選取的資料行。
  
- 優點 - 此方法：
  - 可讓您選擇性地啟用一個資料行或一小部分資料行的記憶體保護區功能。
  - 它可以使用一個步驟來啟用確定性加密資料行的豐富計算。
  - 它不需要建立新的資料行主要金鑰，因此對應用程式的影響較小。
  
- 缺點：
  - 包含資料行的資料表整個內容需要移至資料庫外部才能重新加密，因此僅建議用於小型資料表。 

如需詳細資訊，請參閱以下章節：
  - [輪替資料行主要金鑰以將資料行設為啟用記憶體保護區](#make-columns-enclave-enabled-by-rotating-their-column-master-key)
  - [就地重新加密資料行](#re-encrypt-columns-in-place)
  - [重新加密用戶端上的資料行](#re-encrypt-columns-on-the-client-side)

### <a name="make-columns-enclave-enabled-by-rotating-their-column-master-key"></a>輪替資料行主要金鑰以將資料行設為啟用記憶體保護區

資料行主要金鑰輪替程序會將現有資料行主要金鑰取代為新的資料行主要金鑰。 它包含使用新資料行主要金鑰，重新加密與舊資料行主要金鑰建立關聯的資料行加密金鑰。 此工作流程自 Always Encrypted 初始版本後即存在，而且基於合規性或安全性考量可支援取代資料行主要金鑰 (如果現有資料行主要金鑰洩露)。

使用記憶體保護區的 Always Encrypted 會新增資料行主要金鑰輪替工作流程的新用途。 假設舊的資料行主要金鑰未啟用記憶體保護區，而新的資料行主要金鑰已啟用記憶體保護區，則輪替程序會有效地將與資料行主要金鑰建立關聯的所有資料行加密金鑰設為啟用記憶體保護區。 輪替資料行主要金鑰不包含重新加密資料；因此，其為啟用現有資料行之記憶體保護區功能的建議程序。

輪替資料行主要金鑰並不會變更受影響資料行的加密類型。 因此，它只能解除鎖定確定性加密資料行的就地加密。 若要使用確定性加密來解除鎖定資料行的豐富計算，您需要在輪替資料行主要金鑰之後重新予以加密 (就地)。

您可能也需要使用隨機化加密將字串資料行的定序變更為 BIN2 定序，以解除鎖定豐富計算。 如需詳細資料，請參閱＜定序設定＞一節。

資料行主要金鑰輪替程序相同，不論任一個包含的金鑰是否啟用記憶體保護區。 下列文章包含如何旋轉資料行主要金鑰的詳細資料：

- [使用 SSMS 輪替資料行主要金鑰](configure-always-encrypted-using-sql-server-management-studio.md)
- [使用 PowerShell 輪替資料行主要金鑰](rotate-always-encrypted-keys-using-powershell.md)

為了方便起見，下面提供輪替資料行主要金鑰的 PowerShell 指令碼範例。

#### <a name="pre-requisites"></a>必要條件

- 您已佈建已啟用記憶體保護區的新資料行主要金鑰。
- 您可以同時存取舊和新的資料行主要金鑰。
- 所有受舊資料行主要金鑰保護的字串資料行都會使用 BIN2 定序  (注意：或者，在輪替資料行主要金鑰之後，您可以變更字串資料行的定序)。

#### <a name="steps"></a>步驟

將下列指令碼貼入 Windows PowerShell ISE，並將 \<預留位置\> 取代為特定值：


```powershell
# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database. Modify server/db name or/and the connection string, if needed.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Data Source = " + $serverName + "; Initial Catalog = " +
$databaseName + "; Integrated Security = true"
$database = Get-SqlDatabase -ConnectionString $connStr

# Set the names of the old/current column master key and the new/target enclave-enabled column master key. (Change the names, if needed).
$oldCmkName = "<old column master key name>"
$newCmkName = "<new column master key name>"

# Authenticate to Azure. Needed only of either column master key is stored in Azure Key Vault.
Add-SqlAzureAuthenticationContext -Interactive

# Initiate the rotation from the current column master key to the new column master key.
Invoke-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName $oldCmkName
-TargetColumnMasterKeyName $newCmkName -InputObject $database

# Complete the rotation of the old column master key.
Complete-SqlColumnMasterKeyRotation -SourceColumnMasterKeyName
$oldCmkName -InputObject $database

# Remove the old column master key metadata.
Remove-SqlColumnMasterKey -Name $oldCmkName -InputObject $database
```


### <a name="re-encrypt-columns-in-place"></a>就地重新加密資料行 

在您已將資料行設為啟用記憶體保護區之後，即可就地執行下列作業 (在記憶體保護區內，而不需要將資料移出資料庫)：

- 輪替資料行主要金鑰 (以將它取代為新金鑰)；例如，遵守標準規定 (其中有些規定定期金鑰輪替)，或基於安全性理由 (如果您的資料行加密金鑰洩露)。
- 例如，將加密類型從確定性加密變更為隨機化加密，以解除鎖定資料行的豐富計算。

#### <a name="prerequisites"></a>Prerequisites

- 您的資料行使用已啟用記憶體保護區的資料行加密金鑰所加密。
- 您已佈建已啟用記憶體保護區的新資料行加密金鑰 (如果您的目標是取代已啟用記憶體保護區的目前資料行加密金鑰，並保護資料行)。
- 您可以存取資料行主要金鑰。

#### <a name="steps"></a>步驟

1. 使用 Always Encrypted 以及針對資料庫連線所啟用的記憶體保護區計算，準備 SSMS 查詢視窗。 如需詳細資料，請參閱[準備已啟用 Always Encrypted 的 SSMS 查詢視窗](#prepare-an-ssms-query-window-with-always-encrypted-enabled)。

2. 在查詢視窗中，發出具有 ALTER COLUMN 子句的 [ALTER TABLE (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/alter-table-transact-sql) 陳述式，並在 ENCRYPTED WITH 子句中指定下列項目：
    
    1. 如果您要輪替目前金鑰，則為已啟用記憶體保護區的新資料行加密金鑰名稱。 如果您不要變更資料行加密金鑰，則需要指定目前金鑰的名稱。
    
    2. 如果您變更加密類型，則為新的加密類型。 如果您不要變更加密類型，則需要指定目前加密類型。
        
       如果您重新加密之資料行使用與預設資料庫定序不同的定序 (BIN2)，則需要包含 COLLATE 片語，以及指定資料行定義中的目前資料行定序 (保留相同的定序)。
        
       > [!NOTE]
       > 如果您的資料行主要金鑰儲存至 Azure Key Vault，則系統可能會提示您登入 Azure。

3. (選擇性) 使用 [DBCC FREEPROCCACHE](../../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md) 清除計畫快取，確定在第一次執行查詢時重新建立任何對所重新加密資料行之查詢的計畫。
    
    如果您未從快取中移除受影響查詢的計畫，則重新加密後的第一次執行查詢可能會失敗。
    
    > [!NOTE]
    > 使用 DBCC FREEPROCCACHE 小心地清除計畫快取，因為它可能會導致暫時性的查詢效能降低。 若要將清除快取的負面影響降到最低，您可以選擇性地僅移除受影響查詢的計畫。 如需詳細資料，請參閱 [DBCC FREEPROCCACHE](../../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md).aspx)。

4. (選擇性) 呼叫 [sp_refresh_parameter_encryption](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-refresh-parameter-encryption-transact-sql)，透過重新加密資料行以更新可能已失效之每個模組 (預存程序、函式、檢視、觸發程序) 的參數中繼資料。

#### <a name="examples"></a>範例

假設 SSN 資料行目前使用已啟用記憶體保護區的資料行加密金鑰 (名為 CEK1) 和確定性加密所加密，而且設定於資料行層級的目前定序是 Latin1\_General\_BIN2，則下面陳述式會使用隨機化加密和相同的金鑰來重新加密資料行。


```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
GO
DBCC FREEPROCCACHE
GO
```


假設 SSN 資料行目前使用已啟用記憶體保護區的資料行加密金鑰 (名為 CEK1) 和確定性加密所加密，而且預設資料庫定序是 BIN2 定序 (但尚未設定於資料行層級)，則下面陳述式會使用已啟用記憶體保護區的新金鑰 (名為 CEK2) 來重新加密資料行 (而不需要變更加密類型)。

```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) 
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK2]
, ENCRYPTION\_TYPE = Deterministic
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
GO
DBCC FREEPROCCACHE
GO
```

假設 SSN 資料行目前使用已啟用記憶體保護區的資料行加密金鑰 (名為 CEK1) 和確定性加密所加密，而且預設資料庫定序是 BIN2 定序 (但尚未設定於資料行層級)，則以下陳述式會使用已啟用記憶體保護區的新金鑰 (名為 CEK2) 和隨機化加密來重新加密資料行。 此外，會以線上模式執行作業。


```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) 
ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1]
, ENCRYPTION_TYPE = Randomized
, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL 
WITH (ONLINE = ON)
GO
DBCC FREEPROCCACHE
GO
```


### <a name="re-encrypt-columns-on-the-client-side"></a>重新加密用戶端上的資料行 

傳統的重新加密 (以及加密或解密) 資料行方法使用用戶端工具 (例如 Always Encrypted 精靈或 PowerShell)。 一般而言，不建議使用此方法，但例外狀況是包含資料行 (將重新加密) 的資料表太小時，以及您目標是結合使用已啟用記憶體保護區的新金鑰來重新加密資料行以及變更加密類型 (從確定性變更為隨機化)。

請注意，如果您使用隨機化加密重新加密資料行，則可能需要將其定序變更為 BIN2 定序 (重新加密之前或之後)，以解除鎖定豐富計算。 如需詳細資料，請參閱＜定序設定＞一節。

如需詳細資料，請參閱：

  - 使用 SSMS 輪替資料行加密金鑰：<https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-wizard>
  - 使用 PowerShell 輪替資料行加密金鑰：<https://docs.microsoft.com/sql/relational-databases/security/encryption/configure-column-encryption-using-powershell>

### <a name="decrypt-a-column-in-place"></a>就地解密資料行

如果使用已啟用記憶體保護區的資料行加密金鑰來加密資料行，則您可以使用 ALTER TABLE 陳述式將它就地解密 (轉換為純文字資料行)。 此外，會以線上模式執行作業。

#### <a name="prerequisites"></a>Prerequisites

- 使用已啟用記憶體保護區的資料行加密金鑰來加密資料行。
- 您可以存取資料行主要金鑰。



#### <a name="steps"></a>步驟

1.  使用 Always Encrypted 以及針對資料庫連線所啟用的記憶體保護區計算，準備 SSMS 查詢視窗。 如需詳細資料，請參閱[準備已啟用 Always Encrypted 的 SSMS 查詢視窗](#prepare-an-ssms-query-window-with-always-encrypted-enabled)。

2.  在查詢視窗中，發出具有 ALTER COLUMN 子句的 [ALTER TABLE (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/alter-table-transact-sql) 陳述式，並在**不**使用 ENCRYPTED WITH 子句的情況下指定所需資料行設定。
    
    > [!NOTE]
    > 如果您的資料行主要金鑰儲存至 Azure Key Vault，則系統可能會提示您登入 Azure。

3.  (選擇性) 使用 [DBCC FREEPROCCACHE](../../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md) 清除計畫快取，確定在第一次執行查詢時重新建立任何對所解密資料行之查詢的計畫。
    
    > [!NOTE]
    > 如果您未從快取中移除受影響查詢的計畫，則解密後的第一次執行查詢可能會失敗。
    
    > [!NOTE]
    > 使用 DBCC FREEPROCCACHE 小心地清除計畫快取，因為它可能會導致暫時性的查詢效能降低。 若要將清除快取的負面影響降到最低，您可以選擇性地僅移除受影響查詢的計畫。 如需詳細資料，請參閱 [DBCC FREEPROCCACHE](../../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)。

4.  (選擇性) 呼叫 [sp\_refresh\_parameter\_encryption](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-refresh-parameter-encryption-transact-sql)，透過解密資料行以更新可能已失效之每個模組 (預存程序、函式、檢視、觸發程序) 的參數中繼資料。

#### <a name="example"></a>範例

假設已加密 SSN 資料行，而且設定於資料行層級的目前定序是 Latin1\_General\_BIN2，則以下陳述式會解密資料行 (並保留定序；或者，例如，您可以選擇將定序變更為相同陳述式中的非 BIN2 定序)。


```sql
ALTER TABLE [dbo].[Employees]
ALTER COLUMN [SSN] [char](11) COLLATE Latin1_General_BIN2
WITH (ONLINE = ON)
GO
DBCC FREEPROCCACHE
GO
```


## <a name="issue-rich-queries-against-encrypted-columns-using-ssms"></a>使用 SSMS 對加密資料行發出豐富查詢

對已啟用記憶體保護區之資料行嘗試豐富查詢的最快方式，是從已啟用 Always Encrypted 參數化的 SSMS 查詢視窗。 如需 SSMS 中此有用功能的詳細資料，請參閱：

- [Parameterization for Always Encrypted – Using SSMS to Insert into, Update and Filter by Encrypted Columns](https://blogs.msdn.microsoft.com/sqlsecurity/2016/12/13/parameterization-for-always-encrypted-using-ssms-to-insert-into-update-and-filter-by-encrypted-columns/) (Always Encrypted 的參數化 - 使用 SSMS 插入、更新並依加密資料行篩選)
- [查詢加密資料行](configure-always-encrypted-using-sql-server-management-studio.md#querying-encrypted-columns)



### <a name="prerequisites"></a>Prerequisites

- 要查詢的資料行已啟用記憶體保護區。
- 您可以存取一或多個資料行主要金鑰。

### <a name="steps"></a>步驟

1.  使用 Always Encrypted 以及針對資料庫連線所啟用的記憶體保護區計算，準備 SSMS 查詢視窗。 如需詳細資料，請參閱[準備已啟用 Always Encrypted 的 SSMS 查詢視窗](#prepare-an-ssms-query-window-with-always-encrypted-enabled)。

2.  啟用 Always Encrypted 的參數化。
    
    1.  從 SSMS 的主功能表中，選取 [查詢]。
    2.  選取 [查詢選項...] 。
    3.  瀏覽至 [執行] > [進階]。
    4.  選取或取消選取 [啟用 Always Encrypted 的參數化]。
    5.  按一下 [確定]。

3.  對加密資料行使用豐富計算來撰寫和執行查詢。 針對目標設為查詢中加密資料行的每個值，您需要宣告 Transact-SQL 變數。 這些變數必須使用內嵌初始化 (無法透過 SET 陳述式設定)。
    
    > [!NOTE]
    > 如果您的資料行主要金鑰儲存至 Azure Key Vault，則系統可能會提示您登入 Azure。

### <a name="example"></a>範例

此範例假設您的資料庫包含使用下列陳述式所建立資料表。

```sql
CREATE TABLE [dbo].[Employees]
(
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [Salary] [int] ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    CONSTRAINT [PK_dbo.Employees] PRIMARY KEY CLUSTERED (
[EmployeeID] ASC
)
) ON [PRIMARY]
GO
```


CEK1 是已啟用記憶體保護區的資料行加密金鑰。

該資料表的下列查詢範例遵守參數化方針：


```sql
DECLARE @SSNPattern CHAR(11) = '%1111%'
DECLARE @MinSalary INT = 1000
SELECT *
FROM [dbo].[Employees]
WHERE SSN LIKE @SSNPattern
    AND [Salary] >= @MinSalary;
GO;
```


## <a name="develop-applications-issuing-rich-queries-in-visual-studio"></a>開發在 Visual Studio 中發出豐富查詢的應用程式

### <a name="set-up-your-you-visual-studio-project"></a>設定 Visual Studio 專案

若要在 .NET Framework 應用程式中使用具有安全記憶體保護區的 Always Encrypted，您需要確定根據 .NET Framework 4.7.2 建置應用程式，並與 Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders NuGet 整合。 此外，如果您將資料行主要金鑰儲存至 Azure Key Vault，則也需要整合應用程式與 Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider NuGet 2.2.0 版或更新版本。 

1. 開啟 Visual Studio。
2. 建立新的 Visual C\# 專案，或開啟現有專案。
3. 請確定您專案的目標至少為 .NET Framework 4.7.2。 以滑鼠右鍵按一下 [方案總管] 中的專案，並選取 [屬性]，然後將 [目標架構] 設定為 .NET Framework 4.7.2。

4. 移至 [工具] (主功能表) > [NuGet 套件管理員] > [套件管理員主控台]，以安裝下列 NuGet 套件。 在 [套件管理員主控台] 中，執行下列程式碼。

  ```powershell
  Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider --IncludePrerelease 
  ```

5. 如果您使用 Azure Key Vault 來儲存資料行主要金鑰，請移至 [工具] (主功能表) > [NuGet 套件管理員] > [套件管理員主控台]，以安裝下列 NuGet 套件。 在 [套件管理員主控台] 中，執行下列程式碼。

  ```powershell
  Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider --IncludePrerelease -Version 2.2.0
  Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
  ```

6. 選取您的專案，然後按一下 [安裝]。
7. 從您的專案 (例如 App.config 或 Web.config) 中，開啟設定檔。
8. 尋找 \<configuration\> 區段。 在 \<configuration\> 區段內，尋找 \<configSections\> 區段。 在 \<configSections\> 內新增下列區段：

  ```
  <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" /\>
  ```

9. 在設定區段的 \<configSections\> 下方，新增下列區段，以指定要用來證明以及與 Intel SGX 記憶體保護區互動的記憶體保護區提供者：

  ```
  \<SqlColumnEncryptionEnclaveProviders\>
      \<providers\>
      \<add name="VBS" type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.VirtualizationBasedSecurityEnclaveProvider, Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,   Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/\>
      \</SqlColumnEncryptionEnclaveProviders\>
  ```
 

### <a name="develop-and-test-your-app"></a>開發和測試應用程式 

若要使用 Always Encrypted 和記憶體保護區計算，您的應用程式需要使用連接字串中的下列兩個關鍵字來連線至資料庫：`Column Encryption Setting = Enabled; Enclave Attestation Url=http://x.x.x.x/Attestation` (其中 xxxx 可以是 IP、網域等)。

此外，您的應用程式需要遵守適用於使用 Always Encrypted 的應用程式一般方針；例如，應用程式必須可以存取與資料庫資料行建立關聯的資料行主要金鑰，而應用程式查詢中會參考這些資料庫資料行。

如需使用 Always Encrypted 開發 .NET Framework 應用程式的詳細資料，請參閱下列文章：

- [搭配使用 Always Encrypted 與 .NET Framework Data Provider 進行開發](develop-using-always-encrypted-with-net-framework-data-provider.md)
- [Always Encrypted：保護 SQL Database 中的敏感性資料並將加密金鑰儲存至 Azure Key Vault](https://docs.microsoft.com/azure/sql-database/sql-database-always-encrypted)

#### <a name="example"></a>範例

下列程式碼是 C\# 主控台應用程式的簡單範例，而此主控台應用程式對具有下列結構描述的資料表發出 LIKE 查詢：

```sql
CREATE TABLE [dbo].[Employees]
(
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11) ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [Salary] [int] ENCRYPTED WITH (
        COLUMN_ENCRYPTION_KEY = [CEK1],
        ENCRYPTION_TYPE = Randomized,
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
    CONSTRAINT [PK_dbo.Employees] PRIMARY KEY CLUSTERED (
[EmployeeID] ASC
)
) ON [PRIMARY]
GO
```

CEK1 假設為已啟用記憶體保護區的資料行加密金鑰。


```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.SqlClient;
using System.Data;
namespace ConsoleApp1
{
   class Program
   {
      static void Main(string\[\] args)
   {

   string connectionString = "Data Source = myserver; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Enclave Attestation Url = http://10.193.16.185/Attestation/attestationservice.svc/signingCertificates; Integrated Security = true";

using (SqlConnection connection = new SqlConnection(connectionString))
{
   connection.Open();
   
   SqlCommand cmd = connection.CreateCommand();
   cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [Salary] FROM [dbo].[Employees] WHERE [SSN] LIKE @SSNPattern AND [Salary] > @MinSalary;";
   
   SqlParameter paramSSNPattern = cmd.CreateParameter();
   
   paramSSNPattern.ParameterName = @"@SSNPattern";
   paramSSNPattern.DbType = DbType.AnsiStringFixedLength;
   paramSSNPattern.Direction = ParameterDirection.Input;
   paramSSNPattern.Value = "%1111";
   paramSSNPattern.Size = 11;
   
   cmd.Parameters.Add(paramSSNPattern);
   
   SqlParameter MinSalary = cmd.CreateParameter();
   
   MinSalary.ParameterName = @"@MinSalary";
   MinSalary.DbType = DbType.Int32;
   MinSalary.Direction = ParameterDirection.Input;
   MinSalary.Value = 900;
   
   cmd.Parameters.Add(MinSalary);
   cmd.ExecuteNonQuery();
   
   SqlDataReader reader = cmd.ExecuteReader();
   while (reader.Read())
   
   {
     Console.WriteLine(reader);
     Console.WriteLine(reader\[0\] + ", " + reader\[1\] + ", " + reader\[2\] + ", " + reader\[3\]);
   }

   Console.ReadKey();

   }
  }
 }
}
```
