---
title: 升級資料庫引擎 | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], after upgrade
- Database Engine [SQL Server], upgrading
ms.assetid: 3c036813-36cf-4415-a0c9-248d0a433859
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 84f032e89730aa9828dada1208c6d794db97260b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62774966"
---
# <a name="upgrade-database-engine"></a>升級 Database Engine
  本主題提供了您在準備和了解升級程序時所需要的資訊，其中涵蓋：  
  
-   已知的升級問題。  
  
-   升級前的工作和考量。  
  
-   升級 [!INCLUDE[ssDE](../../includes/ssde-md.md)]之程序主題的連結。  
  
-   將資料庫移轉到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之程序主題的連結。  
  
-   容錯移轉叢集的考量。  
  
-   升級後的工作和考量。  
  
## <a name="known-upgrade-issues"></a>已知的升級問題  
 在升級 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 之前，請檢閱 [SQL Server Database Engine 回溯相容性](../sql-server-database-engine-backward-compatibility.md)。 如需所支援升級狀況和升級已知問題的相關資訊，請參閱[支援的版本與版本升級](supported-version-and-edition-upgrades.md)。 如需其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件的回溯相容性內容，請參閱[回溯相容性](../../getting-started/backward-compatibility.md)。  
  
> [!IMPORTANT]  
>  從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的一個版本升級到另一個版本之前，請確認您目前使用的功能在您想要升級後的版本中有受到支援。  
  
> [!NOTE]  
>  當您從舊版 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise Edition 升級至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，請選擇 [Enterprise Edition：核心授權] 或 [Enterprise Edition]。 這些 Enterprise Edition 只有在授權模式方面不同。 如需詳細資訊，請參閱 [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。  
  
## <a name="pre-upgrade-checklist"></a>升級前檢查清單  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式支援從舊版升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 您也可以從舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移轉資料庫。 您可以從一個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體移轉到同一部電腦的另一個執行個體，或是從另一部電腦的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體移轉。 移轉選項包括使用複製資料庫精靈、備份與還原功能、使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 匯入與匯出精靈，以及大量匯出/大量匯入方法。  
  
 在升級 [!INCLUDE[ssDE](../../includes/ssde-md.md)]之前，請檢閱下列文章：  
  
-   檢閱 [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。  
  
-   檢閱 [Check Parameters for the System Configuration Checker](check-parameters-for-the-system-configuration-checker.md)。  
  
-   檢閱 [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)。  
  
-   檢閱[支援的版本與版本升級](supported-version-and-edition-upgrades.md)。  
  
-   檢閱[使用 Upgrade Advisor 來準備升級](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)。  
  
-   檢閱[使用 Distributed Replay Utility 來準備升級](../../sql-server/install/use-the-distributed-replay-utility-to-prepare-for-upgrades.md)。  
  
-   檢閱 [SQL Server Database Engine 回溯相容性](../sql-server-database-engine-backward-compatibility.md)。  
  
-   檢閱[移轉查詢計劃](change-the-database-compatibility-mode-and-use-the-query-store.md)。  
  
 在您升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，請檢閱下列問題並進行變更：  
  
-   升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體時，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 編列在 MSX/TSX 關聯性中，請先升級目標伺服器，然後再升級主要伺服器。 如果您先升級主要伺服器，然後再升級目標伺服器， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 將無法連接至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的主要執行個體。  
  
-   從 64 位元版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級成 64 位元版本的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]時，您必須先升級 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，再升級 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
-   從要升級的執行個體備份所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫檔案，好讓您可以在必要時還原它們。  
  
-   對要升級的資料庫執行適當的 Database Console Commands (DBCC)，以確定它們處於一致狀態。  
  
-   除了使用者資料庫以外，也要評估升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件所需的磁碟空間。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件所需的磁碟空間，請參閱[安裝 SQL Server 2014 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。  
  
-   確定現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統資料庫 master、model、msdb 和 tempdb 都設定為自動成長，並確定它們有足夠的硬碟空間。  
  
-   確定所有資料庫伺服器在 master 資料庫中都有登入資訊。 這對於還原資料庫很重要，因為系統登入資訊是位於 master 中。  
  
-   停用所有啟動預存程序，因為升級程序將會在升級的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體上停止及啟動服務。 在啟動時處理的預存程序可能會封鎖升級程序。  
  
-   確認複寫為當前的複寫，然後將之停止。  
  
-   結束所有應用程式，包括具有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 相依性的所有服務。 如果本機應用程式連接到要升級的執行個體，則升級可能會失敗。  
  
-   如需詳細資訊，請參閱[在升級伺服器執行個體時將鏡像資料庫的停機時間減至最少](../database-mirroring/upgrading-mirrored-instances.md)。  
  
## <a name="upgrading-the-database-engine"></a>升級 Database Engine  
 您可以用版本升級覆寫 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更新版本的安裝。 如果在執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式時偵測到舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，所有舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 程式檔都會升級，但是會保留舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體中儲存的所有資料。 此外，舊版的《 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書》將原封不動地保留在電腦上。  
  
> [!WARNING]  
>  執行 SQL Server 2014 安裝程式時，SQL Server 執行個體會因為執行升級前檢查而停止並重新啟動。  
  
> [!CAUTION]  
>  當您升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，會覆寫先前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，所以它不再存在於電腦上。 升級之前，請備份 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫以及與先前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體相關聯的其他物件。  
  
 您可以使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 安裝精靈來升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
### <a name="database-compatibility-level-after-upgrade"></a>升級後的資料庫相容性層級  
 升級之後`tempdb`， `model`、 `msdb`和**資源**資料庫的相容性層級會設定為120。 `master` 系統資料庫會繼續保有升級前的相容性層級。  
  
 如果使用者資料庫的相容性層級在升級前為 100 或更高層級，則在升級後仍會保持相同。 如果升級前的相容性層級為 90，則在升級後的資料庫中，相容性層級會設定為 100 (這是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]所支援的最低相容性層級)。  
  
> [!NOTE]  
>  新的使用者資料庫會繼承 `model` 資料庫的相容性層級。  
  
## <a name="migrating-databases"></a>移轉資料庫  
 您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的備份和還原或是卸離和附加功能，將使用者資料庫移到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 如需詳細資訊，請參閱[使用備份與還原複製資料庫](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)或[資料庫卸離與附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)。  
  
> [!IMPORTANT]  
>  來源和目的地伺服器上具有相同名稱的資料庫將無法移動或複製。 在此情況下，會將它標示為「已存在」。  
  
 如需詳細資訊，請參閱 [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md)。  
  
## <a name="after-upgrading-the-database-engine"></a>升級 Database Engine 之後  
 在升級 [!INCLUDE[ssDE](../../includes/ssde-md.md)]之後，請完成下列工作：  
  
-   重新註冊伺服器。 如需註冊伺服器的詳細資訊，請參閱[註冊伺服器](../../ssms/register-servers/register-servers.md)。  
  
-   為確保查詢結果中語意的一致性，必須重新擴展全文檢索目錄。  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 會安裝新的斷詞工具，供全文索引與語意搜尋之用。 編製索引及查詢時皆可使用斷詞工具。 如不重建全文索引目錄，可能會造成搜尋結果不一致。 當您發出全文索引查詢，尋找在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 斷詞工具中與目前之斷詞工具中斷詞方式相異的片語，可能會無法擷取含有該片語的文件或資料列。 這是索引片語所使用的分解邏輯與查詢所用者不相同所致。 此方案會使用新的斷詞工具重新擴展 (重建) 全文索引目錄，讓索引與查詢時的行為一致。  
  
     如需詳細資訊，請參閱 [sp_fulltext_catalog &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql)。  
  
-   設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝。 為了減少系統的可攻擊介面區， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以選擇性地安裝和啟用主要服務和功能。  
  
-   驗證或移除 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 所產生及套用至分割區資料表和索引上之查詢的 USE PLAN 提示。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 改變了在分割區資料表和索引上處理查詢的方式。 在分割區物件上，針對 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 所產生之計畫使用 USE PLAN 提示的查詢包含了無法在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中使用的計畫。 我們建議您在升級到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]之後，使用以下程序。  
  
     **在查詢中直接指定 USE PLAN 提示時：**  
  
    1.  從查詢中移除 USE PLAN 提示。  
  
    2.  測試查詢。  
  
    3.  如果最佳化工具未選取適當的計畫，請微調查詢，然後考慮使用所要的查詢計劃指定 USE PLAN 提示。  
  
     **在計畫指南中指定 USE PLAN 提示時：**  
  
    1.  使用 sys.fn_validate_plan_guide 函數檢查計畫指南是否有效。 或者，您也可以使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]中的 Plan Guide Unsuccessful 事件來檢查是否有無效的計畫。  
  
    2.  如果此計畫指南無效，請捨棄此計畫指南。 如果最佳化工具未選取適當的計畫，請微調查詢，然後考慮使用所要的查詢計劃指定 USE PLAN 提示。  
  
     當計畫指南中指定了 USE PLAN 提示時，無效的計畫將不會造成查詢失敗。 而是會編譯此查詢，而不使用 USE PLAN 提示。  
  
 在升級之前標示為已啟用或已停用全文檢索的任何資料庫，都會在升級之後維持該狀態。 升級之後，會針對所有已啟用全文檢索的資料庫自動重建及擴展全文檢索目錄。 這是一項耗費時間和資源的作業。 您可以執行下列陳述式來暫停全文檢索索引作業：  
  
```  
EXEC sp_fulltext_service 'pause_indexing', 1;  
```  
  
 若要繼續全文檢索索引母體擴展，請執行下列陳述式：  
  
```  
EXEC sp_fulltext_service 'pause_indexing', 0;  
```  
  
## <a name="see-also"></a>另請參閱  
 [支援的版本與版本升級](supported-version-and-edition-upgrades.md)   
 [使用 SQL Server 的多個版本和實例](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)   
 [回溯相容性](../../getting-started/backward-compatibility.md)   
 [升級複寫的資料庫](upgrade-replicated-databases.md)  
  
  
