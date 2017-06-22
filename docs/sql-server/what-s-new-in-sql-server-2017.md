---
title: "什麼 & #39 的新 SQL Server 2017 |Microsoft 文件"
ms.custom: 
ms.date: 06/19/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b57f375-9242-4bb2-9d4b-c560d5a93524
caps.latest.revision: 71
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: aa08b5e7de9bb317fd781a98ee5d829431b92df6
ms.openlocfilehash: 66c9bc4f2cba20076c357d27fdfacbc767a94c5c
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="what39s-new-in-sql-server-2017"></a>什麼 & #39 的新 SQL Server 2017
SQL Server 2017 表示讓 SQL Server 提供您選擇的開發語言、 資料類型、 在內部部署雲端，以及跨作業系統將 SQL Server 的強大結合至 Linux、 linux Docker 容器和 Windows 平台的主要步驟。

本主題是最新的社群技術預覽 (CTP) 版本和更多詳細的什麼是特定功能區域的新資訊的連結中新增功能的摘要。

![info_tip](../sql-server/media/info-tip.png) 在 Linux 上執行 SQL Server！ 如需詳細資訊，請參閱：
-  [在 Linux 上的 SQL Server 2017 的新功能](https://docs.microsoft.com/sql/linux/sql-server-linux-whats-new)
-  [SQL Server on Linux Documentation](https://docs.microsoft.com/sql/linux/)


**現在就試試看：**    
   -   [![從評估中心下載](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477) **[下載 SQL Server 2017 Community Technology Preview](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="whats-new-in-sql-server-2017-ctp-21-may-2017"></a>新功能 SQL Server 2017 CTP 2.1 (可能 2017)
### <a name="sql-server-database-engine"></a>SQL Server Database Engine  
- 新的 DMF， [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)，導入了公開摘要層級的屬性和交易記錄檔的詳細資訊，則適用於監視交易記錄檔的健全狀況。  
- 此 CTP 中包含錯誤修正和資料庫引擎的效能改進。
- 如需詳細的 2017年清單 CTP 增強功能，在先前的 CTP 版本中，請參閱[What's New in SQL Server 2017 (Database Engine)](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md)。

### <a name="sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS)
- 無法再供透過 SQL Server 安裝程式 CTP 2.1 為準，安裝 SQL Server Reporting Services。
- 註解現在可供報表。 註解可讓您加入至報表中的檢視方塊，並在您的組織與其他人共同作業。 您也可以包含附件與您的註解。
- 如需 SSRS 新功能的詳細資訊 (包括舊版的詳細資訊)，請參閱 [Reporting Services 的新功能](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)。 
- Power BI 報表伺服器的相關資訊，請參閱[開始使用 Power BI 報表伺服器](https://powerbi.microsoft.com/documentation/reportserver-get-started/)。

### <a name="sql-server-machine-learning-services"></a>SQL Server 機器學習服務
- 在此 CTP 中沒有任何新的機器學習服務功能。
- 如需詳細的機器學習服務功能的新資訊，包括從先前的 Ctp 的詳細資料請參閱[What's New in SQL Server 機器學習服務](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)。  

### <a name="sql-server-analysis-services-ssas"></a>SQL Server Analysis Services (SSAS)
- 此 CTP 中沒有任何 SSAS 新功能。  
- 如需有關改善和 bug 修正，在此版本的詳細資訊，請參閱[What's New in SQL Server 2017 Analysis Services](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md)。  

### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
-   您現在可以使用**Use32BitRuntime**參數。
-   已改善的記錄效能。
- 如需詳細的 SSIS 功能的新資訊，包括從先前的 Ctp 的詳細資料請參閱[What's New in SQL Server 2017 Integration Services](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)。  

![horizontal_bar](../sql-server/media/horizontal-bar.png)
## <a name="whats-new-in-sql-server-2017-ctp-20-april-2017"></a>新功能 SQL Server 2017 CTP 2.0 (第 2017 年 4 月)
### <a name="sql-server-database-engine"></a>SQL Server Database Engine
- **繼續線上索引重建**。 繼續線上索引重建可讓您繼續在失敗後的停止處的線上索引重建作業。 例如，在容錯移轉為 replica，或者沒有足夠的磁碟空間的情況。 您可以也暫停，並於之後繼續線上索引重建作業。 例如，您可能需要暫時釋出系統資源，才能執行高優先順序的工作，或如果可用的維護期間太短，大型資料表完成索引重建，在另一個 miniatous 視窗。 最後，可繼續線上索引重建不需要重要的記錄空間，這可讓您可繼續重建作業執行時，執行記錄截斷。 請參閱[ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md)和[線上索引作業的指導方針](../relational-databases/indexes/guidelines-for-online-index-operations.md)。
- **ALTER DATABASE SCOPED CONFIGURATION IDENTITY_CACHE 選項**。 改變資料庫範圍組態 T-SQL 陳述式中加入了新選項 IDENTITY_CACHE。 當這個選項設為 OFF 時，間距可以避免在身分識別資料行的值，萬一意外重新啟動或容錯移轉至次要伺服器的伺服器。 請參閱[ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。  
- CLR 會在.NET Framework 中，已不再支援做為安全性界限使用的程式碼存取安全性 (CAS)。 CLR 組件，以建立`PERMISSION_SET = SAFE`可能能夠存取外部系統資源、 呼叫 unmanaged 程式碼，以及取得 sysadmin 權限。 開頭為[!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]、`sp_configure`選項呼叫`clr strict security`已引入來增強安全性的 CLR 組件。 `clr strict security`根據預設，已啟用，並將`SAFE`和`EXTERNAL_ACCESS`組件如同它們已標示`UNSAFE`。 `clr strict security`選項可以停用回溯相容性，但不是建議使用。 Microsoft 建議所有的組件簽署的憑證或非對稱金鑰對應登入已被授與`UNSAFE ASSEMBLY`master 資料庫中的權限。 如需詳細資訊，請參閱[CLR 嚴格的安全性](../database-engine/configure-windows/clr-strict-security.md)。  
- 圖形模型多對多關聯性的資料庫功能。 這包括新[CREATE TABLE](../t-sql/statements/create-table-sql-graph.md)建立節點和邊緣資料表，以及關鍵字的語法[相符](../t-sql/queries/match-sql-graph.md)查詢。 如需詳細資訊，請參閱[圖形處理與 SQL Server 2017](../relational-databases/graphs/sql-graph-overview.md)。   
- 自動調整是提供深入了解潛在的查詢效能問題的資料庫功能，它可以建議解決方案，並自動修正識別問題。 的自動調整[!INCLUDE[ssnoversion](../includes/ssnoversion.md)]、 潛在的效能問題偵測到，而且可讓您套用的矯正措施時通知您，或者讓[!INCLUDE[ssde](../includes/ssde-md.md)]自動修正效能問題。 如需詳細資訊，請參閱[自動微調](../relational-databases/automatic-tuning/automatic-tuning.md)。  
-   批次模式適應性加入改善 （在資料庫相容性 140） 計畫品質。
-   多重陳述式來改善 （在資料庫相容性 140） 下的計劃品質的 T-SQL tvf 的交錯的執行。
- 查詢存放區現在也會追蹤等候統計資料的摘要資訊。 追蹤每個查詢存放區中的查詢等候統計資料類別可讓效能疑難排解體驗，提供，更詳細的資訊，深入了解工作負載效能，同時保留查詢存放區的重要優點其瓶頸的下一個層級。
- DTC 支援 Alwayson 可用性群組的所有資料庫屬於可用性群組，包括屬於相同的執行個體的資料庫之間的跨資料庫交易。 如需詳細資訊，請參閱[交易-Alwayson 可用性群組和資料庫鏡像](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md)
- 新的資料行**modified_extent_page_count**中引進[sys.dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)以追蹤資料庫的每個資料庫檔案差異變更。
- [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md)現可支援的檔案群組以外的使用者使用的預設檔案群組中載入資料表**ON**關鍵字。
- SQL Server 安裝程式支援最多指定初始的 tempdb 檔案大小**256 GB (262,144 MB)**每個檔案，但出現警告，如果檔案大小設定為值大於**1GB**和如果 IFI 未啟用。
- 新的動態管理檢視 (DMV) [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md)已引入來追蹤每個資料庫的版本存放區使用量。
- 新的 DMV [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)已引入來公開類似於 DBCC LOGINFO VLF 資訊。
- 系統版本設定時態表現在支援 CASCADE DELETE 和 UPDATE CASCADE。
- 此 CTP 中包含資料庫引擎的錯誤修正。
- 如需詳細的 2017年清單 CTP 增強功能，在先前的 CTP 版本中，請參閱[What's New in SQL Server 2017 (Database Engine)](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md)。   

### <a name="sql-server-machine-learning-services"></a>SQL Server 機器學習服務
- SQL Server R 服務有新的名稱，以反映在 CTP 2.0 中的 Python 語言的支援。 您現在可以使用 SQL Server 機器學習服務 （資料庫） 執行 SQL Server 中的 R 或 Python 指令碼。 或者，安裝 Microsoft 機器學習伺服器來部署，並使用 R 和 Python 的模型不需要 SQL Server （獨立）。 
- 兩個平台包含分散式的機器學習和 Microsoft R （版本 9.1.0） 的最新版本的新 MicrosoftML 演算法。
- 如需詳細資訊，請參閱[機器學習最新消息](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)。

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="whats-new-in-sql-server-2017-ctp-14-march-2017"></a>新功能 SQL Server 2017 CTP 1.4 (第 2017 年 3 月)
### <a name="sql-server-database-engine"></a>SQL Server Database Engine
- 此 CTP 中沒有任何新的資料庫引擎功能。
- 此 CTP 中包含資料庫引擎的錯誤修正。
- 如需詳細的 2017年清單 CTP 增強功能，在先前的 CTP 版本中，請參閱[What's New in SQL Server 2017 (Database Engine)](../database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md)。

### <a name="sql-server-r-services"></a>SQL Server R 服務
- 此 CTP 中沒有任何新 R Services 功能。
- 如需 R Services 新功能的詳細資訊，包括舊版 CTP 的詳細資訊，請參閱 [SQL Server R Services 的新功能](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md)。  

### <a name="sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS)
- 此 CTP 中沒有任何 SSRS 新功能。
- 如需 SSRS 新功能的詳細資訊 (包括舊版的詳細資訊)，請參閱 [Reporting Services 的新功能](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)。 

### <a name="sql-server-analysis-services-ssas"></a>SQL Server Analysis Services (SSAS)
- 此 CTP 中沒有任何 SSAS 新功能。  
- 如需詳細資訊，包括 Analysis Services 的最新預覽版本的 SSDT 和 SSMS 中新功能，請參閱[What's New in Analysis Services 2017](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md)。  

### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
- 此 CTP 中沒有任何 SSIS 新功能。
- 如需詳細的 SSIS 功能的新資訊，包括從先前的 Ctp 的詳細資料請參閱[What's New in Integration Services 2017](../integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)。  

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="whats-new-in-sql-server-2017-ctp-13-february-2017"></a>新功能 SQL Server 2017 CTP 1.3 (第 2017 年 2 月)
### <a name="sql-server-database-engine"></a>SQL Server Database Engine
- 間接檢查點效能的改進。
- 新增無叢集可用性群組的支援。
- 新增最小複本認可可用性群組的設定。
- 可用性群組現在可於 Windows 和 Linux 運作，以進行跨作業系統移轉及測試。
- 加入暫時資料表保留原則支援。 如需詳細資訊，請參閱[管理保留歷程記錄資料的系統版本設定時態表中](../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md#using-temporal-history-retention-policy-approach)。
- 新的 DMV SYS.DM_DB_STATS_HISTOGRAM
- 線上非叢集資料行存放區索引組建，並重建所新增的支援
- 5 種可傳回 Linux 處理序相關資訊的新動態管理檢視。 如需詳細資訊，請參閱 [Linux 處理序動態管理檢視](../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md)。   
- 新增[sys.dm_db_stats_histogram (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) ，以供檢查統計資料。

### <a name="sql-server-analysis-services-ssas-ctp-13"></a>SQL Server Analysis Services (SSAS) (CTP 1.3)
- 編碼提示 - 這是一種進階功能，可針對大型記憶體內表格式模型的處理 (資料重新整理) 進行最佳化。 若要進一步了解，請參閱[What's New in Analysis Services 2017](../analysis-services/what-s-new-in-sql-server-analysis-services-2017.md)。 


![horizontal_bar](../sql-server/media/horizontal-bar.png)

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) 與 SQL Server 工程團隊交流 
- [Stack Overflow (tag sql-server)](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect - 報告錯誤及要求功能](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - 有關 R 的一般討論](https://www.reddit.com/r/SQLServer/)

## <a name="see-also"></a>另請參閱    
- ![版本資訊](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) [SQL Server 2017 版本資訊](../sql-server/sql-server-2017-release-notes.md)。 
- [版本支援的功能](https://msdn.microsoft.com/library/cc645993.aspx)
- [硬體及軟體安裝需求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
- [SQL Server 安裝精靈](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
- [安裝 SQL Server 服務更新](http://msdn.microsoft.com/library/6df72a78-6b36-4bc1-948e-04b4ebe46094)
 
 ![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)

