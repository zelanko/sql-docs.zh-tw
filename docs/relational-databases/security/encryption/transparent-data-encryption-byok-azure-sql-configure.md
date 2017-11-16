---
title: "PowerShell：使用您自己的 Azure Key Vault 金鑰來啟用 TDE | Microsoft Docs"
description: "了解如何設定 Azure SQL Database 和資料倉儲，以開始使用透明資料加密 (TDE) 並用於 PowerShell 的靜態加密。"
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: cguyer
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.workload: Inactive
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.openlocfilehash: 122dfa3b81f526ac5433b3c88dc27637007464df
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="powershell-enable-transparent-data-encryption-using-your-own-key-from-azure-key-vault"></a>PowerShell：使用您自己的 Azure Key Vault 金鑰來啟用透明資料加密

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

本使用說明指南逐步解說如何在 SQL Database 或資料倉儲上，使用 Azure Key Vault 的金鑰進行透明資料加密 (TDE) 。 若要深入了解支援自行管理金鑰 (BYOK) 的 TDE，請瀏覽 [TDE 讓您在 Azure SQL 中自行管理金鑰](transparent-data-encryption-byok-azure-sql.md)。 

## <a name="prerequisites"></a>必要條件

- 您必須擁有 Azure 訂用帳戶，而且是該訂用帳戶的系統管理員。
- [建議但非必要] 備妥硬體安全性模組 (HSM) 或本機金鑰存放區，以建立 TDE 保護裝置金鑰內容的本機複本。
- 您必須安裝並執行 Azure PowerShell 4.2.0 或更新的版本。 
- 建立 Azure Key Vault 和金鑰以用於 TDE。
   - [Key Vault 中的 PowerShell 指示](https://docs.microsoft.com/azure/key-vault/key-vault-get-started)
   - [使用硬體安全性模組 (HSM) 與 Key Vault 的指示](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
- 若要用於 TDE，金鑰必須具有下列屬性：
   - 無到期日
   - 未停用
   - 能夠執行「取得」、「包裝金鑰」和「解除包裝金鑰」作業

## <a name="step-1-assign-an-aad-identity-to-your-server"></a>步驟 1： 將 AAD 身分識別指派給您的伺服器 

如果您具備現有的伺服器，請使用下列程序，將 AAD 身分識別新增至您的伺服器：

   ```powershell
   $server = Set-AzureRmSqlServer `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -AssignIdentity
   ```

如果您要建立伺服器，請使用 [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) Cmdlet 與 -Identity 標記，在伺服器建立期間新增 AAD 身分識別：

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

使用 [Set-AzureRmKeyValutAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) Cmdlet 授與伺服器 Key Vault 存取權限之後，您才能將它的金鑰用於 TDE。

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
>Key Vault 的 KeyId 範例：https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h
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

## <a name="step-5-check-the-encryption-state-and-encryption-activity-of-the-database-or-data-warehouse"></a>步驟 5： 檢查加密狀態及資料庫或資料倉儲的加密活動

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

## <a name="next-steps"></a>後續的步驟

- 了解如何輪替伺服器的 TDE 保護裝置，以符合安全性需求：[使用 PowerShell 輪替透明資料加密保護裝置](transparent-data-encryption-byok-azure-sql-key-rotation.md)。
- 萬一發生安全性風險時，了解如何移除可能被盜用的 TDE 保護裝置：[移除可能被盜用的金鑰](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md)。 


