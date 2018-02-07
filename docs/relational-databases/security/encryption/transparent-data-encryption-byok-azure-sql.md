---
title: "TDE - 自行管理金鑰 (BYOK) - Azure SQL | Microsoft Docs"
description: "自行管理金鑰 (BYOK) 支援適用於 SQL Database 和資料倉儲的 Azure Key Vault 透明資料加密 (TDE)。 TDE 與 BYOK 的概觀、優點、運作方式、考量和建議。"
keywords: 
services: sql-database
documentationcenter: 
author: aliceku
manager: craigg
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.custom: 
ms.component: security
ms.workload: On Demand
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 01/31/2018
ms.author: aliceku
ms.openlocfilehash: 8c192f5d1114ddab7d75761b385e91c0f22e481b
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2018
---
# <a name="transparent-data-encryption-with-bring-your-own-key-preview-support-for-azure-sql-database-and-data-warehouse"></a>Azure SQL Database 和資料倉儲的透明資料加密與攜帶您自己的金鑰 (PREVIEW) 支援
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

攜帶您自己的金鑰 (BYOK) 支援[透明資料加密 (TDE)](transparent-data-encryption.md)，可讓您使用名為 TED 保護裝置的非對稱金鑰來加密資料庫加密金鑰 (DEK)。  TDE 保護裝置儲存於 Azure 的雲端式外部金鑰管理系統 [Azure Key Valut](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault) 之中，可供您自行控制。 Azure Key Vault 是首款整合 TDE 與 BYOK 支援的金鑰管理服務。 TDE DEK 會儲存於資料庫的啟動頁面，由 TDE 保護裝置予以加密及解密。 TDE 保護裝置會儲存於 Azure Key Valut 並永遠留在此金鑰保存庫。 如果撤銷了伺服器對金鑰保存庫的存取權，資料庫即無法解密或讀入記憶體中。  TDE 保護裝置設置於邏輯伺服器層級，已與該伺服器建立關聯的所有資料庫均會加以繼承。 

現在，BYOK 支援可讓使用者控制金鑰管理工作，包括金鑰輪替、金鑰保存庫權限、刪除金鑰，以及允許所有使用 Azure Key Valut 功能的 TDE 保護裝置進行稽核、報告。 Key Vault 提供集中式的金鑰管理、利用嚴密監控的硬體安全性模組 (HSM)，並保障金鑰和資料的管理分責，以協助滿足法規的合規要求。  


有 BYOK 的 TDE 具有下列優點：
- 增加自我管理 TDE 保護裝置的透明度和細微控制力   
- 將 TDE 保護裝置 (及其他 Azure 服務中使用的其他金鑰和祕密) 裝載在 Key Vault 中集中管理
- 分隔組織內的金鑰和資料管理責任，以支援分責
- 因為 Key Vault 的設計是讓 Microsoft 看不到或擷取不到任何加密金鑰，所以對您自己的用戶端會有更高的信任。 
- 支援金鑰輪替

> [!IMPORTANT]
> 對於目前使用受服務管理的 TDE 但想要開始使用 Key Vault 的使用者，在切換為 Key Vault 中 TDE 保護裝置的程序期間，TDE 都會保持啟用。 資料庫檔案本身不會有任何停機時間或重新加密。 從受服務管理的金鑰切換至 Key Vault 金鑰，僅需重新加密資料庫加密金鑰 (DEK)，而這是一項快速的線上作業。 
>

## <a name="how-does-tde-with-byok-support-work"></a>有 BYOK 的 TDE 如何支援工作？
 
![伺服器至 Key Vault 的驗證](./media/transparent-data-encryption-byok-azure-sql/tde-byok-server-authentication-flow.PNG)

當 TDE 首次設定為使用 Key Vault 中的 TED 保護裝置時，伺服器就會將每個已啟用 TDE 之資料庫的 DEK 傳送至 Key Vault，以提出包裝金鑰要求。 Key Vault 會傳回儲存在使用者資料庫中加密的資料庫加密金鑰。  

>[!IMPORTANT]
>請務必注意，**TDE 保護裝置一旦儲存在 Azure Key Vault，就會永遠留在 Azure Key Vault**。 邏輯伺服器只能將金鑰作業要求傳送給 Key Vault 內的 TDE 保護裝置金鑰產製原料，**不會存取或快取 TDE 保護裝置**。 Key Vault 系統管理員有權隨時撤銷伺服器的 Key Vault 權限，發生此情況時，該伺服器的所有連線都會截斷。 
>


## <a name="guidelines-for-configuring-tde-with-byok"></a>透過 BYOK 設定 TDE 的指導方針

### <a name="general-guidelines"></a>一般指導方針
- 請確定 Azure Key Valut 和 Azure SQL Database 會在同一個租用戶之中。  **不支援**跨租用戶金鑰保存庫與伺服器的互動。

- 為需要的資源決定使用哪一個訂用帳戶。若稍後要在訂用帳戶之間移動伺服器，必須重新設定使用 BYOK 的 TDE。
- 為 SQL Database TDE 保護裝置專門設定單一訂用帳戶的 Azure Key Valut。  與邏輯伺服器建立關聯的所有資料庫都會使用相同的 TDE 保護裝置，因此必須考量連至邏輯伺服器的資料庫群組。 
- 建議：在內部部署保留一份 TDE 保護裝置複本。  這需要使用硬體安全模組 (HSM) 裝置在本機建立 TDE 保護裝置，以及使用金鑰委付系統儲存 TDE 保護裝置的本機複本。


### <a name="guidelines-for-configuring-azure-key-vault"></a>設定 Azure Key Vault 的指導方針

- 使用已啟用[虛刪除](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete)的金鑰保存庫，萬一意外刪除金鑰或是金鑰保存庫時可防止資料遺失：  
  - 虛刪除的資源會保留一段時間，除非復原或清除，否則保留 90 天。
  - **復原**和**清除**動作本身的權限已在金鑰保存庫的存取原則中建立關聯。 
- 使用邏輯伺服器的 Azure Active Directory (AAD) 身分識別，對其授與金鑰保存庫的存取。  使用入口網站 UI 時，AAD 身分識別會自動建立，而金鑰保存庫的存取權限會授與伺服器。  使用 PowerShell 設定有 BYOK 的 TDE，必須建立 AAD 身分識別，且應驗證完成。 如需使用 PowerShell 時的詳細逐步指示，請參閱[使用 BYOK 設定 TDE](transparent-data-encryption-byok-azure-sql-configure.md)。

  >[!NOTE]
  >如果 AAD 身分識別**意外刪除，或使用了金鑰保存庫的存取原則撤銷伺服器的權限**，伺服器即失去對金鑰保存庫的存取權。
  >
  
- 啟用所有加密金鑰的稽核和報告：Key Vault 提供的記錄檔很容易插入其他安全性資訊和事件管理 (SIEM) 工具中。 Operations Management Suite (OMS) [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-key-vault) 即為整合服務的一個範例。
- 若要確保加密資料庫的高可用性，請使用兩個位於不同的區域的 Azure Key Vault 來設定每一部邏輯伺服器。


### <a name="guidelines-for-configuring-the-tde-protector-asymmetric-key-stored-in-azure-key-vault"></a>設定儲存在 Azure Key Vault 的 TDE 保護裝置 (非對稱金鑰) 指導方針

- 在本機 HSM 裝置上，本機建立加密金鑰。 請確定這是非對稱的 RSA 2048 金鑰，如此才能儲存在 Azure Key Vault。
- 於金鑰委付系統中委付金鑰。  
- 將加密金鑰檔案 (.pfx、.byok 或 .backup) 匯入 Azure Key Vault。 
    
    >[!NOTE] 
    >為了測試之用，可以使用 Azure Key Vault 建立金鑰，但這組金鑰無法委付，因為私密金鑰必須一律留在金鑰保存庫。  請一律備份並委付用來加密產品資料的金鑰，因為金鑰的遺失 (在金鑰保存庫中意外刪除、到期等等) 會導致資料永久遺失。
    >
    
- 請使用沒有到期日的金鑰，且永遠不要為使用中的金鑰設定到期日：**一旦金鑰到期，加密資料庫即失去其 TDE 保護裝置的存取權，並會在 24 小時內卸除**。
- 確認金鑰已啟用，而且有權執行「取得」、「包裝金鑰」、「解除金鑰包裝」作業。
- 在第一次使用 Azure Key Vault 中的金鑰之前，請先建立 Azure Key Vault 金鑰備份。 深入了解 [Backup-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1) 命令。
- 每當對金鑰進行任何變更時 (例如新增 ACL、新增標籤、新增金鑰屬性)，都請建立新備份。
- 輪替金鑰時，請在金鑰保存庫中**保留舊版金鑰**，以便還原較舊的資料庫備份。 當資料庫的 TDE 保護裝置變更時，資料庫的舊備份**不會更新**為使用最新的 TDE 保護裝置。  每個備份在還原時，都會需要用以建立的 TDE 保護裝置。 請遵循[使用 PowerShell 輪替透明資料加密保護裝置](transparent-data-encryption-byok-azure-sql-key-rotation.md)中的指示，執行金鑰輪替。
- 換回受服務管理的金鑰後，請保留所有先前在 Azure Key Vault 使用過的金鑰。  這樣可以確保資料庫備份會隨著儲存在 Azure Key Vault 的 TDE 保護裝置還原。  透過 Azure Key Vault 所建立的 TDE 保護裝置必須善加維護，直到儲存的所有備份都已透過受服務管理的金鑰建立為止。  
- 請使用 [Backup-AzureKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-5.1.1) 建立這些金鑰的可復原備份複本。
- 在沒有資料遺失風險的情況下，若要移除可能在安全性事件中洩露的金鑰，請遵循[移除可能洩露的金鑰](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md)中的步驟。


## <a name="high-availability-geo-replication-and-backup--restore"></a>高可用性、異地複寫及備份與還原

### <a name="high-availability-and-disaster-recovery"></a>高可用性和災害復原

使用 Azure Key Vault 來設定高可用性的方式，取決於您的資料庫和邏輯伺服器設定，以下是兩個不同案例的建議設定。  第一個案例是未設定異地備援的獨立資料庫或邏輯伺服器。  第二個案例是已設定容錯移轉群組或異地備援的資料庫或邏輯伺服器，在這個案例中必須確保每個異地備援複本都有一個在容錯移轉群組中的本機 Azure Key Vault，使異地容錯移轉能順利進行。 在第一個案例中，如果您要求未設定異地備援的資料庫和邏輯伺服器具備高可用性，強烈建議您將伺服器設定為使用兩個不同區域中具有相同金鑰產製原料的兩個不同金鑰保存庫。  方式為使用與邏輯伺服器共置於相同區域中的主要 Key Vault，將金鑰複製到不同 Azure 區域中的金鑰保存庫，來建立 TDE 保護裝置；如此一來，若主要金鑰保存庫在資料庫啟動並執行時發生中斷情形，伺服器即可存取次要金鑰保存庫。 您可以使用 Backup-AzureKeyVaultKey cmdlet 以加密格式來擷取主要金鑰保存庫中的金鑰，然後使用 Restore-AzureKeyVaultKey cmdlet 並在次要區域中指定金鑰保存庫。


![單一伺服器 HA，無異地災害復原](./media/transparent-data-encryption-byok-azure-sql/SingleServer_HA_Config.PNG)

在第二個案例中，必須根據現有的 SQL Database 容錯移轉群組或使用中的資料庫異地複寫複本來設定備援的 Azure Key Vault，以維持 Azure Key Vault 中 TDE 保護裝置的高可用性。  每個異地複寫的伺服器都需要個別的金鑰保存庫，理想情況是與其伺服器共置於相同的 Azure 區域中。 當主要資料庫因為某個區域發生中斷而無法存取，並觸發容錯移轉時，次要資料庫即可以使用次要金鑰保存庫來接管。  

![容錯移轉群組和異地災害復原](./media/transparent-data-encryption-byok-azure-sql/Geo_DR_Config.PNG)

為了確保在容錯移轉期間能持續存取 Azure Key Vault 中的 TDE 保護裝置，必須在資料庫複寫或容錯移轉至次要伺服器之前完成這項設定。 主要和次要伺服器兩者皆必須將 TDE 保護裝置的複本儲存於所有其他 Azure Key Vault 之中，在此範例中即表示相同的金鑰會儲存在這兩個金鑰保存庫中。

若要從某個金鑰保存庫將現有的金鑰新增至另一個金鑰保存庫，請使用 [Add-AzureRmSqlServerKeyVaultKey](https://docs.microsoft.com/en-us/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) cmdlet。

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

若要降低此風險，請執行 [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) Cmdlet 傳回已新增至伺服器的 Key Vault 金鑰清單 (除非已由使用者刪除)。 為確保所有備份都能還原，請確定備份所用的目標伺服器可以存取所有這些金鑰。

   ```powershell
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
若要深入了解 SQL 資料庫的備份復原，請參閱[復原 Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-recovery-using-backups)。 若要深入了解 SQL 資料倉儲的備份復原，請參閱[復原 Azure SQL 資料倉儲](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-restore-database-overview)。
