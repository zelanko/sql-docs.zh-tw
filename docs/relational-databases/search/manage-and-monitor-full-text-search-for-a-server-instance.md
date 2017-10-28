---
title: "管理及監視伺服器執行個體的全文檢索搜尋 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], about
- full-text search [SQL Server], server management
ms.assetid: 2733ed78-6d33-4bf9-94da-60c3141b87c8
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 657d78f548e8368ad2ff4c554fc6f731d7fb27fa
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="manage-and-monitor-full-text-search-for-a-server-instance"></a>管理及監視伺服器執行個體的全文檢索搜尋
  伺服器執行個體的全文檢索管理包括：  
  
-   系統管理工作，例如管理 FDHOST 啟動器服務 (MSSQLFDLauncher)、重新啟動篩選背景程式主機處理序 (如果您變更了服務帳戶認證的話)、設定整個伺服器的全文檢索屬性，以及備份全文檢索目錄。 舉例來說，您可以在伺服器層級中指定預設的全文檢索語言，以與整個伺服器執行個體的預設語言進行區隔。  
  
-   設定全文檢索語言元件 (斷詞工具和字幹分析器、同義字檔案，以及停用字詞和停用字詞表)。  
  
-   設定全文檢索搜尋的使用者資料庫。 這項作業包括針對資料庫建立一個或多個全文檢索目錄，以及針對您想要執行全文檢索查詢的每個資料表或索引檢視表定義全文檢索索引。  
  
##  <a name="props"></a> 檢視或變更全文檢索搜尋的伺服器屬性  
 您可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中檢視 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]執行個體的全文檢索屬性。  
  
#### <a name="to-view-and-change-server-properties-for-full-text-search"></a>檢視與變更全文檢索搜尋的伺服器屬性  
  
1.  在物件總管中，以滑鼠右鍵按一下伺服器，然後按一下 [屬性]。  
  
2.  在 [伺服器屬性] 對話方塊中，按一下 [進階] 頁面檢視全文檢索搜尋的相關伺服器資訊。 全文檢索屬性如下所示：  
  
    -   **預設全文檢索語言**  
  
         指定全文檢索索引資料行的預設語言。 全文檢索索引資料的語言分析相依於資料所用的語言。 這個選項的預設值是伺服器使用的語言。 如需所顯示設定的對應語言，請參閱 [sys.fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)。  
  
    -   **全文檢索升級選項**  
  
         這個伺服器屬性會控制將資料庫從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 升級到更新版本時，要如何移轉全文檢索索引。 這個屬性適用於以下方式的升級：附加資料庫、還原資料庫備份、還原檔案備份，或是使用複製資料庫精靈複製資料庫。  
  
         替代方案如下所示：  
  
         **匯入**  
         匯入全文檢索目錄。 一般而言，匯入的速度明顯比重建的速度更快。 例如，只有使用一個 CPU 時，匯入的執行速度大約比重建的速度快 10 倍。 不過，匯入的全文檢索目錄並不會使用 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]中導入的新增強化斷詞工具，所以您最後可能會想要重建全文檢索目錄。  
  
        > [!NOTE]  
        >  重建可以在多執行緒模式中執行，而且如果有 10 個以上的 CPU 可用，當您允許重建使用所有 CPU 時，重建的執行速度可能會比匯入的速度更快。  
  
         如果無法使用全文檢索目錄，將會重建關聯的全文檢索索引。 只有針對 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫才可以使用此選項。  
  
         **重建**  
         全文檢索目錄會使用新的增強斷詞工具重建。 重建索引可能要花一些時間，而且在升級之後可能需要相當多的 CPU 和記憶體。  
  
         **重設**  
         重設全文檢索目錄。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 全文檢索目錄檔案會遭到移除，但是全文檢索目錄和全文檢索索引的中繼資料則會保留。 在升級之後，所有的全文檢索索引都會停用變更追蹤，而且不會自動啟動搜耙。 當您在升級完成之後手動發出完整母體擴展之前，此目錄將會維持空白狀態。  
  
         如需選擇全文檢索升級選項的資訊，請參閱[升級全文檢索搜尋](../../relational-databases/search/upgrade-full-text-search.md)。  
  
        > [!NOTE]  
        >  也可以使用 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)**upgrade_option** 動作來設定全文檢索升級選項。  
  
##  <a name="metadata"></a> 檢視其他全文檢索伺服器屬性  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數可用來取得全文檢索搜尋之各種伺服器層級屬性的值。 這項資訊可用於管理和疑難排解全文檢索搜尋。  
  
 下表列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 伺服器執行個體的全文檢索屬性及其相關的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 函數。  
  
|屬性|描述|函數|  
|--------------|-----------------|--------------|  
|**IsFullTextInstalled**|全文檢索元件是否會與目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體一起安裝。|[FULLTEXTSERVICEPROPERTY](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)<br /><br /> [SERVERPROPERTY](../../t-sql/functions/serverproperty-transact-sql.md)|  
||||  
|**LoadOSResources**|作業系統斷詞工具和篩選是否已註冊並搭配這個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體使用。|FULLTEXTSERVICEPROPERTY|  
|**VerifySignature**|指定全文檢索引擎是否只載入已簽署的二進位檔。|FULLTEXTSERVICEPROPERTY|  
  
##  <a name="monitor"></a> 監視全文檢索搜尋活動  
 在伺服器執行個體上監視全文檢索搜尋活動時，許多動態管理檢視與函數相當有用。  
  
 **若要檢視有關包含進行中母體擴展活動之全文檢索目錄的資訊**  
  
-   [sys.dm_fts_active_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql.md)  
  
 **若要檢視篩選背景程式主機處理序的目前活動**  
  
-   [sys.dm_fts_fdhosts &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-fdhosts-transact-sql.md)  
  
 **若要檢視有關進行中索引母體擴展的資訊**  
  
-   [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
 **若要檢視在記憶體集區中當做搜耙或搜耙範圍一部分使用的記憶體緩衝區**  
  
-   [sys.dm_fts_memory_buffers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql.md)  
  
 **檢視可供全文檢索搜耙或全文檢索搜耙範圍之全文檢索收集程式元件使用的共用記憶體集區**  
  
-   [sys.dm_fts_memory_pools &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-memory-pools-transact-sql.md)  
  
 **檢視有關每個全文檢索索引批次的資訊**  
  
-   [sys.dm_fts_outstanding_batches &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-outstanding-batches-transact-sql.md)  
  
 **檢視有關與進行中母體擴展相關之特定範圍的資訊**  
  
-   [sys.dm_fts_population_ranges &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-population-ranges-transact-sql.md)  
  
  

