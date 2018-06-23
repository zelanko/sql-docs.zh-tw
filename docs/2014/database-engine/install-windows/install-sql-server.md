---
title: 安裝 SQL Server 2014 |Microsoft 文件
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: bf415bef00710562247bcfd9fa310e2c0728497f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134050"
---
# <a name="install-sql-server-2014"></a>安裝 SQL Server 2014
## <a name="-download-sql-server-2014-express-httpwwwhanselmancomblogdownloadsqlserverexpressaspx"></a>[ 下載 SQL Server 2014 Express ](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx)
  **感謝您到[Scott Hanselman](http://www.hanselman.com/)收集的所有安裝程式封裝連結，在一個地方 ！**
  
 本主題提供可以用於安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 之不同安裝選項的概觀。 如需有關各種[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可安裝的元件和安裝程序，請參閱[安裝 SQL Server 2014](installation-for-sql-server.md)。  
> **注意：** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供 32 位元和 64 位元版本。 64 位元和 32 位元版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是透過安裝精靈或命令提示字元來安裝。 如需有關[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]元件，請參閱[版本和 SQL Server 2014 元件](../../sql-server/editions-and-components-of-sql-server-2016.md)和[支援的 SQL Server 2014 的版本功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
 根據預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程序中不會安裝範例資料庫和範例程式碼。 若要針對非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express Edition 安裝範例資料庫和範例程式碼，請參閱 [CodePlex 網站](http://go.microsoft.com/fwlink/?LinkId=87843)。 如需查閱 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]範例資料庫及範例程式碼的支援資訊，請參閱＜ [資料庫及範例概觀](http://go.microsoft.com/fwlink/?LinkId=110391)＞。  
  
 安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，請先檢閱安裝需求、系統組態檢查與安全性考量。 如需詳細資訊，請參閱 [Planning a SQL Server Installation](../../sql-server/install/planning-a-sql-server-installation.md)。 如需有關不同 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安裝案例的詳細資訊，請參閱下節中的主題。  
  
  
## <a name="install-includesscurrentincludessscurrent-mdmd-components"></a>安裝[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]元件  
  
|主題|描述|  
|-----------|-----------------|  
|[關於 SQL Server Database Engine](../sql-server-database-engine-overview.md)|描述如何安裝及設定 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。|  
|[安裝 SQL Server 複寫](install-sql-server-replication.md)|描述如何安裝及設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication。|  
|[安裝 Distributed Replay](../../tools/distributed-replay/install-distributed-replay-overview.md)|列出安裝 Distributed Replay 功能的主題。|  
|[安裝 SQL Server 管理工具](../../sql-server/install/install-sql-server-management-tools.md)|描述如何安裝及設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理工具。|  
|[安裝 SQL Server PowerShell](install-sql-server-powershell.md)|描述安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 元件時的考量。|  
  
## <a name="how-to-install-includesscurrentincludessscurrent-mdmd"></a>如何安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
|Title|描述|  
|-----------|-----------------|  
|[安裝的使用說明主題](../../sql-server/install/installation-how-to-topics.md)|提供如何從安裝精靈、從命令提示字元、使用組態檔及使用 SysPrep 安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的程序性主題連結。|  
|[在 Server Core 上安裝 SQL Server 2014](install-sql-server-on-server-core.md)|檢閱本主題了解如何在 Windows Server Core 上安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 。|  
|[驗證 SQL Server 安裝](validate-a-sql-server-installation.md)|檢閱 SQL 探索報告的使用狀況，以驗證電腦上所安裝之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。|  
|[檢查 System Configuration Checker 的參數](check-parameters-for-the-system-configuration-checker.md)|討論系統組態檢查 (SCC) 的功能。|  
  
## <a name="configuration"></a>組態  
  
|主題|描述|  
|-----------|-----------------|  
|[設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|本主題提供防火牆組態及如何設定 Windows 防火牆的概觀。|  
|[設定多重主目錄電腦進行 SQL Server 存取](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|此主題描述如何設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和具有進階安全性的 Windows 防火牆，以便在多重主目錄環境中提供給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的網路連接。|  
|[設定 Windows 防火牆以允許 Analysis Services 存取](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|您可以遵循本主題所提供的步驟，設定通訊埠和防火牆設定，以允許存取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 PowerPivot for SharePoint。|  
  
## <a name="related-sections"></a>相關章節  
 [安裝 SQL Server 2014 BI 功能](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 屬於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] BI 平台的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 功能包括 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]，以及數種用來建立或處理分析資料的用戶端應用程式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式文件集中的這一節將說明如何安裝 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]、[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] 及 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
 [SQL Server 容錯移轉叢集安裝](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式文件集中的這一節將說明如何安裝及設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集。  
  
## <a name="see-also"></a>另請參閱  
 [規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)   
 [升級為 SQL Server 2014](upgrade-sql-server.md)   
 [解除安裝 SQL Server 2014](../../sql-server/install/uninstall-sql-server.md)   
 [高可用性解決方案 &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  