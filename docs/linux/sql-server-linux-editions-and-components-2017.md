---
title: "版本和支援的功能的 SQL Server 2017 ~ Linux |Microsoft 文件"
ms.custom: 
ms.date: 09/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.reviewer: 
ms.suite: sql
ms.technology:
- sql-linux
- server-general
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- default components
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
ms.assetid: 
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e1734b7ec7619a6943e1d79a0933b6189ad3162d
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2018
---
# <a name="editions-and-supported-features-of-sql-server-2017-on-linux"></a>版本和支援的功能的 SQL Server 2017 on Linux

本文章提供在 Linux 上的 SQL Server 2017 各種版本所支援功能的詳細資料。 版本及 Windows 上的 SQL Server 支援的功能，請參閱[SQL Server 2017 Windows](../sql-server/editions-and-components-of-sql-server-2017.md)。  
  
安裝需求根據應用程式的需要而異。 不同的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本可配合組織和個人的獨特效能、執行階段和價格需求。 安裝的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 元件也將取決於您的特定需求。 下列章節幫助您了解如何在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的可用版本和元件之間做出最好的選擇。  

如需最新版本資訊和新功能資訊，請參閱下列項目：
- [Linux 上的 SQL Server 版本資訊](sql-server-linux-release-notes.md)
- [新功能 SQL Server on Linux](sql-server-linux-whats-new.md)

如需在 Linux 上無法使用的 SQL Server 功能的清單，請參閱[不支援的功能和服務](sql-server-linux-release-notes.md#Unsupported)。

### <a name="try-sql-server"></a>試用 SQL Server！    
    
[下載 SQL Server 2017](http://www.microsoft.com/sql-server/sql-server-2017)

## <a name="includessnoversionincludesssnoversion-mdmd-editions"></a>[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] 版本  
 下表描述 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的版本。 
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|定義|  
|---------------------------------------|----------------|  
|Enterprise|Premium 供應項目[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)]Enterprise edition 與急速效能，讓關鍵任務工作負載的高服務等級，提供完整的高階資料中心功能。|  
|Standard|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard edition 針對部門和小型組織，執行其應用程式的基本的資料管理，提供及支援在內部部署和雲端的一般開發工具，能夠以最少的 IT 資源的有效的資料庫管理。|  
|Web|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web Edition 對於 Web 主控者和 Web VAP 而言是一個整體擁有成本很低的選擇，可針對小型到大型規模的 Web 屬性提供可擴充、負擔輕鬆而且管理方便的功能。|  
|開發人員|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer Edition 可讓開發人員在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 上建立任何類型的應用程式。 其中包含 Enterprise Edition 的所有功能，但是只授權做為開發和測試系統使用，而不做為實際伺服器使用。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer 是供應用程式建立和測試人員使用的理想選擇。|  
|Express 版本|Express Edition 是入門級免費伺服器，非常適合用來學習及建置桌上型電腦和小型伺服器資料驅動應用程式。 這個版本是獨立軟體廠商、開發人員及建置用戶端應用程式之愛好者的最佳選擇。 如果您需要更進階的資料庫功能， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express 可以順利地升級為其他更高階的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本。|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>搭配用戶端/伺服器應用程式使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  

您可以在執行用戶端/伺服器應用程式的電腦上只安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用戶端元件，這些應用程式會直接連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的執行個體。 如果您要在資料庫伺服器上管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體，或您打算開發 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 應用程式，則用戶端元件安裝也是一個不錯的選項。  
  
## <a name="includessnoversionincludesssnoversion-mdmd-components"></a>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 元件  

SQL Server 2017 on Linux 支援的 SQL Server database engine。 下表描述 database engine 中的功能。   
  
|伺服器元件|Description|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 包含[!INCLUDE[ssDE](../includes/ssde-md.md)]，儲存、 處理和保護資料、 複寫、 全文檢索搜尋、 工具來管理關聯式和 XML 資料，以及資料庫分析整合的核心服務。|  

**開發人員、 企業核心和 Evaluation 版本**  
如需開發人員、 企業核心和 Evaluation edition 所支援的功能，請參閱適用於 SQL Server Enterprise edition 下表中列出的功能。

Developer Edition 只持續支援 1 個 [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md) 用戶端。 
  
##  <a name="Cross-BoxScaleLimits"></a> 調整限制  
  
|功能|Enterprise|Standard|Web|Express| 
|-------------|----------------|--------------|---------|------------------------|
|單一執行個體所使用的計算容量上限 - [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|作業系統最大值|限制為 4 個插槽或 24 個核心的較小者|限制為 4 個插槽或 16 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者| 
|單一執行個體所使用的計算容量上限 - [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|作業系統最大值|限制為 4 個插槽或 24 個核心的較小者|限制為 4 個插槽或 16 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|
|每個執行個體的緩衝集區的最大記憶體 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|作業系統最大值|128 GB|64 GB|1410 MB|
|每個執行個體的資料行存放區區段快取的最大記憶體 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|無限制的記憶體| 32 GB| 16 GB| 352 MB|  
|每個資料庫中的最大記憶體最佳化的資料大小 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|無限制的記憶體| 32 GB| 16 GB| 352 MB|
|關聯式資料庫大小上限|524 PB|524 PB|524 PB|10 GB|  
  
<sup>1</sup> Enterprise edition 含伺服器 + 用戶端存取授權 (CAL) 授權 （不適用於新的協議） 受限於最多 20 個核心每個 SQL Server 執行個體。 核心伺服器授權模式之下沒有任何限制。 如需詳細資訊，請參閱[SQL Server 版本的計算容量限制](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。  
 
##  <a name="RDBMSHA"></a> RDBMS 高可用性  
  
|功能|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------|  
|記錄傳送|是|是|是|否|  
|備份壓縮|是|是|否|否| 
|資料庫快照集|是|否|否|否|
|Alwayson 容錯移轉叢集執行個體<sup>1</sup>|是|是|否|否| 
|Alwayson 可用性群組<sup>2</sup>|是|否|否|否|
|基本可用性群組<sup>3</sup>|否|是|否|否|
|最小複本認可可用性群組|是|是|否|否|
|無叢集的可用性群組|是|是|否|否|
|線上頁面和檔案還原|是|否|否|否|
|線上檢索索引|是|否|否|否|
|繼續線上索引重建|是|否|否|否|
|線上結構描述變更|是|否|否|否|
|快速復原|是|否|否|否|
|鏡像備份|是|否|否|否|
|熱新增記憶體和 CPU|是|否|否|否|
|加密的備份|是|是|否|否|
|混合式備份至 Windows Azure (備份至 URL)|是|是|否|否|
  
<sup>1</sup> Enterprise edition 上的節點數目是作業系統最大值。 Standard Edition 支援兩個節點。 

<sup>2</sup>在 Enterprise 版本中，提供最多 8 個次要複本-包括 2 個同步次要複本的支援。 

<sup>3</sup> standard edition 支援基本可用性群組。 基本可用性群組支援兩個複本，使用一個資料庫。 如需基本可用性群組的詳細資訊，請參閱[基本可用性群組](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)。    

##  <a name="RDBMSSP"></a> RDBMS 延展性和效能  
  
|功能|Enterprise|Standard|Web|Express|  
|-------------|----------------|--------------|---------|------------------------| 
|資料行存放區 <sup>1</sup>|是|是|是|是|  
|叢集資料行存放區索引中的大型物件二進位檔|是|是|是|是|  
|線上非叢集資料行存放區索引重建|是|否|否|否|
|記憶體內部 OLTP <sup>1</sup>|是|是|是|是|
|持續性的主記憶體|是|是|是|是|
|資料表和索引分割區|是|是|是|是|  
|資料壓縮|是|是|是|是|
|資源管理員|是|否|否|否|  
|分割資料表平行處理原則|是|否|否|否|
|NUMA 感知大型分頁記憶體和緩衝區陣列配置|是|否|否|否|
|IO 資源管理|是|否|否|否|  
|延遲持久性|是|是|是|是|
|自動調整|是|否|否|否|
|批次模式自適性聯結|是|否|否|否|
|批次模式記憶體授與意見反應|是|否|否|否|
|交錯執行多重陳述式資料表值函式|是|是|是|是|
|大量插入增強功能|是|是|是|是|


<sup>1</sup> 記憶體內部 OLTP 資料大小和資料行存放區區段快取都限制為版本「縮放限制」區段指定的記憶體數量。 平行處理原則的最大程度是有限的。 索引建立程序平行處理原則 (DOP) 程度限於 2 DOP Standard edition 和 1 DOP Web 和 Express 版本。 這會參考以磁碟式資料表和記憶體最佳化資料表建立的資料行存放區索引。

##  <a name="RDBMSS"></a> RDBMS 安全性  
  
|功能|Enterprise|Standard|Web|Express|
|-------------|----------------|--------------|---------|------------------------------------| 
|資料列層級安全性|是|是|是|是|  
|永遠加密|是|是|是|是| 
|動態資料遮罩|是|是|是|是|   
|基本稽核|是|是|是|是| 
|細部稽核|是|是|是|是| 
|透明資料庫加密|是|否|否|否|   
|使用者定義角色|是|是|是|是| 
|自主資料庫|是|是|是|是| 
|備份的加密|是|是|否|否|  

##  <a name="RDBMSM"></a> RDBMS 管理能力  
  
|功能|Enterprise|Standard|Web|Express|   
|-------------|----------------|--------------|---------|------------------------|  
|專用管理員連接|是|是|是|是，附追蹤旗標|是，附追蹤旗標|   
|PowerShell 指令碼支援|是|是|是|是| 
|資料層應用程式元件作業的支援 - 擷取、部署、升級、刪除|是|是|是|是| 
|原則自動化 (依排程和變更檢查)|是|是|是|否|否|   
|效能資料收集器|是|是|是|否|否| 
|標準效能報告|是|是|是|否|否| 
|計畫指南和計畫指南的計畫凍結|是|是|是|否|否|   
|索引檢視表的直接查詢 (使用 NOEXPAND 提示)|是|是|是|是| 
|自動索引檢視表維護|是|是|是|否|否| 
|分散式分割區檢視|是|否|否|否| 
|平行索引作業|是|否|否|否|  
|查詢最佳化工具自動使用索引檢視表|是|否|否|否| 
|平行一致性檢查|是|否|否|否| 
|SQL Server 公用程式控制點|是|否|否|否|    

##  <a name="Programmability"></a> Programmability  
  
|功能|Enterprise|Standard|Web|Express 
|-------------|----------------|--------------|---------|------------------------|  
|JSON|是|是|是|是|   
|查詢存放區|是|是|是|是|   
|Temporal|是|是|是|是|   
|原生 XML 支援|是|是|是|是| 
|XML 索引|是|是|是|是| 
|MERGE 與 UPSERT 功能|是|是|是|是|   
|日期和時間資料類型|是|是|是|是|  
|國際化支援|是|是|是|是| 
|全文檢索和語意搜尋|是|是|是|是|否| 
|查詢中的語言規格|是|是|是|是|否|   
|Service Broker (訊息)|是|是|否 (僅限用戶端)|否 (僅限用戶端)|否 (僅限用戶端)|   
|Transact-SQL 端點|是|是|是|否|否| 
|圖表|是|是|是|是|  


<sup>1</sup> 使用多個運算節點向外延展時需要標題節點。

## <a name="IS"></a> Integration Services

如需支援版本的 Integration Services (SSIS) 功能資訊[!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]，請參閱[Integration Services 功能的 SQL Server 版本支援](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md)。

##  <a name="SLS"></a> 空間和定位服務  
  
|功能名稱|Enterprise|Standard|Web|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|空間索引|是|是|是|是|   
|平面與 Geodetic 資料類型|是|是|是|是| 
|進階空間程式庫|是|是|是|是|   
|匯入/匯出業界標準空間資料格式|是|是|是|是|   

  
## <a name="next-steps"></a>後續的步驟 
 [版本和的 SQL Server 2017 Windows 支援的功能](../sql-server/editions-and-components-of-sql-server-2017.md)  
 [版本和 SQL Server 2016 Windows 支援的功能](../sql-server/editions-and-components-of-sql-server-2016.md)  
 [版本和 SQL Server 2014 Windows 支援的功能](http://msdn.microsoft.com/library/cc645993(v=sql.120).aspx)  
 [SQL Server 安裝](../database-engine/install-windows/installation-for-sql-server-2016.md)  
 [SQL Server 的產品規格](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb) 

  
  
