---
title: "PowerShell - 移除 TDE 保護裝置 - Azure SQL | Microsoft Docs"
description: "針對使用攜帶您自己的金鑰 (BYOK) 支援之 TDE 的 Azure SQL Database 或資料倉儲，回應可能遭盜用的 TDE 保護裝置的＜如何＞指南。"
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: jhubbard
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
ms.translationtype: HT
ms.sourcegitcommit: 46b16dcf147dbd863eec0330e87511b4ced6c4ce
ms.openlocfilehash: 861a24ef2f0bc26adece27b2612d4bf2d4640a63
ms.contentlocale: zh-tw
ms.lasthandoff: 09/05/2017

---


# <a name="remove-a-transparent-data-encryption-tde-protector-using-powershell"></a>使用 PowerShell 移除透明資料加密 (TDE) 保護裝置

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

## <a name="prerequisites"></a>必要條件
- 您必須擁有 Azure 訂閱，而且是該訂閱的系統管理員。
- 您必須安裝並執行 Azure PowerShell 4.2.0 或更新的版本。 
- 本＜如何＞指南假設 Azure SQL Database 或資料倉儲的 TDE 保護裝置已經使用 Azure Key Vault 的金鑰。 若要深入了解，請參閱[有 BYOK 支援的透明資料加密](transparent-data-encryption-byok-azure-sql.md)。

## <a name="overview"></a>概觀
本＜如何＞指南說明使用攜帶您自己的金鑰 (BYOK) 支援的 TDE 的 Azure SQL Database 或資料倉儲，如何回應可能遭盜用的 TDE 保護裝置。 若要深入了解 TDE 的 BYOK 支援，請參閱[概觀頁面](transparent-data-encryption-byok-azure-sql.md)。 

只有極端情況或測試環境中才執行下列程序。 請仔細檢閱＜如何＞指南，因為從 Azure Key Vault 主動刪除所用 TDE 保護裝置，會導致**資料遺失**。 

如果金鑰曾懷疑遭盜用，例如服務或使用者有未經授權的金鑰存取權，最好刪除金鑰。

請記住，一旦刪除 Key Vault 中的 TDE 保護裝置，即**封鎖伺服器下加密資料庫的所有連線，且將這些資料庫離線，於 24 小時內卸除**。 無法再存取以遭盜用金鑰加密的舊備份。

根據事件回應之後所要的結果，本＜如何＞指南會仔細檢查兩種方法：
- 保持 Azure SQL Database/資料倉儲**可存取**
- 使 Azure SQL Database/資料倉儲**無法存取**

## <a name="to-keep-the-encrypted-resources-accessible"></a>保持加密的資源可存取
1. 建立 [Key Vault 的新機碼](https://docs.microsoft.com/powershell/module/azurerm.keyvault/add-azurekeyvaultkey?view=azurermps-4.1.0)。 請確定這個新金鑰建立的金鑰保存庫，與可能遭盜用的 TDE 保護裝置不同，因為存取控制是佈建在保存庫層級上。 
2. 使用 [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) 和 [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) Cmdlet 將新的金鑰新增至伺服器，並將它更新為伺服器的新 TDE 保護裝置。

   ```powershell
   # Add the key from Key Vault to the server  
   Add-AzureRmSqlServerKeyVaultKey `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -KeyId <KeyVaultKeyId>
   
   # Set the key as the TDE protector for all resources under the server
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -Type AzureKeyVault -KeyId <KeyVaultKeyId> 
   ```

3. 請確定已使用 [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) Cmdlet 將伺服器和任何複本更新為新的 TDE 保護裝置。 

   >[!NOTE]
   > 新的 TDE 保護裝置可能需要幾分鐘才會傳播到所有資料庫及伺服器下的次要資料庫。
   >

   ```powershell
   Get-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>
   ```

4. 使用 Key Vault 的[新金鑰備份](/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey)。

   ```powershell
   <# -OutputFile parameter is optional; 
   if removed, a file name is automatically generated. #>
   Backup-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -OutputFile <DesiredBackupFilePath>
   ```
 
5. 使用 [Remove-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/remove-azurekeyvaultkey) Cmdlet 從 Key Vault 刪除遭盜用的金鑰。 

   ```powershell
   Remove-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName>
   ```
 
6. 使用 [Restore-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/restore-azurekeyvaultkey) Cmdlet 日後可將機碼還原到 Key Vault：
   ```powershell
   Restore-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -InputFile <BackupFilePath>
   ```
 
## <a name="to-make-the-encrypted-resources-inaccessible"></a>使加密的資源無法存取
1. 卸除由可能遭盜用之金鑰加密的資料庫。
資料庫和記錄檔會自動備份，因此資料庫的還原時間點可為任何時間點 (只要您提供金鑰)。 必須先卸除資料庫，再刪除作用中的 TDE 保護裝置，以免可能遺失最多 10 分鐘的最新交易資料。 
2. 將 TDE 保護裝置的金鑰內容備份在 Key Vault 中。
3. 從 Key Vault 移除可能遭盜用的金鑰

## <a name="next-steps"></a>後續的步驟

- 了解如何輪替伺服器的 TDE 保護裝置，以符合安全性需求：[使用 PowerShell 輪替透明資料加密保護裝置](transparent-data-encryption-byok-azure-sql-key-rotation.md)。

- 開始使用攜帶您自己的金鑰支援 TDE：[使用 PowerShell 從 Key Vault 開啟使用自己金鑰的 TDE](transparent-data-encryption-byok-azure-sql-configure.md)。

