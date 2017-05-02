---
title: "系統資料庫的備份與還原 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- system databases [SQL Server], backing up and restoring
- restoring system databases [SQL Server]
- backing up [SQL Server], system databases
- database backups [SQL Server], system databases
- servers [SQL Server], backup
ms.assetid: aef0c4fa-ba67-413d-9359-1a67682fdaab
caps.latest.revision: 57
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5b2e9a63f334206750961a39403daed7e3608ce0
ms.lasthandoff: 04/11/2017

---
# <a name="back-up-and-restore-of-system-databases-sql-server"></a>系統資料庫的備份與還原 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會維護一組系統層級資料庫，即「系統資料庫」**，這對伺服器執行個體的運作而言是不可或缺的。 在每次重大更新之後，有幾個系統資料庫必須加以備份。 您一定要備份的系統資料庫包括 **msdb**、 **master**和 **model**。 如果有任何資料庫在伺服器執行個體上使用複寫，您還必須備份 **distribution** 系統資料庫。 這些系統資料庫的備份可讓您在發生系統失敗 (如硬碟故障) 時還原和復原 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統。  
  
 下表摘要列出所有系統資料庫。  
  
|系統資料庫|描述|需要備份嗎？|復原模式|註解|  
|---------------------|-----------------|---------------------------|--------------------|--------------|  
|[master](../../relational-databases/databases/master-database.md)|記錄 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統之所有系統層級資訊的資料庫。|是|Simple|請視需要經常備份 **master** ，充分地保護資料以滿足您業務的需求。 建議安排定期備份，您可在進行大規模更新之後，以額外的備份來補充。|  
|[model](../../relational-databases/databases/model-database.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上建立之所有資料庫的範本。|是|可由使用者設定*|只在有業務上有需要時才備份 **model** ；例如，在自訂資料庫選項之後立即備份。<br /><br /> **最佳作法** ：我們建議您在必要時僅建立 **model**的完整資料庫備份。 因為 **model** 很小，而且少有變更，所以不需要備份記錄。|  
|[msdb](../../relational-databases/databases/msdb-database.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 用於排程警示和作業以及用於記錄操作員的資料庫。 **msdb** 也包含歷程記錄資料表，例如備份和還原歷程記錄資料表。|是|簡單 (預設值)|每當 **msdb** 更新時就加以備份。|  
|[Resource](../../relational-databases/databases/resource-database.md) (RDB)|唯讀資料庫，其中包含下者隨附之所有系統物件的複本： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|否|—|**Resource** 資料庫位於 mssqlsystemresource.mdf 檔案中，這個檔案中只包含程式碼。 因此， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法備份 **Resource** 資料庫。<br /><br /> 注意：您可以將 mssqlsystemresource.mdf 檔視為二進位 (.exe) 檔案而非資料庫檔案，藉以針對該檔案執行以檔案或磁碟為基礎的備份。 但是您無法在這些備份上使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 還原。 還原 mssqlsystemresource.mdf 的備份副本只能手動完成，而且您必須小心不要使用過期或可能不安全的 **Resource** 資料庫來覆寫目前的資料庫。|  
|[tempdb](../../relational-databases/databases/tempdb-database.md)|用以保存暫存或中繼結果集的工作空間。 每當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體啟動時，就會重新建立此資料庫。 當伺服器執行個體關閉時， **tempdb** 中的任何資料都會被永久刪除。|否|Simple|您不能備份 **tempdb** 系統資料庫。|  
|[設定散發](../../relational-databases/replication/configure-distribution.md)|唯有將伺服器設定為複寫散發者時才會存在的資料庫。 這個資料庫會儲存各種複寫的中繼資料和記錄資料，以及異動複寫的交易。|是|Simple|如需有關何時備份 **distribution** 資料庫的詳細資訊，請參閱[備份及還原複寫的資料庫](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)。|  
  
 *若要了解模型的目前復原模式，請參閱[檢視或變更資料庫的復原模式 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md) 或 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)。  
  
## <a name="limitations-on-restoring-system-databases"></a>還原系統資料庫的限制  
  
-   您只能從伺服器執行個體目前執行之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本所建立的備份還原系統資料庫。 例如，若要還原執行於 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 之伺服器執行個體上的系統資料庫，您必須使用在伺服器執行個體升級至 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 之後所建立的資料庫備份。  
  
-   若要還原任何資料庫， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體必須在執行中。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] master **資料庫必須是可存取的，而且至少部分可用，** 的執行個體才能夠啟動。 如果 **master** 資料庫變得無法使用，您可以使用下列任一方法將資料庫回復到可用狀態：  
  
    -   從現行資料庫備份來還原 **master** 。  
  
         如果您可以啟動伺服器執行個體，應該就能夠從完整資料庫備份來還原 **master** 。  
  
    -   完全重建 **master** 。  
  
         如果 **master** 嚴重損壞，使您無法啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，則必須重建 **master**。 如需詳細資訊，請參閱 [重建系統資料庫](../../relational-databases/databases/rebuild-system-databases.md)。  
  
        > [!IMPORTANT]  
        >  重建 **master** 將會重建所有的系統資料庫。  
  
-   在某些情況下，復原 model 資料庫若發生問題，可能就需要重建系統資料庫，或是置換 model 資料庫的 mdf 和 ldf 檔案。 如需詳細資訊，請參閱 [重建系統資料庫](../../relational-databases/databases/rebuild-system-databases.md)。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [完整資料庫還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
  
-   [還原 master 資料庫 &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md)  
  
-   [檢視或變更資料庫的復原模式 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
-   [移動系統資料庫](../../relational-databases/databases/move-system-databases.md)  
  
## <a name="see-also"></a>另請參閱  
 [散發資料庫](../../relational-databases/replication/distribution-database.md)   
 [master 資料庫](../../relational-databases/databases/master-database.md)   
 [msdb 資料庫](../../relational-databases/databases/msdb-database.md)   
 [Model 資料庫](../../relational-databases/databases/model-database.md)   
 [Resource 資料庫](../../relational-databases/databases/resource-database.md)   
 [tempdb 資料庫](../../relational-databases/databases/tempdb-database.md)  
  
  
