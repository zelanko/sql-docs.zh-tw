---
title: 支援的版本與版本升級 | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- components [SQL Server], adding to existing installations
- versions [SQL Server], upgrading
- upgrading SQL Server, upgrades supported
- cross-language support
ms.assetid: 702359c4-6ca9-42a8-860c-a95a802898a1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a245aab71292e1482bd5a17bd32a27bded640ab
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62775216"
---
# <a name="supported-version-and-edition-upgrades"></a>支援的版本與版本升級
  您可以從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]升級。 本主題列出這些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的支援升級路徑，以及可以升級至 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 的支援版本。  
  
## <a name="pre-upgrade-checklist"></a>升級前檢查清單  
  
-   從 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 的一個版本升級到另一個版本之前，請確認您目前使用的功能在您目標版本中受到支援。  
  
-   在升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，請對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 啟用 Windows 驗證，並確認預設組態： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務帳戶是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系統管理員 (sysadmin) 群組的成員。  
  
-   若要升級到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，您必須執行支援的作業系統。 如需詳細資訊，請參閱＜ [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)＞。  
  
-   當重新啟動暫止時將會封鎖升級  
  
-   如果 Windows Installer 服務未在執行中，將會封鎖升級。  
  
## <a name="unsupported-scenarios"></a>不支援的案例  
  
-   不支援 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 的跨版本執行個體。 在 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體內， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 和 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]元件的版本號碼都必須相同。  
  
-   不支援跨平台升級。 您無法使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式，將 32 位元的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體升級到原生 64 位元。 不過，您還是可以備份或卸離 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之 32 位元執行個體的資料庫，而且如果複寫時未發行這些資料庫，也可以將它們還原或附加至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (64 位元) 的新執行個體。 您必須在 master、msdb 和 model 系統資料庫中重新建立任何登入及其他使用者物件。  
  
-   您無法在升級現有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體期間加入新功能。 將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 之後，可使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝程式加入功能。 如需詳細資訊，請參閱[將功能加入至 SQL Server 2014 的實例 &#40;安裝&#41;](add-features-to-an-instance-of-sql-server-setup.md)。  
  
-   在 WOW 模式下不支援容錯移轉叢集。  
  
-   不支援從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 Evaluation Edition 升級。  
  
## <a name="upgrades-from-earlier-versions-to-sssql14"></a>從舊版升級至 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
> [!NOTE]  
>  下一節＜ [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 對[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 的支援＞會更詳細地描述 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的支援。  
  
-   在 64 位元伺服器的 32 位元子系統 (WOW64) 上，可以將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 32 位元版本升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 64 位元版本只能升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 64 位元伺服器。  
  
> [!NOTE]  
>  當您從舊版 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise Edition 升級至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，請選擇 [Enterprise Edition：核心授權] 或 [Enterprise Edition]。 這些 Enterprise edition 只有在授權模式及支援的核心數目上限方面有差異。 如需詳細資訊，請參閱 [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 支援從下列版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 進行升級：  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 或更新版本  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 或更新版本  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 或更新版本  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 或更新版本  
  
 下表列出從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級至 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 的支援案例。  
  
|升級來源|支援的升級路徑|  
|------------------|----------------------------|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express with Tools，以及<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Small Business|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express with Tools，以及<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Datacenter|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Small Business|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express with Tools，以及<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express with Tools，以及<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express Management Studio，以及<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Business Intelligence|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br />  Business Intelligence|  
  
### <a name="sssql14-support-for-ssversion2005"></a>[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 的 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 支援  
 本節將討論 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 對 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 的支援。 在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 中，您將能夠進行下列作業：  
  
-   使用安裝精靈或是從命令提示字元執行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 安裝程式，將 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 的資料庫引擎執行個體升級到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 。  
  
-   將 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫 (mdf/ldf 檔案) 附加到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 的 Database Engine 執行個體。  
  
-   從備份將 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫還原到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 的 Database Engine 執行個體。  
  
-   將 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 封裝升級到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。 執行封裝並包含自動就地升級。  
  
-   藉由執行 [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] 安裝程式將 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 升級到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 。  
  
-   備份 [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] Cube 並在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]上還原。  
  
-   藉由執行 [!INCLUDE[ssRSversion2005](../../includes/ssrsversion2005-md.md)] 安裝程式將 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 升級到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 。  
  
-   使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]2014 連接到 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 。  
  
 當 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫升級到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 時，資料庫的相容性層級將會從 90 變更為 100。 （在[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]中，資料庫相容性層級的有效值為100、110和120）。[ALTER Database 相容性層級 &#40;transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)討論相容性層級變更如何影響[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]應用程式。  
  
 未在上面清單中指定的任何情況都不受支援，包含但不限於以下項目：  
  
-   在相同電腦上安裝 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (並存安裝)。  
  
-   使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 執行個體當做與 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 執行個體有關之複寫拓撲的成員。  
  
-   在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 執行個體之間設定資料庫鏡像。  
  
-   在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 執行個體之間使用記錄傳送備份交易記錄。  
  
-   在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 執行個體之間設定連結的伺服器。  
  
-   從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Management Studio 管理 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 執行個體。  
  
-   在 [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] Management Studio 中附加 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Cube。  
  
-   從 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] Management Studio 連接到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。  
  
-   從 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] Management Studio 管理 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 服務。  
  
-   對 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 協力廠商自訂 Integration Services 元件的支援，例如執行和升級。  
  
## <a name="sssql14-edition-upgrade"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 版本升級  
 下表列出 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]中支援的版本升級案例。  
  
 如需如何執行版本升級的逐步指示，請參閱[升級至不同版本的 SQL Server 2014 &#40;安裝程式&#41;](upgrade-to-a-different-edition-of-sql-server-setup.md)。  
  
|升級來源|升級目標|  
|------------------|----------------|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]Enterprise （Server + CAL 和 Core） <sup>2</sup>| Business Intelligence|  
| Business Intelligence|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL 或 Core 授權)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]評估 Enterprise <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL 或 Core 授權)<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> 對於獨立安裝，支援從 Evaluation Enterprise (免費版本) 升級到任何付費版本，但對於叢集安裝則不支援。|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]標準<sup>2</sup>| Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL 或 Core 授權)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]開發人員<sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL 或 Core 授權)<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL 或 Core 授權)<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]Express <sup>1</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL 或 Core 授權)<br /><br />  Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
  
 此外，您也可以在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL 授權) 和 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Core 授權) 之間執行版本升級：  
  
|升級前版本|升級後版本|  
|--------------------------|------------------------|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]Enterprise （Server + CAL 授權） <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Core 授權)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Core 授權)|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL 授權)|  
  
 <sup>1</sup>也適用于[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] express with Tools 和[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] express with Advanced Services。  
  
 <sup>2</sup>變更[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]容錯移轉叢集的版本有所限制。 下列狀況不支援 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 容錯移轉叢集：  
  
-   SQL Server 2014 Enterprise 至 SQL Server 2014 Developer、Standard 和 Enterprise Evaluation。  
  
-   SQL Server 2014 Developer 至 SQL Server 2014 Standard 或 Enterprise Evaluation。  
  
-   SQL Server 2014 Standard 至 SQL Server 2014 Enterprise Evaluation。  
  
-   SQL Server 2014 Enterprise Evaluation 至 SQL Server 2014 Standard。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 版本所支援的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [安裝 SQL Server 2014 的硬體和軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [升級至 SQL Server 2014](upgrade-sql-server.md)   
 [使用 Upgrade Advisor 來準備升級](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)  
  
  
