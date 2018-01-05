---
title: "追蹤旗標 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 12/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- trace flags [SQL Server], about trace flags
- trace flags [SQL Server]
- global trace flags [SQL Server]
- flags [SQL Server]
- session trace flags [SQL Server]
- performance [SQL Server], trace
- debugging [SQL Server], trace flags
ms.assetid: b971b540-1ac2-435b-b191-24399eb88265
caps.latest.revision: "171"
author: pmasl
ms.author: pelopes
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: d5c466e35f8e37d7f2559e6766886b5ef80e390e
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/05/2018
---
# <a name="dbcc-traceon---trace-flags-transact-sql"></a>DBCC TRACEON-追蹤旗標 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

追蹤旗標用來暫時設定特定伺服器性質，或關閉特定行為。 例如，如果在啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，設定追蹤旗標 3205，就會停用磁帶機的硬體壓縮。 追蹤旗標經常用來診斷效能問題，或偵錯預存程序或複雜電腦系統。
  
下表列出並描述 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中可用的追蹤旗標。
 
> [!NOTE]
> 某些追蹤旗標已導入特定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本。 如需有關適當版本的詳細資訊，請參閱特定的追蹤旗標與相關聯的 Microsoft 支援文章。

> [!IMPORTANT]
> 在未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本中，不一定支援追蹤旗標行為。 

  
|追蹤旗標|描述|  
|---|---|
|**139**| 正確的 DBCC 範圍中的轉換語意檢查命令要強制[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)， [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)和[DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md)分析時，改進的精確度和轉換邏輯所導入的相容性等級 130 的特定資料類型上有較低的相容性層級的資料庫。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/help/4010261)。<br /><br />**注意：**這個追蹤旗標適用於[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]RTM CU3， [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 和更新版本的組建。<br /><br />**警告：**追蹤旗標 139 並非用於生產環境中，在持續啟用，應該用於只是為了在執行資料庫驗證會檢查所述[Microsoft 支援文章](http://support.microsoft.com/help/4010261). 它應該立即停用完成驗證檢查。<br /><br />**範圍**： 全域只|
|**174**|增加[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]計畫快取 bucket 計數從 40,009 160,001 至 64 位元系統上。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/3026083)。<br /><br />**注意：**請確定您仔細地測試此選項，然後再部署到生產環境。<br /><br />**範圍**： 全域只|
|**176**|重建資料表，其中包含計算資料分割資料行的分割線上時，可讓以解決錯誤修正。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/3213683)。<br /><br />**範圍**： 全域或工作階段|
|**205**|報告錯誤記錄檔的統計資料相關的預存程序可能是正在重新編譯時自動更新統計資料。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/195565)。<br /><br />**範圍**： 全域只|
|**260**|列印擴充預存程序動態連結程式庫 (DLL) 的版本控制相關資訊。 如需有關**GetXpVersion()**，請參閱[建立擴充預存程序](../../relational-databases/extended-stored-procedures-programming/creating-extended-stored-procedures.md)。<br /><br />**範圍：**全域或工作階段|
|**272**|停用識別預先配置，以避免意外重新啟動伺服器或容錯移轉至次要伺服器識別資料行值的間距。 請注意，身分識別快取用來改善插入具有識別資料行的資料表上的效能。<br /><br />**注意：**開頭[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]，若要完成這項作業在資料庫層級，請參閱中的 IDENTITY_CACHE 選項[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).<br /><br />**範圍**： 全域只|
|**610**|控制項使用最低限度記錄插入至索引的資料表。 這個追蹤旗標不需要啟動 SQL Server 2016，如索引資料表的預設會開啟最低限度記錄。 在 SQL Server 2016 中，當大量載入作業會導致新的頁面配置，所有資料列依序填滿，新的頁面是最低限度記錄如果符合所有其他先決條件進行最低限度記錄。 插入現有的頁面 （沒有新的頁面配置），來維護索引順序中的資料列都仍是完整記錄，因為移動的資料列較頁面分割期間負載。 它也是一定要有 ALLOW_PAGE_LOCKS 開啟的最低限度記錄作業 （這是預設的 ON） 索引工作頁面鎖定期間配置，藉此只頁面或記錄範圍配置。如需詳細資訊，請參閱[資料載入效能指南](https://msdn.microsoft.com/library/dd425070.aspx)。<br /><br />**範圍**： 全域或工作階段|
|**634**|停用背景資料行存放區壓縮工作。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會定期執行 Tuple Mover 背景工作可壓縮與解壓縮資料，一次一個資料列群組的資料行存放區索引資料列群組。<br /><br />壓縮資料行存放區可提升查詢效能，但同時也會耗用系統資源。 您仍然可以在手動控制資料行存放區壓縮的時機，請停用背景壓縮工作，以追蹤旗標為 634，然後明確地叫用 ALTER INDEX...重新組織或 ALTER INDEX...在您選擇的階段重建。<br /><br />**範圍：**全域只|
|**652**|停用頁面預先提取掃描。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/920093)。<br /><br />**範圍**： 全域或工作階段|
|**661**|準刪除記錄的移除程序會停用。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/920093)。<br /><br />**範圍**： 全域只|
|**692**|停用快速插入大量資料載入堆積或叢集的索引時。 啟動[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，利用最低限度記錄，資料庫處於簡單或大量記錄的復原模式，來最佳化記錄插入至新頁面插入效能時的預設會啟用快速的插入。 快速插入，每個大量載入批次會擷取新 extent(s) 略過具有可用空間，以將插入的效能最佳化的現有範圍配置查閱。<br /><br /> 快速插入，大量載入小批次大小可能會導致增加物件因此最好是使用每個批次大 batchsize 完全填滿範圍所耗用的未使用空間。 如果增加 batchsize 不可行，這個 traceflag，有助於減少未使用的空間保留，但會犧牲效能。 <br /><br />**注意：**這個追蹤旗標適用於[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]RTM 和更高版本的組建。<br /><br />**範圍**： 全域或工作階段|
|**715**|可讓具有非叢集索引的堆積內的大量載入作業的資料表鎖定。 當啟用這個追蹤旗標時，大量載入作業會取得大量複製資料到資料表時，大量更新 (BU) 鎖定。 大量更新 (BU) 鎖定允許多個執行緒將資料同時大量載入到相同資料表中，同時防止未大量載入資料存取資料表的其他處理序。<br /><br />此行為是類似當使用者明確地指定 TABLOCK 提示時執行大量載入，或當 sp_tableoption 資料表鎖定大量載入指定的資料表已啟用。 不過，當啟用這個追蹤旗標時，這個行為會變得不需要變更任何查詢或資料庫的預設值。<br /><br />**範圍：**全域或工作階段|
|**834**|使用 Microsoft Windows 大型分頁配置之緩衝集區。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/3210239)。<br /><br />**注意：**如果您使用的資料行存放區索引功能[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]至[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，我們不建議開啟追蹤旗標 834。<br /><br />**範圍**： 全域只|
|**845**|啟用鎖定頁面的標準 Sku 上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時的服務帳戶、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]具有鎖定頁面中啟用記憶體特殊權限。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/970070)和文件頁面上的[伺服器記憶體伺服器組態選項](../../database-engine/configure-windows/server-memory-server-configuration-options.md#lock-pages-in-memory-lpim)。<br /><br />**注意：**開頭[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]預設會啟用此行為的標準 Sku 和追蹤旗標 845 不可用。<br /><br />**範圍**： 全域只|
|**902**|安裝累計更新或 Service Pack 時，會略過執行資料庫升級指令碼。 如果您在指令碼升級模式時發生錯誤，建議的進一步指引，請連絡 Microsoft SQL 客戶服務及支援 (CSS)。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/2163980)。<br /><br />**警告：**這個追蹤旗標用來在指令碼升級模式下，疑難排解失敗的更新並不支援在生產環境中連續執行。 資料庫升級指令碼順利執行完整安裝累計更新和 Service Pack 的需求。 不這樣可能會導致未預期的問題與您[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。<br /><br />**範圍**： 全域只|
|**1117**|檔案群組中的檔案已到達的自動成長臨界值時的檔案群組中的所有檔案會都成長。<br /><br />**注意：**開頭[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]這種行為由 ALTER DATABASE 的 AUTOGROW_SINGLE_FILE 和 AUTOGROW_ALL_FILES 選項和追蹤旗標 1117年沒有任何作用。 如需詳細資訊，請參閱[ALTER DATABASE 檔案及檔案群組選項 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md).<br /><br />**範圍：**全域只|
|**1118**|移除伺服器上大部分的單一頁面配置，以減少 SGAM 頁面的競爭情況。 建立新的物件時，根據預設前, 八個分頁被配置不同的範圍 （混合範圍）。 之後若需要更多頁面時，將會從相同的範圍 (統一範圍) 加以配置。 SGAM 頁面可用以追蹤這些混合範圍，因此若出現多個混合頁面配置，它會很快地成為瓶頸。 這個追蹤旗標會在建立新物件時，從相同的範圍配置所有八個頁面，進而將掃描 SGAM 頁面的需求降到最低。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/328551)。<br /><br />**注意：**開頭[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]這種行為由 ALTER DATABASE 的 SET MIXED_PAGE_ALLOCATION 選項和追蹤旗標 1118年沒有任何作用。 如需詳細資訊，請參閱 [ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)。<br /><br />**範圍：**全域只|  
|**1204**|傳回參與死結之鎖定的資源和類型，以及目前受影響的命令。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/832524)。<br /><br />**範圍：**全域只|  
|**1211**|停用以記憶體壓力或鎖定個數為基礎的鎖定擴大。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 不會將資料列或頁面鎖定擴大到資料表鎖定。<br /><br />使用這個追蹤旗標可能產生大量鎖定。 這可能會降低 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的效能，或因記憶體不足而造成 1204 錯誤 (無法配置鎖定資源)。<br /><br />如果同時設定了追蹤旗標 1211 和 1224，將會優先採用 1211。 但是，由於追蹤旗標 1211 會在每一個情況下防止鎖定擴大 (即使是在記憶體壓力下)，所以建議您最好使用 1224。 如此可避免在使用許多鎖定時，發生「鎖定不足」錯誤。<br /><br />**範圍**： 全域或工作階段|  
|**1222**|以不符合任何 XSD 結構描述的 XML 格式來傳回參與死結之鎖定的資源和類型，以及目前受影響的命令。<br /><br />**範圍**： 全域只|  
|**1224**|停用以鎖定個數為基礎的鎖定擴大。 不過，記憶體壓力仍然可以啟動鎖定擴大。 如果鎖定物件使用的記憶體數量超出下列其中一個條件，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 就會將資料列或頁面鎖定擴大至資料表 (或資料分割) 鎖定：<br /><br />-使用的記憶體 40% [!INCLUDE[ssDE](../../includes/ssde-md.md)]。 這是時才適用**鎖定**sp_configure 參數設為 0。<br />的使用所設定的鎖定記憶體 40%**鎖定**sp_configure 的參數。 如需詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)伺服器組態選項。<br /><br />如果同時設定了追蹤旗標 1211 和 1224，將會優先採用 1211。 但是，由於追蹤旗標 1211 會在每一個情況下防止鎖定擴大 (即使是在記憶體壓力下)，所以建議您最好使用 1224。 如此可避免在使用許多鎖定時，發生「鎖定不足」錯誤。<br /><br />**注意：**也可以使用的 LOCK_ESCALATION 選項控制鎖定擴大到 HoBT 層級的資料粒度或資料表層級[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)陳述式。<br /><br />**範圍：**全域或工作階段|
|**1236**|可讓資料庫鎖定資料分割。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/2926217)。<br /><br />**注意：**開頭[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]SP3 和[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]這種行為由引擎和追蹤旗標 1236 SP1 有任何作用。<br /><br />**範圍**： 全域只|
|**1237**|允許 ALTER PARTITION FUNCTION 陳述式來接受目前的使用者定義的工作階段的死結優先權，而不是預設情況下可能的死結的犧牲者。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/help/4025261)。<br /><br />**注意：**開頭[!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)]和資料庫[相容性層級](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)140 這是預設行為，所以追蹤旗標 1237年沒有任何作用。<br /><br />**範圍**： 全域或工作階段或查詢|
|**1260**|停用排程器監視器傾印。<br /><br />**範圍**： 全域只|   
|**1448**|讓複寫記錄讀取器向前移動，即使非同步次要尚未認可收到變更也一樣。 即使這個追蹤旗標已啟用，記錄讀取器一定會等候同步次要。 記錄讀取器不會超過同步次要的最小認可。 這個追蹤旗標會套用至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，而不只可用性群組、可用性資料庫或記錄讀取器執行個體。 立即生效，不必重新啟動。 您可以事先或在非同步次要失敗時啟動這個追蹤旗標。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/937041)。<br /><br />**範圍**： 全域只|   
|**1462**|停用記錄非同步可用性群組的資料流壓縮。 非同步的可用性群組的預設會啟用這項功能，以最佳化網路頻寬。 如需詳細資訊，請參閱 [微調可用性群組的壓縮](../../database-engine/availability-groups/windows/tune-compression-for-availability-group.md)。<br /><br />**範圍**： 全域只| 
|**1800**|可讓[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]最佳化中針對主要與次要複本記錄檔，使用不同的磁區大小的磁碟時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Always On 和記錄傳送的環境。 這個追蹤旗標時才需要在 SQL Server 執行個體上啟用與交易記錄檔位於磁區大小為 512 個位元組的磁碟上。 它是**不**才能包含 4 k 磁區大小的磁碟上啟用。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/3009974)。<br /><br />**範圍：**全域只|
|**2301**|啟用進階的決策支援最佳化。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/920093)。<br /><br />**範圍**： 全域和工作階段和查詢|
|**2312**|可讓您將查詢最佳化工具基數估計模型設定為[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版本而定，資料庫的相容性層級。 如需詳細資訊，請參閱[Microsoft 支援文章](http://support.microsoft.com/kb/2801413)。<br /><br />從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1，才能完成這項作業在查詢層級中，加入 USE 提示 'FORCE_DEFAULT_CARDINALITY_ESTIMATION'[查詢提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用這個追蹤旗標。<br /><br />**範圍**： 全域或工作階段或查詢| 
|**2335**|會導致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]假設在查詢最佳化期間是使用固定的記憶體數量。 它不會限制記憶體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]授與執行查詢。 設定的記憶體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]仍然會依資料快取、 執行查詢和其他取用者使用。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/2413549)。<br /><br />**注意：**請確定您仔細地測試此選項，然後再部署到生產環境。<br /><br />**範圍**： 全域或工作階段或查詢|
|**2340**|會導致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不想使用排序作業 （批次排序） 時產生計劃，最佳化巢狀的迴圈聯結。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/2009160)。<br /><br />從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1，才能完成這項作業在查詢層級中，加入 USE 提示 'DISABLE_OPTIMIZED_NESTED_LOOP'[查詢提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用這個追蹤旗標。<br /><br />**注意：**請確定您仔細地測試此選項，然後再部署到生產環境。<br /><br />**範圍**： 全域或工作階段或查詢|
|**2371**|將固定的自動更新統計資料閾值變更為動態的自動更新統計資料的臨界值。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/2754171)。<br /><br />**注意：**開頭[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]下方和 [資料庫相容性層級](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)130，此行為由引擎所控制，追蹤旗標 2371年沒有作用。<br /><br />**範圍**： 全域只|
|**2389**|啟用自動產生遞增索引鍵 （長條圖修正） 快速統計的資料。 如果設定追蹤旗標 2389年，前端統計資料資料行標示為遞增，將會在查詢編譯時間調整用來預估基數的長條圖。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/2801413)。<br /><br />**注意：**請確定您仔細地測試此選項，然後再部署到生產環境。<br /><br />**注意：** CE 120 版或更新將不會套用這個追蹤旗標。 請改用追蹤旗標 4139。<br /><br />**範圍**： 全域或工作階段或查詢|
|**2390**|啟用自動產生的快速統計資料，以遞增或未知的機碼 （長條圖修正）。 如果設定追蹤旗標 2390年，前端統計資料資料行標示為遞增或不明，將會在查詢編譯時間調整用來預估基數的長條圖。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/2801413)。<br /><br />**注意：**請確定您仔細地測試此選項，然後再部署到生產環境。<br /><br />**注意：** CE 120 版或更新將不會套用這個追蹤旗標。 請改用追蹤旗標 4139。<br /><br />**範圍**： 全域或工作階段或查詢|
|**2422**|可讓[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]中止要求時已經超過設定資源管理員 request_max_cpu_time_sec 所設定的最大時間。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/help/4038419)。<br /><br />**注意：**這個追蹤旗標適用於[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3 和更高版本的組建。<br /><br />**範圍**： 通用|
|**2430**|可讓其他鎖定類別清除。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/2754301)。<br /><br />**範圍**： 全域只| 
|**2453**|可讓資料表變數，以足夠的資料列的數目變更時觸發重新編譯。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/2952444)。<br /><br />**注意：**請確定您仔細地測試此選項，然後再部署到生產環境。<br /><br />**範圍**： 全域或工作階段或查詢|
|**2528**|利用 DBCC CHECKDB、DBCC CHECKFILEGROUP 和 DBCC CHECKTABLE 來停用物件的平行檢查。 依預設，查詢處理器會自動判斷平行處理原則的程度。 最大平行處理原則程度的設定方式與平行查詢相同。 如需詳細資訊，請參閱 [設定 max degree of parallelism 伺服器組態選項](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。<br /><br />**注意：**平行 DBCC 會檢查通常都是啟用 （預設值）。 查詢處理器會重新評估，並且會自動調整的每個資料表或資料表 DBCC checkdb 檢查批次的平行處理原則。<br /><br />一般使用案例時，系統管理員可讓您知道該伺服器負載會增加 DBCC CHECKDB 完成，再以手動方式減少或增加並行處理與其他使用者的工作負載若要停用平行處理原則，因此選擇。 不過，停用平行檢查在 DBCC CHECKDB 可能會造成它需要更長的時間才能完成。<br /><br />**注意：**如果使用 TABLOCK 選項來執行 DBCC CHECKDB，平行處理原則已停用資料表可能已鎖定的時間較長的時間。<br /><br />**注意：**開頭[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]SP2，MAXDOP 選項可用來覆寫 max degree of parallelism 組態選項的 sp_configure 陳述式。<br /><br />**範圍**： 全域或工作階段|
|**2549**|執行 DBCC CHECKDB 命令，假設每個資料庫檔案唯一的磁碟機上。 DBCC CHECKDB 命令會建立內部清單來跨所有資料庫檔案每個唯一的磁碟機讀取的頁數。 此邏輯會判斷唯一根據每個檔案的實體檔案名稱的磁碟機代號的磁碟機。<br /><br />**注意：**不使用這個追蹤旗標，除非您知道每個檔案為基礎的唯一實體磁碟。<br /><br />**注意：**雖然這個追蹤旗標會改善效能的 DBCC CHECKDB 命令的目標使用 PHYSICAL_ONLY 選項，但是某些使用者可能不會看到任何效能改進。 這個追蹤旗標可改善磁碟 I/O 資源使用量，而基礎磁碟資源的效能可能會限制 DBCC CHECKDB 命令的整體效能。 如需詳細資訊，請參閱[Microsoft 支援文章](http://support.microsoft.com/kb/2634571)。<br /><br />**範圍**： 全域只| 
|**2562**|執行 DBCC CHECKDB 命令，在單一"batch"，無論在資料庫中的索引數目。 根據預設，DBCC CHECKDB 命令會嘗試藉由限制的索引或 「 事實 」 使用 「 批次 」 概念所產生的數字，tempdb 資源減到最低。 這個追蹤旗標會強制成一個批次的所有處理。<br /><br />使用此追蹤旗標的其中一個影響是 tempdb 的空間需求可能會增加。 Tempdb 可能成長至最多可達 5%以上的 DBCC CHECKDB 命令正在處理的使用者資料庫。<br /><br />**注意：**雖然這個追蹤旗標會改善效能的 DBCC CHECKDB 命令的目標使用 PHYSICAL_ONLY 選項，但是某些使用者可能不會看到任何效能改進。 這個追蹤旗標可改善磁碟 I/O 資源使用量，而基礎磁碟資源的效能可能會限制 DBCC CHECKDB 命令的整體效能。 如需詳細資訊，請參閱[Microsoft 支援文章](http://support.microsoft.com/kb/2634571)。<br /><br />**範圍**： 全域只|
|**2566**|除非指定 DATA_PURITY 選項，請執行 DBCC CHECKDB 命令沒有資料純度檢查。<br /><br />**注意：**資料行值的完整性檢查依預設會啟用並不需要 DATA_PURITY 選項。 對於從舊版的 SQL Server 升級資料庫，資料行值檢查不會啟用預設 DBCC CHECKDB WITH data_purity，否則已執行之前發生錯誤的資料庫至少一次。 此後，依預設 DBCC CHECKDB 會檢查資料行值的完整性。 如需詳細資訊，請參閱[Microsoft 支援文章](http://support.microsoft.com/kb/945770)。<br /><br />**範圍**： 全域只|
|**3023**|啟用成 BACKUP 命令的預設值的總和檢查碼選項。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/2656988)。<br /><br />**注意：**開頭[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]此行為藉由設定控制**備份總和檢查碼預設**組態選項。 如需詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)伺服器組態選項。<br /><br />**範圍**： 全域和工作階段|
|**3042**|略過預設備份壓縮預先配置演算法，讓備份檔案只會視需要成長以達到其最終大小。 如果您只要配置壓縮備份所需的實際大小，藉以節省空間，這個追蹤旗標就很有用。 使用此追蹤旗標可能會導致效能稍微降低 (可能會增加備份作業的持續時間)。 如需有關預先配置演算法的詳細資訊，請參閱[備份壓縮 &#40;SQL Server &#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md).<br /><br />**範圍**： 全域只|
|**3051**|可讓 SQL Server 備份至 URL 的特定錯誤記錄檔記錄。 如需詳細資訊，請參閱[SQL Server 備份至 URL 的最佳作法和疑難排解](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)。<br /><br />**範圍**： 全域只|  
|**3205**|依預設，如果磁帶機支援硬體壓縮，DUMP 或 BACKUP 陳述式就會使用它。 當使用這個追蹤旗標時，您可以停用磁帶機的硬體壓縮。 當您要與其他不支援壓縮的站台或磁帶機交換磁帶時，這非常有用。<br /><br />**範圍**： 全域或工作階段|  
|**3226**|根據預設，每項成功的備份作業都會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 錯誤記錄檔與系統事件記錄檔中，加入一個項目。 如果您建立非常頻繁的記錄備份，這些成功訊息可能會快速累積，因而產生龐大的錯誤記錄檔中尋找其他訊息便會造成問題。<br /><br />透過這個追蹤旗標，您可以隱藏這些記錄項目。 如果您正執行經常記錄備份，而且沒有任何指令碼相依於這些項目，這樣做就會很有用。<br /><br />**範圍**： 全域只|   
|**3427**|啟用在許多連續的交易，將資料插入暫存資料表中時，要修正問題的[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]耗用更多的 CPU 比[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。 如需詳細資訊，請參閱[Microsoft 技術支援文件](http://support.microsoft.com/help/3216543)<br /><br />**範圍**： 全域只|  
|**3608**|防止[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]自動啟動並復原任何資料庫，除了**主要**資料庫。 如果活動需要**tempdb**起始，然後**模型**復原和**tempdb**建立。 其他資料庫會在存取時啟動和復原。 但是，某些功能 (例如快照集隔離和讀取認可的快照集) 可能無法運作。 用於[移動系統資料庫](../../relational-databases/databases/move-system-databases.md)和[移動使用者資料庫](../../relational-databases/databases/move-user-databases.md)。<br /><br />**注意：**一般作業期間使用。<br /><br />**範圍**： 全域只|   
|**3625**|限制傳回給遮罩某些錯誤訊息，使用的參數不是 sysadmin 固定的伺服器角色的成員，使用者的資訊量 '\*\*\*\*\*\*'。 這樣做有助於避免洩漏機密資訊。<br /><br />**範圍**： 全域只|  
|**4136**|停用參數探測除非 OPTION(RECOMPILE)、 WITH RECOMPILE 或 OPTIMIZE FOR\<值 > 使用。 如需詳細資訊，請參閱[Microsoft 支援文章](http://support.microsoft.com/kb/980653)。 若要達成此目的資料庫層級，請參閱中的 PARAMETER_SNIFFING 選項[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). 若要完成此工作在查詢層級，將 OPTIMIZE FOR UNKNOWN[查詢提示](../../t-sql/queries/hints-transact-sql-query.md)。 從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1 時，若要完成此查詢層級的第二個選項是加入 USE 提示 'PARAMETER_SNIFFING'[查詢提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用這個追蹤旗標。<br /><br />**注意：**請確定您仔細地測試此選項，然後再部署到生產環境。<br /><br />**範圍**： 全域或工作階段|  
|**4137**|會導致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產生相互關聯，底下的查詢最佳化工具基數估計模型的最小的選擇性評估 AND 篩選條件的述詞時使用的計劃[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]及較早版本。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/2658214)。<br /><br />從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1，才能完成這項作業在查詢層級中，加入 USE 提示 'ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES'[查詢提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用舊版 CE 時使用這個追蹤旗標。<br /><br />**注意：**請確定您仔細地測試此選項，然後再部署到生產環境。<br /><br />**注意：** CE 120 版或更新將不會套用這個追蹤旗標。 請改用追蹤旗標 9471。<br /><br />**範圍**： 全域或工作階段或查詢| 
|**4138**|會導致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產生的計劃使用不會將目標調整資料列包含 TOP，OPTION (FAST N) 的查詢，或存在關鍵字。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/2667211)。<br /><br />從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1，才能完成這項作業在查詢層級中，加入 USE 提示 'DISABLE_OPTIMIZER_ROWGOAL'[查詢提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用這個追蹤旗標。<br /><br />**注意：**請確定您仔細地測試此選項，然後再部署到生產環境。<br /><br />**範圍**： 全域或工作階段或查詢| 
|**4139**|啟用自動產生索引鍵資料行狀態不論快速統計資料 （長條圖修正）。 如果設定追蹤旗標 4139，不論前置的統計資料資料行狀態 （遞增、 遞減排序，或固定），用來預估基數長條圖將會調整在查詢編譯時間。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/2952101)。<br /><br />從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1，才能完成這項作業在查詢層級中，加入 USE 提示 'ENABLE_HIST_AMENDMENT_FOR_ASC_KEYS'[查詢提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用這個追蹤旗標。<br /><br />**注意：**請確定您仔細地測試此選項，然後再部署到生產環境。<br /><br />**注意：** CE 70 版則不適用這個追蹤旗標。 請改用 2389年和 2390年的追蹤旗標。<br /><br />**範圍**： 全域或工作階段或查詢|
|**4199**|啟用查詢最佳化工具 (QO) 變更發行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]累計更新和 Service Pack。<br /><br />QO 變更與之前的版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]下的最新資料庫的預設會啟用[相容性層級](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)在指定的產品版本中，但不追蹤旗標 4199 啟用。<br /><br />使用特定的資料庫相容性層級和追蹤旗標 4199 時下, 表摘要說明的行為。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/974006)。<br /><br /><table border="1" frame="void" width="550"><tr valign="middle" align="center"><td>**資料庫相容性層級**</td><td>**TF 4199**</td><td>**從先前的資料庫相容性層級變更 QO**</td><td>**目前版本的 QO 變更 post RTM**</td></tr><tr valign="middle" align="center"><td rowspan="2">**100 到 120**</td><td>關閉</td><td>已停用</td><td>已停用</td></tr><tr valign="middle" align="center"><td>開啟</td><td>已啟用</td><td>已啟用</td></tr><tr valign="middle" align="center"><td rowspan="2">**130**</td><td>關閉</td><td>已啟用</td><td>已停用</td></tr><tr valign="middle" align="center"><td>開啟</td><td>已啟用</td><td>已啟用</td></tr><tr valign="middle" align="center"><td rowspan="2">**140**</td><td>關閉</td><td>已啟用</td><td>已停用</td></tr><tr valign="middle" align="center"><td>開啟</td><td>已啟用</td><td>已啟用</td></tr></table><br /><br />若要達成此目的資料庫層級，請參閱中的 QUERY_OPTIMIZER_HOTFIXES 選項[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).<br /><br />從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1，才能完成這項作業在查詢層級中，加入 USE 提示 'ENABLE_QUERY_OPTIMIZER_HOTFIXES'[查詢提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用這個追蹤旗標。<br /><br />**範圍**： 全域或工作階段或查詢|
|**4610**|增加儲存快取項目 8 倍的雜湊表的大小。 當搭配追蹤旗標 4618 會增加 8,192 TokenAndPermUserStore 快取存放區中的項目數。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/959823)。<br /><br />**範圍：**全域只|
|**4616**|讓應用程式角色可以看見伺服器層級的中繼資料。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，應用程式角色不能存取本身資料庫之外的中繼資料，因為應用程式角色與伺服器層級主體沒有關聯。 這是和舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]不同的一項行為變更。 設定這個全域旗標可停用新限制，使應用程式角色可以存取伺服器層級的中繼資料。<br /><br />**範圍**： 全域只|
|**4618**|限制到 1024，存放區 TokenAndPermUserStore 快取中的項目數目。 當搭配追蹤旗標 4610 會增加 8,192 TokenAndPermUserStore 快取存放區中的項目數。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/959823)。<br /><br />**範圍：**全域只|
|**5004**|暫停 TDE 加密掃描，並會導致加密掃描背景工作結束，而不進行任何運作。 資料庫會繼續處於加密的狀態 （進行中的加密）。 若要繼續重新加密掃描，請停用追蹤旗標 5004 及執行 ALTER DATABASE < 資料庫名稱 > 設定 ENCRYPTION ON。 <br /><br />**範圍：**全域只|
|**6498**|啟用多個大型查詢編譯，才能存取大型閘道沒有足夠記憶體可用時。 它 SQL Server 的目標記憶體，80 百分比為基礎，並可讓一個大型查詢編譯每 25 gb 的記憶體。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/3024815)。<br /><br />**注意：**開頭[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]SP2 和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]這種行為由引擎和追蹤旗標 6498 沒有任何作用。<br /><br />**範圍**： 全域只|
|**6527**|在 CLR 整合中第一次發生記憶體不足的例外狀況時停用記憶體傾印的產生。 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR 會產生第一個記憶體不足例外狀況的小型記憶體傾印。 追蹤旗標的行為如下：<br /><br />-如果使用這種方式啟動追蹤旗標時，絕對不會產生記憶體傾印。 不過，如果使用了其他的追蹤旗標，就可能產生記憶體傾印。<br />-如果在執行中的伺服器上啟用這個追蹤旗標時，記憶體傾印將不會自動產生從該點上。 不過，如果因為在 CLR 中發生記憶體不足的例外狀況而已經產生記憶體傾印，這個追蹤旗標就不會有任何效果。<br /><br />**範圍**： 全域只|
|**6532**|可讓查詢作業中的空間資料類型的效能改善[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。 提升的效能會有所不同，組態中，類型的查詢和物件。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/3107399)。<br /><br />**注意：**開頭[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]這種行為由引擎和追蹤旗標 6532 沒有任何作用。<br /><br />**範圍**： 全域和工作階段|
|**6533**|可讓查詢作業中的空間資料類型的效能改善[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。 提升的效能會有所不同，組態中，類型的查詢和物件。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/3107399)。<br /><br />**注意：**開頭[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]這種行為由引擎和追蹤旗標 6533 沒有任何作用。<br /><br />**範圍**： 全域和工作階段| 
|**6534**|可讓查詢作業中的空間資料類型的效能改善[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。 提升的效能會有所不同，組態中，類型的查詢和物件。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/3107399)。<br /><br />**範圍**： 全域和工作階段|
|**7314**|強制未知有效位數/小數位數被視為與 OLE DB 提供者的雙精度浮點數值的數字值。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/3051993)。<br /><br />**範圍**： 全域和工作階段|  
|**7412**|可讓分析基礎結構的輕量級的查詢執行統計資料。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/3170113)。<br /><br />**範圍**： 全域只|
|**7471**|執行多個[UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md)不同的統計資料，同時針對單一資料表。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/3156157)。<br /><br />**範圍**： 全域只|
|**7745**|強制查詢存放區不排清到磁碟，在資料庫關閉的資料。<br /><br />**注意：**使用這項追蹤可能會導致先前未曾排清至磁碟設為關閉時遺失的查詢存放區資料。 如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]關機 命令 SHUTDOWN WITH NOWAIT 可以而不是這個追蹤旗標用來強制立即關機。<br /><br />**範圍**： 全域只|
|**7752**|啟用查詢存放區非同步載入。<br /><br />**注意：**使用這個追蹤旗標，如果[!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]發生大量的查詢存放區同步負載 （預設行為） 與相關的 QDS_LOADDB 等候。<br /><br />**範圍**： 全域只|
|**7806**|在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]上啟用專用管理員連接 (DAC)。 依預設，[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 上不會保留任何 DAC 資源。 如需詳細資訊，請參閱 [資料庫管理員的診斷連接](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)。<br /><br />**範圍**： 全域只|  
|**8011**|停用資源監視器信號緩衝區。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/920093)。<br /><br />**範圍**： 全域和工作階段|
|**8012**|停用排程器的信號緩衝區。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/920093)。<br /><br />**範圍**： 全域只|
|**8015**|停用自動偵測及 NUMA 設定。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/2813214)。<br /><br />**範圍**： 全域只|
|**8018**|停用例外狀況信號緩衝區。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/920093)。<br /><br />**範圍**： 全域只|
|**8019**|停用信號緩衝區例外狀況的堆疊集合。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/920093)。<br /><br />**範圍**： 全域只|
|**8020**|停用監視的工作集。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/920093)。<br /><br />**範圍**： 全域只|
|**8032**|將快取限制參數還原為 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] RTM 設定，這項設定通常會允許使用更大的快取。 當經常重複使用的快取項目無法納入快取中，以及 [針對特定工作負載最佳化伺服器組態選項](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md) 無法解決計畫快取的問題時，請使用這項設定。<br /><br />**警告：**追蹤旗標 8032 可能會導致效能不佳，如果大型快取較少的記憶體可用為其他記憶體取用者，例如緩衝集區。<br /><br />**範圍**： 全域只|   
|**8048**|將 NUMA 資料分割成 CPU 分割記憶體物件。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/2809338)。<br /><br />**注意：**開頭[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]SP2 和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]這種行為由引擎和追蹤旗標 8048 沒有任何作用。<br /><br />**範圍**： 全域只|  
|**8079**|可讓[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]sp2 升級為質詢硬體配置及自動報告 8 或更多的 Cpu，每個 NUMA 節點的系統上設定軟體 NUMA。 自動軟體式 NUMA 行為是 Hyperthread （HT/邏輯處理器） 感知。 資料分割和標尺背景處理增加的接聽程式，調整數目和網路的其他節點和加密功能的建立。<br /><br />**注意：**這個追蹤旗標適用於[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]SP2。 從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]這種行為由引擎和追蹤旗標 8048 沒有任何作用。<br /><br />**範圍**： 全域只| 
|**8207**|啟用異動複寫的單一更新。 訂閱者的更新可以複寫做成對的刪除和插入。 這可能不符合商務規則，例如引發 UPDATE 觸發程序。 追蹤旗標 8207 更新的方式，而不是 DELETE 或 INSERT 配對複寫只有一個資料列 （單一更新） 會影響的唯一資料行的更新。 如果更新會影響在其擁有唯一的條件約束的資料行，或是更新影響多個資料列，更新仍會複寫為 DELETE 或 INSERT 配對。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/302341)。<br /><br />**範圍**： 全域只|
|**8721**|錯誤記錄檔時自動更新統計資料所執行的報表。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/195565)。<br /><br />**範圍**： 全域只|
|**8744**|停用預先擷取巢狀迴圈運算子。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/920093)。<br /><br />**注意：**不正確使用這個追蹤旗標可能會造成額外的實體時讀取[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行包含巢狀迴圈運算子的計畫。<br /><br />**範圍**： 全域和工作階段|
|**9024**|將全域記錄集區記憶體物件轉換成 NUMA 節點分割的記憶體物件。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/2809338)。<br /><br />**注意：**開頭[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]SP3 和[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]這種行為由引擎和追蹤旗標 9024 SP1 有任何作用。<br /><br />**範圍**： 全域只|
|**9347**|停用排序運算子的批次模式。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]導入新批次模式排序運算子，將提升許多分析查詢的效能。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/3172787)。<br /><br />**範圍**： 全域或工作階段或查詢|
|**9349**|Top N sort 運算子的批次模式下會停用。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]導入新批次模式下最上層 sort 運算子來提升分析的許多查詢的效能。<br /><br />**範圍**： 全域或工作階段或查詢|
|**9389**|啟用動態記憶體授與的批次模式運算子。 如果查詢不會取得所有需要的記憶體，它會用到 tempdb 產生額外的 I/O，可能會影響查詢效能資料。 如果啟用動態記憶體授與追蹤旗標，則批次模式運算子可能會要求額外的記憶體，並避免溢出到 tempdb，額外的記憶體是否可用。<br /><br />**範圍**： 全域或工作階段| 
|**9453**|停用批次模式執行。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/help/4016902)。<br /><br />**注意：**請確定您仔細地測試此選項，然後再部署到生產環境。<br /><br />**範圍：**全域工作階段和查詢|
|**9471**|會導致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產生最小的選擇性使用單一資料表的篩選，底下的查詢最佳化工具基數估計模型的計劃[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版本。<br /><br />從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1，才能完成這項作業在查詢層級中，加入 USE 提示 'ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES'[查詢提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用這個追蹤旗標。<br /><br />**注意：**請確定您仔細地測試此選項，然後再部署到生產環境。<br /><br />**注意：** CE 70 版則不適用這個追蹤旗標。 請改用追蹤旗標 4137。<br /><br />**範圍**： 全域或工作階段或查詢| 
|**9476**|會導致[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]產生計畫，而不預設的基底內含項目假設，底下的查詢最佳化工具基數估計模型的方式利用簡單的內含項目假設[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版本。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/3189675)。<br /><br />從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1，才能完成這項作業在查詢層級中，加入 USE 提示 'ASSUME_JOIN_PREDICATE_DEPENDS_ON_FILTERS'[查詢提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用這個追蹤旗標。<br /><br />**注意：**請確定您仔細地測試此選項，然後再部署到生產環境。<br /><br />**範圍**： 全域或工作階段或查詢| 
|**9481**|可讓您將查詢最佳化工具基數估計模型設定為[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和舊版本中，不論資料庫的相容性層級。 如需詳細資訊，請參閱[Microsoft 支援文章](http://support.microsoft.com/kb/2801413)。 若要達成此目的資料庫層級，請參閱中的 LEGACY_CARDINALITY_ESTIMATION 選項[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).<br /><br />從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]SP1，才能完成這項作業在查詢層級中，加入 USE 提示 'FORCE_LEGACY_CARDINALITY_ESTIMATION'[查詢提示](../../t-sql/queries/hints-transact-sql-query.md)而不是使用這個追蹤旗標。<br /><br />**範圍**： 全域或工作階段或查詢|  
|**9485**|停用 DBCC SHOW_STATISTICS 的 SELECT 權限。<br /><br />**範圍**： 全域只|
|**9488**|將資料表值函式的固定的估計設定為預設值是 1 (底下的查詢最佳化工具基數估計模型的預設對應[!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]及較早版本)，當使用的查詢最佳化工具基數估計模型[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]透過[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]版本。<br /><br />**範圍**： 全域或工作階段或查詢|
|**9495**|插入期間，停用平行處理原則...選取的作業和它適用於使用者和暫存資料表。 如需詳細資訊，請參閱[Microsoft 技術支援文件](http://support.microsoft.com/kb/3180087)<br /><br />**範圍**： 全域或工作階段| 
|**9567**|啟用壓縮資料流的 Alwayson 可用性群組自動植入期間。 壓縮可以大幅縮短傳輸時間，自動植入期間，會增加處理器上的負載。 如需詳細資訊，請參閱[自動初始化 Alwayson 可用性群組](../../database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group.md)和[微調可用性群組的壓縮](../../database-engine/availability-groups/windows/tune-compression-for-availability-group.md)。<br /><br />**範圍**： 全域或工作階段|
|**9591**|停用記錄區塊壓縮，在 Alwayson 可用性群組中。 記錄檔區塊壓縮是預設的行為使用中的同步和非同步複本[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]和[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。 在[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，壓縮只能搭配非同步複本。 <br /><br />**範圍**： 全域或工作階段|
|**9592**|啟用記錄同步的可用性群組的資料流壓縮。 這項功能已停用預設會在同步的可用性群組，因為壓縮會增加延遲。 如需詳細資訊，請參閱 [微調可用性群組的壓縮](../../database-engine/availability-groups/windows/tune-compression-for-availability-group.md)。<br /><br />**範圍**： 全域或工作階段| 
|**9939**|啟用平行計劃和平行掃描記憶體最佳化資料表和參考記憶體最佳化資料表或資料表變數的 DML 作業中的資料表變數，只要它們不是中的 DML 作業的目標[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/4013877)。<br /><br />**注意：**如果同時也可以明確啟用追蹤旗標 4199 追蹤旗標 9939 就不需要。<br /><br />**範圍**： 全域或工作階段或查詢|   
|**10204**|停用合併/重新壓縮期間資料行存放區索引重組。 在[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，當重新組織資料行存放區索引時，會自動合併成較大壓縮資料列，以及為壓縮具有大量的任何資料列群組已刪除資料列的任何小型的壓縮資料列的新功能。<br /><br />**注意：**追蹤旗標 10204 不適用於記憶體最佳化資料表建立資料行存放區索引。<br /><br />**範圍**： 全域或工作階段|   
|**10316**|上可建立其他索引[內部記憶體最佳化暫存時態表](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)，預設值，旁邊。 如果您有特定的查詢模式，其中包含未涵蓋的預設索引的資料行，您可以考慮加入額外的。<br /><br />**注意：**系統版本設定時態表的記憶體最佳化資料表的設計可提供高交易處理能力。 請留意建立額外的索引可能會對 DML 作業更新或刪除目前資料表中的資料列的額外負荷。 與其他索引您的目標應該以尋找時態查詢的效能和額外 DML 負擔之間的正確平衡。<br /><br />**範圍**： 全域或工作階段|
|**11023**|停用使用上次的保存的取樣率，取樣率指定的位置不明確的一部份的所有後續的統計資料更新[UPDATE STATISTICS](../../t-sql/statements/update-statistics-transact-sql.md)陳述式。 如需詳細資訊，請參閱此[Microsoft 支援文章](http://support.microsoft.com/kb/4039284)。<br /><br />**範圍**： 通用| 
  
## <a name="remarks"></a>備註  
 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，有三種類型的追蹤旗標： 查詢、 工作階段和全域。 查詢追蹤旗標都可用於特定的查詢內容。 工作階段追蹤旗標用於某個連接，而且只會在該連接顯示出來。 全域追蹤旗標是設在伺服器層級，只要是該伺服器上的連接，都看得到它們。 某些旗標只能啟用為全域旗標，某些則可以啟用為全域或工作階段範圍。  
  
 適用的規則如下：  
-   全域追蹤旗標必須全域啟用， 否則追蹤旗標就沒有效果。 我們建議您啟用全域追蹤旗標，在啟動時，使用**-T**命令列選項。 這可確保在伺服器重新啟動之後的追蹤旗標會保持使用中。  
-   如果追蹤旗標有任一個全域、 工作階段或查詢範圍，它可以啟用適當的範圍內。 以工作階段層級啟用的追蹤旗標絕不會影響其他工作階段，而且當開啟該工作階段的 SPID 登出時，該追蹤旗標的效果也隨之消失。  
  
請利用下列方法之一，將追蹤旗標設為開啟或關閉：
-   使用 DBCC TRACEON 和 DBCC TRACEOFF 命令。  
     例如，若要全域啟用追蹤旗標 2528年，使用 DBCC TRACEON 搭配-1 引數： `DBCC TRACEON (2528, -1)`。 啟用 DBCC TRACEON 全域追蹤旗標的效果會在伺服器重新啟動遺失。 若要關閉全域追蹤旗標，請利用 -1 引數使用 DBCC TRACEOFF。  
-   使用**-T**啟動選項，指定上設定追蹤旗標，在啟動期間。  
     **-T**啟動選項會全域啟用追蹤旗標。 您不能利用啟動選項啟用工作階段層級的追蹤旗標。 這可確保在伺服器重新啟動之後的追蹤旗標會保持使用中。 如需啟動選項的詳細資訊，請參閱 [Database Engine 服務啟動選項](../../database-engine/configure-windows/database-engine-service-startup-options.md)。
-   在查詢層級，使用 QUERYTRACEON[查詢提示](http://support.microsoft.com/kb/2801413)。
  
使用`DBCC TRACESTATUS`命令來判斷所目前作用中的追蹤旗標。
  
## <a name="examples"></a>範例  
 下列範例會設定追蹤旗標 3205 上的所有工作階段的伺服器層級使用 DBCC TRACEON。  
  
```sql  
DBCC TRACEON (3205,-1);  
```

您可以啟用追蹤旗標 4199 和 4137 針對特定查詢所控制的所有 「 影響計畫的 hotfix。
  
```sql
SELECT x FROM correlated WHERE f1 = 0 AND f2 = 1 OPTION (QUERYTRACEON 4199, QUERYTRACEON 4137)
``` 
 
## <a name="see-also"></a>請參閱  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DBCC INPUTBUFFER &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)  
[DBCC OUTPUTBUFFER &#40;TRANSACT-SQL &#41;](../../t-sql/database-console-commands/dbcc-outputbuffer-transact-sql.md)  
[DBCC TRACEOFF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)  
[DBCC TRACEON &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)  
[DBCC TRACESTATUS &#40;TRANSACT-SQL &#41;](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)  
[EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
[SET NOCOUNT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/set-nocount-transact-sql.md)  
[ALTER DATABASE SET 選項 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)  
[查詢提示 (TRANSACT-SQL)](../../t-sql/queries/hints-transact-sql-query.md)

