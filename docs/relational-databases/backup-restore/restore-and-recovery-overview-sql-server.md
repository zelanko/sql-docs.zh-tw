---
title: 還原和復原概觀 (SQL Server) | Microsoft 文件
description: 本文概述依序還原一組 SQL Server 備份，以復原失敗的 SQL Server 資料庫時所涉及的各項作業。
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring tables [SQL Server]
- backups [SQL Server], restore scenarios
- database backups [SQL Server], restore scenarios
- database restores [SQL Server]
- restoring [SQL Server]
- restores [SQL Server]
- table restores [SQL Server]
- restoring databases [SQL Server], about restoring databases
- database restores [SQL Server], scenarios
- accelerated database recovery
ms.assetid: e985c9a6-4230-4087-9fdb-de8571ba5a5f
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5157ab86adbbea5b6e9fa1bdb14264f5418ac07b
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810695"
---
# <a name="restore-and-recovery-overview-sql-server"></a>還原和復原概觀 (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  若要從失敗復原 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，資料庫管理員必須依邏輯正確和有意義的還原順序來還原一組 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 還原及復原，可從一整個資料庫、單一資料檔或資料頁面的備份還原資料，如下所示：  
  
-   資料庫 ( *「完整資料庫還原」* (Complete database restore))  
  
     將會還原並復原整個資料庫，且在還原與復原作業期間，資料庫會離線。  
  
-   資料檔 ( *「檔案還原」* )  
  
     還原與復原一個資料檔或一組檔案。 在檔案還原過程中，包含該檔案的檔案群組會在還原的持續時間內自動離線。 任何存取離線檔案群組的嘗試都會產生錯誤。  
  
-   資料頁 ( *「分頁還原」* (Page restore))  
  
     在完整復原模式或大量記錄復原模式下，您可以還原各個資料庫。 不論檔案群組的數目為何，在任何資料庫上都可以執行分頁還原。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份與還原可以跨所有支援的作業系統運作。 如需支援的作業系統詳細資訊，請參閱 [安裝 SQL Server 2016 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。 如需舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之備份支援的相關資訊，請參閱 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)的＜相容性支援＞一節。  
  
##  <a name="overview-of-restore-scenarios"></a><a name="RestoreScenariosOv"></a> 還原案例概觀  
 *中的* 「還原案例」 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Restore scenario) 是指先從一個或多個備份還原資料，再復原資料庫的程序。 支援的還原實例視資料庫的復原模式與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的版本而定。  
  
 下表介紹各種復原模式可能支援的還原實例。  
  
|中的|在簡單復原模式下|在完整/大量記錄復原模式下|  
|----------------------|---------------------------------|----------------------------------------------|  
|完整資料庫還原|這是基本還原策略。 完整資料庫還原可能只包括還原和復原完整資料庫備份。 此外，完整資料庫還原也可能包括還原完整資料庫備份，接著再還原和復原差異備份。<br /><br /> 如需詳細資訊，請參閱[完整資料庫還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)。|這是基本還原策略。 完整資料庫還原包括還原完整資料庫備份和選用的差異備份 (如果有的話)，然後依照順序還原所有後續的記錄備份。 復原最後一個記錄備份，並且加以還原 (RESTORE WITH RECOVERY)，即完成完整資料庫還原。<br /><br /> 如需詳細資訊，請參閱[完整資料庫還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)。|  
|File restore **\***|還原一個或多個損毀的唯讀檔案，而不還原整個資料庫。 唯有當資料庫至少有一個唯讀檔案群組時，才能使用檔案還原。|還原一個或多個檔案，而不還原整個資料庫。 可以在資料庫離線時，或在資料庫仍在線上時 (適用於某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本) 執行檔案還原。 在檔案還原期間，包含正在還原中之檔案的檔案群組一律為離線狀態。|  
|分頁還原|不適用|還原一個或多個損毀的頁面。 可以在資料庫離線時，或在資料庫仍在線上時 (適用於某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本) 執行頁面還原。 在分頁還原期間，正在還原中的頁面一律為離線狀態。<br /><br /> 未中斷的記錄備份鏈結必須可用 (直到目前記錄檔)，且必須全部套用，才能使分頁與目前記錄檔保持一樣新。<br /><br /> 如需詳細資訊，請參閱[還原頁面 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)。|  
|分次還原 **\***|在檔案群組層級上，從主要檔案群組開始，接著是所有讀取/寫入次要檔案群組，分階段還原和復原資料庫。|從主要檔案群組開始，在檔案群組層級上分階段還原和復原資料庫。<br /><br /> 如需詳細資訊，請參閱[分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)|  
  
 **\*** 只有 Enterprise 版才支援線上還原。  

### <a name="steps-to-restore-a-database"></a>還原資料庫的步驟
若要執行檔案還原，[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 會執行兩個步驟： 

-   建立任何遺失的資料庫檔案。

-   將資料從備份裝置複製到資料庫檔案。

若要執行資料庫還原，[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 會執行三個步驟： 

-   建立資料庫和交易記錄檔 (若尚未存在的話)。

-   從資料庫的備份媒體將所有資料、記錄和索引頁複製到資料庫檔案。 

-   在所謂的[復原流程](#TlogAndRecovery)中套用交易記錄。

 不論還原資料的方式如何，在復原資料庫之前， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 保證整個資料庫在邏輯上是一致的。 例如，如果您要還原檔案，除非您已經將其向前復原到足以和資料庫保持一致的程度，否則無法加以復原並使其回到線上。  
  
### <a name="advantages-of-a-file-or-page-restore"></a>檔案或分頁還原的優點  
 還原與復原檔案或頁面 (而非整個資料庫) 可提供下列優點：  
  
-   還原較少的資料，可縮短複製和復原資料所需的時間。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上，還原檔案或頁面可以讓資料庫中的其他資料在還原作業期間維持線上狀態。  

## <a name="recovery-and-the-transaction-log"></a><a name="TlogAndRecovery"></a> 復原和交易記錄
針對大多數的還原案例，必須套用交易記錄備份並允許 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行**復原流程**，資料庫才能上線。 復原是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的的流程，為的是讓每個資料庫都能以交易一致 (或正常) 狀態啟動。

在容錯移轉或其他不正常關機的情況下，資料庫可能會停留在緩衝區快取中有些修改尚未寫入資料檔，且未完成交易已在資料檔中作了一些修改的狀態。 啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體時，其會執行每個資料庫的復原；這些復原都是以最後一個[資料庫檢查點](../../relational-databases/logs/database-checkpoints-sql-server.md)為基礎的三個階段所組成：

-   **分析階段**會分析交易記錄來判斷最後一個檢查點為何，並建立中途分頁資料表 (Dirty Page Table，DPT) 和使用中交易資料表 (Active Transaction Table，ATT)。 DPT 包含資料庫關機時已變更的分頁記錄。 ATT 包含資料庫不正常關機時仍在使用中的交易記錄。

-   **重做階段**會向前復原資料庫關機時，記錄中每個已記錄且可能尚未寫入資料檔的修改內容。 其會在 DPT 中找到成功進行全資料庫復原時所需要的[最小記錄序號](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#minlsn) (minLSN)，並標記所有中途分頁上所需重做作業的開始。 在此階段，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 會將所有屬於已認可交易的中途分頁寫入磁碟。

-   **復原階段**會復原 ATT 中找到的未完成交易，確保資料庫的完整性。 回復之後，資料庫會上線，而且不再有交易記錄備份可以套用到資料庫。

每個資料庫復原階段進度的資訊都會記錄在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [錯誤記錄檔](../../tools/configuration-manager/viewing-the-sql-server-error-log.md)中。 資料庫復原進度也可以使用擴充事件進行追蹤。 如需詳細資訊，請參閱部落格文章[資料庫復原進度的新擴充事件](/archive/blogs/sql_server_team/new-extended-events-for-database-recovery-progress)。

> [!NOTE]
> 針對分次還原案例，如果唯讀檔案群組從建立檔案備份以前已經是唯讀，就不需要將記錄備份套用到檔案群組，且檔案還原會跳過它。 

<a name="FastRecovery"></a>
> [!NOTE]
> 為了最大化企業環境中資料庫的可用性，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition 可以在重做階段後，且「復原階段」仍在執行時就讓資料庫上線。 這稱為「快速復原」。

##  <a name="recovery-models-and-supported-restore-operations"></a><a name="RMsAndSupportedRestoreOps"></a> 復原模式和支援的還原作業  
 資料庫可用的還原作業，取決於其復原模式。 下表摘要說明每一種復原模式是否支援給定的還原實例，及其支援的範圍。  
  
|還原作業|完整復原模式|大量記錄復原模式|簡單復原模式|  
|-----------------------|-------------------------|---------------------------------|---------------------------|  
|資料復原|完整復原 (如果有記錄可以使用)。|有損失部分資料的風險。|自上次完整或差異備份之後的任何資料，都會遺失。|  
|時間點還原|記錄備份涵蓋的任何時間。|如果記錄備份含有大量記錄變更，則不允許。|不支援。|  
|File restore **\***|完整支援。|有時。 **\*\***|僅適用於唯讀的次要檔案。|  
|Page restore **\***|完整支援。|有時。 **\*\***|無。|  
|分次 (檔案群組-等級) 還原 **\***|完整支援。|有時。 **\*\***|僅適用於唯讀的次要檔案。|  
  
 **\*** 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 **\*\*** 如需了解必要條件，請參閱此主題稍後的 [簡單復原模式下的還原限制](#RMsimpleScenarios)。  
  
> [!IMPORTANT]  
> 不論資料庫的復原模式為何，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份都無法還原至比建立備份版本還舊的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 版本。  
  
## <a name="restore-scenarios-under-the-simple-recovery-model"></a><a name="RMsimpleScenarios"></a> 簡單復原模式下的還原案例  
 簡單復原模式在還原作業上具有下列限制：  
  
-   檔案還原及分次還原僅適用於唯讀的次要檔案群組。 如需有關這些資訊還原案例，請參閱[檔案還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md) 和[分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)。  
  
-   不允許分頁還原。  
  
-   不允許時間點還原。  
  
 如果這些限制中有任何一項不適合您的復原需要，即建議您考慮使用完整復原模式。 如需詳細資訊，請參閱 [備份概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)。  
  
> [!IMPORTANT]  
> 不論資料庫的復原模式為何，比建立備份之版本還舊的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本，都無法還原 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份。  
  
##  <a name="restore-under-the-bulk-logged-recovery-model"></a><a name="RMblogRestore"></a> 大量記錄復原模式下的還原  
 本節討論大量記錄復原模式的特殊還原考量，此為專門用做完整復原模式的補充。  
  
> [!NOTE]  
> 如需大量記錄復原模式的介紹，請參閱[交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)。  
  
 一般而言，大量記錄復原模式與完整復原模式類似，針對完整復原模式所描述的資訊也同時適用於兩者。 但是，大量記錄復原模式會影響時間點復原與線上還原。  
  
### <a name="restrictions-for-point-in-time-recovery"></a>時間點復原的限制  
 如果大量記錄復原模式下建立的記錄備份包含大量記錄變更，就不允許時間點復原。 嘗試對包含大量變更的記錄備份執行時間點復原將會造成還原作業失敗。  
  
### <a name="restrictions-for-online-restore"></a>對線上還原的限制  
 線上還原順序只有在符合下列條件時才能運作：  
  
-   必須在開始還原順序之前完成所有必要的記錄備份。  
  
-   必須在開始線上還原順序之前先備份大量變更。  
  
-   如果資料庫中存在大量變更，則所有的檔案都必須在線上，或是[無用](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)。 (這表示它不再是資料庫的一部分)。  
  
 如果沒有符合這些條件，線上還原順序就會失敗。  
  
> [!NOTE]  
>  我們建議您先切換到完整復原模式，再開始線上還原。 如需詳細資訊，請參閱[復原模式 &#40;SQL Server &#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)。  
  
 如需有關如何執行線上還原的詳細資訊，請參閱[線上還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)。  
  
##  <a name="database-recovery-advisor-sql-server-management-studio"></a><a name="DRA"></a> Database Recovery Advisor (SQL Server Management Studio)  
Database Recovery Advisor 有助於建構實作最佳化正確還原順序的還原計畫。 我們已經處理了客戶所要求的許多已知資料庫還原問題和增強功能。 Database Recovery Advisor 導入的主要增強功能包括：  
  
-   **還原計畫演算法：** 用來建構還原計畫的演算法已經大幅改善，特別是針對複雜的還原狀況。 相較於舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]而言，可更有效率地處理許多邊緣案例 (包括時間點還原的分岔案例)。  
  
-   **時間點還原：** Database Recovery Advisor 大幅簡化了將資料庫還原到特定時間點的作業。 視覺備份時間表大幅增強時間點還原的支援。 這個視覺化時間表可讓您識別當做還原資料庫之目標復原點的可行時間點。 時間表可加快周遊分岔復原路徑 (跨多個復原分岔之路徑)。 特定時間點還原計畫會自動包含與還原至目標時間點 (日期和時間) 有關的備份。 如需詳細資訊，請參閱[將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)。  
  
如需有關 Database Recovery Advisor 的詳細資訊，請參閱下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理能力部落格：  
  
-   [Recovery Advisor：簡介](/archive/blogs/managingsql/recovery-advisor-an-introduction) \(英文\)  
  
-   [Recovery Advisor：使用 SSMS 來建立/還原分割備份](/archive/blogs/managingsql/recovery-advisor-using-ssms-to-createrestore-split-backups) \(英文\)  

## <a name="accelerated-database-recovery"></a><a name="adr"></a> 加速資料庫復原
[加速資料庫復原](/azure/sql-database/sql-database-accelerated-database-recovery/)可在 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中使用。 加速資料庫復原藉由重新設計 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] [復原流程](#TlogAndRecovery)來大幅改善資料庫可用性，尤其是針對長時間執行的交易。 啟用加速資料庫復原的資料庫，其在容錯移轉或其他非正常關機之後完成復原流程的速度會大幅加快。 啟用時，加速資料庫復原也會大幅加快完成復原已取消長時間執行交易的速度。

您可以使用下列語法，為 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 上的每個資料庫上啟用加速資料庫復原：

```sql
ALTER DATABASE <db_name> SET ACCELERATED_DATABASE_RECOVERY = ON;
```

> [!NOTE]
> 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 上，加速資料庫復原預設為啟用。

## <a name="see-also"></a><a name="RelatedContent"></a> 另請參閱  
 [備份概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)      
 [交易記錄 &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)     
 [SQL Server 交易記錄架構與管理指南](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md)     
 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)     
 [套用交易記錄備份 (SQL Server)](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)