---
title: 使用 Azure Key Vault (AKV) 客戶受控金鑰進行透明資料加密 (TDE) 的常見錯誤和解決方案 | Microsoft Docs
description: 針對具有 Azure Key Vault 設定的透明資料加密 (TDE) 進行疑難排解。
helpviewer_keywords:
- troublshooting, tde akv
- tde akv configuration, troubleshooting
- tde troubleshooting
author: aliceku
manager: craigg
ms.prod: sql
ms.technology: security
ms.reviewer: vanto
ms.topic: conceptual
ms.date: 04/26/2019
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: e6d23fb19b756bbf303a06512fecc3a6d29b8090
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65097451"
---
# <a name="transparent-data-encryption-tde-with-customer-managed-keys-in-azure-key-vault-akv-troubleshooting"></a>使用 Azure Key Vault (AKV) 的客戶受控金鑰進行透明資料加密 (TDE) 的疑難排解

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md.md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]
本主題提供下列問題的相關資訊：  
  
- 需求  
- 如何找出並解決最常見的錯誤

## <a name="requirements"></a>需求
若要對[使用 AKV 設定中客戶受控 TDE 保護裝置的 TDE](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql#guidelines-for-configuring-tde-with-azure-key-vault)進行疑難排解，請讓我們開始確認下列需求：
- 邏輯 SQL 伺服器和金鑰保存庫必須位於相同區域中。
- Azure Active Directory 所提供邏輯 SQL 伺服器身分識別(Azure Key Vault 中的 APPID) 僅限於原始訂用帳戶中的租用戶。  如果伺服器已移至另一個訂用帳戶，就必須重新建立伺服器身分識別 (APPID)。
- 金鑰保存庫必須啟動並執行、了解 [Azure 資源健康狀態](https://docs.microsoft.com/azure/service-health/resource-health-overview)來檢查金鑰保存庫狀態，以及了解[動作群組](https://docs.microsoft.com/azure/azure-monitor/platform/action-groups)來註冊通知。
- 在異地災害復原案例中，這兩個金鑰保存庫必須包含相同的金鑰內容，才能讓容錯移轉運作。
- 邏輯伺服器必須具備 Azure Active Directory (AAD) 身分識別 (APPID)，才能向金鑰保存庫進行驗證。
- APPID 必須能夠存取金鑰保存庫，以及包裝、解除包裝選取為 TDE 保護裝置的金鑰，並取得其權限。

搭配使用 TDE 與 AKV 時遇到的大部分問題，都是由於下列其中一個錯誤設定所致：

### <a name="key-vault-unavailable-or-doesnt-exist"></a>金鑰保存庫無法使用或不存在？
- 意外刪除金鑰保存庫
- 已針對 Azure Key Vault 設定防火牆，但不允許存取 Microsoft 服務

### <a name="no-permissions-to-access-the-key-vault-or-key-doesnt-exist"></a>沒有存取金鑰保存庫的權限或金鑰不存在？
- 意外刪除金鑰
- 意外刪除 SQL APPID
- SQL 已移至不同的訂用帳戶，這需要新的 APPID
- 針對金鑰授與給 APPID 的權限不足 (包裝、解除包裝、取得)
- 撤銷 SQL APPID 的權限


在下一個區段中，我們將列出最常見錯誤的疑難排解步驟。


## <a name="how-to-identify-and-resolve-the-most-common-errors"></a>如何找出並解決最常見的錯誤

## <a name="missing-server-identity"></a>遺漏伺服器身分識別
錯誤訊息：「401 AzureKeyVaultNoServerIdentity - 伺服器上的伺服器識別設定不正確。 請連絡支援人員。」

偵測：使用下列命令，以確保身分識別已指派給邏輯 SQL 伺服器：

- [Azure PowerShell Get-AzureRMSqlServer](https://docs.microsoft.com/powershell/module/AzureRM.Sql/Get-AzureRmSqlServer?view=azurermps-6.13.0) 
- [Azure CLI az-sql-server-show](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-show)

風險降低：為邏輯 SQL 伺服器設定 Azure Active Directory (Azure AD) 身分識別 (APPID)

如果是 PowerShell：使用 Set-AzureRmSqlServer 命令搭配 [-AssignIdentity](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqlserver?view=azurermps-6.13.0) 選項 

如果是 CLI：使用 az sql server update 命令搭配 [--assign_identity](https://docs.microsoft.com/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-update) 選項 

在 Azure 入口網站中，瀏覽至金鑰保存庫，並移至 [存取原則]：  
 - 使用 [新增] 按鈕，為上一個步驟中建立的伺服器新增 APPID。 
 - 指派下列金鑰權限：取得、包裝及解除包裝 

[深入了解](https://docs.microsoft.com/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure?view=sql-server-2017&viewFallbackFrom=azuresqldb-current#step-1-assign-an-azure-ad-identity-to-your-server)

> [!IMPORTANT]
> 如果在初始設定搭配 AKV 的 TDE 之後，邏輯 SQL 伺服器已移至新的訂用帳戶，就必須重複設定 AAD 身分識別的步驟以建立新 APPID。  接著，必須將新 APPID 新增至金鑰保存庫，且需要指派正確的權限。 
>

## <a name="missing-key-vault"></a>遺漏索金鑰保存庫
錯誤訊息:「503 AzureKeyVaultConnectionFailed - 因為嘗試連線至 Azure Key Vault 失敗，所以無法完成伺服器上的作業」

偵測：如何識別金鑰 URI 和金鑰保存庫 

步驟 1:使用下列命令來取得指定邏輯 SQL 伺服器的金鑰 URI：

-[Azure PowerShell get-azurermsqlserverkeyvaultkey](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey?view=azurermps-6.13.0)

-[Azure CLI az-sql-server-tde-key-show](https://docs.microsoft.com/cli/azure/sql/server/tde-key?view=azure-cli-latest#az-sql-server-tde-key-show) 

步驟 2:使用金鑰 URI 來識別金鑰保存庫

PowerShell：您可以檢查 $MyServerKeyVaultKey 的屬性來取得金鑰保存庫的詳細資料

CLI：如需金鑰保存庫的詳細資料，請檢查傳回的伺服器加密保護裝置

風險降低：確認金鑰保存庫可供使用
- 確定金鑰保存庫可供使用且邏輯 SQL Server 可存取
- 如果金鑰保存庫位於防火牆後方，請確定已核取要允許 Microsoft 服務存取金鑰保存庫的方塊
- 如果意外刪除金鑰保存庫，設定必須從一開始就完整


## <a name="missing-key"></a>遺漏金鑰 
錯誤訊息:「404 ServerKeyNotFound - 目前訂用帳戶上找不到要求的伺服器金鑰。」
「409 ServerKeyDoesNotExists - 伺服器金鑰不存在。」

偵測：如何識別金鑰 URI 和金鑰保存庫
- 使用上述 [遺漏金鑰保存庫] 區段中 Cmdlet 識別新增至邏輯 SQL 伺服器的金鑰 URI，來傳回金鑰清單。

風險降低：確認 AKV 中有 TDE 保護裝置
- 識別金鑰保存庫，並在 Azure 入口網站中瀏覽至該保存庫
- 確認有金鑰 URI 所識別的金鑰

## <a name="missing-permissions"></a>遺漏權限 
錯誤訊息:「401 AzureKeyVaultMissingPermissions - 伺服器缺少 Azure Key Vault 的必要權限。」

偵測：如何識別金鑰 URI 和金鑰保存庫
- 使用上述 [遺漏金鑰保存庫] 區段中的 Cmdlet，識別邏輯 SQL 伺服器所使用的金鑰保存庫。

風險降低：確認邏輯 SQL 伺服器具有金鑰保存庫的權限，以及存取金鑰的正確權限
- 在 Azure 入口網站中，瀏覽至金鑰保存庫，移至 [存取原則]，並找出 SQL Server APPID：  
  - 如果 APPID 不存在，請使用 [新增] 按鈕加以新增。 
  - 如果 APPID 已存在，請確定它擁有下列金鑰權限：取得、包裝及解除包裝。
