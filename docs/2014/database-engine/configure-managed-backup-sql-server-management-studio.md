---
title: 設定受管理的備份 (SQL Server Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.managedbackup.configure.f1
ms.assetid: 79397cf6-0611-450a-b0d8-e784a76e3091
caps.latest.revision: 9
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4d09c001bc7c267b2235377a1312609ee8b7b3fa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37209828"
---
# <a name="configure-managed-backup-sql-server-management-studio"></a>設定受管理的備份 (SQL Server Management Studio)
  **Managed Backup**  對話方塊可讓您設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]執行個體的預設值。 本主題描述如何使用此對話方塊來設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]這麼做時，您必須考量的選項與執行個體的預設設定。 當[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]已設定的執行個體，設定會套用至之後建立任何新資料庫。  
  
 如果您想要設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]特定的資料庫，請參閱[啟用及設定 SQL Server Managed Backup to Windows Azure 資料庫](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure)。  
 
> [!NOTE] 
> SQL Server Managed Backup 不支援 Proxy 伺服器。 
  
## <a name="task-list"></a>工作清單  
  
## <a name="includesssmartbackupincludesss-smartbackup-mdmd-functions-using-managed-backup-interface-in-sql-server-management-studio"></a>[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)] 函式使用 Backup Interface 介面在 SQL Server Management Studio  
 在此版本中，您只可以使用 **[管理備份]** 介面設定的執行個體層級的預設設定。 您無法設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]資料庫，暫停或繼續[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]作業或設定電子郵件通知。 如需如何執行作業目前不支援透過**Managed Backup**介面，請參閱[SQL Server Managed Backup to Windows Azure-Retention and Storage Settings](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)。  
  
## <a name="permissions"></a>Permissions  
 **在 SQL Server Management Studio 中檢視 Managed Backup 節點：** 若要在  **[物件總管]** 中檢視 **Managed Backup**節點，您必須是系統管理員，或具有下列為您的使用者帳戶特別授與的權限：  
  
-   `db_backupoperator`  
  
-   `VIEW SERVER STATE`  
  
-   `ALTER ANY CREDENTIAL`  
  
-   `VIEW ANY DEFINITION`  
  
-   `EXECUTE` 在  `smart_admin.fn_is_master_switch_on`。  
  
-   `SELECT` 在  `smart_admin.fn_backup_instance_config`。  
  
 **若要設定 Managed Backup:** 若要設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]在 SQL Server Management Studio，您必須是系統管理員，或具有下列權限：  
  
 中的成員資格`db_backupoperator`與資料庫角色`ALTER ANY CREDENTIAL`權限，並`EXECUTE`權限`sp_delete_backuphistory`預存程序。  
  
 `SELECT` 權限`smart_admin.fn_get_current_xevent_settings`函式。  
  
 `EXECUTE` 權限`smart_admin.sp_get_backup_diagnostics`預存程序。 除此之外，因為它會從內部呼叫其他需要此權限的系統物件，所以還需要 `VIEW SERVER STATE` 權限。  
  
 `EXECUTE` 權限`smart_admin.sp_set_instance_backup`，和`smart_admin.sp_backup_master_switch`。  
  
## <a name="configure-includesssmartbackupincludesss-smartbackup-mdmd-using-sql-server-management-studio"></a>設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]使用 SQL Server Management Studio  
 從 **[物件總管]** 展開 **[管理]** 節點，並以滑鼠右鍵按一下 **[Managed Backup]**。 選取 **[設定]**。 這樣會開啟 **[Managed Backup]** 對話方塊。  
  
 勾選 **[啟用 Managed Backup]** 選項，並指定組態值：  
  
 **[檔案保留]** 期間以天為單位指定，且應介於 1 到 30 之間。  
  
 您選取的 **[SQL 認證]** 應符合儲存體帳戶。 如果您目前沒有儲存驗證資訊的 SQL 認證，您可以按一下 **[建立]** 加以建立。 您也可以使用 CREATE CREDENTIAL Transact-SQL 陳述式來建立認證，並提供識別的儲存體帳戶名稱和 SECRET 參數的存取金鑰。 如需詳細資訊，請參閱 <<c0> [ 建立認證](../relational-databases/backup-restore/sql-server-backup-to-url.md#credential)。  
  
 指定 Windows Azure 儲存體帳戶的 **[儲存體 URL]** 、儲存儲存體帳戶之驗證資訊的 SQL 認證，和備份檔案的保留期限。  
  
 儲存體 URL 格式： https://\<StorageAccount >.blob.core.windows.net/  
  
 若要設定執行個體層級的加密設定，請勾選 **[加密備份]** 選項，並指定演算法，和用於加密的憑證或非對稱金鑰。  這會在執行個體層級進行設定，並且在套用此組態之後用於所有建立的新資料庫。  
  
> [!WARNING]  
>  此對話方塊無法用來指定加密選項，而不設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]。 這些加密選項僅適用於[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]作業。 若要使用加密其他備份程序，請參閱[備份加密](../relational-databases/backup-restore/backup-encryption.md)。  
  
### <a name="considerations"></a>考量  
 如果您設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]執行個體層級，設定會套用至之後建立任何新資料庫。  不過，現有的資料庫將不會自動繼承這些設定。 若要設定[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]上先前已存在的資料庫，您必須特別設定每個資料庫。 如需詳細資訊，請參閱 <<c0> [ 啟用和設定 SQL Server Managed Backup to Windows Azure 資料庫](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md#DatabaseConfigure)。  
  
 如果[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]已暫停，使用`smart_admin.sp_backup_master_switch`，您會看到一則警告訊息 「 Managed Backup 已停用和目前的設定不會生效...」 當您嘗試完成設定。 使用`smart_admin.sp_backup_master_switch`儲存和設定@new_state= 1。 這將會繼續[!INCLUDE[ss_smartbackup](../includes/ss-smartbackup-md.md)]服務和組態設定將會生效。 如需有關預存程序的詳細資訊，請參閱 < [smart_admin.sp_ backup_master_switch &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql)。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server Managed Backup 到 Windows Azure：互通性與共存性](../../2014/database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)  
  
  
