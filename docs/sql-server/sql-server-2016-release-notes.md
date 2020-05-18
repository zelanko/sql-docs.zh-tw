---
title: SQL Server 2016 版本資訊 | Microsoft Docs
description: 建議在安裝或對 Microsoft SQL Server 2016 版本進行疑難排解之前，先閱讀這份版本資訊文件所描述的已知問題。
ms.date: 04/25/2018
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- build notes
- release issues
ms.assetid: c64077a2-bec8-4c87-9def-3dbfb1ea1fb6
author: rothja
ms.author: jroth
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 516a05c1a797278fd5de383acc39284d689ce191
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/13/2020
ms.locfileid: "83151571"
---
# <a name="sql-server-2016-release-notes"></a>SQL Server 2016 版本資訊
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
  本文描述 SQL Server 2016 版 (包括 Service Pack) 的限制和問題。 如需新功能的相關資訊，請參閱 [SQL Server 2016 的新功能](https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2016)。

- [![Download from Evaluation Center](../includes/media/download2.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)  Download SQL Server 2016  from the **[Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**
- [![Azure 虛擬機器小型](../includes/media/azure-vm.png)](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftsqlserver.sql2017-ws2019?tab=Overview) 擁有 Azure 帳戶嗎？  接著前往 **[這裡](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftsqlserver.sql2017-ws2019?tab=Overview)** 來啟動已安裝 SQL Server 2016 SP1 的虛擬機器。
- [![下載 SSMS](../includes/media/download2.png)](../ssms/download-sql-server-management-studio-ssms.md) 如要取得最新版的 SQL Server Management Studio，請參閱 **[下載 SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)** 。

## <a name="sql-server-2016-service-pack-2-sp2"></a><a name="bkmk_2016sp2"></a>SQL Server 2016 Service Pack 2 (SP2)

![info_tip](../sql-server/media/info-tip.png) SQL Server 2016 SP2 包含 2016 SP1 之後發行的所有累計更新，截至並且包含 CU8。

- [![Microsoft 下載中心](../includes/media/download2.png)](https://www.microsoft.com/download/details.aspx?id=56836) [下載 SQL Server 2016 Service Pack 2 (SP2)](https://www.microsoft.com/download/details.aspx?id=56836)
- 如需完整的更新清單，請參閱 [SQL Server 2016 Service Pack 2 版本資訊](https://support.microsoft.com/help/4052908/sql-server-2016-service-pack-2-release-information)

SQL Server 2016 SP2 安裝在安裝之後可能需要重新開機。 最佳做法是在 SQL Server 2016 SP2 安裝後規劃和執行重新開機。

SQL Server 2016 SP2 中包含有關效能和規模調整的改善。

|功能|描述|詳細資訊|
|---|---|---|
|已改善散發 DB 清除程序 |   過度龐大的散發資料庫資料表會造成封鎖和死結情況。 改善的清除程序旨在排除其中一些封鎖或死結情況。 |   [KB4040276](https://support.microsoft.com/help/4040276/fix-indirect-checkpoints-on-the-tempdb-database-cause-non-yielding) \(機器翻譯\)  |
|變更追蹤清除    |   已改善針對變更追蹤資料表的變更追蹤清除效能和效率。    |   [KB4052129](https://support.microsoft.com//help/4052129/update-for-manual-change-tracking-cleanup-procedure-in-sql-server-2016) \(機器翻譯\) |
|使用 CPU 逾時來取消 Resource Governor 要求   |   藉由實際取消要求來改善查詢要求的處理 (如果針對要求達到 CPU 閾值)。 此行為會在追蹤旗標 2422 下啟用。 |   [KB4038419](https://support.microsoft.com/help/4038419/add-cpu-timeout-to-resource-governor-request-max-cpu-time-sec) \(英文\)   |
|使用 SELECT INTO 來在檔案群組中建立目標資料表    |   從 SQL Server 2016 SP2 開始，SELECT INTO T-SQL 語法開始支援將資料表載入其他檔案群組，而不是使用 T-SQL 語法中 ON <Filegroup name> 關鍵字使用者的預設檔案群組。 |       |
|改善 TempDB 的間接檢查點    |   已改善 TempDB 的間接檢查點，以最小化 DPLists 上的執行緒同步鎖定競爭。 此改善可讓 SQL Server 2016 上的 TempDB 工作負載，在 TempDB 的間接檢查點為 ON 的情況下，預設便能進行擴增。    |   [KB4040276](https://support.microsoft.com/help/4040276) \(機器翻譯\) |
|已改善大型記憶體機器上的資料庫備份效能  |   SQL Server 2016 SP2 將於備份期間清空進行中 I/O 的方式最佳化，進而大幅提升小型至中型資料庫的備份效能。 我們已在對 2TB 的機器進行系統資料庫備份時，觀察到超過 100x 的改善。 效能提升會隨著資料庫大小增加而減少，因為要備份的分頁和備份 I/O 與反覆運算緩衝集區相較之下需要更多時間。 針對在配備大量記憶體的大型高階伺服器上裝載多個小型資料庫的客戶，此變更有助於提升備份效能。    |       |
|針對啟用 TDE 之資料庫的 VDI 備份壓縮支援   |   SQL Server 2016 SP2 新增了 VDI 支援，可讓 VDI 備份解決方案針對啟用 TDE 的資料庫利用壓縮功能。 此改善引入新的備份格式，以針對啟用 TDE 的資料庫支援備份壓縮。 SQL Server 引擎會透明地處理新的和舊的備份格式以還原備份。   |       |
|複寫代理程式設定檔參數的動態載入    |   這個新的增強功能能以動態方式載入複寫代理程式參數，而不需要重新啟動代理程式。 這個變更僅適用於最常使用的代理程式設定檔參數。 |       |
|針對統計資料建立/更新支援 MAXDOP 選項 |    這個增強功能允許針對 CREATE/UPDATE 統計資料陳述式指定 MAXDOP 選項，也會在建立或重建所有索引類型而更新統計資料時，確保使用的是正確的 MAXDOP 設定 (如果 MAXDOP 選項存在)   |   [KB4041809](https://support.microsoft.com/help/4041809) \(機器翻譯\) |
|針對累加統計資料改善自動統計資料更新 |    在特定案例下，當資料表中的多個分割區發生數個資料變更，且累加統計資料的總修改計數器超過自動更新閾值，但沒有任何個別分割區超過自動更新閾值時，統計資料更新可能會延遲，直到資料表中發生更多修改為止。 此行為已在追蹤旗標 11024 下修正。   |       |

SQL Server 2016 SP2 中已包含支援能力和診斷相關的改善。

|功能|描述|詳細資訊|
|---|---|---|
|針對可用性群組中資料庫的完整 DTC 支援    |   SQL Server 2016 中目前不支援可用性群組中資料庫的跨資料庫交易。 在 SQL Server 2016 SP2 中，我們針對可用性群組資料庫的分散式交易推出完整支援。   |       |
|更新 sys.databases 的 is_encrypted 資料行，以正確反映 TempDB 的加密狀態 |   TempDB 之 sys.databases 中的 is_encryptedcolumn 資料行的值為 1，即使在您關閉所有使用者資料庫的加密並重新啟動 SQL Server 之後也一樣。 預期的行為是該值為 0，因為在此情況下 TempDB 已經不再加密。 從 SQL Server 2016 SP2 開始，sys.databases.is_encrypted 現在會正確地反映 TempDB 的加密狀態。  |       |
|新的 DBCC CLONEDATABASE 選項，以產生驗證的複製品和備份   |   在 SQL Server 2016 SP2 中，DBCC CLONEDATABASE 有兩個新的選項：產生驗證的複製品，或產生備份複製品。 當使用 WITH VERIFY_CLONEDB 選項建立複製品資料庫時，系統會建立並驗證一致的資料庫複製品，且 Microsoft 將會支援它以用於生產環境。 已推出新的屬性，以驗證複製品是否已驗證 SELECT DATABASEPROPERTYEX('clone_database_name', 'IsVerifiedClone')。 使用 BACKUP_CLONEDB 選項建立複製品時，在相同的資料夾中會產生備份作為資料檔案，以讓客戶能輕鬆將複製品移動到其他伺服器，或將它傳送到 Microsoft 客戶支援 (CSS) 以進行疑難排解。  |       |
|針對 DBCC CLONEDATABASE 的 Service Broker (SSB) 支援    |   已增強 DBCC CLONEDATABASE 命令，以允許撰寫 SSB 物件指令碼。  |   [KB4092075](https://support.microsoft.com/help/4092075) \(機器翻譯\) |
|新的 DMV 以監視 TempDB 版本存放空間使用量    |   SQL Server 2016 SP2 中已推出新的 sys.dm_tran_version_store_space_usage DMV，以允許監視 TempDB 的版本存放空間使用量。 在生產環境伺服器上執行時，DBA 現在可以根據每個資料庫的版本存放空間使用量需求，主動規劃 TempDB 大小，而不會產生任何效能負擔。 |       |
|針對複寫代理程式的完整傾印支援 | 目前，如果複寫代理程式遇到未處理的例外狀況，預設會建立例外狀況徵兆的小型傾印。 這會使對未處理的例外狀況進行疑難排解變得非常困難。 我們透過此變更推出新的登錄機碼，它將允許針對複寫代理程式建立完整傾印。  |       |
|針對讀取可用性群組路由失敗的擴充事件增強功能 |   在之前，read_only_rout_fail xEvent 會在路由清單存在，但路由清單中的伺服器沒有任何一個可供連線的情況下觸發。 SQL Server 2016 SP2 包含可協助進行疑難排解的額外資訊，並且也會針對觸發此 xEvent 的程式碼項目提供額外資訊。  |       |
|新的 DMV 以監視交易記錄 |   新增 DMV sys.dm_db_log_stats，可傳回摘要層級屬性，以及資料庫交易記錄檔的相關資訊。 |       |
|新的 DMV 以監視 VLF 資訊 |   新的 DMV sys.dm_db_log_info 已在 SQL Server 2016 SP2 中推出，以將類似 DBCC LOGINFO 的 VLF 資訊公開，以監視、警示和防止客戶會遇到的可能 T-Log 問題。    |       |
|sys.dm_os_sys_info 中的處理器資訊|   已新增資料行至 sys.dm_os_sys_info DMV，以公開處理器的相關資訊，如 socket_count 和 cores_per_numa。  |       |
|sys.dm_db_file_space_usage 中的範圍修改資訊| 已新增資料行至 sys.dm_db_file_space_usage，以追蹤自上次完整備份之後的已修改範圍數目。  |       |
|sys.dm_exec_query_stats 中的區段資訊 |   已新增資料行至 sys.dm_exec_query_stats，以追蹤略過和讀取的資料行存放區區段數目，如 total_columnstore_segment_reads 和 total_columnstore_segment_skips。   |   [KB4051358](https://support.microsoft.com/help/4051358) \(英文\) |
|針對散發資料庫設定正確的相容性層級  |   安裝 Service Pack 之後，散發資料庫相容性層級會變更為 90。 這是因為 sp_vupgrade_replication 預存程序中的程式碼路徑所造成。 SP 現在已經過變更，可為散發資料庫設定正確的相容性層級。   |       |
|公開最後一個已知的良好 DBCC CHECKDB 資訊    |   已新增資料庫選項，來以程式設計方式傳回最後一次成功執行 DBCC CHECKDB 的日期。 使用者現在可以查詢 DATABASEPROPERTYEX([database], 'lastgoodcheckdbtime')，以取得代表在所指定伺服器上最後一次成功執行 DBCC CHECKDB 的日期/時間單一值。  |       |
|Showplan XML 增強功能| [使用統計資料來編譯查詢計劃的相關資訊](https://blogs.msdn.microsoft.com/sql_server_team/sql-server-2017-showplan-enhancements/) \(英文\)，包括統計資料名稱、修改計數器、取樣百分比，以及統計資料最後一次更新的時間。 請注意，此功能只新增到 CE 模型 120 和更新版本。 例如，CE 70 並不支援此功能。| |
| |如果查詢最佳化工具使用「資料列目標」邏輯，則會將新屬性 [EstimateRowsWithoutRowgoal](https://blogs.msdn.microsoft.com/sql_server_team/more-showplan-enhancements-row-goal/) \(英文\) 新增到執行程序表 XML。| |
| |實際執行程序表 XML 中的新執行階段屬性 [UdfCpuTime 和 UdfElapsedTime](https://blogs.msdn.microsoft.com/sql_server_team/more-showplan-enhancements-udfs/) \(英文\)，以追蹤在純量使用者定義函數 (UDF) 中花費的時間。| |
| |在實際執行程序表 XML 中將 CXPACKET 等候類型新增至[前 10 個可能的等候清單](https://blogs.msdn.microsoft.com/sql_server_team/new-showplan-enhancements/) \(英文\) - 平行查詢執行經常包含 CXPACKET 等候，但此類型的等候並沒有在實際執行程序表 XML 中報告。 |       |
| |擴充執行階段溢出警告，以報告在平行處理原則運算子溢出期間寫入至 TempDB 的分頁數目。| |
|針對含增補字元定序之資料庫的複寫支援  |   使用增補字元定序的資料庫上，現已可支援複寫。 |       |
|適當處理具有可用性群組容錯移轉的 Service Broker |   在目前的實作中，當可用性群組資料庫上啟用 Service Broker 時，在 AG 容錯移轉期間，所有源自主要複本的 Service Broker 連線都會保持開啟。 此改善的目標是在 AG 容錯移轉期間關閉所有這類的開啟連線。 |       |
|已改善平行處理原則等候疑難排解 |   透過新增 [CXCONSUMER](https://blogs.msdn.microsoft.com/sql_server_team/making-parallelism-waits-actionable/) \(英文\) 等候。   |       |
|已改善針對相同資訊的 DMV 之間的一致性 |   sys.dm_exec_session_wait_stats DMV 現在會使用 sys.dm_os_wait_stats DMV 一致地追蹤 CXPACKET 和 CXCONSUMER 等候。 |       |
|已改善查詢內平行處理原則死結的疑難排解 | 新的 exchange_spill 擴充事件，以報告在平行處理原則運算子溢出期間寫入至 TempDB 的分頁數目 (具有 xEvent 欄位名稱 worktable_physical_writes)。| |
| |sys.dm_exec_query_stats、sys.dm_exec_procedure_stats 和 sys.dm_exec_trigger_stats DMV (如 total_spills) 中的溢出資料行，現在也包含由平行處理原則運算子所溢出的資料。| |
| |已針對平行處理原則死結案例改善 XML 死結圖表，並新增更多屬性至 exchangeEvent 資源。| |
| |已針對涉及批次模式運算子的死結改善 XML 死結圖表，並新增更多屬性至 SyncPoint 資源。| |
|動態重新載入部分複寫代理程式設定檔參數 |   在目前的複寫代理程式實作中，對代理程式設定檔參數所做的任何變更，都需要停止並重新啟動代理程式。 此改善可讓參數以動態方式重新載入，而不需要重新啟動複寫代理程式。   |       |

![horizontal-bar.png](media/horizontal-bar.png)

## <a name="sql-server-2016-service-pack-1-sp1"></a><a name="bkmk_2016sp1"></a>SQL Server 2016 Service Pack 1 (SP1)
![info_tip](../sql-server/media/info-tip.png) SQL Server 2016 SP1 包含截至 SQL Server 2016 RTM CU3 的所有累計更新，包括安全性更新 MS16-136。 它包含 SQL Server 2016 累積更新提供的解決方案彙總，截至並且包含最新的累積更新 - CU3 和 2016 年 11 月 8 日發行的安全性更新 MS16-136。

SQL Server SP1 Standard、Web、Express 和 Local DB 版本提供下列功能 (除非另有附註)：
- 一律加密
- 異動資料擷取 (Express 未提供)
- columnstore
- 壓縮
- 動態資料遮罩
- 細部稽核
- 記憶體內部 OLTP (Local DB 未提供)
- 多個 Filestream 容器 (Local DB 未提供)
- 資料分割
- PolyBase
- 資料列層級安全性

下表摘要說明 SQL Server 2016 SP1 中提供的重要改善。

|功能|描述|詳細資訊|
|---|---|---|
|在 TF 715 下，使用自動 TABLOCK 大量插入堆積| 追蹤旗標 715 可啟用資料表鎖定，以將作業大量載入到不含非叢集索引的堆積。|[將 SAP 工作負載移轉至 SQL Server 的速度加快 2.5 倍](https://blogs.msdn.microsoft.com/sql_server_team/migrating-sap-workloads-to-sql-server-just-got-2-5x-faster/)|
|CREATE 或 ALTER|部署預存程序、觸發程序、使用者定義的函式和檢視等物件。|[SQL Server 資料庫引擎部落格](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/11/17/create-or-alter-another-great-language-enhancement-in-sql-server-2016-sp1/)|
|支援複寫的 DROP TABLE|支援複寫的 DROP TABLE，可卸除複寫發行項。|[KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactiona)|
|Filestream RsFx 驅動程式簽署|Filestream RsFx 驅動程式經過 Windows 硬體開發人員中心儀表板入口網站 (Dev Portal) 簽署與認證，可確保在 Windows Server 2016/Windows 10 上安裝 SQL Server 2016 SP1 Filestream RsFx 驅動程式時不會發生任何問題。|[將 SAP 工作負載移轉至 SQL Server 的速度加快 2.5 倍](https://blogs.msdn.microsoft.com/sql_server_team/migrating-sap-workloads-to-sql-server-just-got-2-5x-faster/)|
|SQL 服務帳戶的 LPIM - 以程式設計方式進行識別|允許 DBA 以程式設計方式識別在記憶體中鎖定分頁 (LPIM) 的權限是否在服務啟動時生效。|[Developers Choice:Programmatically identify LPIM and IFI privileges in SQL Server](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-programmatically-identify-lpim-and-ifi-privileges-in-sql-server) (開發人員選擇：以程式設計方式識別 SQL Server 中的 LPIM 和 IFI 權限)|
|手動變更追蹤清除|新的預存程序可視需要清除變更追蹤內部資料表。| [KB 3173157](https://support.microsoft.com/help/3173157/adds-a-stored-procedure-for-the-manual-cleanup-of-the-change-tracking)|
|本機暫存資料表的平行 INSERT..SELECT 變更|INSERT..SELECT 作業的新平行 INSERT。|[SQL Server 客戶諮詢小組](https://blogs.msdn.microsoft.com/sqlcat/2016/07/21/real-world-parallel-insert-what-else-you-need-to-know/)|
|Showplan XML|擴充診斷功能，包括針對查詢啟用授與警告和最大記憶體、啟用追蹤旗標，並會呈現其他診斷資訊。 | [KB 3190761](https://support.microsoft.com/help/3190761/update-to-improve-diagnostics-by-expose-data-type-of-the-parameters-fo)|
|儲存類別記憶體|提升在 Windows Server 2016 中使用儲存類別記憶體的交易處理能力，進而確保能依據重要順序大幅度加速交易認可時間。|[SQL Server 資料庫引擎部落格](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/12/02/transaction-commit-latency-acceleration-using-storage-class-memory-in-windows-server-2016sql-server-2016-sp1/)|
|USE HINT|使用查詢選項 `OPTION(USE HINT('<option>'))`，以改變使用支援的查詢層級提示的查詢最佳化工具行為。 與 QUERYTRACEON 不同的是，USE HINT 選項不需要系統管理員權限。|[Developers Choice:USE HINT query hints](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-use-hint-query-hints/) (開發人員選擇：USE HINT 查詢提示)|
|XEvent 新增項目|新的 XEvent 和 Perfmon 診斷功能可改善對延遲的疑難排解。|[擴充事件](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)|

此外，請注意下列修正：
- 為響應 DBA 和 SQL 社群的意見反應，自 SQL 2016 SP1 起已將 Hekaton 記錄訊息數降至最低。
- 檢閱新的[追蹤旗標](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)。
- 現在，WideWorldImporters 範例資料庫的完整版本可以使用 SQL Server 2016 SP1 以上的 Standard Edition 和 Express Edition，並已於 [Github]( https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0) 中提供。 此範例不需要任何變更。 在 RTM Enterprise Edition 中建立的資料庫備份可使用 SP1 的 Standard 和 Express。

SQL Server 2016 SP1 安裝可能需要在安裝後重新開機。 最佳做法是在 SQL Server 2016 SP1 安裝後規劃和執行重新開機。

### <a name="download-pages-and-more-information"></a>下載頁面和詳細資訊

- [下載 Microsoft SQL Server 2016 Service Pack 1](https://www.microsoft.com/download/details.aspx?id=54276)
- [SQL Server 2016 Service Pack 1 (SP1) 已發行](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/)
- [SQL Server 2016 Service Pack 1 版本資訊](https://support.microsoft.com/kb/3182545)
- ![info_tip](../sql-server/media/info-tip.png) [SQL Server 更新中心](https://msdn.microsoft.com/library/ff803383.aspx)提供所有支援版本的連結和資訊，包括 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 的 Service Pack

![horizontal-bar.png](media/horizontal-bar.png)

##  <a name="sql-server-2016-release---general-availability-ga"></a><a name="bkmk_2016_ga"></a> SQL Server 2016 Release - General Availability (GA)
-   [Database Engine (GA)](#bkmk_ga_instalpatch)
-   [Stretch Database (GA)](#bkmk_ga_stretch)
-   [查詢存放區 (GA)](#bkmk_ga_query_store)
-   [產品文件 (GA)](#bkmk_ga_docs)

### <a name="repl_icon_warn--install-patch-requirement-ga"></a>![repl_icon_warn](../database-engine/availability-groups/windows/media/repl-icon-warn.gif) <a name="bkmk_ga_instalpatch"></a> 安裝修補程式需求 (GA)
**問題和對客戶的影響：** Microsoft 發現影響 Microsoft VC++ 2013 Runtime 二進位檔的問題，SQL Server 2016 必須安裝這些二進位檔。 已提供修正此問題的更新。 如果不安裝 VC Runtime 二進位檔的這項更新，SQL Server 2016 就可能在特定情況下遇到穩定性問題。 安裝 SQL Server 2016 之前，請先檢查電腦是否需要 [KB 3164398](https://support.microsoft.com/kb/3164398)中所述的填補。 修補程式也包含在 [SQL Server 2016 RTM 的累計更新套件 1 (CU1)](https://www.microsoft.com/download/details.aspx?id=53338)。

**解決方案：** 使用下列其中一個解決方案：

- 安裝 [KB 3138367 - Visual C++ 2013 年和 Visual C++ 的可轉散發套件的更新](https://support.microsoft.com/kb/3138367)。 此 KB 是慣用的解決方式。 您可以在安裝 SQL Server 2016 之前或之後安裝此更新。

    如已安裝 SQL Server 2016，請依序執行下列步驟︰

    1.  下載適當的 *vcredist_\*exe*。
    1.  停止資料庫引擎所有執行個體的 SQL Server 服務。
    1.  安裝 **KB 3138367**。
    1.  重新啟動電腦。


 - 安裝  [KB 3164398 - SQL Server 2016 MSVCRT 必要條件的重大更新](https://support.microsoft.com/kb/3164398)。

    如果使用 **KB 3164398**，就可以在 SQL Server 安裝期間，透過 Microsoft Update 或從 Microsoft 下載中心安裝。

    - **在 SQL Server 2016 安裝期間：** 如果執行 SQL Server 安裝程式的電腦可以存取網際網路，則 SQL Server 安裝程式會檢查更新是否為完整 SQL Server 安裝的一部分。 如果您接受更新，安裝程式會在安裝期間下載並更新二進位檔案。

    - **Microsoft Update：** Microsoft Update 現提供更新作為重要的非安全性 SQL Server 2016 更新。 透過 Microsoft Update 安裝，SQL Server 2016 會在更新後要求重新啟動伺服器。

    - **下載中心：** 最後，Microsoft 下載中心會提供更新。 您可以下載更新的軟體，將它安裝在有 SQL Server 2016 的伺服器上。


### <a name="stretch-database"></a><a name="bkmk_ga_stretch"></a>Stretch Database

#### <a name="problem-with-a-specific-character-in-a-database-or-table-name"></a>資料庫或資料表名稱中的特定字元問題

**問題和對客戶的影響：** 嘗試在資料庫或資料表上啟用 Stretch Database 會失敗，並發生錯誤。 如果物件的名稱包含從小寫轉換為大寫時視為不同字元的字元，則會發生此問題。 導致此問題的字元範例是字元 "ƒ" (鍵入 ALT+159 所建立)。

**因應措施：** 如果您想要啟用資料庫或資料表的 Stretch Database，重新命名物件並移除問題字元是唯一的選項。

#### <a name="problem-with-an-index-that-uses-the-include-keyword"></a>使用 INCLUDE 關鍵字的索引問題

**問題和對客戶的影響：** 如果資料表的索引使用 INCLUDE 關鍵字在索引中包含其他資料行，則嘗試啟用此資料表的 Stretch Database 會因發生錯誤而失敗。

**因應措施：** 卸除使用 INCLUDE 關鍵字的索引，啟用資料表的 Stretch Database，然後重新建立索引。 如果這樣做，請務必依照貴組織的維護作法和原則，以確保對受影響資料表的使用者造成最小的影響或不受影響。

### <a name="query-store"></a><a name="bkmk_ga_query_store"></a>Query Store

#### <a name="problem-with-automatic-data-cleanup-on-editions-other-than-enterprise-and-developer"></a>Enterprise 和 Developer 以外版本的自動資料清除問題

 **問題和對客戶的影響：** Enterprise 和 Developer 以外版本的自動資料清除會失敗。
因此，如果不手動清除資料，查詢存放區所使用的空間會與日俱增，直到達到設定的限制。 如果不降低，此問題也會填滿為錯誤記錄檔配置的磁碟空間，因為每次嘗試執行清除都會產生傾印檔案。 啟動清除的期間長短取決於工作負載的頻率，但不超過 15 分鐘。

 **因應措施：** 如果您打算在 Enterprise 和 Developer 以外的版本上使用查詢存放區，您必須明確關閉清除原則。 它可以從 SQL Server Management Studio ([資料庫屬性] 頁面)，或透過 TRANSACT-SQL 指令碼完成︰

```ALTER DATABASE <database name> SET QUERY_STORE (OPERATION_MODE = READ_WRITE, CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 0), SIZE_BASED_CLEANUP_MODE = OFF)```

此外，請考慮手動清除選項，以防止查詢存放區轉換為唯讀模式。 例如，執行下列查詢，定期清理整個資料空間︰

```ALTER DATABASE <database name> SET QUERY_STORE CLEAR```

亦請執行下列查詢存放區預存程序，定期清理執行階段統計資料、特定的查詢或計劃︰

- `sp_query_store_reset_exec_stats`

- `sp_query_store_remove_plan`

- `sp_query_store_remove_query`


###  <a name="product-documentation-ga"></a><a name="bkmk_ga_docs"></a> 產品文件 (GA)
 **問題和對客戶的影響：** SQL Server 2016 文件的可下載版本尚未提供。 當您嘗試使用 Help Library 管理員 **從線上安裝內容**時，您會看到 SQL Server 2012 及 SQL Server 2014 文件，但沒有 SQL Server 2016 文件的選項。

 **因應措施：** 使用下列其中一項因應措施：

 ![管理 SQL Server 的說明設定](../sql-server/media/docs-sql2016-managehelpsettings.png "管理 SQL Server 的說明設定")

-   使用選項 [選擇線上或本機說明]  ，並設定「我想要使用線上說明」的說明。

-   使用選項 [從線上安裝內容]  ，並下載 SQL Server 2014 內容。

 **F1 說明：** 依設計，當您在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中按下 F1 時，瀏覽器即會顯示 F1 說明文章的線上版本。 此問題是以瀏覽器為基礎的說明，即使您已設定並安裝本機說明也是一樣。

**更新內容：** 在 SQL Server Management Studio 和 Visual Studio 中，說明檢視器應用程式可能會在新增文件程序期間停止回應。 若要解決此問題，請完成下列步驟。 如需此問題的詳細資訊，請參閱 [Visual Studio 說明檢視器凍結在啟動顯示畫面上](https://msdn.microsoft.com/library/mt654096.aspx)。

* 以 [記事本] 開啟 %LOCALAPPDATA%\Microsoft\HelpViewer2.2\HlpViewer_SSMS16_en-US.settings | HlpViewer_VisualStudio14_en-US.settings 檔案，將下列程式碼中的日期變更為未來的日期。

```
     Cache LastRefreshed="12/31/2017 00:00:00"
```

## <a name="additional-information"></a>其他資訊
+ [SQL Server 2016 安裝](../database-engine/install-windows/installation-for-sql-server-2016.md)
+ [SQL Server 更新中心 - 所有已支援版本的連結和資訊](https://msdn.microsoft.com/library/ff803383.aspx)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png "MS_Logo_X-Small")
