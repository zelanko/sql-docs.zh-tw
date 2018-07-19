---
title: PowerShell 與 CLI：使用您自己的 Azure Key Vault 金鑰啟用 SQL TDE | Microsoft Docs
description: 了解如何設定 Azure SQL Database 和資料倉儲，以開始使用透明資料加密 (TDE) 並用於 PowerShell 或 CLI 的靜態加密。
keywords: ''
documentationcenter: ''
author: aliceku
manager: craigg
editor: ''
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.tgt_pltfrm: ''
ms.devlang: azurecli, powershell
ms.topic: conceptual
ms.date: 06/28/2018
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 5b6a5d6eafc76b80a169332f8c71309440c4ef0f
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093312"
---
# <a name="powershell-and-cli-enable-transparent-data-encryption-using-your-own-key-from-azure-key-vault"></a>PowerShell 與 CLI：使用 Azure Key Vault 中您自己的金鑰來啟用透明資料加密

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

本使用說明指南逐步解說如何在 SQL Database 或資料倉儲上，使用 Azure Key Vault 的金鑰進行透明資料加密 (TDE) 。 若要深入了解支援自行管理金鑰 (BYOK) 的 TDE，請瀏覽 [TDE 讓您在 Azure SQL 中自行管理金鑰](transparent-data-encryption-byok-azure-sql.md)。 

## <a name="prerequisites-for-powershell"></a>PowerShell 的必要條件

- 您必須擁有 Azure 訂用帳戶，而且是該訂用帳戶的系統管理員。
- [建議但非必要] 備妥硬體安全性模組 (HSM) 或本機金鑰存放區，以建立 TDE 保護裝置金鑰內容的本機複本。
- 您必須安裝並執行 Azure PowerShell 4.2.0 或更新的版本。 
- 建立 Azure Key Vault 和金鑰以用於 TDE。
   - [Key Vault 中的 PowerShell 指示](https://docs.microsoft.com/azure/key-vault/key-vault-get-started)
   - [使用硬體安全性模組 (HSM) 與 Key Vault 的指示](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
 - 金鑰保存庫必須具有以下屬性才能供 TDE 使用：
   - [虛刪除](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-ovw-soft-delete)
   - [如何透過 PowerShell 使用金鑰保存庫虛刪除](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-soft-delete-powershell) 
- 若要用於 TDE，金鑰必須具有下列屬性：
   - 無到期日
   - 未停用
   - 能夠執行「取得」、「包裝金鑰」和「解除包裝金鑰」作業

## <a name="step-1-assign-an-azure-ad-identity-to-your-server"></a>步驟 1： 將 Azure AD 身分識別指派給您的伺服器 

若您有現有的伺服器，請使用下列項目將 Auzre AD 身分識別新增至您的伺服器：

   ```powershell
   $server = Set-AzureRmSqlServer `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -AssignIdentity
   ```

如果您要建立伺服器，請使用 [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) Cmdlet 與 -Identity 標籤，在伺服器建立期間新增 Azure AD 身分識別：

   ```powershell
   $server = New-AzureRmSqlServer `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -Location <RegionName> `
   -ServerName <LogicalServerName> `
   -ServerVersion "12.0" `
   -SqlAdministratorCredentials <PSCredential> `
   -AssignIdentity 
   ```

## <a name="step-2-grant-key-vault-permissions-to-your-server"></a>步驟 2： 授與伺服器 Key Vault 權限

使用 [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) Cmdlet 將金鑰保存庫的存取權限授與伺服器之後，您才能將它的金鑰用於 TDE。

   ```powershell
   Set-AzureRmKeyVaultAccessPolicy  `
   -VaultName <KeyVaultName> `
   -ObjectId $server.Identity.PrincipalId `
   -PermissionsToKeys get, wrapKey, unwrapKey
   ```

## <a name="step-3-add-the-key-vault-key-to-the-server-and-set-the-tde-protector"></a>步驟 3： 將 Key Vault 金鑰新增至伺服器，並設定 TDE 保護裝置

- 使用 [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) Cmdlet 將金鑰從 Key Vault 新增至伺服器。
- 使用 [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) Cmdlet，將金鑰設為所有伺服器資源的 TDE 保護裝置。
- 使用 [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) Cmdlet，確認 TDE 保護裝置已如預期方式設定。

> [!Note]
> Key Vault 名稱和金鑰名稱的組合長度不能超過 94 個字元。
> 

>[!Tip]
>Key Vault 的 KeyId 範例： https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h
>

   ```powershell
   <# Add the key from Key Vault to the server #>
   Add-AzureRmSqlServerKeyVaultKey `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -KeyId <KeyVaultKeyId>

   <# Set the key as the TDE protector for all resources under the server #>
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> 

   <# To confirm that the TDE protector was configured as intended: #>
   Get-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> 
   ```

## <a name="step-4-turn-on-tde"></a>步驟 4： 開啟 TDE 

使用 [Set-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) Cmdlet 來開啟 TDE。

   ```powershell
   Set-AzureRMSqlDatabaseTransparentDataEncryption `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName> `
   -State "Enabled"
   ```

目前，資料庫或資料倉儲都已啟用 TDE，並具有 Key Vault 加密金鑰。

## <a name="step-5-check-the-encryption-state-and-encryption-activity"></a>步驟 5： 檢查加密狀態與加密活動

使用 [Get-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) 取得加密狀態，並使用 [Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) 檢查資料庫或資料倉儲的加密進度。

   ```powershell
   # Get the encryption state
   Get-AzureRMSqlDatabaseTransparentDataEncryption `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName> `

   <# Check the encryption progress for a database or data warehouse #>
   Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName>  
   ```

## <a name="other-useful-powershell-cmdlets"></a>其他有用的 PowerShell Cmdlet

- 使用 [Set-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) Cmdlet 來關閉 TDE。

   ```powershell
   Set-AzureRMSqlDatabaseTransparentDataEncryption `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -DatabaseName <DatabaseName> `
   -State "Disabled”
   ```
 
- 使用 [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) Cmdlet 傳回新增至伺服器的 Key Vault 金鑰清單。

   ```powershell
   <# KeyId is an optional parameter, to return a specific key version #>
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>
   ```
 
- 使用 [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey)，從伺服器移除 Key Vault 金鑰。

   ```powershell
   <# The key set as the TDE Protector cannot be removed. #>
   Remove-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>   
   ```
 
## <a name="troubleshooting"></a>疑難排解

如果發生問題，請檢查下列項目：
- 如果找不到 Key Vault，請使用 [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription) Cmdlet，確認您使用正確的訂用帳戶。

   ```powershell
   Get-AzureRmSubscription `
   -SubscriptionId <SubscriptionId>
   ```

- 如果您無法將新的金鑰新增至伺服器，或新的金鑰無法更新為 TDE 保護裝置，請檢查下列項目：
   - 金鑰不應該有到期日
   - 金鑰必須啟用「取得」、「包裝金鑰」和「解除包裝金鑰」作業。

## <a name="next-steps"></a>後續步驟

- 了解如何輪替伺服器的 TDE 保護裝置，以符合安全性需求：[使用 PowerShell 輪替透明資料加密保護裝置](transparent-data-encryption-byok-azure-sql-key-rotation.md)。
- 萬一發生安全性風險時，了解如何移除可能被盜用的 TDE 保護裝置：[移除可能被盜用的金鑰](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md)。 

## <a name="prerequisites-for-cli"></a>CLI 的必要條件

- 您必須擁有 Azure 訂用帳戶，而且是該訂用帳戶的系統管理員。
- [建議但非必要] 備妥硬體安全性模組 (HSM) 或本機金鑰存放區，以建立 TDE 保護裝置金鑰內容的本機複本。
- 命令列介面 2.0 版或更新版本。 若要安裝最新版本並連線至您的 Azure 訂用帳戶，請參閱[安裝及設定 Azure 跨平台命令列介面 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)。 
- 建立 Azure Key Vault 和金鑰以用於 TDE。
   - [使用 CLI 2.0 管理 Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-manage-with-cli2)
   - [使用硬體安全性模組 (HSM) 與 Key Vault 的指示](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
 - 金鑰保存庫必須具有以下屬性才能供 TDE 使用：
   - [虛刪除](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-ovw-soft-delete)
   - [如何透過 CLI 使用金鑰保存庫虛刪除](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-soft-delete-cli) 
- 若要用於 TDE，金鑰必須具有下列屬性：
   - 無到期日
   - 未停用
   - 能夠執行「取得」、「包裝金鑰」和「解除包裝金鑰」作業
   
## <a name="step-1-create-a-server-and-assign-an-azure-ad-identity-to-your-server"></a>步驟 1： 建立伺服器並將 Azure AD 身分識別指派給您的伺服器
      cli
      # create server (with identity) and database
      az sql server create -n "ServerName" -g "ResourceGroupName" -l "westus" -u "cloudsa" -p "YourFavoritePassWord99@34" -I 
      az sql db create -n "DatabaseName" -g "ResourceGroupName" -s "ServerName" 
      

 
## <a name="step-2-grant-key-vault-permissions-to-your-server"></a>步驟 2： 授與伺服器 Key Vault 權限
      cli
      # create key vault, key and grant permission
      az keyvault create -n "VaultName" -g "ResourceGroupName" 
      az keyvault key create -n myKey -p software --vault-name "VaultName" 
      az keyvault set-policy -n "VaultName" --object-id "ServerIdentityObjectId" -g "ResourceGroupName" --key-permissions wrapKey unwrapKey get list 
      

 
## <a name="step-3-add-the-key-vault-key-to-the-server-and-set-the-tde-protector"></a>步驟 3： 將 Key Vault 金鑰新增至伺服器，並設定 TDE 保護裝置
  
     cli
     # add server key and update encryption protector
      az sql server key create -g "ResourceGroupName" -s "ServerName" -t "AzureKeyVault" -u "FullVersionedKeyUri 
      az sql server tde-key update -g "ResourceGroupName" -s "ServerName" -t AzureKeyVault -u "FullVersionedKeyUri" 
      
  
  > [!Note]
> Key Vault 名稱和金鑰名稱的組合長度不能超過 94 個字元。
> 

>[!Tip]
>Key Vault 的 KeyId 範例： https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h
>
  
## <a name="step-4-turn-on-tde"></a>步驟 4： 開啟 TDE 
      cli
      # enable encryption
      az sql db tde create -n "DatabaseName" -g "ResourceGroupName" -s "ServerName" --status Enabled 
      

目前，資料庫或資料倉儲都已啟用 TDE，並具有 Key Vault 加密金鑰。

## <a name="step-5-check-the-encryption-state-and-encryption-activity"></a>步驟 5： 檢查加密狀態與加密活動

     cli
      # get encryption scan progress
      az sql db tde show-activity -n "DatabaseName" -g "ResourceGroupName" -s "ServerName" 

      # get whether encryption is on or off
      az sql db tde show-configuration -n "DatabaseName" -g "ResourceGroupName" -s "ServerName" 

## <a name="sql-cli-references"></a>SQL CLI 參考

https://docs.microsoft.com/en-us/cli/azure/sql?view=azure-cli-latest 

https://docs.microsoft.com/en-us/cli/azure/sql/server/key?view=azure-cli-latest 

https://docs.microsoft.com/en-us/cli/azure/sql/server/tde-key?view=azure-cli-latest 

https://docs.microsoft.com/en-us/cli/azure/sql/db/tde?view=azure-cli-latest 

