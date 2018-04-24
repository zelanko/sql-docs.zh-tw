---
title: SQL Server 2017 的版本及支援功能 | Microsoft Docs
ms.custom: ''
ms.date: 11/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.technology:
- server-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- 32-bit vs. 64-bit editions [SQL Server]
- default components
- Workgroup Edition [SQL Server]
- Internet servers [SQL Server]
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- client/server applications [SQL Server]
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- 64-bit edition [SQL Server]
- IIS [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
ms.assetid: ''
caps.latest.revision: 121
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 9b2fc5b5571127ccab0a0dc4b4656a6d9378057d
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="editions-and-supported-features-of-sql-server-2017"></a>SQL Server 2017 的版本及支援功能
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

本主題提供各種 SQL Server 2017 版本支援的功能的詳細資料。 

如需舊版的資訊，請參閱：

* [SQL Server 2016](editions-and-components-of-sql-server-2016.md)。  
* [SQL Server 2014](http://msdn.microsoft.com/library/cc645993(v=sql.120).aspx)。

  
安裝需求根據應用程式的需要而異。 不同的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本可配合組織和個人的獨特效能、執行階段和價格需求。 安裝的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 元件也將取決於您的特定需求。 下列章節幫助您了解如何在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的可用版本和元件之間做出最好的選擇。  

SQL Server Evaluation Edition 提供了 180 天的試用期。  
  
如需最新版本資訊和新功能資訊，請參閱下列項目：
- [SQL Server 2017 版本資訊](../sql-server/sql-server-2017-release-notes.md)
- [SQL Server 2017 的新功能](../sql-server/what-s-new-in-sql-server-2017.md)

### <a name="try-sql-server"></a>試用 SQL Server！    
    
> [![從 Evaluation Center 下載](../analysis-services/media/download.png)](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2017-ctp/) **[從 Evaluation Center 下載 SQL Server 2017](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-ctp/)**    

<!---    
> ![Azure Virtual Machine small](../analysis-services/media/azure-virtual-machine-small.png) **[Spin up a Virtual Machine with SQL Server 2016 already installed](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SQL2016SP1-WS2016?tab=Overview?wt.mc_id=sqL16_vm)**   
--->

## <a name="includessnoversionincludesssnoversion-mdmd-editions"></a>[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] 版本  
 下表描述 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的版本。 
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|定義|  
|---------------------------------------|----------------|  
|Enterprise|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise Edition 這套頂級產品不但提供完整的高階資料中心功能，而且具備急速效能、不受限制的虛擬化以及端對端商業智慧 - 為關鍵任務工作負載提供最高的服務等級，並且讓使用者獲得資料洞察能力。|  
|Standard|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard Edition 針對部門和小型組織提供基本的資料管理與商業智慧資料庫來執行應用程式，並且支援內部部署和雲端的一般開發工具 - 以最少的 IT 資源提供最有效率的資料庫管理。|  
|Web|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web Edition 對於 Web 主控者和 Web VAP 而言是一個整體擁有成本很低的選擇，可針對小型到大型規模的 Web 屬性提供可擴充、負擔輕鬆而且管理方便的功能。|  
|Developer|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer Edition 可讓開發人員在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上建立任何類型的應用程式。 其中包含 Enterprise Edition 的所有功能，但是只授權做為開發和測試系統使用，而不做為實際伺服器使用。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer 是供應用程式建立和測試人員使用的理想選擇。|  
|Express 版本|Express Edition 是入門級免費伺服器，非常適合用來學習及建置桌上型電腦和小型伺服器資料驅動應用程式。 這個版本是獨立軟體廠商、開發人員及建置用戶端應用程式之愛好者的最佳選擇。 如果您需要更進階的資料庫功能， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express 可以順利地升級為其他更高階的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express LocalDB 是輕量版 Express，其中包含所有程式設計功能，以使用者模式執行，並配備快速的零設定安裝，而且所需必要條件很少。|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-an-internet-server"></a>搭配網際網路伺服器使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
 在網際網路伺服器中，例如執行 Internet Information Services (IIS) 的伺服器，您通常會安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用戶端工具。 用戶端工具包括連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體的應用程式所使用的用戶端連接元件。  
  
>[!NOTE]
>雖然您可以在執行 IIS 的電腦上安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體，但通常只有針對具有單一伺服器電腦的小型網站才會這麼做。 大部分網站會將它們的中介層 IIS 系統放在一部伺服器或伺服器叢集上，並將其資料庫放在另一部伺服器或伺服器聯盟上。  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>搭配用戶端/伺服器應用程式使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
 您可以在執行用戶端/伺服器應用程式的電腦上只安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用戶端元件，這些應用程式會直接連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的執行個體。 如果您要在資料庫伺服器上管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體，或您打算開發 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 應用程式，則用戶端元件安裝也是一個不錯的選項。  
  
 用戶端工具選項會安裝下列 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能：回溯相容性元件、 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]、連接元件、管理工具、軟體開發套件和《 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》元件。 如需詳細資訊，請參閱[安裝 SQL Server](../database-engine/install-windows/install-sql-server.md)。  
  
## <a name="deciding-among-includessnoversionincludesssnoversion-mdmd-components"></a>在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 元件之間作決定  
 使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安裝精靈的 [特徵選取] 頁面來選取要併入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]安裝的元件。 依預設，不會選取樹狀結構中的任何功能。  
  
 請使用下表中的資訊來判斷最符合您需求的功能集。  
  
|伺服器元件|描述|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 包含 [!INCLUDE[ssDE](../includes/ssde-md.md)]；儲存、處理和保護資料用的核心服務；複寫；全文檢索搜尋；管理關聯式和 XML 資料用的工具；資料庫內分析整合，以及存取 Hadoop 與其他異質資料來源用的 Polybase 整合，和 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 伺服器。|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 包括用來建立及管理線上分析處理 (OLAP) 和資料採礦應用程式的工具。|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 包括伺服器和用戶端元件，可用來建立、管理和部署表格式、矩陣、圖形化和自由形式報表。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 也是一個可延伸的平台，可讓您用來開發報表應用程式。|  
|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 是一組圖形化工具和可程式化物件，用來移動、複製和轉換資料。 其中還包括 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] 的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)](DQS) 元件。|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) 是用於主要資料管理的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 方案。 MDS 可設定為管理任何網域 (產品、客戶、帳戶) 而且包括階層、更細微的安全性、交易、資料版本控制和商務規則，以及可用來管理資料的 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 。|  
|Machine Learning 服務 (資料庫內)|Machine Learning 服務 (資料庫內) 支援使用企業資料來源之可調整的分散式 Machine Learning 解決方案。 在 SQL Server 2016 中，支援 R 語言。 SQL Server 2017 支援 R 和 Python。|
|Machine Learning 伺服器 (獨立式)|Machine Learning 伺服器 (獨立式) 支援在多種平台上部署分散式、可調整的 Machine Learning 解決方案，以及使用多種企業資料來源，包括 Linux、Hadoop 和 Teradata。 在 SQL Server 2016 中，支援 R 語言。 SQL Server 2017 支援 R 和 Python。|

  
|管理工具|描述|  
|----------------------|-----------------|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 是一個整合式環境，可存取、設定、管理及開發 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的元件。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 可讓所有技能等級的開發人員和管理員使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。<br /><br /> 下載並安裝 <br />                [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 下載 SQL Server Management Studio  [的](http://msdn.microsoft.com/library/mt238290.aspx)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服務、伺服器通訊協定、用戶端通訊協定和用戶端別名提供基本組態管理。|  
|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 提供圖形化使用者介面來監視 [!INCLUDE[ssDE](../includes/ssde-md.md)] 或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的執行個體。|  
|[!INCLUDE[ssDE](../includes/ssde-md.md)] Tuning Advisor|[!INCLUDE[ssDE](../includes/ssde-md.md)] Tuning Advisor 協助您建立一組最佳的索引、索引檢視表和分割區。|  
|Data Quality Client|提供相當簡單且高度直覺式的圖形使用者介面來連接 DQS 伺服器，以及執行資料清除作業。 此外還可讓您集中監控資料清除作業期間執行的各種活動。|  
|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 提供 IDE，可用來為下列商業智慧元件建立方案： [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]及 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]。<br /><br /> (先前稱為 Business Intelligence Development Studio)。<br /><br /> [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 也包含「資料庫專案」，為資料庫開發人員提供整合環境，以實現 Visual Studio 內任何 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 平台 (內部和外部部署) 適用的所有資料庫設計工作。 資料庫開發人員可以使用 Visual Studio 中的增強伺服器總管，輕鬆建立或編輯資料庫物件和資料，或執行查詢。|  
|連接元件|安裝用於用戶端和伺服器之間通訊的元件以及用於 DB-Library、ODBC 和 OLE DB 的網路程式庫。|  
  
|文件集|描述|  
|-------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的核心文件集。| 

**Developer 和 Evaluation 版本**  
如需 Developer 和 Evaluation 版本所支援的功能，請參閱下列各表中針對 SQL Server Enterprise Edition 列出的功能。

Developer edition 會持續支援的只有 1 個用戶端[SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md)。 
  
##  <a name="Cross-BoxScaleLimits"></a> 調整限制  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|
|單一執行個體所使用的計算容量上限 - [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|作業系統最大值|限制為 4 個插槽或 24 個核心的較小者|限制為 4 個插槽或 16 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者| 
|單一執行個體所使用的計算容量上限 - [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|作業系統最大值|限制為 4 個插槽或 24 個核心的較小者|限制為 4 個插槽或 16 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|  
|每個 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]執行個體的緩衝集區記憶體上限|作業系統最大值|128 GB|64 GB|1410 MB|1410 MB|
|每個 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]執行個體的資料行存放區區段快取記憶體上限|無限制的記憶體| 32 GB| 16 GB| 352 MB| 352 MB|  
|每個 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]資料庫的記憶體最佳化資料大小上限|無限制的記憶體| 32 GB| 16 GB| 352 MB| 352 MB|  
|每個 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]執行個體使用的記憶體上限|作業系統最大值|表格式：16 GB<br /><br /> MOLAP：64 GB|不適用|不適用|不適用|  
|每個 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]執行個體使用的記憶體上限|作業系統最大值|64 GB|64 GB|4 GB|不適用|
|關聯式資料庫大小上限|524 PB|524 PB|524 PB|10 GB|10 GB|  
  
<sup>1</sup> 新合約不適用的 Enterprise Edition (含伺服器 + 用戶端存取授權 (CAL)) 授權限制為每個 SQL Server 執行個體最多 20 個核心。 核心伺服器授權模式之下沒有任何限制。 如需詳細資訊，請參閱 [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。  
 
##  <a name="RDBMSHA"></a> RDBMS 高可用性  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Server Core 支援 <sup>1</sup>|是|是|是|是|是|  
|記錄傳送|是|是|是|否|否|  
|資料庫鏡像|是|是<br /><br /> 僅限 FULL 安全性|僅限見證|僅限見證|僅限見證| 
|備份壓縮|是|是|否|否|否| 
|資料庫快照集|是|是|是|是|是|
|AlwaysOn 容錯移轉叢集執行個體 <sup>2</sup>|是|是|否|否|否|  
|AlwaysOn 可用性群組 <sup>3</sup>|是|否|否|否|否|
|基本可用性群組 <sup>4</sup>|否|是|否|否|否|
|線上頁面和檔案還原|是|否|否|否|否|
|線上檢索索引|是|否|否|否|否|
|繼續線上索引重建|是|否|否|否|否|
|線上結構描述變更|是|否|否|否|否|
|快速復原|是|否|否|否|否|
|鏡像備份|是|否|否|否|否|
|熱新增記憶體和 CPU|是|否|否|否|否|
|資料庫復原建議程式|是|是|是|是|是|
|加密的備份|是|是|否|否|否|
|混合式備份至 Windows Azure (備份至 URL)|是|是|否|否|否|
|無叢集的可用性群組|是|是|否|否|否|否|
|最小複本認可可用性群組|是|是|是|否|否|否|
  

<sup>1</sup>如需在 Server Core 上安裝 SQL Server 的詳細資訊，請參閱[在 Server Core 上安裝 SQL Server](../database-engine/install-windows/install-sql-server-on-server-core.md)。 

<sup>2</sup> 在 Enterprise Edition 上，節點數目是作業系統最大值。 Standard Edition 支援兩個節點。 

<sup>3</sup> Enterprise Edition 最多支援 8 個次要複本，包括 2 個同步次要複本。 

<sup>4</sup> Standard Edition 支援基本可用性群組。 基本可用性群組支援兩個複本，使用一個資料庫。 如需基本可用性群組的詳細資訊，請參閱[基本可用性群組](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)。  


##  <a name="RDBMSSP"></a> RDBMS 延展性和效能  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|資料行存放區 <sup>1</sup>|是|是|是|是|是|  
|叢集資料行存放區索引中的大型物件二進位檔|是|是|是|是|是|  
|線上非叢集資料行存放區索引重建|是|否|否|否|否|
|記憶體內部 OLTP <sup>1</sup>|是|是|是|是 <sup>2</sup>|是|
|Stretch Database|是|是|是|是|是|
|持續性的主記憶體|是|是|是|是|是|
|多個執行個體支援|50|50|50|50|50|
|資料表和索引分割區|是|是|是|是|是|  
|資料壓縮|是|是|是|是|是|
|資源管理員|是|否|否|否|否|  
|分割資料表平行處理原則|是|否|否|否|否|
|多個檔案資料流容器|是|是|是|是|是|
|NUMA 感知大型分頁記憶體和緩衝區陣列配置|是|否|否|否|否|
|緩衝集區擴充|是|是|否|否|否|
|IO 資源管理|是|否|否|否|否|  
|延遲持久性|是|是|是|是|是|
|自動調整|是|否|否|否|否|
|批次模式自適性聯結|是|否|否|否|否|
|批次模式記憶體授與意見反應|是|否|否|否|否|
|交錯執行多重陳述式資料表值函式|是|是|是|是|是|
|大量插入增強功能|是|是|是|是|是|


<sup>1</sup> 記憶體內部 OLTP 資料大小和資料行存放區區段快取都限制為版本「縮放限制」區段指定的記憶體數量。 平行處理原則的最大程度是有限的。 索引建置的平行處理原則 (DOP) 程度限制為 2 DOP (Standard Edition) 和 1 DOP (Web Edition 和 Express Edition)。 這會參考以磁碟式資料表和記憶體最佳化資料表建立的資料行存放區索引。

<sup>2</sup> 這項功能不會納入 LocalDB 安裝選項。

##  <a name="RDBMSS"></a> RDBMS 安全性  
  
|功能|Enterprise|Standard|Web|Express|Express with Advanced Services|  
|-------------|----------------|--------------|---------|-------------|------------------------------------| 
|資料列層級安全性|是|是|是|是|是|  
|永遠加密|是|是|是|是|是| 
|動態資料遮罩|是|是|是|是|是|   
|基本稽核|是|是|是|是|是| 
|細部稽核|是|是|是|是|是| 
|透明資料庫加密|是|否|否|否|否|   
|可延伸金鑰管理|是|否|否|否|否| 
|使用者定義角色|是|是|是|是|是| 
|自主資料庫|是|是|是|是|是| 
|備份的加密|是|是|否|否|否|  

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
  
##  <a name="SSMS"></a> 管理工具  
  
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
  
##  <a name="RDBMSM"></a> RDBMS 管理能力  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|使用者執行個體|否|否|否|是|是| 
|LocalDB|否|否|否|是|否| 
|專用管理員連接|是|是|是|是，附追蹤旗標|是，附追蹤旗標|   
|SysPrep 支援 <sup>1</sup>|是|是|是|是|是| 
|PowerShell 指令碼支援 <sup>2</sup>|是|是|是|是|是| 
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
|緩衝集區延伸模組|是|是|否|否|否| 
  
 <sup>1</sup> 如需詳細資訊，請參閱 [使用 SysPrep 安裝 SQL Server 的考量](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)。  
 
 <sup>2</sup> 在 Linux 上，以 Linux 上的 SQL Server 為目標的 Windows 電腦支援 PowerShell 指令碼。 
##  <a name="DevTools"></a> 開發工具  
  
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
|基本 Python 整合|是|是|是|是|否|
|進階 Python 整合|是|否|否|否|否| 
|Machine Learning 伺服器 (獨立式)|是|否|否|否|否|   
|Polybase 計算節點|是|是 <sup>1</sup>|是 <sup>1</sup>、 <sup>2</sup>|是 <sup>1</sup>,|是 <sup>1</sup>, | 
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
|圖表|是|是|是|是|是|  


<sup>1</sup> 使用多個運算節點向外延展時需要標題節點。

## <a name="IS"></a> Integration Services

如需 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 版本支援的 SQL Server Integration Services (SSIS) 功能相關資訊，請參閱 [SQL Server 版本支援的 Integration Services 功能](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md)。

##  <a name="MDS"></a> Master Data Services  
 如需 [!INCLUDE[ssNoVersion_md](../includes/ssNoVersion_md.md)] 版本所支援之 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 和 Data Quality Services 功能的資訊，請參閱 [SQL Server 版本支援的 Master Data Services 和 Data Quality Services 功能](../master-data-services/master-data-services-and-data-quality-services-features-support.md)。 

  
##  <a name="DW"></a> 資料倉儲  
  
|功能|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|建立不含資料庫的 Cube|是|是|否|否|否 |   
|自動產生暫存和資料倉儲結構描述|是|是|否|否|否| 
|異動資料擷取|是|是|否|否|否| 
|星型聯結查詢最佳化|是|否|否|否|否| 
|可擴充的唯讀 Analysis Services 組態|是|否|否|否|否| 
|分割區資料表和索引上的查詢平行處理|是|否|否|否|否|   
|全域批次彙總|是|否|否|否|否| 

##  <a name="SSAS"></a> Analysis Services  
  
如需 [!INCLUDE[ssNoVersion_md](../includes/ssNoVersion_md.md)] 版本所支援之 Analysis Services 功能的資訊，請參閱 [SQL Server 版本支援的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。 
  
##  <a name="BIMD"></a> BI 語意模型 (多維度)  
  
如需 [!INCLUDE[ssNoVersion_md](../includes/ssNoVersion_md.md)] 版本所支援之 Analysis Services 功能的資訊，請參閱 [SQL Server 版本支援的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。
   
##  <a name="BIT"></a> BI 語意模型 (表格式)  
  
如需 [!INCLUDE[ssNoVersion_md](../includes/ssNoVersion_md.md)] 所支援之 Analysis Services 功能的資訊，請參閱 [SQL Server 版本支援的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。
  
##  <a name="PPSP"></a> Power Pivot for SharePoint  
  
如需 [!INCLUDE[ssNoVersion_md](../includes/ssNoVersion_md.md)] 版本所支援之 Power Pivot for SharePoint 功能的資訊，請參閱 [SQL Server 版本支援的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。
  
##  <a name="DM"></a> 資料採礦  
  
如需 [!INCLUDE[ssNoVersion_md](../includes/ssNoVersion_md.md)] 版本所支援之資料採礦功能的資訊，請參閱 [SQL Server 版本支援的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。
  
##  <a name="SSRS"></a> Reporting Services  
  
如需 [!INCLUDE[ssNoVersion_md](../includes/ssNoVersion_md.md)] 版本所支援之 Reporting Services 功能的資訊，請參閱 [SQL Server 版本支援的 Reporting Services 功能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)。

##  <a name="BIC"></a> 商業智慧用戶端  

如需 [!INCLUDE[ssNoVersion_md](../includes/ssNoVersion_md.md)] 版本所支援之商業智慧用戶端功能的資訊，請參閱 [SQL Server 版本支援的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)或 [SQL Server 版本支援的 Reporting Services 功能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)。
  
##  <a name="SLS"></a> 空間和定位服務  
  
|功能名稱|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|空間索引|是|是|是|是|是|   
|平面與 Geodetic 資料類型|是|是|是|是|是| 
|進階空間程式庫|是|是|是|是|是|   
|匯入/匯出業界標準空間資料格式|是|是|是|是|是|   
  
##  <a name="ADS"></a> 其他資料庫服務  
  
|功能名稱|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------| 
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|是|是|是|是|是|   
|Database Mail|是|是|是|否|否| 
  
##  <a name="Other"></a> 其他元件  
  
|功能名稱|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------|  
|StreamInsight|StreamInsight Premium 版|StreamInsight Standard 版|StreamInsight Standard 版|否|否| 
|StreamInsight HA|StreamInsight Premium 版|否|否|否|否|   

> [![Download SSMS](../analysis-services/media/download.png)](../ssms/download-sql-server-management-studio-ssms.md) **[Download the latest version of SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)**     
  
## <a name="next-steps"></a>後續步驟 
 [SQL Server 的產品規格](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)   
 [SQL Server 安裝](../database-engine/install-windows/installation-for-sql-server-2016.md)  
 
 [!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]