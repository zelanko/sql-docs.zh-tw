---
title: "SQL Server 2017 的新功能 | Microsoft Docs"
ms.custom: 
ms.date: 10/19/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b57f375-9242-4bb2-9d4b-c560d5a93524
caps.latest.revision: "71"
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 9abddcd8544221c5d6dff0eeb12dc441df632933
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="whats-new-in-sql-server-2017"></a>SQL Server 2017 的新功能
SQL Server 2017 將 SQL Server 的強大能力整合到 Linux、以 Linux 為基礎的 Docker 容器和 Windows 中，是讓 SQL Server 成為可選擇開發語言、資料類型、內部部署或雲端以及作業系統之平台的重要一步。 本主題摘要說明特定功能區的新功能，並包含其他詳細資料的連結。 如需 Linux 上之 SQL Server 的詳細資訊，請參閱 [Linux 上的 SQL Server](https://docs.microsoft.com/sql/linux/) 文件

[![從 Evaluation Center 下載](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=829477) **試用看看：** [下載 SQL Server 2017 版 - 2017 年 10月：](http://go.microsoft.com/fwlink/?LinkID=829477)。

> [!NOTE]
> 除了下列變更，在正式發行版本之後還會定期發行累積更新。 這些累積更新提供許多改善和修正程式。 如需最新 CU 版本的資訊，請參閱 [SQL Server 2017 累積更新](http://aka.ms/sql2017cu)。

## <a name="sql-server-2017-database-engine"></a>SQL Server 2017 資料庫引擎

SQL Server 2017 包含許多新的 Database Engine 功能、增強功能和效能提升。 
- **CLR 組件**現在可以新增至白名單，以解決 CTP 2.0 中所述的 `clr strict security` 問題。 新增了 [sp_add_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md)、[sp_drop_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) 和 [sys.trusted_asssemblies](../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md) 以支援信任組件的白名單 (RC1)。  
- **繼續線上索引重建**可從容錯移轉至複本或磁碟空間不足等失敗後的停止處繼續線上索引重建作業，或暫停並於稍後繼續線上索引重建作業。 請參閱 [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md) 和[線上索引作業的指導方針](../relational-databases/indexes/guidelines-for-online-index-operations.md)。 (CTP 2.0)
- ALTER DATABASE SCOPED CONFIGURATION 的 **IDENTITY_CACHE** 選項可讓您在伺服器意外地重新啟動或容錯移轉至次要伺服器時，避免識別欄位的值出現間隙。 請參閱 [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。 (CTP 2.0)
- 新一代的查詢處理功能改進會調整最佳化策略，使其符合您應用程式工作負載的執行階段條件。 為了這個第一版**自適性查詢處理**功能家族，我們推出了三項新的功能更新：**批次模式自適性聯結**、**批次模式記憶體授與回饋**，以及適用於多陳述式資料表值函式的**交錯執行**。  請參閱 [SQL 資料庫中的自適性查詢處理](../relational-databases/performance/adaptive-query-processing.md)。
- **自動資料庫調整**可深入探索潛在的查詢效能問題、建議解決方法，而且可以自動修正找到的問題。 請參閱[自動調整](../relational-databases/automatic-tuning/automatic-tuning.md)。 (CTP 2.0)
- 新增可模型化多對多關聯性的**圖表資料庫功能**，包括新增用於建立節點和邊緣資料表的 [CREATE TABLE](../t-sql/statements/create-table-sql-graph.md) 語法，以及用於查詢的關鍵字 [MATCH](../t-sql/queries/match-sql-graph.md)。 請參閱[圖形處理與 SQL Server 2017](../relational-databases/graphs/sql-graph-overview.md)。 (CTP 2.0)
- 預設會啟用 sp_configure 選項 `clr strict security` 以增強 CLR 組件的安全性。 請參閱 [CLR 嚴格安全性](../database-engine/configure-windows/clr-strict-security.md)。 (CTP 2.0)
- 安裝程式現在可針對每個檔案最多指定 **256 GB** (262,144 MB) 的初始 tempdb 檔案大小，並在檔案大小設定為大於 1 GB 且 IFI 未啟用時出現警告。 (CTP 2.0)
- [sys.dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md) 中的 **modified_extent_page_count** 資料行會追蹤每個資料庫檔案中的差異變更，並啟用智慧型備份解決方案，以根據資料庫中已變更頁面的百分比來執行差異備份或完整備份。 (CTP 2.0)
- [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md) T-SQL 語法現在支援使用 **ON** 關鍵字，將資料表載入使用者預設值以外的檔案群組中。 (CTP 2.0)
- 現在支援在屬於 **AlwaysOn 可用性群組**的所有資料庫 (包括屬於相同執行個體的資料庫) 之間進行跨資料庫交易。 請參閱[交易 - AlwaysOn 可用性群組和資料庫鏡像](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md) (CTP 2.0)
- 新的 [可用性群組] 功能包括無叢集支援、最小複本認可可用性群組設定，以及 Windows-Linux 跨 OS 移轉和測試。 (CTP 1.3)
- 新的動態管理檢視：
    - [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md) 會公開摘要層級屬性和交易記錄檔的相關資訊，適用於監視交易記錄健全狀況。 (CTP 2.1)
    - [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md) 會追蹤每個資料庫的版本存放區使用量，適用於主動根據每個資料庫的版本存放區使用量來規劃 tempdb 大小。 (CTP 2.0)
    - [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md) 會公開 VLF 資訊，以便監視、警示及防止潛在交易記錄問題。 (CTP 2.0)
    - [sys.dm_db_stats_histogram](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 是可查看統計資料的新動態管理檢視。 (CTP 1.3)
    - **sys.dm_os_host_info** 提供 Windows 和 Linux 作業系統資訊。 (CTP 1.0)
- **Database Tuning Advisor (DTA)** 包含其他選項並提升效能。 (CTP 1.2)
- **記憶體內部增強功能**包括經記憶體最佳化的資料表中之計算資料行的支援，以及原生編譯模組中之 JSON 函式和 CROSS APPLY 運算子的完整支援。 (CTP 1.1)
- 新的**字串函式**包括 CONCAT_WS、TRANSLATE 和 TRIM，而且 STRING_AGG 函式現在支援 WITHIN GROUP。 (CTP 1.1)
- CSV 和 Azure Blob 檔案有新的**大量存取選項** (BULK INSERT 和 OPENROWSET(BULK...))。 (CTP 1.1)
- **記憶體最佳化物件的增強功能**包括經記憶體最佳化資料表的 sp_spaceused 和 8 個索引限制排除、經記憶體最佳化資料表和原生編譯 T-SQL 模組的 sp_rename，以及原生編譯 T-SQL 模組的 CASE 和 TOP (N) WITH TIES。 經記憶體最佳化檔案群組檔案現在可以在 Azure 儲存體上儲存、備份及還原。 (CTP 1.0)
- **DATABASE SCOPED CREDENTIAL** 是新的安全性實體類別，支援 CONTROL、ALTER、REFERENCES、TAKE OWNERSHIP 和 VIEW DEFINITION 權限。 ADMINISTER DATABASE BULK OPERATIONS 現在會顯示在 sys.fn_builtin_permissions 中。 (CTP 1.0)
- 新增了資料庫 **COMPATIBILITY_LEVEL 140**。 (CTP 1.0)  

如需詳細資訊，請參閱 [SQL Server 2017 Database Engine 的新功能](~/database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md)。

## <a name="sql-server-2017-integration-services-ssis"></a>SQL Server 2017 Integration Services (SSIS)
- SSIS 中新的 [相應放大] 功能有下列新的和已變更的功能。 如需詳細資訊，請參閱 [SQL Server 2017 Integration Services 的新功能](~/integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)。 (RC1)
    -   相應放大主機現在支援高可用性。
    -   相應放大背景工作中執行記錄的容錯移轉處理已獲得改善。
    -   為了一致性和可讀性，預存程序 **[catalog].[create_execution]** 的參數 *runincluster* 已重新命名為 *runinscaleout*。
    -   SSIS 目錄有新的全域屬性，可指定執行 SSIS 套件的預設模式。
- 在 SSIS 的新 [相應放大] 功能中，您現在可以在觸發執行時使用 **Use32BitRuntime** 參數。 (CTP 2.1)
- SQL Server 2017 Integration Services (SSIS) 現在支援 **Linux 上的 SQL Server**，並新增套件讓您從命令列在 Linux 上執行 SSIS 套件。 如需詳細資訊，請參閱[宣佈對 Linux 提供 SSIS 支援的部落格文章](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)。 (CTP 2.1)
- SSIS 的新 [相應放大] 功能讓您更容易在多部電腦上執行 SSIS。 請參閱 [Integration Services 相應放大](~/integration-services/scale-out/integration-services-ssis-scale-out.md)。(CTP 1.0)
- OData 來源和 OData 連線管理員現在支援連線到 Microsoft Dynamics AX Online 和 Microsoft Dynamics CRM Online 的 OData 摘要。 (CTP 1.0)

如需詳細資訊，請參閱 [SQL Server 2017 Integration Services 的新功能](~/integration-services/what-s-new-in-integration-services-in-sql-server-2017.md)。

## <a name="sql-server-2017-master-data-services-mds"></a>SQL Server 2017 Master Data Services (MDS)
- 從 SQL Server 2012、SQL Server 2014 及 SQL Server 2016 升級至 SQL Server 2017 Master Data Services 時的體驗與效能已獲得改善。 
- 您現在可以在 Web 應用程式的 [總管] 頁面中，檢視實體、集合和階層的排序清單。
- 使用暫存預存程序來暫存數百萬筆記錄的效能已獲得改善。
- 在 [管理群組] 頁面上展開 [實體] 資料夾以指派模型權限時的效能已獲得改善。 [管理群組] 頁面位於 Web 應用程式的 [安全性] 區段。 如需效能改進的詳細資訊，請參閱 [https://support.microsoft.com/help/4023865?preview](https://support.microsoft.com/help/4023865?preview)。 如需指派權限的詳細資訊，請參閱[指派模型物件權限 (Master Data Services)](../master-data-services/assign-model-object-permissions-master-data-services.md)。

## <a name="sql-server-2017-analysis-services-ssas"></a>SQL Server 2017 Analysis Services (SSAS) 
SQL Server Analysis Services 2017 為表格式模型引進許多增強功能。 其中包括：
- 以表格式模型作為 Analysis Services 的預設安裝選項。 (CTP 2.0)
- 物件層級安全性，以保護表格式模型的中繼資料。 (CTP 2.0)
- 日期關聯性，以輕鬆地根據日期欄位建立關聯性。 (CTP 2.0)
- 新的 [取得資料] (Power Query) 資料來源，以及 M 查詢的現有 DirectQuery 資料來源支援。 (CTP 2.0) 
- SSDT 的 DAX 編輯器。 (CTP 2.0)
- 編碼提示，這是一種進階功能，可針對大型記憶體內部表格式模型的資料重新整理進行最佳化。 (CTP 1.3)
- 支援表格式模型的 **1400 相容性層級**。 若要建立新的或升級現有的表格式模型專案至 1400 相容性層級，請下載並安裝 [SQL Server Data Tools (SSDT) 17.0 RC2](https://go.microsoft.com/fwlink?LinkId=837939)。 (CTP 1.1)
- 1400 相容性層級之表格式模型的最新 [取得資料] 體驗。 請參閱 [Analysis Services 小組部落格](https://blogs.msdn.microsoft.com/analysisservices/2016/12/16/introducing-a-modern-get-data-experience-for-sql-server-2017-on-windows-ctp-1-1-for-analysis-services/)。 (CTP 1.1)
- [隱藏成員] 屬性，可隱藏不完全階層中的空白成員。 (CTP 1.1)
- 新的 [詳細資料列] 終端使用者動作，可**顯示彙總資訊的詳細資料**。 [SELECTCOLUMNS](https://msdn.microsoft.com/library/mt761759.aspx) 和 **DETAILROWS** 函式，可建立詳細資料列運算式。 (CTP 1.1)
- DAX **IN** 運算子，可指定多個值。 (CTP 1.1)

如需詳細資訊，請參閱 [SQL Server Analysis Services 2017 的新功能](~/analysis-services/what-s-new-in-sql-server-analysis-services-2017.md)。

## <a name="sql-server-2017-reporting-services-ssrs"></a>SQL Server 2017 Reporting Services (SSRS)
無法再透過 SQL Server 安裝程式安裝 SQL Server Reporting Services。 請前往 Microsoft 下載中心以[下載 Microsoft SQL Server 2017 Reporting Services](https://www.microsoft.com/download/details.aspx?id=55252)。 
- 報表現在提供留言功能，可新增觀點並與其他人共同作業。 您也可以在留言內包含附件。
- 在最新版的報表產生器和 SQL Server Data Tools 中，您可以藉由在查詢設計工具中拖放所需的欄位，來對支援的 SQL Server Analysis Services 表格式資料模型建立原生 DAX 查詢。 請參閱 [Reporting Services 部落格](https://blogs.msdn.microsoft.com/sqlrsteamblog/2017/03/09/query-designer-support-for-dax-now-available-in-report-builder-and-sql-server-data-tools/)。
- 為了進行現代化應用程式的開發和自訂，SSRS 現在支援完全符合 OpenAPI 的 RESTful API。 您現在可以在 [swaggerhub](https://app.swaggerhub.com/apis/microsoft-rs/SSRS/2.0) 上找到完整的 API 規格和文件。

如需詳細資訊，請參閱 [SQL Server Reporting Services (SSRS) 的新功能](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)。

## <a name="machine-learning-in-sql-server-2017"></a>SQL Server 2017 中的機器學習服務 

SQL Server R Services 現在已重新命名為 **SQL Server Machine Learning 服務**，以反映 R 語言以外的 Python 支援。 您可以使用 Machine Learning 服務 (資料庫內) 在 SQL Server 中執行 R 或 Python 指令碼，或安裝 **Microsoft Machine Learning 伺服器 (獨立式)** 來部署及取用不需要 SQL Server 的 R 與 Python 模型。 

SQL Server 開發人員現在能夠存取廣大的 Python ML 及 AI 程式庫，可用於開放原始碼生態系統，且附有 Microsoft 的最新創新：

- **revoscalepy** - RevoScaleR 的這個 Python 對應項目包括了線性及羅吉斯迴歸的平行演算法、決策樹、梯度上升樹及隨機森林，以及一組用於資料轉換和資料移動的豐富 API、遠端計算內容及資料來源。
- **microsoftml** - 這個機器學習演算法及轉換的最新型套件具有 Python 繫結，包括深度類神經網路、迅速的決策樹及決策森林，以及用於線性及羅吉斯迴歸的最佳化演算法。 您也可以取得以 ResNet 模型為基礎的預先訓練模型，用於影像擷取或情感分析。
- **透過 T-SQL 進行 Python 作業化** - 使用預存程序 `sp_execute_external_script` 輕鬆部署 Python 程式碼。 將資料從 SQL 串流到 Python 處理序及使用 MPI 通道平行處理，以獲得優異效能。
- **SQL Server 計算內容中的 Python** - 資料科學家及開發人員可以在遠端從他們的開發環境執行 Python 程式碼，不必四處移動資料即可探索資料及開發模型。
- **原生計分** -  Transact-SQL 中的 PREDICT 函式可用來在任何 SQL Server 2017 執行個體中執行計分，即使未安裝 R 亦然。 您需要採取的動作是使用其中一個支援的 RevoScaleR 與 revoscalepy 演算法將模型定型，並將模型儲存為新的壓縮二進位檔格式。
- **套件管理** - T-SQL 現在支援 CREATE EXTERNAL LIBRARY 陳述式，可讓 DBA 更能全面管理 R 套件。 使用角色來控制權限或共用套件存取權、將 R 套件儲存在資料庫中並與使用者共用這些套件。
- **效能改進** - 預存程序 `sp_execute_external_script` 已最佳化，可支援資料行存放區的批次模式執行。


如需詳細資訊，請參閱 [SQL Server Machine Learning 服務的新功能](~/advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)。

## <a name="next-steps"></a>後續的步驟
- 請參閱 [SQL Server 2017 版本資訊](sql-server-2017-release-notes.md)。
- 了解 [Linux 上的 SQL Server 2017 新功能](https://docs.microsoft.com/sql/linux/sql-server-linux-whats-new)。
- 了解 [SQL Server 2016 的新功能](what-s-new-in-sql-server-2016.md)。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
