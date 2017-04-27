---
title: "SQL Server 2016 的版本及支援功能 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "SQL 版本"
ms.assetid: 5da61ff5-12b9-48e6-b3c8-0dacca1751c4
caps.latest.revision: 175
author: sabotta
ms.author: carlasab
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b9b9db3ca911b8fd8eed6304b9d3a8f51e9e9ba2
ms.lasthandoff: 04/11/2017

---
# <a name="editions-and-supported-features-for-sql-server-2016"></a>SQL Server 2016 的版本及支援功能
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  本主題提供不同 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]版本所支援功能的詳細資料。  
  
 SQL Server Evaluation Edition 提供了 180 天的試用期。  
  
 如需最新版本資訊和新功能資訊，請參閱下列項目：
- [SQL Server 2016 版本資訊](../sql-server/sql-server-2016-release-notes.md)
- [SQL Server 2016 的新功能](../sql-server/what-s-new-in-sql-server-2016.md)

    
 **試用 SQL Server 2016！**    
    
 > [![Download from Evaluation Center](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) **[Download SQL Server 2016  from the Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)**    
    
> ![Azure Virtual Machine small](../analysis-services/media/azure-virtual-machine-small.png) **[Spin up a Virtual Machine with SQL Server 2016 already installed](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.SQL2016SP1-WS2016?tab=Overview?wt.mc_id=sqL16_vm)**    
    
**Developer 和 Evaluation 版本**  
 如需 Developer 和 Evaluation 版本所支援的功能，請參閱下列各表中針對 SQL Server Enterprise Edition 列出的功能。
如需已新增至 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1 之 Developer 版本的功能清單，請參閱 [SQL Server 2016 SP1 版本 (英文)](https://aka.ms/uw6cw4)。   
  
##  <a name="Cross-BoxScaleLimits"></a> Scale Limits  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|
|單一執行個體所使用的計算容量上限 - [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|作業系統最大值|限制為 4 個插槽或 24 個核心的較小者|限制為 4 個插槽或 16 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者| 
|單一執行個體所使用的計算容量上限 - [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|作業系統最大值|限制為 4 個插槽或 24 個核心的較小者|限制為 4 個插槽或 16 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|  
|每個 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]執行個體的緩衝集區記憶體上限|作業系統最大值|128 GB|64 GB|1410 MB|1410 MB|
|每個 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]執行個體的資料行存放區區段快取記憶體上限|無限制的記憶體| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 MB<sup>2</sup>| 352 MB<sup>2</sup>|  
|每個 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]資料庫的記憶體最佳化資料大小上限|無限制的記憶體| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 MB<sup>2</sup>| 352 MB<sup>2</sup>|  
|每個 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]執行個體使用的記憶體上限|作業系統最大值|表格式：16 GB<br /><br /> MOLAP：64 GB|不適用|不適用|不適用|  
|每個 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]執行個體使用的記憶體上限|作業系統最大值|64 GB|64 GB|4 GB|不適用|
|關聯式資料庫大小上限|524 PB|524 PB|524 PB|10 GB|10 GB|  
  
<sup>1</sup> 新合約不適用的 Enterprise Edition (含伺服器 + 用戶端存取授權 (CAL)) 授權限制為每個 SQL Server 執行個體最多 20 個核心。 核心伺服器授權模式之下沒有任何限制。 如需詳細資訊，請參閱 [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。  
  
<sup>2</sup> 適用於 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1。 

##  <a name="RDBMSHA"></a> RDBMS High Availability  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Server Core 支援 <sup>1</sup>|是|是|是|是|是|  
|記錄傳送|是|是|是|否|否|  
|資料庫鏡像|是|是<br /><br /> 僅限 FULL 安全性|僅限見證|僅限見證|僅限見證| 
|備份壓縮|是|是|否|否|否| 
|資料庫快照集|是|是 <sup>3</sup>|是 <sup>3</sup>|是 <sup>3</sup>|是 <sup>3</sup>|
|AlwaysOn 容錯移轉叢集執行個體|是<br /><br /> 節點數目是作業系統最大值|是<br /><br /> 支援 2 個節點|否|否|否|  
|AlwaysOn 可用性群組|是<br /><br /> 最多 8 個次要複本，包括 2 個同步次要複本。|否|否|否|否|
|基本可用性群組 <sup>2</sup>|否|是<br /><br /> 支援 2 個節點|否|否|否|
|線上頁面和檔案還原|是|否|否|否|否|
|線上檢索索引|是|否|否|否|否|
|線上結構描述變更|是|否|否|否|否|
|快速復原|是|否|否|否|否|
|鏡像備份|是|否|否|否|否|
|熱新增記憶體和 CPU|是|否|否|否|否|
|資料庫復原建議程式|是|是|是|是|是|
|加密的備份|是|是|否|否|否|
|混合式備份至 Windows Azure (備份至 URL)|是|是|否|否|否|  
  
 <sup>1</sup> 如需在 Server Core 上安裝 SQL Server 2016 的詳細資訊，請參閱 [在 Server Core 上安裝 SQL Server 2016](../database-engine/install-windows/install-sql-server-on-server-core.md)。 

<sup>2</sup> 如需基本可用性群組的詳細資訊，請參閱 [基本可用性群組](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)。  

<sup>3</sup> 適用於 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1。
  
##  <a name="RDBMSSP"></a> RDBMS Scalability and Performance  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|資料行存放區 <sup>1</sup>|是|是 <sup>2</sup>|是 <sup>2</sup>|是<sup>2</sup>|是<sup>2</sup>|  
|記憶體內部 OLTP <sup>1</sup>|是|是 <sup>2</sup>|是 <sup>2</sup>|是 <sup>2</sup>、 <sup>3</sup>|是 <sup>2</sup>|
|Stretch Database|是|是|是|是|是|
|持續性的主記憶體|是|是|是|是|是|
|多個執行個體支援|50|50|50|50|50|
|資料表和索引分割區|是|是 <sup>2</sup>|是 <sup>2</sup>|是 <sup>2</sup>|是 <sup>2</sup>|  
|資料壓縮|是|是 <sup>2</sup>|是 <sup>2</sup>|是 <sup>2</sup>|是 <sup>2</sup>|
|資源管理員|是|否|否|否|否|  
|分割資料表平行處理原則|是|否|否|否|否|
|多個檔案資料流容器|是|是 <sup>2</sup>|是 <sup>2</sup>|是 <sup>2</sup>|是 <sup>2</sup>|
|NUMA 感知大型分頁記憶體和緩衝區陣列配置|是|否|否|否|否|
|緩衝集區擴充|是|是|否|否|否|
|IO 資源管理|是|否|否|否|否|  
|延遲持久性|是|是|是|是|是|

<sup>1</sup> 記憶體內部 OLTP 資料大小和資料行存放區區段快取都限制為版本「縮放限制」區段指定的記憶體數量。 平行處理原則的最大程度是有限的。 索引建置的平行處理原則 (DOP) 程度限制為 2 DOP (Standard Edition) 和 1 DOP (Web Edition 和 Express Edition)。 這會參考以磁碟式資料表和記憶體最佳化資料表建立的資料行存放區索引。

<sup>2</sup> 適用於 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1。 

<sup>3</sup> 這項功能不會納入 LocalDB 安裝選項。
##  <a name="RDBMSS"></a> RDBMS Security  
  
|功能|Enterprise|Standard|Web|Express|Express with Advanced Services|  
|-------------|----------------|--------------|---------|-------------|------------------------------------| 
|資料列層級安全性|是|是|是 <sup>1</sup>|是 <sup>1</sup>|是 <sup>1</sup>|  
|永遠加密|是|是 <sup>1</sup>|是 <sup>1</sup>|是 <sup>1</sup>|是 <sup>1</sup>| 
|動態資料遮罩|是|是|是 <sup>1</sup>|是 <sup>1</sup>|是 <sup>1</sup>|   
|基本稽核|是|是|是|是|是| 
|細部稽核|是|是 <sup>1</sup>|是 <sup>1</sup>|是 <sup>1</sup>|是 <sup>1</sup>| 
|透明資料庫加密|是|否|否|否|否|   
|可延伸金鑰管理|是|否|否|否|否| 
|使用者定義角色|是|是|是|是|是| 
|自主資料庫|是|是|是|是|是| 
|備份的加密|是|是|否|否|否|  

<sup>1</sup> 適用於 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1。  
##  <a name="Replication"></a> Replication  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|異質性訂閱者|是|是|否|否|否|  
|合併式複寫|是|是|是 (僅限訂閱者)|是 (僅限訂閱者)|是 (僅限訂閱者)|   
|Oracle 發行|是|否|否|否|否| 
|點對點異動複寫|是|否|否|否|否|   
|快照式複寫|是|是|是 (僅限訂閱者)|是 (僅限訂閱者)|是 (僅限訂閱者)|   
|SQL Server 變更追蹤|是|是|是|是|是| 
|異動複寫|是|是|是 (僅限訂閱者)|是 (僅限訂閱者)|是 (僅限訂閱者)|   
|異動複寫至 Azure|是|是|否|否|否|   
|異動複寫可更新訂閱|是|否|否|否|否|  
  
##  <a name="SSMS"></a> Management Tools  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL 管理物件 (SMO)|是|是|是|是|是|  
|SQL 組態管理員|是|是|是|是|是|   
|SQL CMD (命令提示字元工具)|是|是|是|是|是|      
|Distributed Replay - 管理工具|是|是|是|是|否|  
|Distribute Replay - Client|是|是|是|否|否|  
|Distributed Replay - Controller|是 (最多 16 個用戶端)|是 (1 個用戶端)|是 (1 個用戶端)|否|否|   
|SQL Profiler|是|是|否 <sup>1</sup>|否 <sup>1</sup>|否 <sup>1</sup>|  
|SQL Server Agent|是|是|是|否|否| 
|Microsoft System Center Operations Manager 管理組件|是|是|是|否|否|  
|Database Tuning Advisor (DTA)|是|是 <sup>2</sup>|是 <sup>2</sup>|否|否|      
  
 <sup>1</sup> 您可以使用 SQL Server Standard 和 SQL Server Enterprise Edition 來分析 SQL Server Web、SQL Server Express、SQL Server Express with Tools 和 SQL Server Express with Advanced Services。  
  
 <sup>2</sup> 僅針對 Standard Edition 功能啟用微調。  
  
##  <a name="RDBMSM"></a> RDBMS Manageability  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|使用者執行個體|否|否|否|是|是| 
|LocalDB|否|否|否|是|否| 
|專用管理員連接|是|是|是|是，附追蹤旗標|是，附追蹤旗標|   
|PowerShell 指令碼支援|是|是|是|是|是| 
|SysPrep 支援 <sup>1</sup>|是|是|是|是|是| 
|資料層應用程式元件作業的支援 - 擷取、部署、升級、刪除|是|是|是|是|是| 
|原則自動化 (依排程和變更檢查)|是|是|是|否|否|   
|效能資料收集器|是|是|是|否|否| 
|能夠在多重執行個體管理中註冊為受管理的執行個體|是|是|是|否|否|   
|標準效能報告|是|是|是|否|否| 
|計畫指南和計畫指南的計畫凍結|是|是|是|否|否|   
|索引檢視表的直接查詢 (使用 NOEXPAND 提示)|是|是|是|是|是| 
|自動索引檢視表維護|是|是|是|否|否| 
|分散式分割區檢視|是|否|否|否|否| 
|平行索引作業|是|否|否|否|否|  
|查詢最佳化工具自動使用索引檢視表|是|否|否|否|否| 
|平行一致性檢查|是|否|否|否|否| 
|SQL Server 公用程式控制點|是|否|否|否|否|    
|緩衝集區擴充|是|是|否|否|否| 
  
 <sup>1</sup> 如需詳細資訊，請參閱 [使用 SysPrep 安裝 SQL Server 的考量](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)。  
 
<sup>2</sup> 適用於 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1。 
  
##  <a name="DevTools"></a> Development Tools  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Microsoft Visual Studio 整合|是|是|是|是|是| 
|Intellisense (Transact-SQL 和 MDX)|是|是|是|是|是| 
|SQL Server Data Tools (SSDT)|是|是|是|是|否|    
|MDX 編輯、偵錯和設計工具|是|是|否|否|否|   
  
##  <a name="Programmability"></a> Programmability  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|基本的 R 整合|是|是|是|是|否|   
|進階的 R 整合|是|否|否|否|否| 
|R Server (Standalone)|是|否|否|否|否|   
|Polybase 計算節點|是|是 <sup>1</sup>|是 <sup>1</sup>、 <sup>2</sup>|是 <sup>1</sup>、 <sup>2</sup>|是 <sup>1</sup>、 <sup>2</sup>| 
|Polybase 前端節點|是|否|否|否|否| 
|JSON|是|是|是|是|是|   
|查詢存放區|是|是|是|是|是|   
|Temporal|是|是|是|是|是|   
|Common Language Runtime (CLR) 整合|是|是|是|是|是|   
|原生 XML 支援|是|是|是|是|是| 
|XML 索引|是|是|是|是|是| 
|MERGE 與 UPSERT 功能|是|是|是|是|是|   
|FILESTREAM 支援|是|是|是|是|是| 
|FileTable|是|是|是|是|是| 
|日期和時間資料類型|是|是|是|是|是|  
|國際化支援|是|是|是|是|是| 
|全文檢索和語意搜尋|是|是|是|是|否| 
|查詢中的語言規格|是|是|是|是|否|   
|Service Broker (訊息)|是|是|否 (僅限用戶端)|否 (僅限用戶端)|否 (僅限用戶端)|   
|Transact-SQL 端點|是|是|是|否|否| 

<sup>1</sup> 使用多個運算節點向外延展時需要標題節點。

<sup>2</sup> 適用於 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1。
  
## <a name="IS"></a> Integration Services

如需有關 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 版本所支援之 Integration Services (SSIS) 功能的資訊，請參閱 [SQL Server 版本支援的 Integration Services 功能](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md)。

##  <a name="MDS"></a> Master Data Services  
 如需 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 版本所支援之 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]和 Data Quality Services 功能的資訊，請參閱 [SQL Server 2016 版本支援的 Master Data Services 和 Data Quality Services 功能](../master-data-services/master-data-services-and-data-quality-services-features-support.md)。 

  
##  <a name="DW"></a> Data Warehouse  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|建立不含資料庫的 Cube|是|是|否|否|否 |   
|自動產生暫存和資料倉儲結構描述|是|是|否|否|否| 
|異動資料擷取|是|是 <sup>1</sup>|否|否|否| 
|星型聯結查詢最佳化|是|否|否|否|否| 
|可擴充的唯讀 Analysis Services 組態|是|否|否|否|否| 
|分割區資料表和索引上的查詢平行處理|是|否|否|否|否|   
|全域批次彙總|是|否|否|否|否| 

<sup>1</sup> 適用於 [!INCLUDE[ssSQL15_md](../includes/sssql15-md.md)] SP1。  
##  <a name="SSAS"></a> Analysis Services  
  
如需 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]版本所支援之 Analysis Services 功能的資訊，請參閱 [SQL Server 2016 版本支援的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。 
  
##  <a name="BIMD"></a> BI Semantic Model (Multi Dimensional)  
  
如需 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]版本所支援之 Analysis Services 功能的資訊，請參閱 [SQL Server 2016 版本支援的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。
   
##  <a name="BIT"></a> BI Semantic Model (Tabular)  
  
如需 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]版本所支援之 Analysis Services 功能的資訊，請參閱 [SQL Server 2016 版本支援的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。
  
##  <a name="PPSP"></a> Power Pivot for SharePoint  
  
如需 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]版本所支援之 Power Pivot for SharePoint 功能的資訊，請參閱 [SQL Server 2016 版本支援的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。
  
##  <a name="DM"></a> Data Mining  
  
如需 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]版本所支援之資料採礦功能的資訊，請參閱 [SQL Server 2016 版本支援的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。
  
##  <a name="SSRS"></a> Reporting Services  
  
如需 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]版本所支援之 Reporting Services 功能的資訊，請參閱 [SQL Server 2016 版本支援的 Reporting Services 功能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)。

##  <a name="BIC"></a> Business Intelligence Clients  

如需 [!INCLUDE[ssCurrent_md](../includes/sscurrent-md.md)]版本所支援之 Business Intelligence Client 功能的資訊，請參閱 [SQL Server 2016 版本支援的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md) 或 [SQL Server 2016 版本支援的 Reporting Services 功能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)。
  
##  <a name="SLS"></a> Spatial and Location Services  
  
|功能名稱|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|空間索引|是|是|是|是|是|   
|平面與 Geodetic 資料類型|是|是|是|是|是| 
|進階空間程式庫|是|是|是|是|是|   
|匯入/匯出業界標準空間資料格式|是|是|是|是|是|   
  
##  <a name="ADS"></a> Additional Database Services  
  
|功能名稱|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------| 
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|是|是|是|是|是|   
|Database Mail|是|是|是|否|否| 
  
##  <a name="Other"></a> Other Components  
  
|功能名稱|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------|  
|StreamInsight|StreamInsight Premium 版|StreamInsight Standard 版|StreamInsight Standard 版|否|否| 
|StreamInsight HA|StreamInsight Premium 版|否|否|否|否|   
  
> [![Download SSMS](../analysis-services/media/download.png)](https://msdn.microsoft.com/library/mt238290.aspx) **[Download the latest version of SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)**    
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2016 的產品規格](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)   
 [SQL Server 2016 安裝](../database-engine/install-windows/installation-for-sql-server-2016.md)  
  
  

