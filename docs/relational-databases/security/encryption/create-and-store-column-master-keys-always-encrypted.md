---
title: 建立及儲存資料行主要金鑰 (永遠加密) | Microsoft Docs
ms.custom: ''
ms.date: 07/01/2016
ms.prod: sql
ms.prod_service: security, sql-database"
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
ms.assetid: 856e8061-c604-4ce4-b89f-a11876dd6c88
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0ea144a638bd64446e61b5bcbfed8397d5784d6a
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/05/2019
ms.locfileid: "67585424"
---
# <a name="create-and-store-column-master-keys-always-encrypted"></a>建立及儲存資料行主要金鑰 (永遠加密)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

「資料行主要金鑰」  是用來在永遠加密中，加密資料行加密金鑰的金鑰保護型金鑰。 資料行主要金鑰必須儲存在受信任的金鑰存放區，且需要加密或解密資料的應用程式、設定永遠加密和管理永遠加密金鑰的工具必須能存取該金鑰。

本文章提供選取金鑰存放區，以及建立永遠加密之資料行主要金鑰的詳細資訊。 如需詳細概觀，請參閱 [永遠加密的金鑰管理概觀](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。

## <a name="selecting-a-key-store-for-your-column-master-key"></a>選取資料行主要金鑰的金鑰存放區

永遠加密支援以多個金鑰存放區來儲存永遠加密的資料行主要金鑰。 支援的金鑰存放區會依您使用的驅動程式和版本而有所不同。

有兩種高階金鑰存放區可以考慮 - 本機金鑰存放區  ，和集中式金鑰存放區  。

###  <a name="local-or-centralized-key-store"></a>本機或集中式金鑰存放區？

* **本機金鑰存放區** - 僅能供包含本機金鑰存放區之電腦上的應用程式使用。 換句話說，您需要將金鑰存放區和金鑰複寫到每一部執行應用程式的電腦上。 本機金鑰存放區的其中一個範例是 Windows 憑證存放區。 使用本機金鑰存放區時，您需要確定金鑰存放區存在於每部裝載您應用程式的電腦上，且電腦包含您應用程式存取使用永遠加密保護之資料所需的資料行主要金鑰。 當您第一次提供資料行主要金鑰時，或是當您變更 (輪替) 金鑰時，必須先確認金鑰已部署至裝載您應用程式的所有電腦。

* **集中式金鑰存放區** - 服務多部電腦上的應用程式。 集中式金鑰存放區的其中一個範例是 [Azure 金鑰保存庫](https://azure.microsoft.com/services/key-vault/)。 集中式金鑰存放區通常能簡化金鑰管理，因為您不需要在多部電腦上維護多份的資料行主要金鑰。 您需要確保您的應用程式已設定為連接至集中式金鑰存放區。

### <a name="which-key-stores-are-supported-in-always-encrypted-enabled-client-drivers"></a>已啟用永遠加密的用戶端驅動程式中支援哪些金鑰存放區？

已啟用永遠加密的用戶端驅動程式，是已具有將永遠加密納入用戶端應用程式之內建支援的 SQL Server 用戶端驅動程式。 已啟用永遠加密的驅動程式包含受歡迎之金鑰存放區的幾個內建提供者。 請注意，有些驅動程式也可讓您實作並註冊自訂的資料行主要金鑰存放區提供者，以便您可以使用任何金鑰存放區，即使它沒有內建提供者。 在內建提供者與自訂提供者之間做決定時，請考慮使用內建提供者通常表示您的應用程式有較少的變更 (在某些情況下，只需要變更資料庫的連接字串)。

可用的內建提供者取決於選取的驅動程式、驅動程式版本和作業系統。  請查閱您特定驅動程式的永遠加密文件，以判斷目前支援哪些金鑰存放區，以及驅動程式是否支援自訂金鑰存放區提供者。

- [搭配 .NET Framework Data Provider for SQL Server 使用永遠加密來開發應用程式](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)


### <a name="supported-tools"></a>支援的工具

您可以使用 [SQL Server Management Studio](../../../ssms/sql-server-management-studio-ssms.md) 和 [SqlServer PowerShell 模組](https://blogs.technet.microsoft.com/dataplatforminsider/2016/06/30/sql-powershell-july-2016-update) 來設定永遠加密和管理永遠加密金鑰。 如需這些工具支援的金鑰存放區清單，請參閱︰

- [使用 SQL Server Management Studio 設定永遠加密](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)
- [使用 PowerShell 設定永遠加密](../../../relational-databases/security/encryption/configure-always-encrypted-using-powershell.md)


## <a name="creating-column-master-keys-in-windows-certificate-store"></a>在 Windows 憑證存放區中建立資料行主要金鑰    

資料行主要金鑰可以是儲存在 Windows 憑證存放區中的憑證。 請注意，已啟用永遠加密的驅動程式不會驗證到期日或憑證授權單位鏈結。 憑證只當作金鑰組使用，其中包含公開和私密金鑰。

若要成為有效的資料行主要金鑰，憑證必須︰
* 是 X.509 憑證。
* 儲存在兩個憑證存放區位置的其中一個︰本機  或目前使用者  。 (若要在本機電腦憑證存放區位置中建立憑證，您必須是目標電腦的系統管理員。)
* 包含私密金鑰 (憑證中建議的金鑰長度為 2048 位元或更多)。
* 針對金鑰交換而建立。


有多種方法可以建立作為有效資料行主要金鑰的憑證，但最簡單的選項是建立自我簽署的憑證。


### <a name="create-a-self-signed-certificate-using-powershell"></a>使用 PowerShell 建立自我簽署憑證

使用 [New-SelfSignedCertificate](/powershell/module/pkiclient/new-selfsignedcertificate) Cmdlet 來建立自我簽署的憑證。 下列範例示範如何產生可以作為永遠加密之資料行主要金鑰的憑證。

```
# New-SelfSignedCertificate is a Windows PowerShell cmdlet that creates a self-signed certificate. The below examples show how to generate a certificate that can be used as a column master key for Always Encrypted.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:CurrentUser\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048 

# To create a certificate in the local machine certificate store location you need to run the cmdlet as an administrator.
$cert = New-SelfSignedCertificate -Subject "AlwaysEncryptedCert" -CertStoreLocation Cert:LocalMachine\My -KeyExportPolicy Exportable -Type DocumentEncryptionCert -KeyUsage KeyEncipherment -KeySpec KeyExchange -KeyLength 2048
```

### <a name="create-a-self-signed-certificate-using-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 建立自我簽署的憑證

如需詳細資訊，請參閱 [使用 SQL Server Management Studio 設定永遠加密](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)。
如需使用 SSMS，並將永遠加密金鑰儲存在 Windows 憑證存放區中的逐步教學課程，請參閱 [永遠加密精靈教學課程 (Windows 憑證存放區)](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted/)。


### <a name="making-certificates-available-to-applications-and-users"></a>讓憑證可供應用程式和使用者使用

如果您的資料行主要金鑰是儲存在「本機」  憑證存放區位置的憑證，您需要使用私密金鑰匯出憑證，並將它匯入到裝載預期要加密或解密儲存在加密資料行中之資料的應用程式，或是裝載用於設定永遠加密及管理永遠加密金鑰之工具的所有電腦。 此外，每位使用者必須具有儲存在本機電腦憑證存放區位置之憑證的讀取權限，才能使用此憑證作為資料行主要金鑰。

如果您的資料行主要金鑰是儲存在「目前使用者」  憑證存放區位置的憑證，您需要使用私密金鑰匯出憑證，並針對執行預期要加密或解密儲存在加密資料行中之資料的應用程式，或是執行用於設定永遠加密及管理永遠加密金鑰之工具的所有使用者帳戶，將它匯入到目前使用者憑證存放區位置。 登入電腦之後不需要設定權限，使用者可以存取其目前使用者憑證存放區位置中的所有憑證。

#### <a name="using-powershell"></a>使用 PowerShell
使用 [Import-PfxCertificate](/powershell/module/pkiclient/import-pfxcertificate) 和 [Export-PfxCertificate](/powershell/module/pkiclient/export-pfxcertificate) Cmdlet 匯入及匯出憑證。

#### <a name="using-microsoft-management-console"></a>使用 Microsoft Management Console 

若要授與使用者對於儲存在本機電腦憑證存放區位置之憑證的「讀取」  ，請遵循下列步驟︰

1.  開啟 [命令提示字元]，並輸入 **mmc**。
2.  在 MMC 主控台的 [檔案]  功能表上，按一下 [新增/移除嵌入式管理單元]  。
3.  在 [新增/移除嵌入式管理單元]  對話方塊中，按一下 [新增]  。
4.  在 [新增獨立嵌入式管理單元]  對話方塊中，按一下 [憑證]  ，然後按 [新增]  。
5.  在 [憑證嵌入式管理單元]  對話方塊中，按一下 [電腦帳戶]  ，然後按 [完成]  。
6.  在 [新增獨立嵌入式管理單元]  對話方塊中，按一下 [關閉]  。
7.  在 [新增/移除嵌入式管理單元]  對話方塊中，按一下 [確定]  。
8.  從 [憑證]  嵌入式管理單元的 [憑證] > [個人]  資料夾中找到憑證，以滑鼠右鍵按一下 [憑證]，再指向 [所有工作]  ，然後按一下 [管理私密金鑰]  。
9.  在 [安全性]  對話方塊方塊中，視需要新增使用者帳戶的讀取權限。

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="creating-column-master-keys-in-azure-key-vault"></a>在 Azure 金鑰保存庫中建立資料行主要金鑰

Azure 金鑰保存庫可協助保護密碼編譯金鑰和密碼，並且是存放永遠加密資料行主要金鑰的方便選項，尤其是當應用程式裝載在 Azure 時。 若要在 [Azure 金鑰保存庫](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)建立金鑰，您需要 [Azure 訂用帳戶](https://azure.microsoft.com/free/) 和 Azure 金鑰保存庫。

#### <a name="using-powershell"></a>使用 PowerShell

下列範例會建立新的 Azure 金鑰保存庫和金鑰，並將權限授與所需的使用者。

```
# Create a column master key in Azure Key Vault.
Connect-AzAccount
$SubscriptionId = "<Azure subscription ID>"
$resourceGroup = "<resource group name>"
$azureLocation = "<key vault location>"
$akvName = "<key vault name>"
$akvKeyName = "<column master key name>"
$azureCtx = Set-AzContext -SubscriptionId $SubscriptionId # Sets the context for the below cmdlets to the specified subscription.
New-AzResourceGroup -Name $resourceGroup -Location $azureLocation # Creates a new resource group - skip, if you desire group already exists.
New-AzKeyVault -VaultName $akvName -ResourceGroupName $resourceGroup -Location $azureLocation -SKU premium # Creates a new key vault - skip if your vault already exists.
Set-AzKeyVaultAccessPolicy -VaultName $akvName -ResourceGroupName $resourceGroup -PermissionsToKeys get, create, delete, list, update, import, backup, restore, wrapKey, unwrapKey, sign, verify -UserPrincipalName $azureCtx.Account
$akvKey = Add-AzureKeyVaultKey -VaultName $akvName -Name $akvKeyName -Destination HSM
```

#### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)

如需使用 SSMS，並將永遠加密金鑰儲存在 Azure 金鑰保存庫中的逐步教學課程，請參閱 [永遠加密精靈教學課程 (Azure 金鑰保存庫)](https://azure.microsoft.com/documentation/articles/sql-database-always-encrypted-azure-key-vault)。

### <a name="making-azure-key-vault-keys-available-to-applications-and-users"></a>讓 Azure 金鑰保存庫金鑰可供應用程式和使用者使用

使用 Azure Key Vault 金鑰作為資料行主要金鑰時，您的應用程式必須向 Azure 驗證，且應用程式的身分識別必須對金鑰保存庫有下列權限︰*get*、*unwrapKey* 和 *verify*。 

若要佈建由儲存在 Azure 金鑰保存庫中之資料行主要金鑰所保護的資料行加密金鑰，您需要 *get*、 *unwrapKey*、 *wrapKey*、 *sign*和 *verify* 權限。 此外，若要在 Azure 金鑰保存庫中建立新的金鑰，您需要 *create* 權限；若要列出金鑰保存庫的內容，您需要 *list* 權限。

#### <a name="using-powershell"></a>使用 PowerShell

若要讓使用者和應用程式能存取 Azure Key Vault 中的實際金鑰，您必須設定保存庫的存取原則 ([Set-AzKeyVaultAccessPolicy](https://docs.microsoft.com/powershell/module/az.keyvault/set-azkeyvaultaccesspolicy))：

```
$vaultName = "<vault name>"
$resourceGroupName = "<resource group name>"
$userPrincipalName = "<user to grant access to>"
$clientId = "<client Id>"

# grant users permissions to the keys:
Set-AzKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
# grant applications permissions to the keys:
Set-AzKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list
```

## <a name="creating-column-master-keys-in-hardware-security-modules-using-cng"></a>使用 CNG 在硬體安全性模組中建立資料行主要金鑰

永遠加密的資料行主要金鑰可以儲存在實作 Cryptography Next Generation (CNG) API 的金鑰存放區中。 這種類型的存放區通常是硬體安全性模組 (HSM)。 HSM 是保護和管理數位金鑰，並提供密碼編譯處理的實體裝置。 HSM 傳統上為插入卡或直接連接到電腦 (本機 HSM) 或網路伺服器的外部裝置形式。

若要讓 HSM 可供指定電腦上的應用程式使用，實作 CNG 的金鑰儲存提供者 (KSP)，必須安裝及設定在電腦上。 永遠加密用戶端驅動程式 (驅動程式內的資料行主要金鑰存放區提供者)，使用 KSP 來加密和解密資料行加密金鑰 (使用金鑰存放區中儲存的資料行主要金鑰所保護)。

Windows 包含 Microsoft 軟體金鑰儲存提供者 - 以軟體為基礎的 KSP，您可以用它進行測試用途。 請參閱 [CNG 金鑰儲存提供者](/windows/desktop/SecCertEnroll/cng-key-storage-providers)。

### <a name="creating-column-master-keys-in-a-key-store-using-cngksp"></a>使用 CNG/KSP 在金鑰存放區中建立資料行主要金鑰

資料行主要金鑰應該是使用 RSA 演算法的非對稱金鑰 (公開/私密金鑰組)。 建議的金鑰長度為 2048 或更多。

#### <a name="using-hsm-specific-tools"></a>使用 HSM 特定工具
請參閱您的 HSM 文件。

#### <a name="using-powershell"></a>使用 PowerShell

您可以使用 .NET API，在 PowerShell 中使用 CNG 在金鑰存放區中建立金鑰。


```
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
```

#### <a name="using-sql-server-management-studio"></a>使用 SQL Server Management Studio

請參閱 [Provisioning Column Master using SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt757096.aspx#Anchor_2)(使用 SQL Server Management Studio (SSMS) 佈建資料行主要金鑰)。


### <a name="making-cng-keys-available-to-applications-and-users"></a>讓 CNG 金鑰可供應用程式和使用者使用

請參閱您的 HSM 和 KSP 文件，以了解如何在電腦上設定 KSP，以及如何將應用程式和使用者的存取權授與 HSM。

## <a name="creating-column-master-keys-in-hardware-security-modules-using-capi"></a>使用 CAPI 在硬體安全性模組中建立資料行主要金鑰

永遠加密的資料行主要金鑰可以儲存在實作密碼編譯 API (CAPI) 的金鑰存放區中。 一般而言，這類型的存放區是硬體安全性模組 (HSM)，可保護和管理數位金鑰，並提供密碼編譯處理的實體裝置。 HSM 傳統上為插入卡或直接連接到電腦 (本機 HSM) 或網路伺服器的外部裝置形式。

若要讓 HSM 可供指定電腦上的應用程式使用，實作 CAPI 的密碼編譯服務提供者 (CSP)，必須安裝及設定在電腦上。 永遠加密用戶端驅動程式 (驅動程式內的資料行主要金鑰存放區提供者)，使用 CSP 來加密和解密資料行加密金鑰 (使用金鑰存放區中儲存的資料行主要金鑰所保護)。 注意:CAPI 是已被取代的舊版 API。 如果 KSP 可用於您的 HSM，您應該使用它，而不要使用 CSP/CAPI。

CSP 必須支援 RSA 演算法才能搭配永遠加密。

Windows 包含下列以軟體為基礎 (不受 HSM 支援 HSM) 的 CSP，它們支援 RSA 且可以用於測試用途：Microsoft Enhanced RSA 和 AES 密碼編譯提供者。

### <a name="creating-column-master-keys-in-a-key-store-using-capicsp"></a>使用 CAPI/CSP 在金鑰存放區中建立資料行主要金鑰

資料行主要金鑰應該是使用 RSA 演算法的非對稱金鑰 (公開/私密金鑰組)。 建議的金鑰長度為 2048 或更多。

#### <a name="using-hsm-specific-tools"></a>使用 HSM 特定工具
請參閱您的 HSM 文件。

#### <a name="using-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS)
請參閱＜使用 SQL Server Management Studio 設定永遠加密＞的＜佈建資料行主要金鑰＞一節。

 
### <a name="making-cng-keys-available-to-applications-and-users"></a>讓 CNG 金鑰可供應用程式和使用者使用
請參閱您的 HSM 和 CSP 文件，以了解如何在電腦上設定 CSP，以及如何將應用程式和使用者的存取權授與 HSM。
 
 
## <a name="next-steps"></a>Next Steps  
  
- [使用 PowerShell 設定永遠加密金鑰](../../../relational-databases/security/encryption/configure-always-encrypted-keys-using-powershell.md)
- [使用 PowerShell 輪替永遠加密金鑰](../../../relational-databases/security/encryption/rotate-always-encrypted-keys-using-powershell.md)
- [使用 SQL Server Management Studio 設定永遠加密](../../../relational-databases/security/encryption/configure-always-encrypted-using-sql-server-management-studio.md)

  
## <a name="additional-resources"></a>其他資源  

- [永遠加密的金鑰管理概觀](../../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)
- [Always Encrypted (資料庫引擎)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [搭配 .NET Framework Data Provider for SQL Server 使用永遠加密來開發應用程式](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [永遠加密部落格](https://blogs.msdn.microsoft.com/sqlsecurity/tag/always-encrypted/)
    

