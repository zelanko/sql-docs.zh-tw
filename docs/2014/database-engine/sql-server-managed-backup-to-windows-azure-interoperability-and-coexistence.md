---
title: SQL Server 受管理的備份至 Azure:互通性與共存 |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 78fb78ed-653f-45fe-a02a-a66519bfee1b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 70d941786fd06e48bf071b8448b84c8f4857f8c8
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176071"
---
# <a name="sql-server-managed-backup-to-azure-interoperability-and-coexistence"></a>SQL Server 受管理的備份至 Azure:互通性與共存性
  本主題說明[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]與 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中之數項功能的互通性與並存性。 這些功能包括：AlwaysOn 可用性群組、資料庫鏡像、備份維護計畫、記錄傳送、臨機操作備份、卸離資料庫, 以及卸載資料庫。  
  
### <a name="alwayson-availability-groups"></a>AlwaysOn Availability Groups  
 設定為僅支援[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]Azure 解決方案的 AlwaysOn 可用性群組。 僅限內部部署或混合式 AlwaysOn 可用性群組組態皆不予支援。 如需詳細資訊和其他考慮, 請參閱[針對可用性群組設定 SQL Server 受管理的備份至 Azure](../../2014/database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)  
  
### <a name="database-mirroring"></a>資料庫鏡像  
 只有主體資料庫才支援[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 若主體與鏡像皆設定成使用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，將會略過鏡像資料庫不予備份。 但在容錯移轉事件時，[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]會在鏡像完成角色切換並上線之後，開始執行備份程序。 在此情況下，備份會儲存在新容器中。 在容錯移轉事件時，若未將鏡像設定成使用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，便不會執行備份。 建議將主體及鏡像均設為使用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，如此一來在容錯移轉事件時，才能執行備份。  
  
> [!TIP]  
>  如果您想要在使用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]預設設定的執行個體上建立鏡像資料庫，建議停用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]執行個體的預設值，使其不會套用到鏡像資料庫，待完成主體與鏡像資料庫的設定之後，再重新啟用執行個體的預設值。  
  
### <a name="maintenance-plan"></a>維護計劃  
 不支援在啟用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]時，使用維護計劃建立資料庫備份。 維護計劃會導致記錄鏈結中斷，且[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]可能無法確保還原期間的資料庫復原能力。 若已在執行個體層級啟用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，也同樣適用此規則。  
  
> [!TIP]  
>  相同資料庫或執行個體所設定的[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]可支援只複製備份的維護計畫。  
  
### <a name="log-shipping"></a>記錄傳送  
 您無法針對相同的資料庫，同時設定記錄傳送和[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 這樣做會影響使用任一功能的資料庫復原能力。  
  
### <a name="ad-hoc-backups-using-transact-sql-and-sql-server-management-studio"></a>使用 Transact-SQL 和 SQL Server Management Studio 的隨選備份  
 根據使用的備份和儲存媒體類型，使用 Transact-SQL 或 SQL Server Management Studio 在[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]之外建立臨選或一次性備份會影響[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]程序。 記錄備份到不同的 azure 儲存體帳戶, 而[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]不是使用或 azure Blob 儲存體服務的任何其他目的地, 將導致記錄鏈中斷。 建議您使用[smart_admin. sp_backup_on_demand &#40; &#41; transact-sql](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)預存程式, 在已[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]啟用的資料庫上起始備份。 您可以使用此預存程序起始完整的資料庫備份或記錄備份。  
  
### <a name="drop-database-and-detach-database"></a>卸除資料庫和卸離資料庫  
 如果啟用[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的資料庫遭到卸離或卸除，雖然無法進行其他備份，但是先前的備份會保留在儲存體中，直到保留期限到期為止，之後會清除備份。  
  
### <a name="changes-to-recovery-model"></a>復原模式的變更  
  
-   如果您將資料庫的復原模式從 [**簡單**] 變更為 [**完整**] 或 [**大量記錄**], 您可以[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]選擇為資料庫設定。 從[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]的觀點來看，這就像是新資料庫一樣。  
  
-   如果您將資料庫的復原模式從 [**完整**] 或 [**大量記錄**] 變更為 [**簡單**] (已[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]啟用), 則不會再排程備份作業。 保留週期設定仍然有效，而且備份檔案會保留在儲存體帳戶中，直到保留週期到期為止。 如果您想保留備份，建議您將檔案下載至不同的儲存體帳戶或內部部署的位置。 這些設定會保留下來, 如果復原模式設定回**完整**或**大量記錄**, 則可以重複使用。  
  
### <a name="log-backups-using-other-backup-tools-or-custom-scripts"></a>使用其他備份工具或自訂指令碼的記錄備份  
 設定為在相同資料庫上執行記錄備份的任何兩個備份將會導致備份記錄鏈結中斷。 雖然 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 在偵測到鏈結中斷時會嘗試排程完整備份來修復備份鏈結中的中斷，但這就表示會繼續定期中斷及兩個競爭工具所執行的記錄備份。 這樣也可能會影響資料庫的復原能力，因為無法預期任何工具必須擁有循序的完整備份組。 雖然這適用於任何兩項功能或執行記錄備份的工具，但是對於執行特定範例 (如以下所述) 也很實用。 這也是設定維護計畫或記錄傳送之相關問題的根本，如本主題的稍早章節所述。  
  
 **以 Data Protection Manager (DPM) 為基礎的備份:** Microsoft Data Protection Manager 可讓您執行完整和增量備份。 累加備份是指在建立 T 記錄備份之後執行記錄截斷的記錄備份。 因此不支援針對相同資料庫設定 DPM 和[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。  
  
 **協力廠商工具或腳本:** 執行記錄備份而造成記錄截斷的任何協力廠商工具或腳本, [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]與不相容, 而且也不受支援。  
  
 如果您已[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]針對資料庫實例啟用, 而且想要進行臨機操作備份, 您可以使用先前章節中所述的[smart_admin sp_backup_on_demand &#40;transact-sql&#41; ](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)預存程式。 如果您在[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]之外也需要定期排程或執行備份，您可以使用 [只複製備份]。  如需詳細資訊，請參閱[只複製備份 &#40;SQL Server&#41;](../relational-databases/backup-restore/copy-only-backups-sql-server.md)。  
  
  
