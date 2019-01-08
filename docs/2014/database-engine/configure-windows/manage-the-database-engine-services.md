---
title: 管理資料庫引擎服務 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, accessing
- Database Engine [SQL Server], services
- managing services [SQL Server], about service management
- services [SQL Server]
- SQL Server Agent service, managing
- SQL Server services, about SQL Server service
- MSSQLServer
- server configuration [SQL Server]
- managing services [SQL Server]
- SQL Server Agent service
- services [SQL Server], managing
- administering SQL Server, services
- SQL Server services
ms.assetid: aa732e43-53ba-4eea-bb9b-089da0766fc1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e747a85c816c8e57757be9acb61b14204266ff35
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/30/2018
ms.locfileid: "52639234"
---
# <a name="manage-the-database-engine-services"></a>管理 Database Engine Services
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在作業系統上作為服務執行。 服務是在系統背景中執行的應用程式類型， 通常可以提供核心作業系統功能，例如 Web 服務、事件記錄或檔案服務。 服務不需在電腦桌面上顯示使用者介面，即可直接執行。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 和數種其他的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件，都會以服務的形式來執行。 這些服務通常在啟動作業系統時就會跟著啟動， 這需視安裝期間的指定項目而定；有些服務預設不會啟動。 本節描述各種 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務的管理方式。 開始登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體之前，您必須知道如何啟動、停止、暫停、繼續和重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體。 登入之後，您可以執行諸如管理伺服器或查詢資料庫的工作。  
  
## <a name="using-the-sql-server-service"></a>使用 SQL Server 服務  
 啟動 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的執行個體時，您也會啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。 啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務之後，使用者即可與伺服器建立新的連接。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務可在本機或從遠端以服務的形式來啟動和停止。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務是預設執行個體，則稱為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)；如果是具名執行個體，則稱為 MSSQL$\<執行個體名稱>。  
  
## <a name="using-sql-server-configuration-manager"></a>使用 SQL Server 組態管理員  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員可讓您停止、啟動或暫停各種 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員無法管理 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 服務。  
  
 您也可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員來檢視選定服務的屬性。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員是一個 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC) 嵌入式管理單元。 如需 MMC 及嵌入式管理單元之運作方式的詳細資訊，請參閱 Windows 說明。  
  
 **存取 SQL Server 組態管理員**  
  
-   指向 **[開始]** 功能表上的 **[所有程式]**，然後依序指向 [ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 **[組態工具]**，再按一下 **[SQL Server 組態管理員]**。  
  
 **使用 Windows 8 存取 SQL Server 組態管理員**  
  
 由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console 程式的內嵌式管理單元，而不是獨立的程式，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員不會在執行 Windows 8.0 時做為應用程式出現。 若要開啟 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員，請在 [搜尋] 常用鍵的 [應用程式] 下，輸入 **SQLServerManager12.msc** (適用於 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])、**SQLServerManager11.msc** (適用於 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) 或 **SQLServerManager10.msc** (適用於 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)])，然後按 **Enter** 鍵。  
  
## <a name="in-this-section"></a>本章節內容  
  
|||  
|-|-|  
|[管理服務的安全性需求](security-requirements-for-managing-services.md)|[避免自動啟動 SQL Server 的執行個體 &#40;SQL Server 組態管理員&#41;](scm-services-prevent-automatic-startup-of-an-instance.md)|  
|[設定 Windows 服務帳戶與權限](configure-windows-service-accounts-and-permissions.md)|[變更 SQL Server 的服務啟動帳戶 &#40;SQL Server 組態管理員&#41;](scm-services-change-the-service-startup-account.md)|  
|[使用 (或不使用) 網路執行 SQL Server](run-sql-server-with-or-without-a-network.md)|[設定伺服器啟動選項 &#40;SQL Server 組態管理員&#41;](scm-services-configure-server-startup-options.md)|  
|[SQL Server Browser 服務 &#40;Database Engine 和 SSAS&#41;](sql-server-browser-service-database-engine-and-ssas.md)|[變更 SQL Server 所使用之帳戶的密碼 &#40;SQL Server 組態管理員&#41;](scm-services-change-the-password-of-the-accounts-used.md)|  
|[Database Engine 服務啟動選項](database-engine-service-startup-options.md)|[設定 SQL Server 錯誤記錄檔](scm-services-configure-sql-server-error-logs.md)|  
|[啟動、停止、暫停、繼續、重新啟動 Database Engine、SQL Server Agent 或 SQL Server Browser 服務](start-stop-pause-resume-restart-sql-server-services.md)|[變更伺服器驗證模式](change-server-authentication-mode.md)|  
|[以單一使用者模式啟動 SQL Server](start-sql-server-in-single-user-mode.md)|[SQL 寫入器服務](sql-writer-service.md)|  
|[以最低組態啟動 SQL Server](start-sql-server-with-minimal-configuration.md)|[廣播關機訊息 &#40;命令提示字元&#41;](broadcast-a-shutdown-message-command-prompt.md)|  
|[連接至另一部電腦 &#40;SQL Server 組態管理員&#41;](scm-services-connect-to-another-computer.md)|[登入 SQL Server 的執行個體 &#40;命令提示字元&#41;](log-in-to-an-instance-of-sql-server-command-prompt.md)|  
|[將 SQL Server 執行個體設定為自動啟動 &#40;SQL Server 組態管理員&#41;](scm-services-set-an-instance-to-start-automatically.md)|[設定 Database Engine 對檔案系統的存取權限](configure-file-system-permissions-for-database-engine-access.md)|  
  
## <a name="related-content"></a>相關內容  
 [設定 SQL Server Agent](../../ssms/agent/sql-server-agent.md)  
  
 [登入 SQL Server](logging-in-to-sql-server.md)  
  
  
