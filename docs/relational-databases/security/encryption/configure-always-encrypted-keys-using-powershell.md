---
title: 使用 PowerShell 設定 Always Encrypted 金鑰 | Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 3bdf8629-738c-489f-959b-2f5afdaf7d61
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5e8f0eb293390e88f0c7d8f982c0525b5a62f871
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387996"
---
# <a name="configure-always-encrypted-keys-using-powershell"></a>使用 PowerShell 設定永遠加密金鑰
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

    
本文提供使用 [SqlServer PowerShell 模組](../../../relational-databases/scripting/sql-server-powershell-provider.md)佈建永遠加密金鑰的步驟。 您可以使用 PowerShell 佈建永遠加密金鑰， [用不用角色隔離皆可](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md#KeyManagementRoles)，控制能夠存取金鑰存放區中實際加密金鑰以及能夠存取資料庫的人員。 

如需永遠加密金鑰管理概觀，包括一些高階的最佳做法建議，請參閱 [Overview of Key Management for Always Encrypted](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)(永遠加密金鑰管理概觀)。
如需如何開始針對永遠加密使用 SqlServer PowerShell 模組的詳細資訊，請參閱 [Configure Always Encrypted using PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)(使用 PowerShell 設定永遠加密)。


## <a name="KeyProvisionWithoutRoles"></a> 不使用角色隔離的金鑰佈建

本節所述的金鑰佈建方法，不支援安全性系統管理員與 DBA 之間的角色隔離。 下列步驟有些會結合實體金鑰作業和金鑰中繼資料作業。 因此，使用 DevOps 模型的組織，或是如果資料庫裝載於雲端且主要目標是限制雲端管理員 (而不是內部部署 DBA) 存取敏感性資料，建議利用這種方法佈建金鑰。 如果潛在的對象包括 DBA，或是 DBA 不應具有存取敏感性資料的權限，即不建議使用。

請先確定 PowerShell 環境是在不同於裝載資料庫之電腦的安全電腦上執行，再執行與存取純文字金鑰或金鑰存放區相關的任何步驟 (下表中的 [存取純文字金鑰/金鑰存放區]  資料行)。 如需詳細資訊，請參閱 ***金鑰管理的安全性考量***。


工作  |發行項  |存取純文字金鑰/金鑰存放區  |存取資料庫   
---------|---------|---------|---------
步驟 1： 在金鑰存放區中建立資料行主要金鑰。<br><br>**注意：** SqlServer PowerShell 模組不支援此步驟。 若要從命令列完成這項工作，請使用所選金鑰存放區的特有工具。 |[建立及儲存資料行主要金鑰 (永遠加密)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md) | 是 | 否     
步驟 2：  啟動 PowerShell 環境並匯入 SqlServer PowerShell 模組。  |   [Configure Always Encrypted using PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)   |    否    | 否         
步驟 3：  連接到您的伺服器和資料庫。     |     [連接到資料庫](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase)    |    否     | 是         
步驟 4：  建立包含資料行主要金鑰位置相關資訊的 *SqlColumnMasterKeySettings* 物件。 SqlColumnMasterKeySettings 是存在於 PowerShell 記憶體中的物件。 使用金鑰存放區特有的 Cmdlet。   |     [New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)        |   否      | 否         
步驟 5：  在資料庫中建立資料行主要金鑰的相關中繼資料。      |    [New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br><br>**注意︰** 實際上，這個 Cmdlet 發出 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 陳述式來建立金鑰中繼資料。|    否     |    是
步驟 6：  向 Azure 驗證，如果您的資料行主要金鑰儲存在 Azure 金鑰保存庫中。 | [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)    |  是   | 否         
步驟 7：  產生新的資料行加密金鑰，並使用資料行主要金鑰將它加密，然後在資料庫中建立資料行加密金鑰中繼資料。     |    [New-SqlColumnEncryptionKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkey)<br><br>**注意：** 請使用一種可在內部產生並加密資料行加密金鑰的 Cmdlet。<br><br>**注意：** 實際上，這個 Cmdlet 會發出 [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) 陳述式來建立金鑰中繼資料。  | 是 | 是
  

## <a name="windows-certificate-store-without-role-separation-example"></a>不使用角色隔離的 Windows 憑證存放區 (範例)

此指令碼是產生資料行主要金鑰 (此金鑰為 Windows 憑證存放區中的憑證)、產生並加密資料行加密金鑰，以及在 SQL Server 資料庫中建立金鑰中繼資料的端對端範例。


```
# Create a column master key in Windows Certificate Store.
$cert1 = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert1.Thumbprint

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings


# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName  -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="azure-key-vault-without-role-separation-example"></a>不使用角色隔離的 Azure 金鑰保存庫 (範例)

此指令碼是佈建和設定 Azure 金鑰保存庫、在保存庫產生資料行加密金鑰、產生並加密資料行加密金鑰，以及在 Azure SQL 資料庫中建立金鑰中繼資料的端對端範例。


```
# Create a column master key in Azure Key Vault.
Connect-AzAccount
$SubscriptionId = "<Azure SubscriptionId>"
$resourceGroup = "<resource group name>"
$azureLocation = "<datacenter location>"
$akvName = "<key vault name>"
$akvKeyName = "<key name>"
$azureCtx = Set-AzConteXt -SubscriptionId $SubscriptionId # Sets the context for the below cmdlets to the specified subscription.
New-AzResourceGroup -Name $resourceGroup -Location $azureLocation # Creates a new resource group - skip, if you desire group already exists.
New-AzKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation # Creates a new key vault - skip if your vault already exists.
Set-AzKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, delete, list, update, import, backup, restore, wrapKey,unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination "Software"

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database (Azure SQL database).
$serverName = "<Azure SQL server name>.database.windows.net"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Authentication = Active Directory Integrated"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName] 

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlAzureKeyVaultColumnMasterKeySettings -KeyURL $akvKey.ID

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Authenticate to Azure
Add-SqlAzureAuthenticationContext -Interactive

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="cngksp-without-role-separation-example"></a>不使用角色隔離的 CNG/KSP (範例)

下列指令碼是在執行新一代密碼編譯 API (CNG) 的金鑰存放區中產生資料行主要金鑰、產生並加密資料行加密金鑰，以及在 SQL Server 資料庫中建立金鑰中繼資料的端對端範例。

此範例會利用使用 Microsoft 軟體金鑰儲存提供者的金鑰存放區。 您可以選擇修改範例以使用另一個存放區，例如您的硬體安全性模組。 為此，您必須確定實作裝置 CNG 的金鑰存放區提供者 (KSP) 已正確安裝在您的電腦上。 您必須以裝置的 KSP 名稱取代「Microsoft 軟體金鑰儲存提供者」。


```
# Create a column master key in a key store that has a CNG provider, a.k.a key store provider (KSP).
$cngProviderName = "Microsoft Software Key Storage Provider" # If you have an HSM, you can use a KSP for your HSM instead of a Microsoft KSP
$cngAlgorithmName = "RSA"
$cngKeySize = 2048 # Recommended key size for Always Encrypted column master keys
$cngKeyName = "AlwaysEncryptedKey" # Name identifying your new key in the KSP
$cngProvider = New-Object System.Security.Cryptography.CngProvider($cngProviderName)
$cngKeyParams = New-Object System.Security.Cryptography.CngKeyCreationParameters
$cngKeyParams.provider = $cngProvider
$cngKeyParams.KeyCreationOptions = [System.Security.Cryptography.CngKeyCreationOptions]::OverwriteExistingKey
$keySizeProperty = New-Object System.Security.Cryptography.CngProperty("Length", [System.BitConverter]::GetBytes($cngKeySize), [System.Security.Cryptography.CngPropertyOptions]::None);
$cngKeyParams.Parameters.Add($keySizeProperty)
$cngAlgorithm = New-Object System.Security.Cryptography.CngAlgorithm($cngAlgorithmName)
$cngKey = [System.Security.Cryptography.CngKey]::Create($cngAlgorithm, $cngKeyName, $cngKeyParams)

# Import the SqlServer module.
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCngColumnMasterKeySettings -CngProviderName $cngProviderName -KeyName $cngKeyName

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName
```

## <a name="KeyProvisionWithRoles"></a> 使用角色隔離的金鑰佈建

對於安全性管理員不能存取資料庫，而資料庫管理員不能存取金鑰存放區或純文字金鑰，本節提供加密設定步驟。


### <a name="security-administrator"></a>安全性系統管理員

執行與存取純文字金鑰或金鑰存放區相關的任何步驟 (下表中的 [存取純文字金鑰/金鑰存放區]  資料行) 前，請確定︰
1.  PowerShell 環境執行所在的安全電腦，與裝載您資料庫的電腦不同。
2.  貴組織的 DBA 沒有電腦存取權 (會破壞的角色隔離的目的)。

如需詳細資訊，請參閱 [金鑰管理的安全性考量](overview-of-key-management-for-always-encrypted.md#security-considerations-for-key-management)。


工作  |發行項  |存取純文字金鑰/金鑰存放區  |存取資料庫  
---------|---------|---------|---------
步驟 1： 在金鑰存放區中建立資料行主要金鑰。<br><br>**注意：** SqlServer 模組不支援此步驟。 若要從命令列完成這項工作，您需要使用金鑰存放區類型特有的工具。     | [建立及儲存資料行主要金鑰 (永遠加密)](../../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)  |    是    | 否 
步驟 2：  啟動 PowerShell 工作階段並匯入 SqlServer 模組。      |     [匯入 SqlServer 模組](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#importsqlservermodule)     | 否 | 否         
步驟 3：  建立包含資料行主要金鑰位置相關資訊的 *SqlColumnMasterKeySettings* 物件。 *SqlColumnMasterKeySettings* 是存在於 PowerShell 記憶體中的物件。 使用金鑰存放區特有的 Cmdlet。 |      [New-SqlAzureKeyVaultColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlazurekeyvaultcolumnmasterkeysettings)<br><br>[New-SqlCertificateStoreColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcertificatestorecolumnmasterkeysettings)<br><br>[New-SqlCngColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcngcolumnmasterkeysettings)<br><br>[New-SqlCspColumnMasterKeySettings](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcspcolumnmasterkeysettings)   | 否         | 否         
步驟 4：  向 Azure 驗證，如果您的資料行主要金鑰儲存在 Azure 金鑰保存庫中。 |    [Add-SqlAzureAuthenticationContext](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/add-sqlazureauthenticationcontext)    |是|否         
步驟 5：  產生資料行加密金鑰，使用資料行主要金鑰加密，以產生資料行加密金鑰的加密值。     |   [New-SqlColumnEncryptionKeyEncryptedValue](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnencryptionkeyencryptedvalue)     |    是    | 否        
步驟 6：  將資料行主要金鑰 (資料行主要金鑰的提供者名稱與索引鍵資料行) 的位置與資料行加密金鑰的加密值提供給 DBA。  | 請參閱以下的範例。        |   否      | 否         

### <a name="dba"></a>DBA 

DBA 使用接收自安全性系統管理員的資訊 (前文步驟 6)，在資料庫中建立和管理永遠加密金鑰中繼資料。

工作  |發行項  |存取純文字金鑰  |存取資料庫   
---------|---------|---------|---------
步驟 1：  從安全性系統管理員處取得資料行主要金鑰位置以及資料行加密金鑰的加密值。 |請參閱以下的範例。 | 否 | 否
步驟 2：  啟動 PowerShell 環境並匯入 SqlServer 模組。  | [Configure Always Encrypted using PowerShell](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)  | 否 | 否
步驟 3：  連接到您的伺服器和資料庫。 | [連接到資料庫](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md#connectingtodatabase) | 否 | 是
步驟 4：  建立包含資料行主要金鑰位置相關資訊的 SqlColumnMasterKeySettings 物件。 SqlColumnMasterKeySettings 是存在於記憶體中的物件。 | New-SqlColumnMasterKeySettings | 否 | 否
步驟 5： 在資料庫中建立資料行主要金鑰的相關中繼資料 | [New-SqlColumnMasterKey](https://docs.microsoft.com/powershell/sqlserver/sqlserver/vlatest/new-sqlcolumnmasterkey)<br>**注意︰** 實際上，這個 Cmdlet 發出 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md) 陳述式來建立資料行主要金鑰中繼資料。 | 否 | 是
步驟 6： 在資料庫中建立資料行加密金鑰的中繼資料。 | New-SqlColumnEncryptionKey<br>**注意：** DBA 會利用只建立資料行加密金鑰中繼資料的 Cmdlet 變化。<br>實際上，這個 Cmdlet 會發出 [CREATE COLUMN ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-column-encryption-key-transact-sql.md) 陳述式來建立資料行加密金鑰中繼資料。 | 否 | 是
  
## <a name="windows-certificate-store-with-role-separation-example"></a>使用角色隔離的 Windows 憑證存放區 (範例)

### <a name="security-administrator"></a>安全性系統管理員


```
# Create a column master key in Windows Certificate Store.
$storeLocation = "CurrentUser"
$certPath = "Cert:" + $storeLocation + "\My"
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation $certPath -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage DataEncipherment -KeySpec KeyExchange

# Import the SqlServer module
Import-Module "SqlServer"

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlCertificateStoreColumnMasterKeySettings -CertificateStoreLocation "CurrentUser" -Thumbprint $cert.Thumbprint

# Generate a column encryption key, encrypt it with the column master key to produce an encrypted value of the column encryption key.
$encryptedValue = New-SqlColumnEncryptionKeyEncryptedValue -TargetColumnMasterKeySettings $cmkSettings

# Share the location of the column master key and an encrypted value of the column encryption key with a DBA, via a CSV file on a share drive
$keyDataFile = "Z:\keydata.txt"
"KeyStoreProviderName, KeyPath, EncryptedValue" > $keyDataFile
$cmkSettings.KeyStoreProviderName + ", " + $cmkSettings.KeyPath + ", " + $encryptedValue >> $keyDataFile

# Read the key data back to verify
$keyData = Import-Csv $keyDataFile
$keyData.KeyStoreProviderName
$keyData.KeyPath
$keyData.EncryptedValue 
```

### <a name="dba"></a>DBA

```
# Obtain the location of the column master key and the encrypted value of the column encryption key from your Security Administrator, via a CSV file on a share drive.
$keyDataFile = "Z:\keydata.txt"
$keyData = Import-Csv $keyDataFile

# Import the SqlServer module
Import-Module "SqlServer"

# Connect to your database.
$serverName = "<server name>"
$databaseName = "<database name>"
$connStr = "Server = " + $serverName + "; Database = " + $databaseName + "; Integrated Security = True"
$connection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$connection.ConnectionString = $connStr
$connection.Connect()
$server = New-Object Microsoft.SqlServer.Management.Smo.Server($connection)
$database = $server.Databases[$databaseName]

# Create a SqlColumnMasterKeySettings object for your column master key. 
$cmkSettings = New-SqlColumnMasterKeySettings -KeyStoreProviderName $keyData.KeyStoreProviderName -KeyPath $keyData.KeyPath

# Create column master key metadata in the database.
$cmkName = "CMK1"
New-SqlColumnMasterKey -Name $cmkName -InputObject $database -ColumnMasterKeySettings $cmkSettings

# Generate a  column encryption key, encrypt it with the column master key and create column encryption key metadata in the database. 
$cekName = "CEK1"
New-SqlColumnEncryptionKey -Name $cekName -InputObject $database -ColumnMasterKey $cmkName -EncryptedValue $keyData.EncryptedValue
```  
 
## <a name="next-steps"></a>Next Steps    

- [使用 PowerShell 設定資料行加密](../../../relational-databases/security/encryption/configure-column-encryption-using-powershell.md)    
- [使用 PowerShell 更換永遠加密金鑰](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
    
## <a name="additional-resources"></a>其他資源    
    
- [Always Encrypted 的金鑰管理概觀](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [使用 PowerShell 設定 Always Encrypted](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)
- [Always Encrypted (資料庫引擎)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [永遠加密 (用戶端開發)](../../../relational-databases/security/encryption/always-encrypted-client-development.md)
- [永遠加密部落格](https://blogs.msdn.microsoft.com/sqlsecurity/tag/always-encrypted/)

