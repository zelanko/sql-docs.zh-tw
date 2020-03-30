---
title: 備份資料庫 (備份選項頁面) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.backupdatabase.options.f1
- swb.backupdatabase.options.f1
ms.assetid: df0ddcdb-c94e-472b-b786-469ae8117b93
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f461997fbbbbc7e63256b67b8fecf40381aab788
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2020
ms.locfileid: "67940970"
---
# <a name="back-up-database-backup-options-page"></a>備份資料庫 (備份選項頁面)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用 [備份資料庫]  對話方塊的 [備份選項]  頁面，即可檢視或修改資料庫備份選項。  
  
 **若要使用 SQL Server Management Studio 建立備份**  
  
-   [建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [建立差異資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
> [!IMPORTANT]  
>  您可以定義資料庫維護計畫來建立資料庫備份。 如需詳細資訊，請參閱[維護計劃](../../relational-databases/maintenance-plans/maintenance-plans.md)和[使用維護計畫精靈](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)。  
  
> [!NOTE]  
>  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 指定備份工作時，您可以按下 [指令碼][!INCLUDE[tsql](../../includes/tsql-md.md)][ 按鈕，然後選取指令碼的目的地，以產生相對應的 ](../../t-sql/statements/backup-transact-sql.md)**BACKUP** 指令碼。  
  
## <a name="options"></a>選項。  
  
### <a name="backup-set"></a>備份組  
 [備份組]  面板的選項可以讓您指定與備份作業建立之備份組相關的選擇性資訊。  
  
 **名稱**  
 指定備份組名稱。 系統會根據資料庫名稱與備份類型自動建議預設名稱。  
  
 如需備份組的相關資訊，請參閱[媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)。  
  
 **說明**  
 輸入備份組的描述。  
  
 **備份組逾期時間**  
 選擇下列逾期選項其中之一。 如果選擇 [URL]  作為備份目的地，便會停用此選項。  
  
|||  
|-|-|  
|**之後**|指定必須經過多少天之後，這個備份組才會逾期而能夠覆寫。 這個值可以介於 0 到 99999 日之間；值為 0 日意指備份組永遠不會過期。<br /><br /> 備份逾期的預設值是設定在 [預設備份媒體保留期限 (以天為單位)]  選項中的值。 若要存取，請以滑鼠右鍵按一下 [物件總管] 中的伺服器名稱並選取 [屬性]  ；然後按一下 [伺服器屬性]  對話方塊的 [資料庫設定]  頁面。|  
|**開啟**|指定備份組過期而可以被覆寫的特定日期。|  
  
### <a name="compression"></a>壓縮  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (或更新版本) 支援 [備份壓縮](../../relational-databases/backup-restore/backup-compression-sql-server.md)。  
  
 **設定備份壓縮**  
 在 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] (或更新的版本) 中，選取下列其中一個備份壓縮值：  
  
|||  
|-|-|  
|**使用預設伺服器設定**|按一下即可使用伺服器層級的預設值。<br /><br /> 此預設值是由 [備份壓縮預設]  伺服器組態選項所設定。 有關如何檢視這個選項目前之設定的詳細資訊，請參閱 [檢視或設定備份壓縮預設伺服器組態選項](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)。|  
|**壓縮備份**|不論目前的伺服器層級預設值為何，按一下即可壓縮備份。<br /><br /> **\*\* 重要 \*\*** 根據預設，壓縮會大幅增加 CPU 使用量，而且壓縮程序所耗用的額外 CPU 可能會對並行作業造成不良的影響。 因此，您可能會想要在由[資源管理員](../../relational-databases/resource-governor/resource-governor.md)所限制之 CPU 使用量的工作階段中建立低優先權的壓縮備份。 如需詳細資訊，請參閱本主題稍後介紹的＜ [使用資源管理員進行備份壓縮，以限制 CPU 使用率 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)限制的工作階段中，建立低優先權的壓縮備份。|  
|**不要壓縮備份**|不論目前的伺服器層級預設值為何，按一下即可建立未壓縮備份。|  
  
### <a name="encryption"></a>加密  
 若要建立加密的備份，請核取 [加密備份]  核取方塊。 選取要加密步驟所要使用的加密演算法，並提供現有憑證或非對稱金鑰清單中的憑證或非對稱金鑰。 可用於加密的演算法包括：  
  
-   AES 128  
  
-   AES 192  
  
-   AES 256  
  
-   三重 DES  
  
> [!TIP]  
>  如果選擇附加至現有的備份集，則會停用加密選項。  
>   
>  這建議作法是讓您備份憑證或金鑰，並將其儲存在不同位置，而不是加密備份。  
>   
>  僅支援位於可延伸金鑰管理 (EKM) 中的金鑰。  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [備份檔案和檔案群組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [資料庫損毀時備份交易記錄 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
  
