---
title: 還原和復原概觀 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
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
ms.assetid: e985c9a6-4230-4087-9fdb-de8571ba5a5f
caps.latest.revision: 44
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 72c827235057c77fe42de062dc2c09050dd1a698
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37197488"
---
# <a name="restore-and-recovery-overview-sql-server"></a>還原和復原概觀 (SQL Server)
  若要從失敗復原 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，資料庫管理員必須依邏輯正確和有意義的還原順序來還原一組 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 還原及復原，可從一整個資料庫、單一資料檔或資料頁面的備份還原資料，如下所示：  
  
-   資料庫 ( *「完整資料庫還原」*(Complete database restore))  
  
     將會還原並復原整個資料庫，且在還原與復原作業期間，資料庫會離線。  
  
-   資料檔 ( *「檔案還原」*)  
  
     還原與復原一個資料檔或一組檔案。 在檔案還原過程中，包含該檔案的檔案群組會在還原的持續時間內自動離線。 任何存取離線檔案群組的嘗試都會產生錯誤。  
  
-   資料頁 ( *「分頁還原」*(Page restore))  
  
     在完整復原模式或大量記錄復原模式下，您可以還原各個資料庫。 不論檔案群組的數目為何，在任何資料庫上都可以執行分頁還原。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份與還原可以跨所有支援的作業系統運作，不管它們是 64 位元還是 32 位元系統都一樣。 如需支援的作業系統資訊，請參閱[硬體和軟體需求，安裝 SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。 如需舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之備份支援的相關資訊，請參閱 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)的＜相容性支援＞一節。  
  
 **本主題內容：**  
  
-   [還原案例概觀](#RestoreScenariosOv)  
  
-   [復原模式及支援的還原作業](#RMsAndSupportedRestoreOps)  
  
-   [簡單復原模式下的還原限制](#RMsimpleScenarios)  
  
-   [大量記錄復原模式下的還原](#RMblogRestore)  
  
-   [Database Recovery Advisor (SQL Server Management Studio)](#DRA)  
  
-   [相關內容](#RelatedContent)  
  
##  <a name="RestoreScenariosOv"></a> 還原案例概觀  
 *中的* 「還原案例」 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Restore scenario) 是指先從一個或多個備份還原資料，再復原資料庫的程序。 支援的還原實例視資料庫的復原模式與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的版本而定。  
  
 下表介紹各種復原模式可能支援的還原實例。  
  
|中的|在簡單復原模式下|在完整/大量記錄復原模式下|  
|----------------------|---------------------------------|----------------------------------------------|  
|完整資料庫還原|這是基本還原策略。 完整資料庫還原可能只包括還原和復原完整資料庫備份。 此外，完整資料庫還原也可能包括還原完整資料庫備份，接著再還原和復原差異備份。<br /><br /> 如需詳細資訊，請參閱[完整資料庫還原 &#40;簡單復原模式&#41;](complete-database-restores-simple-recovery-model.md)。|這是基本還原策略。 完整的資料庫還原包括還原完整資料庫備份和選用的差異備份 (如果有的話)，然後依照順序還原所有後續的記錄備份。 復原最後一個記錄備份，並且加以還原 (RESTORE WITH RECOVERY)，即完成完整資料庫還原。<br /><br /> 如需詳細資訊，請參閱[完整資料庫還原 &#40;完整復原模式&#41;](complete-database-restores-full-recovery-model.md)。|  
|File restore **\***|還原一個或多個損毀的唯讀檔案，而不還原整個資料庫。 唯有當資料庫至少有一個唯讀檔案群組時，才能使用檔案還原。|還原一個或多個檔案，而不還原整個資料庫。 可以在資料庫離線時，或在資料庫仍在線上時 (適用於某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本) 執行檔案還原。 在檔案還原期間，包含正在還原中之檔案的檔案群組一律為離線狀態。|  
|分頁還原|不適用|還原一個或多個損毀的頁面。 可以在資料庫離線時，或在資料庫仍在線上時 (適用於某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本) 執行頁面還原。 在分頁還原期間，正在還原中的頁面一律為離線狀態。<br /><br /> 未中斷的記錄備份鏈結必須可用 (直到目前記錄檔)，而且它們必須全都套用，才能使分頁與目前記錄檔保持一樣新。<br /><br /> 如需詳細資訊，請參閱[還原頁面 &#40;SQL Server&#41;](restore-pages-sql-server.md)。|  
|分次還原 **\***|在檔案群組層級上，從主要檔案群組開始，接著是所有讀取/寫入次要檔案群組，分階段還原和復原資料庫。|從主要檔案群組開始，在檔案群組層級上分階段還原和復原資料庫。|  
  
 **\*** 只有 Enterprise 版才支援線上還原。  
  
 不論還原資料的方式如何，在復原資料庫之前， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 保證整個資料庫在邏輯上是一致的。 例如，如果您要還原檔案，除非您已經將其向前復原到足以和資料庫保持一致的程度，否則無法加以復原並使其回到線上。  
  
### <a name="advantages-of-a-file-or-page-restore"></a>檔案或分頁還原的優點  
 還原與復原檔案或頁面 (而非整個資料庫) 可提供下列優點：  
  
-   還原較少的資料，可縮短複製和復原資料所需的時間。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上，還原檔案或頁面可以讓資料庫中的其他資料在還原作業期間維持線上狀態。  
  
##  <a name="RMsAndSupportedRestoreOps"></a> 復原模式及支援的還原作業  
 資料庫可用的還原作業，取決於其復原模式。 下表摘要說明每一種復原模式是否支援給定的還原實例，及其支援的範圍。  
  
|還原作業|完整復原模式|大量記錄復原模式|簡單復原模式|  
|-----------------------|-------------------------|---------------------------------|---------------------------|  
|資料復原|完整復原 (如果有記錄可以使用)。|有損失部分資料的風險。|自上次完整或差異備份之後的任何資料，都會遺失。|  
|時間點還原|記錄備份涵蓋的任何時間。|如果記錄備份含有大量記錄變更，則不允許。|不支援。|  
|File restore **\***|完整支援。|有時。**\*\***|僅適用於唯讀的次要檔案。|  
|Page restore **\***|完整支援。|有時。**\*\***|無。|  
|分次 (檔案群組-等級) 還原 **\***|完整支援。|有時。**\*\***|僅適用於唯讀的次要檔案。|  
  
 **\*** 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 **\*\*** 如需了解必要條件，請參閱此主題稍後的 [簡單復原模式下的還原限制](#RMsimpleScenarios)。  
  
> [!IMPORTANT]  
>  不論資料庫的復原模式為何，比建立備份之版本還舊的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本，都無法還原 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份。  
  
##  <a name="RMsimpleScenarios"></a> 簡單復原模式下的還原案例  
 簡單復原模式在還原作業上具有下列限制：  
  
-   檔案還原及分次還原僅適用於唯讀的次要檔案群組。 如需有關這些資訊還原案例，請參閱[檔案還原 &#40;簡單復原模式&#41;](file-restores-simple-recovery-model.md) 和[分次還原 &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)。  
  
-   不允許分頁還原。  
  
-   不允許時間點還原。  
  
 如果這些限制中有任何一項不適合您的復原需要，即建議您考慮使用完整復原模式。 如需詳細資訊，請參閱 [備份概觀 &#40;SQL Server&#41;](backup-overview-sql-server.md)。  
  
> [!IMPORTANT]  
>  不論資料庫的復原模式為何，比建立備份之版本還舊的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本，都無法還原 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 備份。  
  
##  <a name="RMblogRestore"></a> 大量記錄復原模式下的還原  
 本節討論大量記錄復原模式的特殊還原考量，此為專門用做完整復原模式的補充。  
  
> [!NOTE]  
>  如需大量記錄復原模式的介紹，請參閱[交易記錄 &#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)。  
  
 一般而言，大量記錄復原模式與完整復原模式類似，針對完整復原模式所描述的資訊也同時適用於兩者。 但是，大量記錄復原模式會影響時間點復原與線上還原。  
  
### <a name="restrictions-for-point-in-time-recovery"></a>時間點復原的限制  
 如果大量記錄復原模式下建立的記錄備份包含大量記錄變更，就不允許時間點復原。 嘗試對包含大量變更的記錄備份執行時間點復原將會造成還原作業失敗。  
  
### <a name="restrictions-for-online-restore"></a>對線上還原的限制  
 線上還原順序只有在符合下列條件時才能運作：  
  
-   必須在開始還原順序之前完成所有必要的記錄備份。  
  
-   必須在開始線上還原順序之前先備份大量變更。  
  
-   如果資料庫中有大量變更存在，所有的檔案都必須在線上，或者是[無用](remove-defunct-filegroups-sql-server.md) (這表示它不再是資料庫的一部分)。  
  
 如果沒有符合這些條件，線上還原順序就會失敗。  
  
> [!NOTE]  
>  我們建議您先切換到完整復原模式，再開始線上還原。 如需詳細資訊，請參閱[復原模式 &#40;SQL Server &#41;](recovery-models-sql-server.md)。  
  
 如需有關如何執行線上還原的詳細資訊，請參閱[線上還原 &#40;SQL Server&#41;](online-restore-sql-server.md)。  
  
##  <a name="DRA"></a> Database Recovery Advisor (SQL Server Management Studio)  
 Database Recovery Advisor 有助於建構實作最佳化正確還原順序的還原計畫。 我們已經處理了客戶所要求的許多已知資料庫還原問題和增強功能。 Database Recovery Advisor 導入的主要增強功能包括：  
  
-   **還原計畫演算法：**  用來建構還原計畫的演算法已經大幅改善，特別是針對複雜的還原狀況。 相較於舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]而言，可更有效率地處理許多邊緣案例 (包括時間點還原的分岔案例)。  
  
-   **時間點還原：**  Database Recovery Advisor 大幅簡化資料庫還原到特定時間點的作業。 視覺備份時間表大幅增強時間點還原的支援。 這個視覺化時間表可讓您識別當做還原資料庫之目標復原點的可行時間點。 時間表可加快周遊分岔復原路徑 (跨多個復原分岔之路徑)。 特定時間點還原計畫會自動包含與還原至目標時間點 (日期和時間) 有關的備份。 如需詳細資訊，請參閱[將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)。  
  
 如需有關 Database Recovery Advisor 的詳細資訊，請參閱下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理能力部落格：  
  
-   [Recovery Advisor：簡介](http://blogs.msdn.com/b/managingsql/archive/2011/07/13/recovery-advisor-an-introduction.aspx)  
  
-   [Recovery Advisor：使用 SSMS 建立/還原分割備份](http://blogs.msdn.com/b/managingsql/archive/2011/07/13/recovery-advisor-using-ssms-to-create-restore-split-backups.aspx)  
  
##  <a name="RelatedContent"></a> 相關內容  
 無。  
  
## <a name="see-also"></a>另請參閱  
 [備份概觀 &#40;SQL Server&#41;](backup-overview-sql-server.md)  
  
  
