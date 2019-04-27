---
title: 設定受管理的備份 (SQL Server Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.managedbackup.configure.f1
ms.assetid: 79397cf6-0611-450a-b0d8-e784a76e3091
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2f8c9664baa2803bbab4282b6897d49f0ddb1831
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62812705"
---
# <a name="configure-managed-backup-sql-server-management-studio"></a>設定受管理的備份 (SQL Server Management Studio)
  **[受管理的備份]** 對話方塊可讓您設定執行個體的 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 預設值。 本主題說明如何使用此對話方塊來設定執行個體的 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 預設設定，和您在這麼做時必須考量的選項。 在設定執行個體的 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 時，設定會套用至之後建立的任何新資料庫。  
  
 如果您想要設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]特定的資料庫，請參閱[啟用及設定 SQL Server Managed Backup to Windows Azure 資料庫](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure)。  
 
> [!NOTE] 
> SQL Server Managed Backup 不支援 Proxy 伺服器。 
  
## <a name="task-list"></a>工作清單  
  
## <a name="includesssmartbackupincludesss-smartbackup-mdmd-functions-using-managed-backup-interface-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中使用 Backup Interface 介面的 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 函數  
 在此版本中，您只可以使用 **[管理備份]** 介面設定的執行個體層級的預設設定。 您無法設定資料庫的 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 、暫停或繼續 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 作業，或設定電子郵件通知。 如需如何執行作業目前不支援透過**Managed Backup**介面，請參閱[SQL Server Managed Backup to Windows Azure - 保留和儲存體設定](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)。  
  
## <a name="permissions"></a>Permissions  
 **檢視 Managed Backup 節點是 SQL Server Management Studio:** 若要檢視**Managed Backup**中的節點**物件總管 中**，您必須是系統管理員，或具有下列權限，特別授與您的使用者帳戶：  
  
-   `db_backupoperator`  
  
-   `VIEW SERVER STATE`  
  
-   `ALTER ANY CREDENTIAL`  
  
-   `VIEW ANY DEFINITION`  
  
-   `EXECUTE` 在  `smart_admin.fn_is_master_switch_on`。  
  
-   `SELECT` 在  `smart_admin.fn_backup_instance_config`。  
  
 **若要設定 Managed Backup：** 若要在 SQL Server Management Studio 中設定 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ，您必須是系統管理員，或具有下列權限：  
  
 `db_backupoperator` 資料庫角色的成員資格，且該角色必須具有 `ALTER ANY CREDENTIAL` 權限，以及 `sp_delete_backuphistory` 預存程序的 `EXECUTE` 權限。  
  
 `smart_admin.fn_get_current_xevent_settings` 函數的 `SELECT` 權限。  
  
 `EXECUTE` 權限`smart_admin.sp_get_backup_diagnostics`預存程序。 除此之外，因為它會從內部呼叫其他需要此權限的系統物件，所以還需要 `VIEW SERVER STATE` 權限。  
  
 `smart_admin.sp_set_instance_backup` 的 `EXECUTE` 權限和 `smart_admin.sp_backup_master_switch`。  
  
## <a name="configure-includesssmartbackupincludesss-smartbackup-mdmd-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 設定 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]  
 從 **[物件總管]** 展開 **[管理]** 節點，並以滑鼠右鍵按一下 **[Managed Backup]**。 選取 **[設定]**。 這樣會開啟 **[Managed Backup]** 對話方塊。  
  
 勾選 **[啟用 Managed Backup]** 選項，並指定組態值：  
  
 **[檔案保留]** 期間以天為單位指定，且應介於 1 到 30 之間。  
  
 您選取的 **[SQL 認證]** 應符合儲存體帳戶。 如果您目前沒有儲存驗證資訊的 SQL 認證，您可以按一下 **[建立]** 加以建立。 您也可以使用 CREATE CREDENTIAL Transact-SQL 陳述式來建立認證，並提供識別的儲存體帳戶名稱和 SECRET 參數的存取金鑰。 如需詳細資訊，請參閱＜ [Create a Credential](../relational-databases/backup-restore/sql-server-backup-to-url.md#credential)＞。  
  
 指定 Windows Azure 儲存體帳戶的 **[儲存體 URL]** 、儲存儲存體帳戶之驗證資訊的 SQL 認證，和備份檔案的保留期限。  
  
 儲存體 URL 格式： https://\<StorageAccount >.blob.core.windows.net/  
  
 若要設定執行個體層級的加密設定，請勾選 **[加密備份]** 選項，並指定演算法，和用於加密的憑證或非對稱金鑰。  這會在執行個體層級進行設定，並且在套用此組態之後用於所有建立的新資料庫。  
  
> [!WARNING]  
>  若未設定 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]，則此對話方塊無法用來指定加密選項。 這些加密選項僅適用於 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 作業。 若要在其他備份程序中使用加密，請參閱 [Backup Encryption](../relational-databases/backup-restore/backup-encryption.md)。  
  
### <a name="considerations"></a>考量  
 如果您在執行個體層級設定 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ，設定會套用至之後建立的任何新資料庫。  不過，現有的資料庫將不會自動繼承這些設定。 若要在先前已存在的資料庫上設定 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] ，您必須個別設定每個資料庫。 如需詳細資訊，請參閱 <<c0> [ 啟用和設定 SQL Server Managed Backup to Windows Azure 資料庫](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure)。  
  
 如果[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]已暫停，使用`smart_admin.sp_backup_master_switch`，您會看到一則警告訊息 「 Managed Backup 已停用和目前的設定不會生效...」，當您嘗試完成設定。 使用`smart_admin.sp_backup_master_switch`儲存和設定@new_state= 1。 這將會繼續 [!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 服務，且組態設定將會生效。 如需有關預存程序的詳細資訊，請參閱 < [smart_admin.sp_ backup_master_switch &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Managed 的 Backup，到 Windows Azure 位置表示：互通性與共存性](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
  
