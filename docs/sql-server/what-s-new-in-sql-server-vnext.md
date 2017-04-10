---
title: "SQL Server vNext 的新功能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "server-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0b57f375-9242-4bb2-9d4b-c560d5a93524
caps.latest.revision: 71
author: "craigg-msft"
ms.author: "craigg"
manager: "jhubbard"
caps.handback.revision: 65
---
# SQL Server vNext 的新功能
SQL Server vNext 代表將 SQL Server 發展為平台的主要步驟，可選擇開發語言、資料類型、雲端內部部署，以及將 SQL Server 威力帶入 Linux、以 Linux 為基礎的 Docker 容器和 Windows 的跨作業系統。

本主題是最新 Community Technical Preview (CTP) 版本的新功能摘要，連結至特定功能區域更詳細的新功能資訊。

![info_tip](../sql-server/media/info-tip.png) 在 Linux 上執行 SQL Server！ 如需詳細資訊，請參閱：
-  [What's new for SQL Server vNext on Linux](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-whats-new) (Linux 上的 SQL Server vNext 新功能)
-  [SQL Server on Linux Documentation](https://docs.microsoft.com/en-us/sql/linux/) (Linux 上的 SQL Server 文件)


**現在就試試看：**    
   -   [![從評估中心下載](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477) **[下載 SQL Server vNext Community Technology Preview](http://go.microsoft.com/fwlink/?LinkID=829477)**


## <a name="whats-new-in-sql-server-vnext-ctp-13-february-2017"></a>SQL Server vNext CTP 1.3 的新功能 (2017 年 2 月)
### <a name="sql-server-database-engine"></a>SQL Server Database Engine
- 間接檢查點效能的改進。
- 新增無叢集可用性群組的支援。
- 新增最小複本認可可用性群組的設定。
- 可用性群組現在可於 Windows 和 Linux 運作，以進行跨作業系統移轉及測試。
- 新增時態表保留原則的支援，
- 新的 DMV SYS.DM_DB_STATS_HISTOGRAM
- 新增建置及重建線上非叢集資料行存放區索引的支援
- 5 種可傳回 Linux 處理序相關資訊的新動態管理檢視。 如需詳細資訊，請參閱 [Linux 處理序動態管理檢視](../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md)。   
- 新增 [sys.dm_db_stats_histogram (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)，以供檢查統計資料。

### <a name="sql-server-analysis-services-ssas-ctp-13"></a>SQL Server Analysis Services (SSAS) (CTP 1.3)
- 編碼提示 - 這是一種進階功能，可針對大型記憶體內表格式模型的處理 (資料重新整理) 進行最佳化。 若要深入了解，請參閱 [Analysis Services vNext 的新功能](../analysis-services/what-s-new-in-sql-server-analysis-services-vnext.md)。 

## <a name="whats-new-in-sql-server-vnext-ctp-12-january-2017"></a>SQL Server vNext CTP 1.2 的新功能 (2017 年 1 月)
### <a name="sql-server-database-engine"></a>SQL Server Database Engine
- 非叢集資料行存放區的線上索引建置及重建支援。
- 此 CTP 中也包含 Database Engine 的錯誤修正。
- 如需舊 CTP 版本中 vNext CTP 增強功能的詳細清單，請參閱 [SQL Server vNext 的新功能 (Database Engine)](../database-engine/configure-windows/what-s-new-in-sql-server-vnext-database-engine.md)。

### <a name="sql-server-r-services"></a>SQL Server R 服務
- 此 CTP 中沒有任何新 R Services 功能。
- 如需 R Services 新功能的詳細資訊，包括舊版 CTP 的詳細資訊，請參閱 [SQL Server R Services 的新功能](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md)。  

### <a name="sql-server-reporting-services-ssrs"></a>SQL Server Reporting Services (SSRS)
- 此 CTP 中沒有任何 SSRS 新功能。
- 如需 SSRS 新功能的詳細資訊 (包括舊版的詳細資訊)，請參閱 [Reporting Services 的新功能](../reporting-services/sql-server-reporting-services-ssrs-中的新功能.md)。 

### <a name="sql-server-analysis-services-ssas"></a>SQL Server Analysis Services (SSAS)
- 此 CTP 中沒有任何 SSAS 新功能。  
- 如需詳細資訊，請參閱 [Analysis Services 的新功能](../analysis-services/what-s-new-in-sql-server-analysis-services-vnext.md)。  

### <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)
- 此 CTP 中沒有任何 SSIS 新功能。
- 如需 SSIS 新功能的詳細資訊，包括舊版 CTP 的詳細資訊，請參閱 [Integration Services vNext 的新功能](../integration-services/what-s-new-in-integration-services-in-sql-server-vnext.md)。  

### <a name="master-data-services-mds"></a>Master Data Services (MDS)
- 此 CTP 中沒有任何 Master Data Services 新功能。

##  <a name="infotipimageshiproominfotippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) 與 SQL Server 工程團隊交流 
- [Stack Overflow (tag sql-server)](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect - 報告錯誤及要求功能](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - 有關 R 的一般討論](https://www.reddit.com/r/SQLServer/)

## <a name="see-also"></a>另請參閱    
 + [![版本資訊](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png)](SQL%20Server%20vNext%20Release%20Notes.md)[ SQL Server VNext 版本資訊](../sql-server/sql-server-vnext-release-notes.md)。 
+ [版本支援的功能](https://msdn.microsoft.com/library/cc645993.aspx)
 + [[硬體及軟體安裝需求](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)](Hardware%20and%20Software%20Requirements%20for%20Installing%20SQL%20Server%202016.md)
 + [安裝精靈](../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md)
 
 + [安裝程式和服務安裝](Setup%20and%20Servicing%20Installation.md)
 
 ![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)