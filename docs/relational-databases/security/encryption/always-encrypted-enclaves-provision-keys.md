---
title: 佈建已啟用記憶體保護區的金鑰 | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2019
ms.prod: sql
ms.reviewer: vanto
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 6b87620704416df94cf21cda05d1a64a8159eb32
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "73595583"
---
# <a name="provision-enclave-enabled-keys"></a>佈建已啟用記憶體保護區的金鑰
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

本文描述如何佈建已啟用記憶體保護區的金鑰，其支援位於伺服器端安全記憶體保護區內用於[具備安全記憶體保護區 Always Encrypted](always-encrypted-enclaves.md) 的計算。 

在您佈建已啟用記憶體保護區的金鑰時，適用[管理 Always Encrypted 金鑰](overview-of-key-management-for-always-encrypted.md)的一般方針和流程。 本文說明適用於具備安全記憶體保護區 Always Encrypted 的詳細資料。

若要使用 SQL Server Management Studio 或 PowerShell 佈建已啟用安全記憶體保護區的資料行主要金鑰，請確認新的金鑰支援記憶體保護區計算。 這會使工具 (SSMS 或 PowerShell) 產生 `CREATE COLUMN MASTER KEY` 陳述式，在資料庫中的資料行主要金鑰中繼資料內設定 `ENCLAVE_COMPUTATIONS`。 如需詳細資訊，請參閱 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)。 

工具也會使用資料行主要金鑰對資料行主要屬性進行數位簽署，並會將簽章儲存在資料庫中繼資料內。 簽章能防止 `ENCLAVE_COMPUTATIONS` 被惡意竄改。 SQL 用戶端驅動程式會先驗證簽章，才允許使用記憶體保護區。 這可讓安全性系統管理員控制在記憶體保護區內計算哪些資料行資料。

`ENCLAVE_COMPUTATIONS` 是固定的，這表示您在中繼資料中定義資料行主要金鑰後，便無法進行變更。 若要使用指定資料行主要金鑰所加密資料行來加密金鑰啟用記憶體保護區計算，您需要輪替資料行主要金鑰，並以已啟用記憶體保護區的資料行主要金鑰來加以取代。 請參閱[輪替已啟用記憶體保護區的金鑰](always-encrypted-enclaves-rotate-keys.md)。

> [!NOTE]
> 目前，SSMS 和 PowerShell 都支援儲存在 Azure Key Vault 或 Windows 憑證存放區中已啟用記憶體保護區的資料行主要金鑰。 不支援硬體安全性模組 (使用 CNG 或 CAPI)。

若要建立已啟用記憶體保護區的資料行加密金鑰，您需要確認您選取已啟用記憶體保護區的資料行主要金鑰來加密新金鑰。 

下列各節提供詳細資料，說明如何使用 SSMS 和 PowerShell 來佈建已啟用記憶體保護區的金鑰。

## <a name="provision-enclave-enabled-keys-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 佈建已啟用記憶體保護區的金鑰
在 SQL Server Management Studio 18.3 或更新版本中，您可以：
- 使用 [新增資料行主要金鑰]  對話方塊來佈建已啟用記憶體保護區的資料行主要金鑰。
- 使用 [新增資料行加密金鑰]  對話方塊來佈建已啟用記憶體保護區的資料行加密金鑰。

> [!NOTE]
> [Always Encrypted 精靈](always-encrypted-wizard.md)目前不支援產生已啟用記憶體保護區的金鑰。 但是，您可以先使用上述對話方塊來建立已啟用記憶體保護區的金鑰，然後在執行精靈時，為您所想要加密資料行選取已存在的啟用記憶體保護區資料行加密。

### <a name="provision-enclave-enabled-column-master-keys-with-the-new-column-master-key-dialog"></a>使用 [新增資料行主要金鑰] 對話方塊來佈建已啟用記憶體保護區的資料行主要金鑰
請遵循[使用 [新增資料行主要金鑰] 對話方塊佈建資料行主要金鑰](configure-always-encrypted-keys-using-ssms.md#provision-column-master-keys-with-the-new-column-master-key-dialog)中步驟來佈建已啟用記憶體保護區的資料行主要金鑰。 請確認選取 [允許記憶體保護區計算]  。 請參閱以下的螢幕擷取畫面：

![允許記憶體保護區運算](./media/always-encrypted-enclaves/allow-enclave-computations.png)

> [!NOTE]
> 只有在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 執行個體包含正確初始化的安全記憶體保護區時，才會出現 [允許記憶體保護區計算]  核取方塊。 如需詳細資訊，請參閱[設定 Always Encrypted 的記憶體保護區類型](../../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)。

> [!TIP]
> 若要檢查特定資料行主要金鑰是否已啟用記憶體保護區，請在 [物件總管] 中以滑鼠右鍵按一下該資料行主要金鑰，並選取 [屬性]  。 若金鑰已啟用記憶體保護區，視窗中便會出現 [記憶體保護區計算:  允許]，其顯示金鑰的屬性。 或者，您可以使用 [sys.column_master_keys (Transact-SQL)](../../system-catalog-views/sys-column-master-keys-transact-sql.md) 檢視。

### <a name="provision-enclave-enabled-column-encryption-keys-with-the-new-column-encryption-key-dialog"></a>使用 [新增資料行加密金鑰] 對話方塊來佈建已啟用記憶體保護區的資料行加密金鑰
請遵循[使用 [新增資料行加密金鑰] 對話方塊佈建資料行加密金鑰](configure-always-encrypted-keys-using-ssms.md#provision-column-encryption-keys-with-the-new-column-encryption-key-dialog)中步驟來佈建已啟用記憶體保護區的資料行加密金鑰。 選取資料行主要金鑰時，請確認該資料行主要金鑰已啟用記憶體保護區。

> [!TIP]
> 若要檢查特定資料行加密金鑰是否已啟用記憶體保護區，請在 [物件總管] 中以滑鼠右鍵按一下該資料行加密金鑰，並選取 [屬性]  。 若金鑰已啟用記憶體保護區，視窗中便會出現 [記憶體保護區計算:  允許]，其顯示金鑰的屬性。

## <a name="provision-enclave-enabled-keys-using-powershell"></a>使用 PowerShell 佈建已啟用記憶體保護區的金鑰
若要使用 PowerShell 佈建來佈建已啟用記憶體保護區的金鑰，您需要 SqlServer PowerShell 模組版本 21.1.18179 或更新版本。

一般而言，[使用 PowerShell 佈建 Always Encrypted 金鑰](configure-always-encrypted-keys-using-powershell.md)中所描述 PowerShell 的 Always Encrypted 金鑰佈建工作流程 (搭配或不搭配角色隔離)，其也適用於已啟用記憶體保護區的金鑰。 本節描述已啟用記憶體保護區的金鑰特定詳細資料。

SqlServer PowerShell 模組會使用 `-AllowEnclaveComputations` 參數延伸 [**New-SqlCertificateStoreColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings) 和 [**New-SqlAzureKeyVaultColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlazurekeyvaultcolumnmasterkeysettings) Cmdlet，允許您在佈建流程期間指定已啟用記憶體保護區的資料行主要金鑰。 其中任何一個 Cmdlet 都會建立本機物件，包含資料行主要金鑰的屬性 (儲存在 Azure Key Vault 或 Windows 憑證存放區中)。 若進行指定，`-AllowEnclaveComputations` 屬性便會在本機物件中將金鑰標記為已啟用記憶體保護區。 這也會使 Cmdlet 存取參考的資料行主要金鑰 (位於 Azure Key Vault 或 Windows 憑證存放區中)，以對金鑰屬性進行數位簽署。 在您為已啟用記憶體保護區資料行的新主要金鑰建立設定物件後，您便可以在後續引動 [**New-SqlColumnMasterKey**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcolumnmasterkey) Cmdlet 時使用該金鑰，來建立描述資料庫中新金鑰的中繼資料物件。

佈建已啟用記憶體保護區資料行加密金鑰的過程，與佈建未啟用記憶體保護區資料行加密金鑰的過程沒有任何不同。 您只需要確認用來加密新資料行加密金鑰的資料行主要金鑰已啟用記憶體保護區。

> [!NOTE]
> SqlServer PowerShell 模組目前不支援佈建儲存在硬體安全性模組 (使用 CNG 或 CAPI) 中已啟用記憶體保護區的金鑰。

### <a name="example---provision-enclave-enabled-keys-using-windows-certificate-store"></a>範例 - 使用 Windows 憑證存放區佈建已啟用記憶體保護區的金鑰
以下端對端範例會示範如何佈建已啟用記憶體保護區的金鑰，並儲存 Windows 憑證存放區中的資料行主要金鑰。 指令碼是以[不使用角色隔離的 Windows 憑證存放區 (範例)](configure-always-encrypted-keys-using-powershell.md#windows-certificate-store-without-role-separation-example) 中範例為基礎。 值得注意的是在 [**New-SqlCertificateStoreColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings) Cmdlet 中使用了 `-AllowEnclaveComputations` 參數；此為兩個範例中工作流程間的唯一差異。

```powershell
# Create a column master key in Windows Certificate Store.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Create a SqlColumnMasterKeySettings object for your column master key
# using the -AllowEnclaveComputations parameter.
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName  -InputObject $database -ColumnMasterKey $cmkName
```

### <a name="example---provision-enclave-enabled-keys-using-azure-key-vault"></a>範例 - 使用 Azure Key Vault 佈建已啟用記憶體保護區的金鑰
以下端對端範例會示範如何佈建啟用記憶體保護區的金鑰，並將資料行主要金鑰儲存在 Azure Key Vault 中。 指令碼是以[不使用角色隔離的 Azure Key Vault (範例)](configure-always-encrypted-keys-using-powershell.md#azure-key-vault-without-role-separation-example) 中範例為基礎。 請務必注意已啟用記憶體保護區金鑰與未啟用記憶體保護區金鑰工作流程間的兩項差異。 
- 在以下指令碼中，[**New-SqlCertificateStoreColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlcertificatestorecolumnmasterkeysettings) 使用 `-AllowEnclaveComputations` 參數來讓新資料行主要金鑰啟用記憶體保護區。 
- 以下指令碼會在呼叫 [**New-SqlAzureKeyVaultColumnMasterKeySettings**](https://docs.microsoft.com/powershell/module/sqlserver/new-sqlazurekeyvaultcolumnmasterkeysettings) Cmdlet 前，呼叫 [**Add-SqlAzureAuthenticationContext**](https://docs.microsoft.com/powershell/module/sqlserver/add-sqlazureauthenticationcontext) Cmdlet 來登入 Azure。 先登入 Azure 是必要的，因為 `-AllowEnclaveComputations` 參數會讓 **New-SqlAzureKeyVaultColumnMasterKeySettings** 呼叫 Azure Key Vault 來簽署資料行主要金鑰的屬性。

```powershell
# Create a column master key in Azure Key Vault.
Import-Module Az
Connect-AzAccount
$SubscriptionId = "<Azure SubscriptionId>"
$resourceGroup = "<resource group name>"
$azureLocation = "<datacenter location>"
$akvName = "<key vault name>"
$akvKeyName = "<key name>"
$azureCtx = Set-AzConteXt -SubscriptionId $SubscriptionId # Sets the context for the below cmdlets to the specified subscription.
New-AzResourceGroup -Name $resourceGroup -Location $azureLocation # Creates a new resource group - skip, if your desired group already exists.
New-AzKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation # Creates a new key vault - skip if your vault already exists.
Set-AzKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, delete, list, wrapKey,unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination "Software"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
# Change the authentication method in the connection string, if needed.
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$database = Get-SqlDatabase -ConnectionString $connStr

# Authenticate to Azure - it is required before calling the next cmdlet.
Add-SqlAzureAuthenticationContext -Interactive

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlAzureKeyVaultColumnMasterKeySettings -KeyURL $akvKey.ID -AllowEnclaveComputations

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="next-steps"></a>後續步驟
- [使用具有安全記憶體保護區的 Always Encrypted 查詢資料行](always-encrypted-enclaves-query-columns.md)
- [使用具有安全記憶體保護區的 Always Encrypted 就地設定資料行加密](always-encrypted-enclaves-configure-encryption.md)
- [為現有加密資料行啟用具有安全記憶體保護區的 Always Encrypted](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [使用具有安全記憶體保護區的 Always Encrypted 開發應用程式](always-encrypted-enclaves-client-development.md) 

## <a name="see-also"></a>另請參閱  
- [教學課程：使用 SSMS，開始使用具有安全記憶體保護區的 Always Encrypted](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [為具有安全記憶體保護區的 Always Encrypted 管理金鑰](always-encrypted-enclaves-manage-keys.md)
- [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 