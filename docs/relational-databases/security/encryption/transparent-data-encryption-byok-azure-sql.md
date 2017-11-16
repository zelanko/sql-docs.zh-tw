---
title: "TDE - 攜帶您自己的金鑰 - Azure SQL | Microsoft Docs"
description: "使用 Azure Key Vault for SQL Database 和資料倉儲攜帶您自己的金鑰支援透明資料加密的概觀。 本文涵蓋功能、運作方式、考量和建議等各方優點。"
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
ms.openlocfilehash: 35e51899bda60ccb5b176de0a3d7fabcc86faad7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="transparent-data-encryption-with-bring-your-own-key-support-for-azure-sql-database-and-data-warehouse"></a>Azure SQL Database 和資料倉儲的透明資料加密與攜帶您自己的金鑰支援

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

攜帶您自己的金鑰 (BYOK) 支援[透明資料加密 (TDE)](transparent-data-encryption.md)，可讓您充分掌控 TDE 加密金鑰，並控制存取的人員與時間。 [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)，Azure 的雲端式外部金鑰管理系統，是 TDE 用以整合 BYOK 支援的第一項金鑰管理服務。 使用 BYOK，資料庫加密金鑰即受到儲存在 Key Vault 的非對稱金鑰保護。 非對稱金鑰是在伺服器層級設定，該伺服器底的所有資料庫都繼承它。 

使用 BYOK 支援，使用者現在可以控制金鑰管理工作，包括金鑰輪替、金鑰保存庫權限、刪除金鑰，以及啟用所有加密金鑰的稽核/報告。 Key Vault 提供集中式的金鑰管理、利用嚴密監控的硬體安全性模組 (HSM)，並促進金鑰和資料的分開管理作業，以協助符合法規合規性。 

有 BYOK 的 TDE 具有下列優點：
- 增加自我管理 TDE 保護裝置的透明度和細微控制力   
- 將 TDE 加密金鑰 (及其他 Azure 服務中使用的其他金鑰和密碼) 裝載在 Key Vault 中集中管理
- 組織內分開管理金鑰和資料以支援分隔角色
- 因為 Key Vault 的設計是讓 Microsoft 看不到或擷取不到任何加密金鑰，所以對您自己的用戶端會有更高的信任。 
- 支援金鑰輪替

> [!IMPORTANT]
> 對於使用服務管理的 TDE 但想要開始使用 Key Vault 的人，從切換程序開始到金鑰進入 Key Vault，都會一直保持 TDE。 資料庫檔案本身不會有任何停機時間或重新加密。 從服務管理的金鑰切換至 Key Vault 金鑰，需要重新加密資料庫加密金鑰，這是一項快速的線上作業。
>

## <a name="how-does-tde-with-byok-support-work"></a>有 BYOK 的 TDE 如何支援工作？
 
![伺服器至 Key Vault 的驗證](./media/transparent-data-encryption-byok-azure-sql/tde-byok-server-authentication-flow.PNG)

當 TDE 設定為使用 Key Vault 金鑰時，伺服器就會將每個已啟用 TDE 之資料庫的資料庫加密金鑰傳送至 Key Vault，以提出「包裝金鑰」要求。 Key Vault 會傳回儲存在使用者資料庫中加密的資料庫加密金鑰。 

請務必注意，**金鑰一旦儲存在 Key Vault，就永遠留在 Key Vault**。 Key Vault 中以硬體安全性模組 (HSM) 備份的金鑰，永遠不會離開 HSM 安全性界限。 伺服器只能將金鑰作業要求傳送給 Key Vault 內的 TDE 保護裝置金鑰內容。 Key Vault 系統管理員有權隨時撤銷伺服器的 Key Vault 權限，發生此情況時，會截斷該伺服器的所有連線。 

## <a name="considerations"></a>考量

使用有 BYOK 的 TDE 會給您帶來兩項額外的金鑰管理工作，以及金鑰保存庫本身的使用相關成本。 這些考量會在下兩節中討論。

### <a name="key-management-responsibilities"></a>金鑰管理責任

照料應用程式資源的加密金鑰管理是很重要的責任。 透過 Key Vault 使用有 BYOK 的 TDE，以下是可預見的金鑰管理工作：
- **金鑰輪替：** TDE 保護裝置應根據內部法規或規範需求輪替。 金鑰輪替可以透過 TDE 保護裝置的金鑰保存庫完成。  
- **金鑰保存庫權限**：Key Vault 內的權限會跨金鑰保存庫和伺服器層級佈建。 使用金鑰保存庫的存取原則可以隨時撤銷伺服器的金鑰保存庫權限。
- **刪除金鑰**：為額外安全或符合合規性，可從 Key Vault 及 SQL 伺服器卸除金鑰。
- **所有加密金鑰的稽核/報告**：Key Vault 提供的記錄檔很容易插入到其他安全性資訊和事件管理 (SIEM) 工具中。 Operations Management Suite (OMS) [記錄分析](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-key-vault)是已整合的一個範例服務。

### <a name="pricing-considerations"></a>定價考量 

有 BYOK 支援的 TDE 是 Azure SQL Database 和資料倉儲的內建安全性功能，無任何額外費用。 不過，使用 Key Vault 本身會有相關成本。 伺服器執行的 Key Vault 作業會依 Key Vault [定價](https://azure.microsoft.com/pricing/details/key-vault/)，像一般保存庫作業一樣收費。 伺服器會針對下列事件向 Key Vault 傳送要求：
- SQL 執行個體重新啟動
- 金鑰變換
- 每 6 小時檢查伺服器的金鑰保存庫權限是否有任何變更

## <a name="important-warnings"></a>重要的警告

### <a name="loss-of-access-to-keys"></a>遺失金鑰存取權

一旦伺服器不再能存取 TDE 保護裝置 (無論是因為移除了 Key Vault 權限或刪除了金鑰)，**封鎖伺服器下加密資料庫的所有連線，且將這些資料庫離線，於 24 小時內卸除**。 無法再存取使用不能取用之金鑰加密的舊備份。 如發生懷疑金鑰遭盜用的極端情況 (例如，服務或使用者有未經授權的金鑰存取權)，最好遵循[移除可能遭盜用的金鑰](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md)的指導方針刪除金鑰。 必須先卸除資料庫，再刪除作用中的 TDE 保護裝置，以免可能遺失最多 10 分鐘的資料。  

### <a name="expired-keys"></a>過期的金鑰

因為 TDE 保護裝置的可用性會直接影響資料庫可用性，所以過期的金鑰不能新增至 SQL server。 如果金鑰已當成 TDE 保護裝置用於伺服器，稍後並在 Azure Key Vault 中新增到期日，則**金鑰一旦過期，加密的資料庫就無法再存取其 TDE 保護裝置，並於 24 小時內卸除。**

### <a name="deleted-server-identities"></a>刪除的伺服器識別 

伺服器的 Key Vault 存取權是透過伺服器的唯一 Azure Active Directory (AAD) 識別管理。 因此，如果從 AAD 中刪除伺服器的識別，伺服器就會失去其金鑰保存庫的存取權。 因此，會**封鎖伺服器下加密資料庫的所有連線，且將這些資料庫離線，於 24 小時內卸除**。

## <a name="limitations"></a>限制

用於 TDE 的金鑰保存庫必須和 SQL Database 或資料倉儲伺服器在相同的 AAD 租用戶中。 不支援跨租用戶金鑰保存庫與伺服器的互動。 正在使用 Key Vault 金鑰加密的資源，無法在 Azure 訂閱間移動。 在訂閱間移動資源會中斷能讓 TDE 使用 BYOK 的必要 Key Vault 存取控制項。 如有任何資源必須移至另一個訂閱，請將 TDE 模式從 BYOK 變更為[服務管理 TDE](transparent-data-encryption-azure-sql.md)。 

不支援資料庫或資料倉儲的唯一 TDE 保護裝置。 TDE 保護裝置是在伺服器層級設定，伺服器下所有資源都繼承它。 

## <a name="guidelines-for-managing-encrypted-databases"></a>管理加密資料庫的指導方針

### <a name="high-availability-and-disaster-recovery"></a>高可用性和災害復原
  
有兩種方式可以設定使用 Key Vault 之伺服器的異地複寫： 

- **不同的金鑰保存庫**：每部伺服器都可以存取不同的金鑰保存庫 (最好每個都在自己的 Azure 區域內)。 這是建議的組態，因為每部伺服器都有自己的一份 TDE 保護裝置供加密的異地複寫資料庫使用。 如果其中一部伺服器的 Azure 區域離線，其他伺服器可以繼續存取異地複寫資料庫。   

- **共用的金鑰保存庫**：所有伺服器共用相同的金鑰保存庫。 此組態很容易設定，但如果金鑰保存庫所在地的 Azure 區域離線，則所有伺服器都無法讀取加密的異地複寫資料庫或自己的加密資料庫。 
 
若要開始，請使用 [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) Cmdlet 將每部伺服器的 Key Vault 金鑰新增至異地複寫連結中的其他伺服器。  
(Key Vault 的 KeyId 範例：*https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h*)

   ```powershell
   <# Include the version guid in the KeyId #>
   Add-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```

>[!NOTE]
>金鑰保存庫名稱和金鑰名稱的組合字元長度不能超過 94 個字元。
>

請遵循[作用中異地複寫概觀](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)的步驟，設定這些伺服器的作用中異地複寫，並觸發容錯移轉。  

### <a name="backup-and-restore"></a>備份與還原

一旦以使用 Key Vault 金鑰的 TDE 加密資料庫，則產生的任何備份也會以相同的 TDE 保護裝置加密。

若要還原以 Key Vault 的 TDE 保護裝置加密的備份，請確定金鑰內容仍在原始的保存庫中，使用原來的金鑰名稱。 當資料庫的 TDE 保護裝置變更時，資料庫的舊備份**不會**更新為使用最新的 TDE 保護裝置。 因此，建議您保留 Key Vault 所有舊版的 TDE 保護裝置，以便還原資料庫備份。 

如果還原備份可能用到的金鑰不再位於原始的金鑰保存庫中，則會傳回下列錯誤訊息：「目標伺服器 <Servername> 無法存取在 <時間戳記 #1> 和 <時間戳記 #2> 之間建立的所有 AKV URI。 請在還原所有 AKV URI 後重新作業。」

為降低此風險，請執行 [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) Cmdlet 傳回已新增至伺服器的 Key Vault 金鑰清單。 為確保還原所有的備份，請確定備份所用的目標伺服器可以存取所有這些金鑰。

   ```powershell
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
若要深入了解 SQL 資料庫的備份復原，請參閱[復原 Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups)。 若要深入了解 SQL 資料倉儲的備份復原，請參閱[復原 Azure SQL 資料倉儲](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-restore-database-overview)。

## <a name="best-practices"></a>最佳做法

### <a name="key-management"></a>金鑰管理 

為確保快速修復金鑰，並且能夠在 Azure 之外存取資料，我們建議︰
- 在本機 HSM 裝置上，本機建立加密金鑰。 (請確定這是非對稱的 RSA 2048 金鑰，以便它可存放在 Azure Key Vault。)
- 將加密金鑰檔案 (.pfx、.byok 或 .backup) 匯入 Azure Key Vault。 請考慮使用已啟用 [soft-delete](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete) 的金鑰保存庫，以確保在意外刪除金鑰時能夠取得復原保護。
- 第一次使用 Azure 金鑰保存庫中的金鑰之前，請先備份 Azure 金鑰保存庫金鑰。 深入了解 [Backup-AzureKeyVaultKey](https://msdn.microsoft.com/library/mt126292.aspx) 命令。
- 每當對金鑰進行任何變更時 (例如新增 ACL、新增標籤、新增金鑰屬性)，請務必先另行備份 Azure Key Vault 金鑰。
- 金鑰變換期間，請在金鑰保存庫中**保留舊版金鑰**，以便可以還原較舊的資料庫備份。 

強烈建議在生產案例中先在本機建立 TDE 加密金鑰，再匯入非對稱金鑰，因為這樣做可讓系統管理員在金鑰委付系統中委付金鑰。 如果非對稱金鑰是在 Azure Key Vault 中建立，由於私密金鑰永遠不會離開保存庫，因此無法委付金鑰。 您應該委付用來保護重要資料的金鑰。 遺失非對稱金鑰會導致資料永久無法復原。

### <a name="pre-configuration-for-replicated-databases"></a>已複寫資料庫的預先組態

如果要將加密的資料庫複寫到另一部伺服器，請**先**確定伺服器可以存取另一部伺服器的 Key Vault 金鑰內容複本，再移動或複製資料庫。  

我們建議每部伺服器都可以存取其他伺服器所用之 Key Vault 金鑰內容的複本，它儲存在不同的金鑰保存庫中 (最好每個都和伺服器位於相同的 Azure 區域)。 使用這項設定，每部伺服器就有自己的一份 TDE 保護裝置供加密的異地複寫資料庫使用。 如果其中一部伺服器的 Azure 區域離線，其他伺服器可以繼續存取複寫的資料庫。

## <a name="next-steps"></a>後續的步驟

- 開始使用攜帶您自己的金鑰支援 TDE：[使用 PowerShell 從 Key Vault 開啟使用自己金鑰的 TDE](transparent-data-encryption-byok-azure-sql-configure.md)。
- 了解如何輪替伺服器的 TDE 保護裝置，以符合安全性需求：[使用 PowerShell 輪替透明資料加密保護裝置](transparent-data-encryption-byok-azure-sql-key-rotation.md)。
- 發生安全性風險時，了解如何移除可能遭盜用的 TDE 保護裝置：[移除可能遭盜用的金鑰](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md)。 
