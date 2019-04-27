---
title: SQL Server 2014 的版本和元件 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
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
ms.assetid: e5186f02-dd91-47d0-8fa4-de3f41c76903
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9610dc1cc729dc555d42c0dfe5eeb117f9cfba18
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806338"
---
# <a name="editions-and-components-of-sql-server-2014"></a>SQL Server 2014 的版本和元件
  安裝需求根據應用程式的需要而異。 不同的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本可配合組織和個人的獨特效能、執行階段和價格需求。 安裝的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 元件也將取決於您的特定需求。 下列章節幫助您了解如何在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的可用版本和元件之間做出最好的選擇。  
  
## <a name="principal-editions-of-includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的主要版本  
 下表描述 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的主要版本。 如需詳細資訊，請參閱[支援的 SQL Server 2014 的版本功能](../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|定義|  
|---------------------------------------|----------------|  
|Enterprise (64 位元和 32 位元)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Enterprise Edition 這套頂級供應項目不但提供完整的高階資料中心功能，而且具備急速效能、不受限制的虛擬化以及端對端商業智慧 - 為關鍵任務工作負載提供最高的服務等級，並且讓使用者獲得資料洞察能力。|  
|Business Intelligence (64 位元和 32 位元)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Business Intelligence Edition 提供了一套完整的平台，讓組織能夠建置並部署安全、可擴充且可管理的 BI 方案。 此外，它提供了創新的功能，例如瀏覽器架構的資料探索和視覺效果、功能強大的資料結合功能，以及強化的整合管理。|  
|Standard (64 位元和 32 位元)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Standard Edition 針對部門和小型組織提供基本的資料管理與商業智慧資料庫來執行應用程式，並且支援內部部署和雲端的一般開發工具 - 以最少的 IT 資源提供最有效率的資料庫管理。|  
  
## <a name="specialized-editions-of-includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的特殊版本  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的特殊版本是以商業工作負載為目標。 下表描述 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的特殊版本。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|描述|  
|---------------------------------------|-----------------|  
|Web (64 位元和 32 位元)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Web Edition 對於 Web 主控者和 Web VAP 而言是一個整體擁有成本很低的選擇，可針對小型到大型規模的 Web 屬性提供可擴充、負擔輕鬆而且管理方便的功能。|  
  
## <a name="breadth-editions-of-includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 的廣泛版本  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的廣泛版本是針對特定客戶案例所設計，將免費提供或以非常低廉的成本提供。 下表描述 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的廣泛版本。  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|描述|  
|---------------------------------------|-----------------|  
|Developer (64 位元和 32 位元)|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Developer Edition 可讓開發人員在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]上建立任何類型的應用程式。 其中包含 Enterprise Edition 的所有功能，但是只授權做為開發和測試系統使用，而不做為實際伺服器使用。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer 是供應用程式建立和測試人員使用的理想選擇。|  
|Express (64 位元和 32 位元) Edition|[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Express Edition 是入門級免費伺服器，非常適合用來學習及建置桌上型電腦和小型伺服器資料驅動應用程式。 這個版本是獨立軟體廠商、開發人員及建置用戶端應用程式之愛好者的最佳選擇。 如果您需要更進階的資料庫功能， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express 可以順利地升級為其他更高階的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express LocalDB 是輕量版 Express，其中包含所有程式設計功能但是以使用者模式執行，並配備快速的零設定安裝，而且所需必要條件很少。|  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-an-internet-server"></a>搭配網際網路伺服器使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
 在網際網路伺服器中，例如執行 Internet Information Services (IIS) 的伺服器，您通常會安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用戶端工具。 用戶端工具包括連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]執行個體的應用程式所使用的用戶端連接元件。  
  
> [!NOTE]  
>  雖然您可以在執行 IIS 的電腦上安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體，但通常只有針對具有單一伺服器電腦的小型網站才會這麼做。 大部分網站會將它們的中介層 IIS 系統放在一部伺服器或伺服器叢集上，並將其資料庫放在另一部伺服器或伺服器聯盟上。  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-with-clientserver-applications"></a>搭配用戶端/伺服器應用程式使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
 您可以在執行用戶端/伺服器應用程式的電腦上只安裝 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 用戶端元件，這些應用程式會直接連接到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的執行個體。 如果您要在資料庫伺服器上管理 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行個體，或您打算開發 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 應用程式，則用戶端元件安裝也是一個不錯的選項。  
  
 用戶端工具選項會安裝下列 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 功能：回溯相容性元件、 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]、連接元件、管理工具、軟體開發套件和《 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書》元件。 如需詳細資訊，請參閱 <<c0> [ 從安裝精靈安裝 SQL Server 2014&#40;安裝&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)。</c0>  
  
## <a name="deciding-among-includessnoversionincludesssnoversion-mdmd-components"></a>在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 元件之間作決定  
 使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安裝精靈的 [特徵選取] 頁面來選取要併入 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]安裝的元件。 依預設，不會選取樹狀結構中的任何功能。  
  
 請使用下表中的資訊來判斷最符合您需求的功能集。  
  
|伺服器元件|描述|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 包含 [!INCLUDE[ssDE](../includes/ssde-md.md)]、用來儲存、處理及保護資料安全的核心服務、複寫、全文檢索搜尋功能、用來管理關聯式和 XML 資料的工具，以及 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 伺服器。|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 包括用來建立及管理線上分析處理 (OLAP) 和資料採礦應用程式的工具。|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 包括伺服器和用戶端元件，可用來建立、管理和部署表格式、矩陣、圖形化和自由形式報表。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 也是一個可延伸的平台，可讓您用來開發報表應用程式。|  
|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 是一組圖形化工具和可程式化物件，用來移動、複製和轉換資料。 其中還包括 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] 的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)](DQS) 元件。|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) 是用於主要資料管理的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 方案。 MDS 可設定為管理任何網域 (產品、客戶、帳戶) 而且包括階層、更細微的安全性、交易、資料版本控制和商務規則，以及可用來管理資料的 [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] 。|  
  
|管理工具|描述|  
|----------------------|-----------------|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 是一個整合式環境，可存取、設定、管理及開發 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的元件。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 可讓所有技能等級的開發人員和管理員使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 組態管理員對 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服務、伺服器通訊協定、用戶端通訊協定和用戶端別名提供基本組態管理。|  
|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 提供圖形化使用者介面來監視 [!INCLUDE[ssDE](../includes/ssde-md.md)] 或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的執行個體。|  
|[!INCLUDE[ssDE](../includes/ssde-md.md)] Tuning Advisor|[!INCLUDE[ssDE](../includes/ssde-md.md)] Tuning Advisor 協助您建立一組最佳的索引、索引檢視表和分割區。|  
|Data Quality Client|提供相當簡單且高度直覺式的圖形使用者介面來連接 DQS 伺服器，以及執行資料清除作業。 此外還可讓您集中監控資料清除作業期間執行的各種活動。|  
|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 提供 IDE，可用來為下列商業智慧元件建立方案： [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]及 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]。<br /><br /> (先前稱為 Business Intelligence Development Studio)。<br /><br /> [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 也包含「資料庫專案」，為資料庫開發人員提供整合環境，以實現 Visual Studio 內任何 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 平台 (內部和外部部署) 適用的所有資料庫設計工作。 資料庫開發人員可以使用 Visual Studio 中的增強伺服器總管，輕鬆建立或編輯資料庫物件和資料，或執行查詢。|  
|連接元件|安裝用於用戶端和伺服器之間通訊的元件以及用於 DB-Library、ODBC 和 OLE DB 的網路程式庫。|  
  
|文件集|描述|  
|-------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 線上叢書|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的核心文件集。|  
  
## <a name="see-also"></a>另請參閱  
 [規劃 SQL Server 安裝](install/planning-a-sql-server-installation.md)   
 [從安裝精靈安裝 SQL Server 2014&#40;安裝程式&#41;](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
  
