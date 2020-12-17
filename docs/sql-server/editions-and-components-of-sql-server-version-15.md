---
description: " 的版本和支援功能[!INCLUDE[sssqlv15-md](../includes/sssqlv15-md.md)]"
title: SQL Server 2019 的版本及支援功能 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
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
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: e0a8f226602ab41422715368fb12c13809fa6b40
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477149"
---
# <a name="editions-and-supported-features-of-sssqlv15-md"></a> 的版本和支援功能[!INCLUDE[sssqlv15-md](../includes/sssqlv15-md.md)]

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx](../includes/applies-to-version/sqlserver.md)]

此主題提供各種 [!INCLUDE[sssqlv15-md](../includes/sssqlv15-md.md)] 版本所支援之功能的詳細資料。

如需舊版的資訊，請參閱：

* [SQL Server 2017](editions-and-components-of-sql-server-2017.md)
* [SQL Server 2016](editions-and-components-of-sql-server-2016.md)

安裝需求根據應用程式的需要而異。 不同的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本可配合組織和個人的獨特效能、執行階段和價格需求。 安裝的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 元件也將取決於您的特定需求。 下列章節幫助您了解如何在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的可用版本和元件之間做出最好的選擇。

[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Evaluation 版本提供 180 天的試用期。

如需最新版本資訊和新功能資訊，請參閱下列項目：

* [[!INCLUDE[sssqlv15-md](../includes/sssqlv15-md.md)] 版本資訊](../sql-server/sql-server-version-15-release-notes.md)
* [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2019 的新功能](../sql-server/what-s-new-in-sql-server-ver15.md)

**試用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]！：[從評估中心下載 [!INCLUDE[sssqlv15-md](../includes/sssqlv15-md.md)]](https://www.microsoft.com//evalcenter/evaluate-sql-server)**

## <a name="ssnoversion-editions"></a>[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] 版本

下表描述 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的版本。

|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|定義|
|---------------------------------------|----------------|
|Enterprise|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise 版本這套頂級供應項目不但提供完整的高階資料中心功能，而且具備急速效能、不受限制的虛擬化<sup>1</sup>，以及端對端商業智慧，能針對任務關鍵性工作負載，以及使用者存取資料見解的能力提供最高的服務等級。|
|標準|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard 版本針對部門和小型組織提供基本的資料管理與商業智慧資料庫來執行應用程式，並且支援適用於內部部署與雲端的一般開發工具，能以最少的 IT 資源提供最有效率的資料庫管理。|
|Web|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web Edition 對於 Web 主機服務提供者和 Web VAP 而言是一個擁有權總成本低廉的選項，可針對小型到大型規模的 Web 資產提供具延展性、負擔輕鬆且管理方便的功能。|
|開發人員|[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer Edition 可讓開發人員在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上建立任何類型的應用程式。 其中包含 Enterprise Edition 的所有功能，但是只授權做為開發和測試系統使用，而不做為實際伺服器使用。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer 是供應用程式建立和測試人員使用的理想選擇。|
|Express 版本|Express Edition 是入門級免費伺服器，非常適合用來學習及建置桌上型電腦和小型伺服器資料驅動應用程式。 這個版本是獨立軟體廠商、開發人員及建置用戶端應用程式之愛好者的最佳選擇。 如果您需要更進階的資料庫功能， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express 可以順利地升級為其他更高階的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express LocalDB 是輕量版 Express，其中包含所有程式設計功能，以使用者模式執行，並配備快速的零設定安裝，而且所需必要條件很少。|

<sup>1</sup> 不受限制的虛擬化可供具有[軟體保證](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default)的客戶在 Enterprise Edition 中使用。 部署必須遵守授權指南。 如需詳細資訊，請參閱我們的定價和授權頁面。

## <a name="using-ssnoversion-with-clientserver-applications"></a>搭配用戶端/伺服器應用程式使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]

您可以在執行用戶端/伺服器應用程式的電腦上只安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用戶端元件，這些應用程式會直接連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的執行個體。 如果您要在資料庫伺服器上管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體，或您打算開發 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 應用程式，則用戶端元件安裝也是一個不錯的選項。

用戶端工具選項會安裝下列 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能：回溯相容性元件、 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]、連接元件、管理工具、軟體開發套件和《 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》元件。 如需詳細資訊，請參閱[安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]](../database-engine/install-windows/install-sql-server.md)。

### <a name="running-with-iis"></a>使用 IIS 執行

在網際網路伺服器 (例如執行 Internet Information Services (IIS) 的伺服器) 上，您通常會安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用戶端工具。 用戶端工具包括連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體的應用程式所使用的用戶端連接元件。

>[!NOTE]
>雖然您可以在執行 IIS 的電腦上安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體，但通常只有針對具有單一伺服器電腦的小型網站才會這麼做。 大部分網站會將它們的中介層 IIS 系統放在一部伺服器或伺服器叢集上，並將其資料庫放在另一部伺服器或伺服器聯盟上。

## <a name="deciding-among-ssnoversion-components"></a>在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 元件之間作決定

使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安裝精靈的 [特徵選取] 頁面來選取要併入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]安裝的元件。 依預設，不會選取樹狀結構中的任何功能。

請使用下表中的資訊來判斷最符合您需求的功能集。

|伺服器元件|描述|
|-----------------------|-----------------|
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 包含 [!INCLUDE[ssDE](../includes/ssde-md.md)]，這是適用於儲存、處理和保護資料；複寫；全文檢索搜尋；用來管理關聯式和 XML 資料的工具；資料庫內分析整合，以及適用於存取 Hadoop 與其他異質資料來源的 PolyBase 整合，以及機器學習服務以搭配關聯式資料執行 Python 和 R 指令碼的核心服務。|
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 包括用來建立及管理線上分析處理 (OLAP) 和資料採礦應用程式的工具。|
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 包括伺服器和用戶端元件，可用來建立、管理和部署表格式、矩陣、圖形化和自由形式報表。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 也是一個可延伸的平台，可讓您用來開發報表應用程式。|
|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 是一組圖形化工具和可程式化物件，用來移動、複製和轉換資料。 其中還包括 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] 的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)](DQS) 元件。|
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) 是用於主要資料管理的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 方案。 MDS 可設定為管理任何網域 (產品、客戶、帳戶) 而且包括階層、更細微的安全性、交易、資料版本控制和商務規則，以及可用來管理資料的 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 。|
|Machine Learning 服務 (資料庫內)|Machine Learning 服務 (資料庫內) 支援使用企業資料來源之可調整的分散式 Machine Learning 解決方案。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2016 中，支援 R 語言。 [!INCLUDE[sssqlv15-md](../includes/sssqlv15-md.md)] 支援 R 和 Python。|
|Machine Learning 伺服器 (獨立式)|Machine Learning 伺服器 (獨立式) 支援在多種平台上部署分散式、可調整的 Machine Learning 解決方案，以及使用多種企業資料來源，包括 Linux 和 Hadoop。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2016 中，支援 R 語言。 [!INCLUDE[sssqlv15-md](../includes/sssqlv15-md.md)] 支援 R 和 Python。|

|管理工具|描述|
|----------------------|-----------------|
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) 是一個整合式環境，可存取、設定、管理 (Manage)、管理 (Administer) 及開發 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的元件。 SSMS 可讓所有技能等級的開發人員和管理員使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 最新版本的 SSMS 會更新 SMO，其包含 [SQL 評定 API](../tools/sql-assessment-api/sql-assessment-api-overview.md)。<br /><br/> 下載和安裝 <br />[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 從[下載 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Studio](https://msdn.microsoft.com/library/mt238290.aspx)|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服務、伺服器通訊協定、用戶端通訊協定和用戶端別名提供基本組態管理。|
|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 提供圖形化使用者介面來監視 [!INCLUDE[ssDE](../includes/ssde-md.md)] 或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的執行個體。|
|[!INCLUDE[ssDE](../includes/ssde-md.md)] Tuning Advisor|[!INCLUDE[ssDE](../includes/ssde-md.md)] Tuning Advisor 協助您建立一組最佳的索引、索引檢視表和分割區。|
|Data Quality Client|提供相當簡單且高度直覺式的圖形使用者介面來連接 DQS 伺服器，以及執行資料清除作業。 此外還可讓您集中監控資料清除作業期間執行的各種活動。|
|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 提供 IDE，可用來為下列商業智慧元件建立方案： [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]及 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]。<br /><br /> (先前稱為 Business Intelligence Development Studio)。<br /><br /> [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 也包含「資料庫專案」，為資料庫開發人員提供整合環境，以實現 Visual Studio 內任何 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 平台 (內部和外部部署) 適用的所有資料庫設計工作。 資料庫開發人員可以使用 Visual Studio 中的增強伺服器總管，輕鬆建立或編輯資料庫物件和資料，或執行查詢。|
|連接元件|安裝用於用戶端和伺服器之間通訊的元件以及用於 DB-Library、ODBC 和 OLE DB 的網路程式庫。|

|文件|描述|
|-------------------|-----------------|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的核心文件集。|

**Developer 和 Evaluation 版本** 如需 Developer 和 Evaluation 版本所支援的功能，請參閱下列各表中針對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise 版本列出的功能。

Developer 版本會繼續支援 1 個 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md) 用戶端。

## <a name="scale-limits"></a><a name="Cross-BoxScaleLimits"></a> 調整限制

|功能|Enterprise|標準|Web|Express with<br/>Advanced Services|Express|
|-------|--------:|------:|---:|-------------------------------:|-----:|
|單一執行個體所使用的計算容量上限 - [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|作業系統最大值|限制為 4 個插槽或 24 個核心的較小者|限制為 4 個插槽或 16 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|
|單一執行個體所使用的計算容量上限 - [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|作業系統最大值|限制為 4 個插槽或 24 個核心的較小者|限制為 4 個插槽或 16 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|限制為 1 個插槽或 4 個核心的較小者|
|每個 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]執行個體的緩衝集區記憶體上限|作業系統最大值|128 <nobr/>GB|64 <nobr/>GB|1410 <nobr/>MB|1410<nobr/> MB|
|每個 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]執行個體的資料行存放區區段快取記憶體上限|無限制的記憶體| 32 <nobr/>GB| 16 <nobr/>GB| 352 <nobr/>MB| 352 <nobr/>MB|
|每個 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]資料庫的記憶體最佳化資料大小上限|無限制的記憶體| 32 <nobr/>GB| 16 <nobr/>GB| 352 <nobr/>MB| 352 <nobr/>MB|
|每個 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]執行個體使用的記憶體上限|作業系統最大值|16 <nobr/>GB<sup>2</sup><br /><br /> 64 <nobr/>GB<sup>3</sup>|N/A|N/A|N/A|
|每個 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]執行個體使用的記憶體上限|作業系統最大值|64 <nobr/>GB|64 <nobr/>GB|4 <nobr/>GB|N/A|
|關聯式資料庫大小上限|524 <nobr/> PB|524 <nobr/> PB|524 <nobr/> PB|10 <nobr/>GB|10 <nobr/>GB|

<sup>1</sup> 以含伺服器 + 用戶端存取使用權 (CAL) 的 Enterprise 版本為基礎的授權 (不適用新合約) 具有每個 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體最多 20 個核心的限制。 核心伺服器授權模式之下沒有任何限制。 如需詳細資訊，請參閱 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本的計算容量限制](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。

<sup>2</sup> 表格式

<sup>3</sup> MOLAP

## <a name="rdbms-high-availability"></a><a name="RDBMSHA"></a> RDBMS 高可用性

|功能|Enterprise|標準|Web|Express with<br/>Advanced Services|快速|
|-------|:--------:|:------:|:-:|--------------------------------:|:-----:|
|Server Core 支援<sup>1</sup>|是|是|是|是|是|
|記錄傳送|是|是|是|否|否|
|資料庫鏡像|是|是<sup>2</sup>|是<sup>3</sup>|是<sup>3</sup>|是<sup>3</sup>|
|備份壓縮|是|是|否|否|否|
|資料庫快照集|是|是|是|是|是|
|Always On 容錯移轉叢集執行個體<sup>4</sup>|是|是|否|否|否|
|Always On 可用性群組<sup>5</sup>|是|否|否|否|否|
|基本可用性群組<sup>6</sup>|否|是|否|否|否|
|自動讀取寫入連線重新路由 |是|否|否|否|否|
|線上頁面和檔案還原|是|否|否|否|否|
|線上索引建立與重建|是|否|否|否|否|
|繼續線上索引重建|是|否|否|否|否|
|線上結構描述變更|是|否|否|否|否|
|快速復原|是|否|否|否|否|
|加速資料庫復原|是|是|是|否|否|
|鏡像備份|是|否|否|否|否|
|熱新增記憶體和 CPU|是|否|否|否|否|
|資料庫復原建議程式|是|是|是|是|是|
|加密的備份|是|是|否|否|否|
|混合式備份至 Windows Azure (備份至 URL)|是|是|是|否|否|
|無叢集可用性群組 <sup>5、6</sup>|是|是|否|否|否|
|適用於災害復原的容錯移轉伺服器<sup>7</sup>|是|是|否|否|否|
|適用於高可用性的容錯移轉伺服器<sup>7</sup>|是|是|否|否|否|
|Azure 中適用於災害復原的容錯移轉伺服器<sup>7</sup>|是|是|否|否|否|

<sup>1</sup> 如需在 Server Core 上安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的詳細資訊，請參閱[在 Server Core 上安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]](../database-engine/install-windows/install-sql-server-on-server-core.md)。

<sup>2</sup> 僅限 FULL 安全性

<sup>3</sup> 僅限見證

<sup>4</sup> 在 Enterprise 版本上，節點數目是作業系統最大值。 Standard Edition 支援兩個節點。

<sup>5</sup> Enterprise 版本最多支援 8 個次要複本，包括 5 個同步次要複本。

<sup>6</sup> Standard 版本支援基本可用性群組。 基本可用性群組支援兩個複本，使用一個資料庫。 如需基本可用性群組的詳細資訊，請參閱[基本可用性群組](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md)。

<sup>7</sup> 需要[軟體保證](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default)。

## <a name="rdbms-scalability-and-performance"></a><a name="RDBMSSP"></a> RDBMS 延展性和效能

|功能|Enterprise|標準|Web|Express with<br/>Advanced Services|快速|
|------:|:--------:|:------:|:-:|:-------------------------------:|:------:|
|資料行存放區<sup>1</sup> <sup>2</sup>|是|是|是|是|是|
|叢集資料行存放區索引中的大型物件二進位檔|是|是|是|是|是|
|線上非叢集資料行存放區索引重建|是|否|否|否|否|
|記憶體內部資料庫：記憶體內部 OLTP<sup>1</sup>|是|是|是|是<sup>3</sup>|是|
|記憶體內部資料庫：混合式緩衝集區|是|是|否|否|否|
|記憶體內部資料庫：記憶體最佳化的 tempdb 中繼資料|是|否|否|否|否|
|記憶體內部資料庫：持續性記憶體支援|是|是|是|是|是|
|Stretch Database|是|是|是|是|是|
|多個執行個體支援|50|50|50|50|50|
|資料表和索引分割區|是|是|是|是|是|
|資料壓縮|是|是|是|是|是|
|資源管理員|是|否|否|否|否|
|分割資料表平行處理原則|是|否|否|否|否|
|多個 Filestream 容器|是|是|是|是|是|
|NUMA 感知大型分頁記憶體和緩衝區陣列配置|是|否|否|否|否|
|緩衝集區延伸|是|是|否|否|否|
|I/O 資源治理|是|否|否|否|否|
|預先讀取|是|否|否|否|否|
|進階掃描|是|否|否|否|否|
|延遲持久性|是|是|是|是|是|
|智慧型資料庫：自動調整|是|否|否|否|否|
|智慧型資料庫：資料列存放區的批次模式 <sup>1</sup>|是|否|否|否|否|
|智慧型資料庫：資料列模式記憶體授與回應|是|否|否|否|否|
|智慧型資料庫：近似計算相異|是|是|是|是|是|
|智慧型資料庫：資料表變數延遲編譯|是|是|是|是|是|
|智慧型資料庫：純量 UDF 內嵌|是|是|是|是|是|
|批次模式自適性聯結|是|否|否|否|否|
|批次模式記憶體授與意見反應|是|否|否|否|否|
|交錯執行多重陳述式資料表值函式|是|是|是|是|是|
|大量插入增強功能|是|是|是|是|是|

<sup>1</sup> 記憶體內部 OLTP 資料大小和資料行存放區區段快取，都會有依版本指定的記憶體數量限制，如[縮放限制](#Cross-BoxScaleLimits)一節中所述。 [批次模式](../relational-databases/query-processing-architecture-guide.md#batch-mode-execution)作業的平行處理原則程度 (DOP) 限制如下：[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard Edition 為 2，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Web Edition 和 Express Edition 為 1。 這會參考以磁碟式資料表和記憶體最佳化資料表建立的資料行存放區索引。

<sup>2</sup> 彙總下推、字串述詞下推和 SIMD 最佳化是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise 版本的可擴縮性增強功能。 如需詳細資料，請參閱[資料行存放區索引 - 新功能](../relational-databases/indexes/columnstore-indexes-what-s-new.md)。

<sup>3</sup> 這項功能不會納入 LocalDB 安裝選項。

## <a name="rdbms-security"></a><a name="RDBMSS"></a> RDBMS 安全性

|功能|Enterprise|標準|Web|Express with<br/>Advanced Services|Express|
|-------|:--------:|:------:|:-:|:-----:|:-----------------------:|:-----:|
|資料列層級安全性|是|是|是|是|是|
|Always Encrypted|是|是|是|是|是|
|具有安全記憶體保護區的 Always Encrypted|是|是|是|是|是|
|動態資料遮罩|是|是|是|是|是|
|伺服器稽核|是|是|是|是|是|
|資料庫稽核|是|是|是|是|是|
|透明資料庫加密|是|是|是|否|否|
|可延伸金鑰管理|是|是|否|否|否|
|使用者定義角色|是|是|是|是|是|
|自主資料庫|是|是|是|是|是|
|備份的加密|是|是|否|否|否|
|資料分類和稽核|是|是|是|是|是|

## <a name="replication"></a><a name="Replication"></a> 複寫

|功能|Enterprise|標準|Web|Express with<br/>Advanced Services|快速|
|-------|:---------:|:-------:|:--:|:--------------------------------:|:------:|
|異質性訂閱者|是|是|否|否|否|
|合併式複寫|是|是|是<sup>1</sup>|是<sup>1</sup>|是<sup>1</sup>|
|Oracle 發行|是|否|否|否|否|
|點對點異動複寫|是|否|否|否|否|
|快照式複寫|是|是|是<sup>1</sup>|是<sup>1</sup>|是<sup>1</sup>|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 變更追蹤|是|是|是|是|是|
|異動複寫|是|是|是<sup>1</sup>|是<sup>1</sup>|是<sup>1</sup>|
|異動複寫至 Azure|是|是|否|否|否|
|異動複寫可更新訂閱|是|是|否|否|否|

<sup>1</sup> 僅限訂閱者

## <a name="management-tools"></a><a name="SSMS"></a> 管理工具

|功能|Enterprise|標準|Web|Express with Advanced Services|Express|
|-------|:--------:|:------:|:-:|:----------------------------:|:-----:|
|SQL 管理物件 (SMO)|是|是|是|是|是|
|SQL 評定 API|是|是|是|是|是|
|SQL 弱點評定 |是|是|是|是|是|
|SQL 組態管理員|是|是|是|是|是|
|SQL CMD (命令提示字元工具)|是|是|是|是|是|
|Distributed Replay - 管理工具|是|是|是|是|否|
|Distribute Replay - Client|是|是|是|否|否|
|Distributed Replay - Controller|是<sup>1</sup>|是<sup>2</sup>|是<sup>2</sup>|否|否|
|SQL Profiler|是|是|否<sup>3</sup>|否<sup>3</sup>|否<sup>3</sup>|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent|是|是|是|否|否|
|Microsoft System Center Operations Manager 管理組件|是|是|是|否|否|
|Database Tuning Advisor (DTA)|是|是<sup>4</sup>|是<sup>4</sup>|否|否|

<sup>1</sup> 最多 16 個用戶端

<sup>2</sup> 1 個用戶端

<sup>3</sup> [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Web、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express with Tools 及 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express with Advanced Services 可使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Standard 及 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Enterprise 版本加以剖析。

<sup>4</sup> 僅針對 Standard 版本功能啟用調整

## <a name="rdbms-manageability"></a><a name="RDBMSM"></a> RDBMS 管理能力

|功能|Enterprise|標準|Web|Express with<br/>Advanced Services|快速|
|-------|:--------:|:------:|:-:|:-------------------------------:|:-----:|
|使用者執行個體|否|否|否|是|是|
|LocalDB|否|否|否|是|否|
|專用管理員連接|是|是|是|是<sup>1</sup>|是<sup>1</sup>|
|SysPrep 支援<sup>2</sup>|是|是|是|是|是|
|PowerShell 指令碼支援<sup>3</sup>|是|是|是|是|是|
|資料層應用程式元件作業的支援 - 擷取、部署、升級、刪除|是|是|是|是|是|
|原則自動化 (依排程和變更檢查)|是|是|是|否|否|
|效能資料收集器|是|是|是|否|否|
|能夠在多重執行個體管理中註冊為受管理的執行個體|是|是|是|否|否|
|標準效能報告|是|是|是|否|否|
|計畫指南和計畫指南的計畫凍結|是|是|是|否|否|
|索引檢視表的直接查詢 (使用 NOEXPAND 提示)|是|是|是|是|是|
|直接查詢 SQL Server Analysis Services|是|是|否|否|是|
|自動索引檢視表維護|是|是|是|否|否|
|分散式分割區檢視|是|否|否|否|否|
|平行索引作業|是|否|否|否|否|
|查詢最佳化工具自動使用索引檢視表|是|否|否|否|否|
|平行一致性檢查|是|否|否|否|否|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 公用程式控制點|是|否|否|否|否|
|緩衝集區延伸|是|是|否|否|否|
|適用於巨量資料叢集的主要執行個體|是|是|否|否|否|
|相容性認證|是|是|是|是|是|

<sup>1</sup> 具有追蹤旗標

<sup>2</sup> 如需詳細資訊，請參閱[使用 SysPrep 安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的考量](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)。

<sup>3</sup> 在 Linux 上，以 Linux 上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 為目標的 Windows 電腦支援 PowerShell 指令碼。

## <a name="development-tools"></a><a name="DevTools"></a> 開發工具

|功能|Enterprise|標準|Web|Express with<br/>Advanced Services|快速|
|-------|:--------:|:------:|:-:|:-------------------------------:|:-----:|
|Microsoft Visual Studio 整合|是|是|是|是|是|
|Intellisense (Transact-SQL 和 MDX)|是|是|是|是|是|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools (SSDT)|是|是|是|是|否|
|MDX 編輯、偵錯和設計工具|是|是|否|否|否|

## <a name="programmability"></a><a name="Programmability"></a> Programmability

|功能|Enterprise|標準|Web|Express with<br/>Advanced Services|快速
|-------|:--------:|:------:|:-:|:-------------------------------:|:-----:|
|基本 R 整合<sup>1</sup>|是|是|是|是|否|
|進階 R 整合<sup>2</sup>|是|否|否|否|否|
|基本 Python 整合|是|是|是|是|否|
|進階 Python 整合|是|否|否|否|否|
|Machine Learning 伺服器 (獨立式)|是|否|否|否|否|
|PolyBase 計算節點|是|是<sup>3</sup>|是<sup>3</sup>|是<sup>3</sup>|是<sup>3</sup> |
|PolyBase 前端節點<sup>4</sup>|是|是|否|否|否|
|JSON|是|是|是|是|是|
|查詢存放區|是|是|是|是|是|
|Temporal|是|是|是|是|是|
|Common Language Runtime (CLR) 整合|是|是|是|是|是|
|Java Language Runtime 整合|是|是|是|是|是|
|原生 XML 支援|是|是|是|是|是|
|XML 索引|是|是|是|是|是|
|MERGE 與 UPSERT 功能|是|是|是|是|是|
|FILESTREAM 支援|是|是|是|是|是|
|FileTable|是|是|是|是|是|
|日期和時間資料類型|是|是|是|是|是|
|國際化支援|是|是|是|是|是|
|全文檢索和語意搜尋|是|是|是|是|否|
|查詢中的語言規格|是|是|是|是|否|
|Service Broker (訊息)|是|是|否<sup>5</sup>|否<sup>5</sup>|否<sup>5</sup>|
|Transact-SQL 端點|是|是|是|否|否|
|圖形|是|是|是|是|是|
|UTF-8 支援|是|是|是|是|是|

<sup>1</sup> 基本整合僅限使用 2 個核心及記憶體內部資料集。

<sup>2</sup> 進階整合可依硬體限制，使用所有可用核心來平行處理任何大小的資料集。

<sup>3</sup> 使用多個計算節點相應放大需要前端節點。

<sup>4</sup> 在 SQL Server 2019 之前，PolyBase 前端節點需要 Enterprise 版本。

<sup>5</sup> 僅限用戶端

## <a name="integration-services"></a><a name="IS"></a> Integration Services

如需 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 的各版本所支援的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Integration Services (SSIS) 功能相關資訊，請參閱 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本支援的 Integration Services 功能](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md)。

## <a name="master-data-services"></a><a name="MDS"></a> Master Data Services

如需 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 的各版本所支援的 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] 和 Data Quality Services 功能相關資訊，請參閱 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本支援的 Master Data Services 和 Data Quality Services 功能](../master-data-services/master-data-services-and-data-quality-services-features-support.md)。

## <a name="data-warehouse"></a><a name="DW"></a> 資料倉儲

|功能|Enterprise|標準|Web|Express with<br/>Advanced Services|快速|
|-------|:--------:|:------:|:-:|:-------------------------------:|:-----:|
|自動產生暫存和資料倉儲結構描述|是|是|否|否|否|
|變更資料擷取|是|是|否|否|否|
|星型聯結查詢最佳化|是|否|否|否|否|
|分割區資料表和索引上的查詢平行處理|是|否|否|否|否|
|全域批次彙總|是|否|否|否|否|

## <a name="analysis-services"></a><a name="SSAS"></a> Analysis Services

如需 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 的各版本所支援的 Analysis Services 功能相關資訊，請參閱 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本支援的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)。

## <a name="reporting-services"></a><a name="SSRS"></a> Reporting Services

如需 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 的各版本所支援的 Reporting Services 功能相關資訊，請參閱 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本支援的 Reporting Services 功能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)。

## <a name="business-intelligence-clients"></a><a name="BIC"></a> 商業智慧用戶端

如需 [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 各版本所支援的商業智慧用戶端功能相關資訊，請參閱 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本支援的 Analysis Services 功能](../analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016.md)或 [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本支援的 Reporting Services 功能](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md)。

## <a name="spatial-and-location-services"></a><a name="SLS"></a> 空間和定位服務

|功能名稱|Enterprise|標準|Web|Express with<br/>Advanced Services|Express|
|-------------|:-------:|:------:|:-:|:-------------------------------:|:-----:|
|空間索引|是|是|是|是|是|
|平面與 Geodetic 資料類型|是|是|是|是|是|
|進階空間程式庫|是|是|是|是|是|
|匯入/匯出業界標準空間資料格式|是|是|是|是|是|

## <a name="additional-database-services"></a><a name="ADS"></a> 其他資料庫服務

|功能名稱|Enterprise|標準|Web|Express with<br/>Advanced Services|快速|
|------------|:--------:|:------:|:-:|:-------------------------------:|:-----:|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Migration Assistant|是|是|是|是|是|
|Database Mail|是|是|是|否|否|

## <a name="other-components"></a><a name="Other"></a> 其他元件

|功能名稱|Enterprise|標準|Web|Express with<br/>Advanced Services|快速|
|------------|:--------:|:------:|:-:|:-------------------------------:|:-----:|
|StreamInsight|StreamInsight Premium 版|StreamInsight Standard 版|StreamInsight Standard 版|否|否|
|StreamInsight HA|StreamInsight Premium 版|否|否|否|否|

## <a name="next-steps"></a>後續步驟

[[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的產品規格](https://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)

[[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的安裝](../database-engine/install-windows/installation-for-sql-server-2016.md)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
