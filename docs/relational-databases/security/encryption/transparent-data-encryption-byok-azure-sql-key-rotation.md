---
title: "PowerShell - 輪替 TDE 保護裝置 - Azure SQL | Microsoft Docs"
description: "了解如何輪替 Azure SQL 伺服器的透明資料加密 (TDE) 保護裝置。"
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: quick start create, mvc
ms.workload: Inactive
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: hero-article
ms.date: 08/07/2017
ms.author: ryzhang26
ms.openlocfilehash: b682c9059d9a6365beebeff549d4c2840c04d477
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2017
---
# <a name="rotate-the-transparent-data-encryption-tde-protector-using-powershell"></a>使用 PowerShell 輪替透明資料加密 (TDE) 保護裝置 
[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

本＜如何＞指南說明使用 Azure Key Vault 之 TDE 保護裝置的 Azure SQL 伺服器金鑰輪替。 輪替 Azure SQL 伺服器的 TDE 保護裝置，表示切換到保護伺服器資料庫的新非對稱金鑰。 金鑰輪替是一項線上作業，應該只需要幾秒鐘即可完成，因為這只是解密和重新加密資料庫的資料加密金鑰，不是整個資料庫。

本指南討論在伺服器上輪替 TDE 保護裝置的兩個選項。

> [!NOTE]
> 輪替金鑰之前，必須先繼續暫停的 SQL 資料倉儲。
>

> [!IMPORTANT]
> 變換之後**請勿刪除**舊版金鑰。  金鑰變換後，有些資料仍使用舊版金鑰加密，例如較舊的資料庫備份。 
>

## <a name="prerequisites"></a>必要條件

- 本＜如何＞指南假設 Azure SQL Database 或資料倉儲的 TDE 保護裝置已經使用 Azure Key Vault 的金鑰。 請參閱[有 BYOK 支援的透明資料加密](transparent-data-encryption-byok-azure-sql.md)。
- 您必須安裝並執行 Azure PowerShell 3.7.0 版或更新的版本。 
- [建議但非必要] 先在硬體安全性模組 (HSM) 或本機金鑰存放區中建立 TDE 保護裝置的金鑰內容，再將金鑰內容匯入 Azure Key Vault。 若要深入了解，請遵循[使用硬體安全性模組 (HSM) 與 Key Vault 的指示](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)。

## <a name="option-1-auto-rotation"></a>選項 1：自動輪替

使用相同的金鑰名稱和金鑰保存庫，產生 Key Vault 中現有 TDE 保護裝置金鑰的新版本。 Azure SQL 服務使用這個新版本在 24 小時內啟動。 

使用 [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) Cmdlet 建立 TDE 保護裝置的新版本：

   ```powershell
   Add-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -Destination <HardwareOrSoftware>
   ```

## <a name="option-2-manual-rotation"></a>選項 2：手動輪替

選項會使用 [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey)、[Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) 和 [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) Cmdlet 新增全新的金鑰，可能使用新的金鑰名稱或甚至是另一個金鑰保存庫。 

>[!NOTE]
>金鑰保存庫名稱和金鑰名稱的組合長度不能超過 94 個字元。
>

   ```powershell
   # Add a new key to Key Vault
   Add-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -Destination <HardwareOrSoftware>

   # Add the new key from Key Vault to the server
   Add-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>   
  
   <# Set the key as the TDE protector for all resources 
   under the server #>
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
  
## <a name="other-useful-powershell-cmdlets"></a>其他有用的 PowerShell Cmdlet

- 若要將 TDE 保護裝置從 Microsoft 管理切換至 BYOK 模式，請使用 [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) Cmdlet。

   ```powershell
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```

- 若要將 TDE 保護裝置從 BYOK 模式切換至 Microsoft 管理，請使用 [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) Cmdlet。

   ```powershell
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type ServiceManaged `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName> 
   ``` 

## <a name="next-steps"></a>後續的步驟

- 發生安全性風險時，了解如何移除可能遭盜用的 TDE 保護裝置：[移除可能遭盜用的金鑰](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md)。 

- 開始使用攜帶您自己的金鑰支援 TDE：[使用 PowerShell 從 Key Vault 開啟使用自己金鑰的 TDE](transparent-data-encryption-byok-azure-sql-configure.md)。
