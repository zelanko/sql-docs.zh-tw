---
title: 安裝 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: quickstart
helpviewer_keywords:
- AdventureWorks sample database
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
caps.latest.revision: 59
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: aff3b9f7c8e3640ef0452f1d8a8439259e72f235
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43021552"
---
# <a name="install-sql-server"></a>安裝 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
 
 > 如需舊版 SQL Server 的相關內容，請參閱[安裝 SQL Server 2014](install-sql-server.md)。

 從 [!INCLUDE[sssql15](../../includes/sssql15-md.md)] 開始，[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 才可以用作 64 位元應用程式。 下列重要詳細資料說明如何取得 SQL Server 及其安裝方式。

## <a name="installation-details"></a>安裝詳細資料
  
*  **選項**：透過安裝精靈、命令提示字元或 sysprep 安裝。
 
*  **需求**︰安裝前，請先花點時間檢閱 [規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md) 

* **程序**︰如需安裝程序的完整指示，請參閱 [安裝 SQL Server](../../database-engine/install-windows/installation-for-sql-server-2016.md) 。

* **範例資料庫與範例程式碼**： 
    * 這些範例預設不會隨著 SQL Server 安裝程式一起安裝 
    * 若要安裝 Express 版本以外之 SQL Server 隨附的這些範例，請參閱 [GitHub](http://github.com/Microsoft/sql-server-samples)
    

## <a name="get-the-installation-media"></a>取得安裝媒體

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="how-to-install-includessnoversionincludesssnoversion-mdmd"></a>[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 安裝方式
 
|Title|Description|  
|-----------|-----------------|  
|[在 Server Core 上安裝 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/install-sql-server-on-server-core.md)|檢閱本文以了解如何在 Windows Server Core 上安裝 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]。|  
|[檢查 System Configuration Checker 的參數](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md)|討論系統組態檢查 (SCC) 的功能。|  
|[從安裝精靈安裝 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] &#40;安裝程式&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)|使用 [安裝精靈] 進行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 標準安裝的程序文章。|  
|[從命令提示字元安裝 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)|提供用來執行自動安裝之範例語法和安裝參數的程序文章。|  
|[使用組態檔安裝 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/install-sql-server-2016-using-a-configuration-file.md)|提供用來透過設定檔執行安裝程式之語法例範和安裝參數的程序文章。|  
|[使用 SysPrep 安裝 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/install-sql-server-using-sysprep.md)|提供用來透過 SysPrep 執行安裝程式之語法範例和安裝參數的程序文章。|  
|[將功能新增至 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 執行個體 &#40;安裝程式&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)|用於更新現有 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 執行個體元件的程序文章。|  
|[修復失敗的 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 安裝](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)|用於修復損毀之 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 安裝的程序文章。|  
|[重新命名主控 SQL Server 獨立式執行個體的電腦](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)|用於更新儲存在 sys.servers 中之系統中繼資料的程序文章。|  
|[安裝 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 服務更新](../../database-engine/install-windows/install-sql-server-servicing-updates.md)|安裝 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 更新的程序文章。|  
|[檢視與讀取 SQL Server 安裝程式記錄檔](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)|用於檢查安裝記錄檔中之錯誤的程序文章。|  
|[驗證 SQL Server 安裝](../../database-engine/install-windows/validate-a-sql-server-installation.md)|檢閱 SQL 探索報告的使用狀況，以驗證電腦上所安裝之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的版本與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。|  
  
  
## <a name="how-to-install-individual-components"></a>如何安裝個別的元件  
  
|主題|Description|  
|-----------|-----------------|  
|[安裝 SQL Server Database Engine](../../database-engine/install-windows/install-sql-server-database-engine.md)|描述如何安裝及設定 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。|  
|[安裝 SQL Server 複寫](../../database-engine/install-windows/install-sql-server-replication.md)|描述如何安裝及設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication。|  
|[安裝 Distributed Replay - 概觀](../../tools/distributed-replay/install-distributed-replay-overview.md)|列出說明 Distributed Replay 功能安裝的文章。|  
|[安裝 SQL Server 管理工具與 SSMS](http://msdn.microsoft.com/library/af68d59a-a04d-4f23-9967-ad4ee2e63381)|描述如何安裝及設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理工具。|  
|[安裝 SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)|描述安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 元件時的考量。|  
  

## <a name="how-to-configure-sql-server"></a>如何設定 SQL Server  
  
|主題|Description|  
|-----------|-----------------|  
|[設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|本文提供防火牆設定及如何設定 Windows 防火牆的概觀。|  
|[設定多重主目錄電腦進行 SQL Server 存取](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|本文描述如何設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和具有進階安全性的 Windows 防火牆，以便在多重主目錄環境中提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的網路連線。|  
|[設定 Windows 防火牆以允許 Analysis Services 存取](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|您可以遵循本文所提供的步驟，設定通訊埠和防火牆設定，以允許存取 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] for SharePoint。|  
  
## <a name="related-sections"></a>相關章節  
[ [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 的版本和支援的功能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)  
[安裝 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] 商業智慧功能](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
  [SQL Server 容錯移轉叢集安裝](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 
  
## <a name="see-also"></a>另請參閱  

[規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)   
 [升級至 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../database-engine/install-windows/upgrade-sql-server.md)   
 [解除安裝 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]](../../sql-server/install/uninstall-sql-server.md)   
 [高可用性解決方案 &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  
