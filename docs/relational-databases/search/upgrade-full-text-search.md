---
description: 升級全文檢索搜尋
title: 升級全文檢索搜尋 | Microsoft 文件
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], installing
- migrating full-text indexes [SQL Server]
- upgrading Full-Text Search
- installing Full-Text Search
- full-text search [SQL Server], upgrading
ms.assetid: 2fee4691-f2b5-472f-8ccc-fa625b654520
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4759838a20e721031db8e4ea5e644cc3822285a8
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868942"
---
# <a name="upgrade-full-text-search"></a>升級全文檢索搜尋
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  將全文檢索搜尋升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的作業會在安裝期間完成，而且當您使用 [複製資料庫精靈] 以附加、還原或複製舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料庫檔案和全文檢索目錄時，也會完成此作業。  
  
  
##  <a name="upgrade-a-server-instance"></a><a name="Upgrade_Server"></a> 升級伺服器執行個體  
 進行就地升級時， [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的執行個體會與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]並存安裝，而資料會進行移轉。 如果舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已安裝全文檢索搜尋，系統就會自動安裝新版全文檢索搜尋。 並存安裝表示下列各個元件可存在於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體層級。  
  
 斷詞工具、字幹分析器和篩選  
 各個執行個體現在會使用自己的斷詞工具、字幹分析器和篩選集，而不再使用這些元件的作業系統版本。 您還能在個別執行個體層級中，輕易地註冊和設定這些元件。 如需詳細資訊，請參閱 [設定及管理搜尋的斷詞工具與字幹分析器](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md) 和 [設定及管理搜尋的篩選](../../relational-databases/search/configure-and-manage-filters-for-search.md)。  
  
 篩選背景程式主機  
 全文檢索篩選背景程式主機處理序可安全無虞地載入並驅動用於索引和查詢的擴充外部元件，例如斷詞工具、字幹分析器和篩選，而無損全文檢索引擎的完整性。 伺服器執行個體會針對所有多執行緒篩選使用多執行緒處理序，而針對所有單一執行緒篩選使用單一執行緒處理序。  
  
> [!NOTE]  
>  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 針對 FDHOST 啟動器服務 (MSSQLFDLauncher) 導入了服務帳戶。 這個服務會將服務帳戶資訊傳播至特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的篩選背景程式主機處理序。 如需設定服務帳戶的相關資訊，請參閱 [設定全文檢索篩選背景程式啟動器的服務帳戶](../../relational-databases/search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)。  
  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中，每個全文檢索索引都位於屬於檔案群組、具有實體路徑而且被視為資料庫檔案的全文檢索目錄中。 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本中，全文檢索目錄是包含一組全文檢索索引的邏輯或虛擬物件。 因此，新的全文檢索目錄不會被視為具有實體路徑的資料庫檔案。 不過，在升級含有資料檔案的任何全文檢索目錄期間，系統會在相同的磁碟上建立新的檔案群組。 這會在升級之後保留舊磁碟 I/O 行為。 如果根路徑存在，則任何來自該目錄的全文檢索索引都會放置於新的檔案群組中。 如果舊的全文檢索目錄路徑無效，升級作業就會將全文檢索索引保留在與基底資料表相同的檔案群組中，或是保留在分割區資料表的主要檔案群組中。  
  
  
##  <a name="full-text-upgrade-options"></a><a name="FT_Upgrade_Options"></a> 全文檢索升級選項  
 將伺服器執行個體升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]時，使用者介面可讓您選擇下列其中一個全文檢索升級選項。  
  
**匯入**  
 匯入全文檢索目錄。 一般而言，匯入的速度明顯比重建的速度更快。 例如，只有使用一個 CPU 時，匯入的執行速度大約比重建的速度快 10 倍。 不過，匯入的全文檢索目錄並不會使用與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]最新版本一起安裝的新斷詞工具。 為確保查詢結果的一致性，必須重建全文檢索目錄。  
  
> [!NOTE]  
>  重建可以在多執行緒模式中執行，而且如果有 10 個以上的 CPU 可用，當您允許重建使用所有 CPU 時，重建的執行速度可能會比匯入的速度更快。  
  
 如果無法使用全文檢索目錄，將會重建關聯的全文檢索索引。 只有針對 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫才可以使用此選項。  
  
 如需有關匯入全文檢索索引之影響的詳細資訊，請參閱本主題後面的「選擇全文檢索升級選項的考量」。  
  
 **重建**  
 全文檢索目錄會使用新的增強斷詞工具重建。 重建索引可能需要一些時間，而且在升級之後可能需要相當多的 CPU 和記憶體。  
  
 **重設**  
 重設全文檢索目錄。 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]進行升級時，全文檢索目錄檔案會遭到移除，但是全文檢索目錄和全文檢索索引的中繼資料則會保留。 在升級之後，所有的全文檢索索引都會停用變更追蹤，而且不會自動啟動搜耙。 當您在升級完成之後手動發出完整母體擴展之前，此目錄將會維持空白狀態。  
  
##  <a name="considerations-for-choosing-a-full-text-upgrade-option"></a><a name="Choosing_Upgade_Option"></a> 選擇全文檢索升級選項的考量  
 當您為升級作業選擇升級選項時，請考慮下列事項：  
  
-   您需要查詢結果中的一致性嗎？  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 會安裝新的斷詞工具，供全文索引與語意搜尋之用。 編製索引及查詢時皆可使用斷詞工具。 如不重建全文索引目錄，可能會造成搜尋結果不一致。 當您發出全文索引查詢，尋找在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 斷詞工具中與目前之斷詞工具中斷詞方式相異的片語，可能會無法擷取含有該片語的文件或資料列。 這是索引片語所使用的分解邏輯與查詢所用者不相同所致。 此方案會使用新的斷詞工具重新擴展 (重建) 全文索引目錄，讓索引與查詢時的行為一致。 您可以選擇 [重建] 選項以完成這個作業，也可以在選擇 [匯入] 選項之後手動重建。  
  
-   是否有任何全文檢索索引建立在整數全文檢索索引鍵資料行上？  
  
     重建會執行內部最佳化，以便在某些情況中改善已升級之全文檢索索引的查詢效能。 具體而言，如果您擁有包含全文檢索索引的全文檢索目錄，其中基底資料表的全文檢索索引鍵資料行是整數資料類型，則重建會在升級之後達到理想的全文檢索查詢效能。 在此情況中，我們強烈建議您使用 **[重建]** 選項。  
  
    > [!NOTE]  
    >  若為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中的全文檢索索引，我們建議當做全文檢索索引鍵的資料行必須是整數資料類型。 如需詳細資訊，請參閱 [改善全文檢索索引的效能](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)。  
  
-   將伺服器執行個體保持在線上狀態的優先權為何？  
  
     在升級期間匯入或重建會耗用大量 CPU 資源，因而延遲將其餘伺服器執行個體升級並保持在線上狀態的時間。 如果盡可能將伺服器執行個體保持在線上狀態很重要，而且您願意在升級之後執行手動母體擴展，則適合使用 **[重設]** 。  
  
## <a name="ensure-consistent-query-results-after-importing-a-full-text-index"></a>確保匯入全文檢索索引之後的查詢結果一致性  
 新舊斷詞工具的行為稍微不同，因此如果已在將 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]時匯入全文檢索目錄，則查詢與全文檢索索引內容之間可能會不相符。 在此情況中，若要確保查詢與全文檢索索引內容之間完全相符，請選擇下列其中一個選項：  
  
-   重建包含全文檢索索引的全文檢索目錄 ([ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)*catalog_name* REBUILD)  
  
-   針對全文檢索索引發出 FULL POPULATION ([ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) ON *table_name* START FULL POPULATION)。  
  
 如需斷詞工具的詳細資訊，請參閱 [設定及管理搜尋的斷詞工具與字幹分析器](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)。  
  
## <a name="upgrade-noise-word-files-to-stoplists"></a>將非搜尋字檔案升級為停用字詞表  
當資料庫從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 升級為 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]時，便不再使用非搜尋字檔案。 不過，這些舊的非搜尋字檔案會儲存在 FTDATA\ FTNoiseThesaurusBak 資料夾中，而且您之後可以在更新或建立對應的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 停用字詞表時使用它們。  
  
 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]升級之後：  
  
-   如果您從未在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的安裝中新增、修改或刪除任何非搜尋字檔案，則系統停用字詞表應該能符合您的需求。  
  
-   如果曾在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中修改過非搜尋字檔案，則這些修改會在升級時遺失。 若要重新建立這些更新，您必須在對應的 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 停用字詞表中以手動方式重新建立這些修改。 如需詳細資訊，請參閱 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)。  
  
-   如果不想將任何停用字詞套用至全文檢索索引 (例如，如果刪除或清除了 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 安裝中的非搜尋字檔案)，則必須針對每個已升級的全文檢索索引關閉停用字詞表。 執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式 (以升級後資料庫的名稱取代 *database* ，並以 *table* 的名稱取代 *table*)：  
  
    ```  
    Use database;   
    ALTER FULLTEXT INDEX ON table  
       SET STOPLIST OFF;  
    GO  
    ```  
  
     STOPLIST OFF 子句會移除停用字詞篩選，而且它將會觸發資料表的母體擴展，但不會篩選任何視為非搜尋字的字詞。  
  
## <a name="backup-and-imported-full-text-catalogs"></a>備份與匯入的全文檢索目錄  
 對於升級期間重建或重設的全文檢索目錄 (以及新的全文檢索目錄) 而言，此全文檢索目錄是邏輯概念，而且不會位於檔案群組中。 因此，若要備份 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中的全文檢索目錄，您必須識別包含此目錄之全文檢索索引的每個檔案群組，然後逐一備份它們。 如需詳細資訊，請參閱 [備份並還原全文檢索目錄與索引](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)。  
  
 對於已經從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]匯入的全文檢索目錄而言，此全文檢索目錄仍然是位於其檔案群組中的資料庫檔案。 全文檢索目錄的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 備份程序仍然適用，但是 MSFTESQL 服務不存在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中。 如需 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 程序的相關資訊，請參閱《SQL Server 2005 線上叢書》中的 [備份與還原全文檢索目錄](/previous-versions/sql/sql-server-2005/ms142511(v=sql.90)) 。  
  
##  <a name="migrating-full-text-indexes-when-upgrading-a-database-to-sscurrent"></a><a name="Upgrade_Db"></a> 升級資料庫時移轉全文檢索索引 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 您可以使用附加、還原或 [複製資料庫精靈]，將舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料庫檔案和全文檢索目錄升級為現有的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 伺服器執行個體。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 系統會匯入、重設或重建全文檢索索引 (如果有的話)。 **upgrade_option** 伺服器屬性會控制此伺服器執行個體在這些資料庫升級期間所使用的全文檢索升級選項。  
  
 當您將任何 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫附加、還原或複製到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]時，該資料庫會立即可用，然後自動升級。 根據進行索引的資料數量而定，匯入可能需要數個小時，而重建可能需要十倍以上的時間。 此外，請注意，當升級選項設定為 [匯入] 時，如果全文檢索目錄無法使用，系統就會重建相關聯的全文檢索索引。  
  
 **變更伺服器執行個體的全文檢索升級行為**  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)]:使用 [sp\_fulltext\_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md) 的 **upgrade\_option** 動作  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **：** 使用 [伺服器屬性]**** 對話方塊的 [全文檢索升級選項]****。 如需詳細資訊，請參閱 [管理及監視伺服器執行個體的全文檢索搜尋](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)。  
  
##  <a name="considerations-for-restoring-a-ssversion2005-full-text-catalog-to-sscurrent"></a><a name="Considerations_for_Restore"></a> 還原 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 全文檢索目錄的考量 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 將全文檢索資料從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的其中一種方法是將完整資料庫備份還原至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 匯入 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 全文檢索目錄時，您可以備份和還原資料庫與目錄檔案。 此行為與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的行為相同：  
  
-   完整資料庫備份將會包含全文檢索目錄。 若要參考全文檢索目錄，請使用其 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 檔案名稱：sysft_+*catalog-name*。  
  
-   如果全文檢索目錄處於離線狀態，備份將會失敗。  
  
 如需備份和還原 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 全文檢索目錄的詳細資訊，請參閱《 [線上叢書》中的](./back-up-and-restore-full-text-catalogs-and-indexes.md) 備份與還原全文檢索目錄 [和](/previous-versions/sql/sql-server-2008-r2/ms190643(v=sql.105))檔案備份、還原及全文檢索目錄 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中還原資料庫時，系統會針對此全文檢索目錄建立新的資料庫檔案。 這個檔案的預設名稱為 ftrow_*catalog-name*.ndf。 例如，如果您的 *catalog-name* 是 `cat1`， [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 資料庫檔案的預設名稱會是 `ftrow_cat1.ndf`。 但是，如果預設名稱已經用於目標目錄中，新的資料庫檔案就會命名為 `ftrow_`*catalog-name*`{`*GUID*`}.ndf`，其中 *GUID* 是新檔案的全域唯一識別碼。  
  
 匯入目錄之後，會更新 **sys.database_files** 和 **sys.master_files**以移除目錄項目，而且 **sys.fulltext_catalogs** 中的 **path** 資料行會設成 NULL。  
  
 **備份資料庫**  
  
-   [完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)  
  
-   [交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md) (僅限完整復原模式)  
  
 **還原資料庫備份**  
  
-   [完整資料庫還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
  
-   [完整資料庫還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)  
  
### <a name="example"></a>範例  
 下列範例會在 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 陳述式中使用 MOVE 子句來還原名為 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 的 `ftdb1`資料庫。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫、記錄和目錄檔案都會移至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 伺服器執行個體上的新位置，如下所示：  
  
-   資料庫檔案 `ftdb1.mdf`會移至 `C:\Program Files\Microsoft SQL Server\MSSQL.1MSSQL13.MSSQLSERVER\MSSQL\DATA\ftdb1.mdf`。  
  
-   記錄檔 `ftdb1_log.ldf`會移至記錄磁碟機上的記錄目錄： *log_drive*`:\`*log_directory*`\ftdb1_log.ldf`。  
  
-   對應至 `sysft_cat90` 目錄的目錄檔案會移至 `C:\temp`。 匯入全文檢索索引之後，它們會自動放置於資料庫檔案 C:\ftrow_sysft_cat90.ndf 中，而且系統會刪除 C:\temp。  
  
```  
RESTORE DATABASE [ftdb1] FROM  DISK = N'C:\temp\ftdb1.bak' WITH  FILE = 1,  
   MOVE N'ftdb1' TO N'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA\ftdb1.mdf',  
    MOVE N'ftdb1_log' TO N'log_drive:\log_directory\ftdb1_log.ldf',  
    MOVE N'sysft_cat90' TO N'C:\temp';  
```  
  
##  <a name="attaching-a-sql-server-2005-database-to-sscurrent"></a><a name="Attaching_2005_ft_catalogs"></a> 附加 SQL Server 2005 資料庫 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 和更新版本中，全文檢索目錄是參考一組全文檢索索引的邏輯概念。 全文檢索目錄是不屬於任何檔案群組的虛擬物件。 不過，當您將包含全文檢索目錄檔案的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫附加至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 伺服器執行個體時，系統就會從先前的位置附加這些目錄檔案以及其他資料庫檔案，此行為與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的行為相同。  
  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 上，每個所附加之全文檢索目錄的狀態都與從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]中卸離資料庫時的狀態相同。 如果卸離作業暫停了任何全文檢索索引母體擴展，就會在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]上繼續進行母體擴展，而且全文檢索索引會變成可用於全文檢索搜尋。  
  
 如果 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 找不到全文檢索目錄檔案，或者在附加作業期間移動了全文檢索檔案，但沒有指定新的位置，此行為就會取決於選取的全文檢索升級選項。 如果全文檢索升級選項是 [匯入]**** 或 [重建]****，系統就會重建附加的全文檢索目錄。 如果全文檢索升級選項是 [重設]****，系統就會重設附加的全文檢索目錄。  
  
 如需卸離和附加資料庫的詳細資訊，請參閱[資料庫卸離和附加 &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)、[CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md)、[sp_attach_db](../../relational-databases/system-stored-procedures/sp-attach-db-transact-sql.md) 和 [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
 [全文檢索搜尋使用者入門](../../relational-databases/search/get-started-with-full-text-search.md)   
 [設定及管理搜尋的斷詞工具與字幹分析器](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md)   
 [設定及管理搜尋的篩選](../../relational-databases/search/configure-and-manage-filters-for-search.md)  
  
