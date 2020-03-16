---
title: SQL Server 安裝指南
ms.description: 'An index of content that helps you install SQL Server and associated components through various options such as the installation wizard, command prompt, or sysprep. '
ms.custom: ''
ms.date: 11/14/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- AdventureWorks sample database
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 30155a37f57391edeee916cd2b6629d63a1dcaaa
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/13/2020
ms.locfileid: "79288652"
---
# <a name="sql-server-installation-guide"></a>SQL Server 安裝指南

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

此文章為內容索引，提供在 Windows 上安裝 SQL Server 的指引。

如需了解其他部署案例，請參閱：

- [Linux](../../linux/sql-server-linux-setup.md)
- [Docker 容器](../../linux/sql-server-linux-configure-docker.md)
- [Kubernetes - 巨量資料叢集](../../big-data-cluster/deploy-get-started.md)

從 [!INCLUDE[sssql15](../../includes/sssql15-md.md)] 開始，[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 才可以用作 64 位元應用程式。 下列重要詳細資料說明如何取得 SQL Server 及其安裝方式。

## <a name="getting-started"></a>開始使用
  
* **版本和功能**：請檢閱 SQL Server 不同版本和版次的支援功能，以判斷哪一種最適合您的商務需求。 
    - [[!INCLUDE[ss2019](../../includes/sssqlv15-md.md)]](~/sql-server/editions-and-components-of-sql-server-version-15.md)＞。  
    - [[!INCLUDE[ss2017](../../includes/sssqlv14-md.md)]](~/sql-server/editions-and-components-of-sql-server-2017.md)＞。  
    - [[!INCLUDE[ss2016](../../includes/sssql15-md.md)]](~/sql-server/editions-and-components-of-sql-server-2016.md)＞。  
    - [[!INCLUDE[ss2014](../../includes/sssql14-md.md)]](https://technet.microsoft.com/library/cc645993(v=sql.120).aspx)

*  **需求**：請檢閱[規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)中的安裝需求、系統組態檢查及安全性考量 
  
* **範例資料庫與範例程式碼**： 
    * 這些預設不會隨著 SQL Server 安裝程式一起安裝，但可以找到 
    * 若要針對非 Express 版本的 SQL Server 安裝它們，請參閱[範例位置](../../samples/sql-samples-where-are.md) \(英文\)
    

## <a name="installation-media"></a>安裝媒體

[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 的下載位置因版本而異：

* **SQL Server Enterprise Edition、Standard Edition 與 Express Edition** 的授權可用於生產環境。 如需 Enterprise Edition 和 Standard Edition，請連絡您的軟體廠商取得安裝媒體。 購買資訊和 Microsoft 合作夥伴目錄請見 [Microsoft 授權頁面](https://www.microsoft.com/licensing/product-licensing/sql-server)。
* [免費版 - 最新版本](https://www.microsoft.com/sql-server/sql-server-downloads)
* [免費版 - 其他](https://www.microsoft.com/evalcenter/evaluate-sql-server)


您可以在這裡找到其他 SQL Server 元件： 

* [所有累積更新](https://sqlserverbuilds.blogspot.com/)
* [SQL Server Reporting Services](https://www.microsoft.com/download/details.aspx?id=100122)。 
* [Transact-SQL](https://aka.ms/ssmsfullsetup)
* [Azure Data Studio](https://go.microsoft.com/fwlink/?linkid=2109256)


## <a name="sql-server-installation"></a>SQL Server 安裝
 
|發行項|描述|  
|-----------|-----------------|  
|[安裝精靈](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)|使用從 setup.exe 安裝媒體啟動的安裝精靈 GUI 安裝 SQL Server。 |  
|[命令提示字元](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)|從命令提示字元執行 SQL Server 安裝的範例語法和安裝參數。 | 
|[Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md)|在 Windows Server Core 上安裝 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]。|  
|[檢查 System Configuration Checker 的參數](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|討論系統組態檢查 (SCC) 的功能。|   
|[組態檔](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)|透過組態檔執行安裝程式的範例語法及安裝參數。|  
|[SysPrep](../../database-engine/install-windows/install-sql-server-using-sysprep.md)|透過 SysPrep 執行安裝程式的範例語法及安裝參數。|
|[將功能新增至執行個體](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)|更新現有 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 執行個體的元件。|  
|[SQL Server 容錯移轉叢集安裝](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)| 安裝 SQL Server 容錯移轉叢集執行個體。  | 
|[修復失敗的 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 安裝](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)|修復損毀的 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 安裝。|  
|[以 SQL Server 重新命名電腦](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|在重新命名裝載 SQL Server 獨立執行個體之電腦的主機名稱之後，更新 sys.servers 中儲存的系統中繼資料。 |  
|[安裝 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 服務更新](../../database-engine/install-windows/install-sql-server-servicing-updates.md)|安裝 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 的更新。|  
|[設定記錄檔](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)| 檢視並讀取 SQL Server 安裝程式記錄檔中的錯誤。 |  
|[驗證安裝](../../database-engine/install-windows/validate-a-sql-server-installation.md)|檢閱 SQL 探索報告的使用狀況，以驗證電腦上所安裝之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。|  
  
  
## <a name="individual-component-installation"></a>個別元件安裝 
  
|發行項|描述|  
|-----------|-----------------|  
|[SQL Server 資料庫引擎](../../database-engine/install-windows/install-sql-server-database-engine.md)|安裝和設定 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。|  
|[SQL Server 複寫](../../database-engine/install-windows/install-sql-server-replication.md)|安裝和設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫。|  
|[Distributed Replay](../../tools/distributed-replay/install-distributed-replay-overview.md)|列出說明 Distributed Replay 功能安裝的文章。|  
|[SQL Server 管理工具與 SSMS](https://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)|安裝及設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理工具。|  
|[SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)|安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 元件時的考量。|  
  

## <a name="sql-server-configuration"></a>SQL Server 設定 
  
|發行項|描述|  
|-----------|-----------------|  
|[設定 Windows 防火牆 (SQL Server)](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|防火牆設定及如何設定 Windows 防火牆以允許存取 SQL Server 的概觀。|  
|[設定 Windows 防火牆 (SSAS)](https://docs.microsoft.com/analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access)|設定連接埠與防火牆設定，以允許存取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint。|  
|[設定多重主目錄電腦](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和具有進階安全性的 Windows 防火牆，以便在多重主目錄環境中提供給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的網路連接。|  

 
## <a name="see-also"></a>另請參閱  

[升級 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/upgrade-sql-server.md)   
[解除安裝 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/install/uninstall-sql-server.md)   
[Install SQL Server Reporting Services (SSRS)](../../reporting-services/install-windows/install-reporting-services.md)
[安裝 SQL Server Analysis Services (SSAS)](/analysis-services/instances/install-windows/install-analysis-services)
[安裝 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 商業智慧功能](../../sql-server/install/install-sql-server-business-intelligence-features.md)   
[高可用性解決方案 &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
