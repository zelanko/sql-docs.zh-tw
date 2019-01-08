---
title: SQL Server Managed Backup to Windows Azure |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: afa01165-39e0-4efe-ac0e-664edb8599fd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b4071bee5e13f415be90328bb7ff0b55ff91087c
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52416389"
---
# <a name="sql-server-managed--backup-to-windows-azure"></a>SQL Server Managed Backup 到 Windows Azure
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]管理並將 SQL Server 備份至 Windows Azure Blob 儲存體服務的程序自動化。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 所使用的備份策略會以資料庫的保留週期與交易工作負載為依據。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 支援指定保留時間週期的時間點還原。   
[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]可以在資料庫層級或執行個體層級啟用，以管理 SQL Server 執行個體上的所有資料庫。 SQL Server 可以在內部部署中執行，也可以在 Windows Azure 虛擬機器一類的代管環境中執行。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 建議的 Windows Azure 虛擬機器上執行的 SQL Server。  
  
## <a name="benefits-of-automating-sql-server-backup-using-includesssmartbackupincludesss-smartbackup-mdmd"></a>使用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]將 SQL Server 備份自動化的優點  
  
-   目前自動份分多個資料庫需要制定備份策略、撰寫自訂程式碼及排程備份。 使用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]只需要提供保留週期設定與儲存位置。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 排程、 執行及維護備份。  
  
     [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]可在資料庫層級設定，或以 SQL Server 執行個體的預設值進行設定。 自動化備份使用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]具有下列優點：  
  
    -   藉由在執行個體層級設定預設值，可以將這些設定套用到在此之後所建立的資料庫，以避免新資料庫未被備份及資料遺失的風險。  
  
    -   在資料庫層級啟用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]及設定保留週期這項選擇，可讓您覆寫在執行個體層級所設定的預設值。 這讓您對特定資料庫的復原能力有更細微的控制。  
  
-   有了[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]，您就不需要指定資料庫備份的類型或頻率。  您指定的保留期間和[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]決定之資料庫會將備份儲存在 Windows Azure Blob 儲存體服務的類型和備份的頻率。 如需詳細資訊的準則集，[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]用來建立的備份策略，請參閱[元件和概念](#Concepts)本主題中的區段。  
  
-   如有設定使用加密，等於再為備份資料提供額外的一層保護。 如需詳細資訊，請參閱[備份加密](backup-encryption.md)  
  
 如需使用 Windows Azure Blob 儲存體的優點詳細[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]備份，請參閱[SQL Server 備份及還原與 Windows Azure Blob 儲存體服務](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
## <a name="terms-and-definitions"></a>詞彙和定義  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]  
 SQL Server 功能之一，可以自動備份資料庫備份並依據保留週期維護備份。  
  
 保留週期  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 會使用保留期限決定應該在儲存體中保留哪些備份檔案，才能將資料庫還原至指定時間範圍內的時間點。  支援的值是在 1-30 天的範圍內。  
  
 記錄鏈結  
 連續的記錄備份順序稱為記錄檔鏈結。 記錄鏈結以資料庫的完整備份開始。  
  
##  <a name="Concepts"></a> 需求、 概念和元件  
  
  
###  <a name="Security"></a> 權限  
 Transact-SQL 是用於設定和監視[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的主要介面。 一般情況下，若要執行組態預存程序， **db_backupoperator**資料庫角色**ALTER ANY CREDENTIAL**權限，並`EXECUTE`的權限**sp_delete_backuphistory**就需要預存程序。  用於檢閱資訊的預存程序及函數通常分別需要預存程序的 `Execute` 權限和函數的 `Select`。  
  
###  <a name="Prereqs"></a> 必要條件  
 **必要條件：**  
  
 **Windows Azure 儲存體服務**正由[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]儲存備份的檔案。    概念、 結構和建立 Windows Azure 儲存體帳戶的需求所詳述[Introduction to Key Components and Concepts](sql-server-backup-to-url.md#intorkeyconcepts)一節**SQL Server 備份至 URL**主題。  
  
 **SQL 認證**用來儲存驗證 Windows Azure 儲存體帳戶所需的資訊。 SQL 認證物件儲存帳戶名稱和存取金鑰資訊。 如需詳細資訊，請參閱 < [Introduction to Key Components and Concepts](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)一節**SQL Server 備份至 URL**主題。 如需如何建立 SQL 認證來儲存 Windows Azure 儲存體驗證資訊的逐步解說，請參閱[第 2 課：建立 SQL Server 認證](../../tutorials/lesson-2-create-a-sql-server-credential.md)。  
  
###  <a name="Concepts_Components"></a> 概念和重要元件  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]是管理備份作業的功能。 它會儲存在中繼資料**msdb**資料庫，並使用系統作業寫入完整資料庫和交易記錄備份。  
  
#### <a name="components"></a>元件  
 Transact-SQL 是與 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]互動的主要介面。 系統預存程序可用來啟用、設定及監視 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 系統函數可用來擷取現有的組態設定、參數值和備份檔案資訊。 擴充事件可用來呈現錯誤和警告。 警示機制可透過 SQL Agent 作業和 SQL Server 原則式管理加以啟用。 以下是物件清單及其與 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]相關的功能描述。  
  
 PowerShell 指令程式也可用於設定 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。 SQL Server Management Studio 可使用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] [還原資料庫] **工作，還原** 所建立的備份  
  
|||  
|-|-|  
|系統物件|描述|  
|**MSDB**|儲存 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]所建立之所有備份的中繼資料與備份記錄。|  
|[smart_admin.set_db_backup &#40;-SQL&AMP;#41;&#41;](https://msdn.microsoft.com/library/dn451013(v=sql.120).aspx)|針對資料庫啟用及設定[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的系統預存程序。|  
|[smart_admin.set_instance_backup &#40;-SQL&AMP;#41;&#41;](https://msdn.microsoft.com/library/dn451009(v=sql.120).aspx)|系統預存程序，進而啟用及設定預設設定[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]SQL Server 執行個體。|  
|[smart_admin.sp_ backup_master_switch &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-master-switch-transact-sql)|暫停及繼續[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的系統預存程序。|  
|[smart_admin.sp_set_parameter &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-set-parameter-transact-sql)|啟用及設定[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]監視的系統預存程序。 例如：啟用擴充事件、通知的郵件設定。|  
|[smart_admin.sp_backup_on_demand &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-backup-on-demand-transact-sql)|系統預存程序，用來啟用要使用的資料庫執行臨機操作備份[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]而不會中斷記錄鏈結。|  
|[smart_admin.fn_backup_db_config &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-functions/managed-backup-fn-backup-db-config-transact-sql)|傳回目前的系統函數[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]資料庫，或執行個體上的所有資料庫的狀態和組態值。|  
|[smart_admin.fn_is_master_switch_on &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-functions/managed-backup-fn-is-master-switch-on-transact-sql)|傳回主切換狀態的系統函數。|  
|[smart_admin.sp_get_backup_diagnostics &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-stored-procedures/managed-backup-sp-get-backup-diagnostics-transact-sql)|用於傳回擴充事件記錄之事件的系統預存程序。|  
|[smart_admin.fn_get_parameter &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-parameter-transact-sql)|傳回備份系統設定 (例如監視以及警示郵件設定) 之目前值的系統函數。|  
|[smart_admin.fn_available_backups &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-functions/managed-backup-fn-available-backups-transact-sql)|此預存程序可用於擷取指定資料庫或執行個體中所有資料庫的可用備份。|  
|[smart_admin.fn_get_current_xevent_settings &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-current-xevent-settings-transact-sql)|傳回目前擴充事件設定的系統函數。|  
|[smart_admin.fn_get_health_status &#40;-SQL&AMP;#41;&#41;](/sql/relational-databases/system-functions/managed-backup-fn-get-health-status-transact-sql)|此系統函數可傳回擴充事件對指定期間所記錄的錯誤彙總計算。|  
|[監視 SQL Server Managed Backup 到 Windows Azure](sql-server-managed-backup-to-microsoft-azure.md)|監視擴充事件、發送錯誤與警告的電子郵件通知，以及使用 SQL Server 原則管理[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。|  
  
#### <a name="backup-strategy"></a>備份策略  
 **使用的備份策略[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]:**  
  
 排程的備份類型以及備份頻率取決於資料庫的工作負載。 保留週期設定可用於指定備份檔案保留在儲存體中的時間，以及能否將資料庫復原至保留週期內的時間點。  
  
 **備份容器和檔案命名慣例：**  
  
 對於可用性資料庫之外的所有資料庫，[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]會使用 SQL Server 執行個體名稱命名 Windows Azure 儲存體容器。  對於可用性資料庫，則會使用可用性群組 GUID 來命名 Windows Azure 儲存體容器。  
  
 非可用性資料庫的備份檔案是使用以下慣例命名：使用資料庫名稱、 資料庫 GUID 的前 40 個字元來建立名稱不含 '-'，與時間戳記。 區段之間會插入底線字元做為分隔符號。 完整備份會使用副檔名 **.bak** ，記錄備份則會使用 **.log** 。 對於可用性群組資料庫而言，除了上面所述的檔案命名慣例以外，可用性群組資料庫 GUID 會加在資料庫名稱的 40 個字元之後。 可用性群組資料庫 GUID 值是 sys.databases 中的 group_database_id 值。  
  
 **完整資料庫備份：** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]代理程式排程完整資料庫備份，如果下列任一項為 true。  
  
-   資料庫是第一次啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] ，或是在執行個體層級以預設設定啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 。  
  
-   最後一次完整資料庫備份後，記錄成長已等於或大於 1 GB。  
  
-   最後一次完整資料庫備份後，已經過一週的最大時間間隔。  
  
-   記錄鏈結中斷。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 會藉由比較備份檔案的第一個和最後一個 LSN，定期檢查記錄鏈結是否保持完整。 如果記錄鏈結因故中斷， [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 就會排程完整資料庫備份。 記錄鏈結中斷的最常見原因可能是使用 Transact-SQL 發出的備份命令，或透過 SQL Server Management Studio 中的備份工作。  其他常見的情況包括備份記錄檔的意外刪除，或意外覆寫備份。  
  
 **交易記錄備份：** [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]排程記錄備份，如果下列任一項為真：  
  
-   找不到記錄 (log) 備份記錄 (history)。 第一次啟用 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 時，通常會有此情況。  
  
-   使用的交易記錄空間是 5 MB 或更大。  
  
-   達到最後一次記錄備份後的 2 小時最大時間間隔。  
  
-   交易紀錄備份一律會在完整資料庫備份之後執行。 其目的在保留完整備份之前的記錄檔鏈結。  
  
#### <a name="retention-period-settings"></a>保留週期設定  
 啟用備份時，您必須設定保留期限，以天為單位：最少是 1 天，最多是 30 天。  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 會根據保留週期設定，評估能否在指定的時間內，復原到某個時間點，從而決定所要保留的備份檔案，以及指定所要刪除的備份檔案。 備份的 backup_finish_date 會用於指定及比對保留週期設定所指定的時間。  
  
#### <a name="important-considerations"></a>重要考量因素  
 您必須了解一些會對[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]作業帶來重要影響的注意事項。 如下：  
  
-   當資料庫正在執行完整的資料庫備份作業時， [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 會等待目前作業完成，然後再為相同的資料庫執行另一個完整的資料庫備份。 同樣地，在指定的時間內，只可執行一個交易記錄備份。 不過，完整資料庫備份與交易記錄備份可以同時執行。 失敗會記錄為擴充事件。  
  
-   如果排程超過 10 個並行完整資料庫備份，會透過擴充事件的偵錯通道發出警告。 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 會維護其優先順序佇列，直到所有的備份均已排程並完成為止。  
  
###  <a name="support_limits"></a> 支援限制  
 以下是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 特有的一些限制：  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]代理程式僅支援資料庫備份：完整與記錄備份。  不支援檔案備份自動化。  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]作業目前可以支援 Transact-SQL。 使用擴充事件可完成監視和疑難排解。 PowerShell 和 SMO 支援只可用於設定 SQL Server 執行個體的儲存體和保留週期預設設定，以及依照 SQL Server 原則式管理原則監視備份狀態和整體健康狀況。  
  
-   不支援系統資料庫。  
  
-   Windows Azure Blob 儲存體服務是唯一支援的備份儲存體選項。 不支援備份至磁碟或磁帶。  
  
-   目前 Windows Azure 儲存體允許的分頁 Blob 檔案大小上限是 1 TB。 大於 1 TB 的備份檔案將會失敗。 為避免此情況，建議大型資料庫先行壓縮，然後在設定[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]之前測試備份檔案大小。 測試方法有兩種：一是藉由備份到本機磁碟，一是利用 `BACKUP TO URL` Transact-SQL 陳述式手動備份到 Windows Azure 儲存體。 如需詳細資訊，請參閱 [SQL Server Backup to URL](sql-server-backup-to-url.md)。  
  
-   復原模式：僅支援設定為完整或大量記錄模式的資料庫。  不支援設定為簡單復原模式的資料庫。  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 時，可能會有一些限制。 如需詳細資訊，請參閱[SQL Server Managed Backup to Windows Azure:互通性與共存性](../../database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
|||  
|-|-|  
|**由於工作描述**|**主題**|  
|基本工作，例如為資料庫設定[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]，或在執行個體層級進行預設設定、在執行個體或資料庫層級停用[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]、暫停及重新啟動[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]。|[SQL Server Managed Backup 到 Windows Azure - 保留和儲存體設定](../../database-engine/sql-server-managed-backup-to-windows-azure-retention-and-storage-settings.md)|  
|**教學課程：** 設定與監視 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的逐步指示。|[設定 SQL Server Managed Backup 到 Windows Azure](enable-sql-server-managed-backup-to-microsoft-azure.md)|  
|**教學課程：** 設定與監視可用性群組中資料庫之 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 的逐步指示。|[針對可用性群組設定 SQL Server Managed Backup 到 Windows Azure](../../database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md)|  
|監視[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的相關工具、概念和工作。|[監視 SQL Server Managed Backup 到 Windows Azure](sql-server-managed-backup-to-microsoft-azure.md)|  
|疑難排解[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]的工具和步驟。|[針對 SQL Server Managed Backup 到 Windows Azure 進行疑難排解](../../database-engine/troubleshooting-sql-server-managed-backup-to-windows-azure.md)|  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 備份及還原與 Windows Azure Blob 儲存體服務](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
 [SQL Server 備份至 URL](sql-server-backup-to-url.md)   
 [SQL Server Managed 的 Backup，到 Windows Azure 位置表示：互通性與共存性](../../database-engine/sql-server-managed-backup-to-windows-azure-interoperability-and-coexistence.md)   
 [針對 SQL Server Managed Backup 到 Windows Azure 進行疑難排解](../../database-engine/troubleshooting-sql-server-managed-backup-to-windows-azure.md)  
  
  
