---
title: 在 Azure Key Vault 中使用客戶受控金鑰進行透明資料加密的常見錯誤 | Microsoft Docs
description: 針對使用 Azure Key Vault 設定的透明資料加密 (TDE) 進行疑難排解。
helpviewer_keywords:
- troublshooting, tde akv
- tde akv configuration, troubleshooting
- tde troubleshooting
author: aliceku
ms.prod: sql
ms.technology: security
ms.reviewer: vanto
ms.topic: conceptual
ms.date: 04/26/2019
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: f67d1ed9bf809baaa4d934947e86d3fd1b7ed0b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111527"
---
# <a name="common-errors-for-transparent-data-encryption-with-customer-managed-keys-in-azure-key-vault"></a>在 Azure Key Vault 中使用客戶受控金鑰進行透明資料加密的常見錯誤

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md.md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]
此文章說明在 Azure Key Vault 中使用透明資料加密 (TDE) 搭配客戶受控金鑰的需求，以及如何識別及解決常見的錯誤。

## <a name="requirements"></a>需求

若要在 Key Vault 中使用客戶受控 TDE 保護裝置對 TDE 進行疑難排解，必須符合這些需求：

- 邏輯 SQL Server 執行個體和金鑰保存庫必須位於相同區域中。
- Azure Active Directory (Azure AD) 所提供之邏輯 SQL Server 執行個體身分識別 (Azure Key Vault 中的 AppId) 必須是原始訂用帳戶中的租用戶。 如果將伺服器移至與其建立位置不同的其他訂用帳戶，則必須重新建立伺服器身分識別 (AppId)。
- 金鑰保存庫必須啟動並執行。 若要了解如何檢查金鑰保存庫狀態，請參閱 [Azure 資源健康狀態](https://docs.microsoft.com/azure/service-health/resource-health-overview) \(部分機器翻譯\)。 若要註冊通知，請參閱[動作群組](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups) \(部分機器翻譯\)。
- 在異地災害復原情節中，這兩個金鑰保存庫必須包含相同的金鑰內容，容錯移轉才能運作。
- 邏輯伺服器必須具有 Azure AD 身分識別 (AppId) 才能對金鑰保存庫進行驗證。
- AppId 必須能夠存取金鑰保存庫，且它必須具備選取為 TDE 保護裝置之金鑰的 Get、Wrap 和 Unwrap 權限。

如需詳細資訊，請參閱[使用 Azure Key Vault 設定 TDE 的指導方針](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault) \(部分機器翻譯\)。

## <a name="common-misconfigurations"></a>常見錯誤設定

搭配金鑰保存庫使用 TDE 時，出現的大多數問題都是由下列其中一個錯誤設定所造成：

### <a name="the-key-vault-is-unavailable-or-doesnt-exist"></a>金鑰保存庫無法使用或不存在

- 意外刪除金鑰保存庫。
- 已針對 Azure Key Vault 設定防火牆，但它不允許存取 Microsoft 服務。

### <a name="no-permissions-to-access-the-key-vault-or-the-key-doesnt-exist"></a>沒有存取金鑰保存庫的權限或金鑰不存在

- 意外刪除金鑰。
- 意外刪除邏輯 SQL Server 執行個體 AppId。
- 邏輯 SQL Server 執行個體已移至不同的訂用帳戶。 如果將邏輯伺服器移至不同的訂用帳戶，則必須建立新的 AppId。
- 針對金鑰授與 AppId 的權限不足 (它們不包括 Get、Wrap 和 Unwrap)。
- 已撤銷邏輯 SQL Server 執行個體 AppId 的權限。

## <a name="identify-and-resolve-common-errors"></a>識別及解決常見的錯誤

在此節中，我們列出了最常見錯誤的疑難排解步驟。

### <a name="missing-server-identity"></a>遺漏伺服器身分識別

**錯誤訊息**

「401 AzureKeyVaultNoServerIdentity - 伺服器上的伺服器識別設定不正確。  請連絡支援人員。」

**偵測**

使用下列 Cmdlet 或命令，以確保身分識別已指派給邏輯 SQL Server 執行個體：

- Azure PowerShell：[Get-AzureRMSqlServer](https://docs.microsoft.com/powershell/module/AzureRM.Sql/Get-AzureRmSqlServer?view=azurermps-6.13.0) \(英文\) 

- Azure CLI：[az-sql-server-show](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-show) \(英文\)

**風險降低**

使用下列 Cmdlet 或命令，為邏輯 SQL Server 執行個體設定 Azure AD 身分識別 (AppId)：

- Azure PowerShell：具有 `-AssignIdentity` 選項的 [Set-AzureRmSqlServer](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqlserver?view=azurermps-6.13.0) \(英文\)。

- Azure CLI：具有 `--assign_identity` 選項的 [az sql server update](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-update) \(英文\)。

在 Azure 入口網站中，移至金鑰保存庫，然後移至 [存取原則]  。 完成下列步驟： 

 1. 使用 [新增]  按鈕，為上一個步驟中建立的伺服器新增 AppId。 
 1. 指派下列金鑰權限：取得、包裝及解除包裝 

若要深入了解，請參閱[將 Azure AD 身分識別指派給您的伺服器](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server) \(部分機器翻譯\)。

> [!IMPORTANT]
> 如果在初始設定搭配 Key Vault 的 TDE 之後，邏輯 SQL Server 執行個體已移至新的訂用帳戶，就必須重複設定 Azure AD 身分識別的步驟以建立新的 AppId。 然後，將 AppId 新增至金鑰保存庫，並為金鑰指派正確的權限。 
>

### <a name="missing-key-vault"></a>遺漏索金鑰保存庫

**錯誤訊息**

「503 AzureKeyVaultConnectionFailed - 因為嘗試連線至 Azure Key Vault 失敗，所以無法完成伺服器上的作業。」 

**偵測**

識別金鑰 URI 和金鑰保存庫：

1. 使用下列 Cmdlet 或命令來取得特定邏輯 SQL Server 執行個體的金鑰 URI：

    - Azure PowerShell：[Get-AzureRmSqlServerKeyVaultKey](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey?view=azurermps-6.13.0)

    - Azure CLI：[az-sql-server-tde-key-show](https://docs.microsoft.com/cli/azure/sql/server/tde-key?view=azure-cli-latest#az-sql-server-tde-key-show) \(英文\) 

1. 使用金鑰 URI 來識別金鑰保存庫：

    - Azure PowerShell：您可以檢查 $MyServerKeyVaultKey 變數的屬性來取得金鑰保存庫的詳細資料。

    - Azure CLI：如需金鑰保存庫的詳細資料，請檢查傳回的伺服器加密保護裝置。

**風險降低**

確認金鑰保存庫可供使用：

- 確定金鑰保存庫可供使用且邏輯 SQL Server 執行個體可存取。
- 如果金鑰保存庫位於防火牆後方，請確定已核取要允許 Microsoft 服務存取金鑰保存庫的方塊。
- 如果意外刪除金鑰保存庫，您必須從頭完成該設定。


### <a name="missing-key"></a>遺漏金鑰

**錯誤訊息**

「404 ServerKeyNotFound - 目前訂用帳戶上找不到要求的伺服器金鑰。」  

「409 ServerKeyDoesNotExists - 伺服器金鑰不存在。」 

**偵測**

識別金鑰 URI 和金鑰保存庫：

- 使用[遺漏金鑰保存庫](#missing-key-vault)中的 Cmdlet 或命令來識別新增至邏輯 SQL Server 執行個體的金鑰 URI。 執行命令將傳回金鑰的清單。

**風險降低**

確認 Key Vault 中有 TDE 保護裝置：

1. 識別金鑰保存庫，並在 Azure 入口網站中移至該金鑰保存庫。
1. 確認有金鑰 URI 所識別的金鑰。

### <a name="missing-permissions"></a>遺漏權限

**錯誤訊息**

「401 AzureKeyVaultMissingPermissions - 伺服器缺少 Azure Key Vault 的必要權限。」 

**偵測**

識別金鑰 URI 和金鑰保存庫： 

- 使用[遺漏金鑰保存庫](#missing-key-vault)中的 Cmdlet 或命令來識別邏輯 SQL Server 執行個體所使用的金鑰保存庫。

**風險降低**

確認邏輯 SQL Server 執行個體具有金鑰保存庫的權限，以及存取金鑰的正確權限：

- 在 Azure 入口網站中，移至金鑰保存庫 > [存取原則]  。 尋找邏輯 SQL Server 執行個體的 AppId。  
- 如果 AppId 已存在，請確定 AppID 擁有下列金鑰權限：取得、包裝及解除包裝。
- 如果 AppId 不存在，請使用 [新增]  按鈕加以新增。 

## <a name="next-steps"></a>後續步驟

- 請檢閱[使用 Azure Key Vault 設定 TDE 的指導方針](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault) \(部分機器翻譯\)。
- 深入了解[Azure 資源健康狀態](https://docs.microsoft.com/azure/service-health/resource-health-overview) \(部分機器翻譯\)。
- 重新了解如何[將 Azure AD 身分識別指派給您的伺服器](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server) \(部分機器翻譯\)。
