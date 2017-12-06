---
title: "SQL 命令提示字元公用程式 (Database Engine) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- command prompt utilities [SQL Server]
- command prompt utilities [SQL Server], about command prompt utilities
- command prompt [SQL Server]
- utilities [SQL Server], command prompt
- command prompt [SQL Server], utilities
ms.assetid: 48364bd9-6ea7-45e9-a332-acf3d81bbfae
caps.latest.revision: "90"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b1d08c7596e3ded97a7ef1dddf0b84bd3470bbab
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="sql-command-prompt-utilities-database-engine"></a>SQL 命令提示字元公用程式 (Database Engine)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]命令提示字元公用程式可讓您要編寫指令碼[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]作業。 下表列出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]隨附的命令提示字元公用程式清單。  
  
|**公用程式**|**描述**|**安裝位置**|  
|-----------------|---------------------|----------------------|  
|[bcp 公用程式](../tools/bcp-utility.md)|在 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體和使用者指定之格式的資料檔案之間，用來複製資料。|\<*磁碟機*: > \Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[dta 公用程式](../tools/dta/dta-utility.md)|用來分析工作負載和建議實體設計結構，以最佳化這項工作負載的伺服器效能。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[dtexec 公用程式](../integration-services/packages/dtexec-utility.md)|用以設定及執行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。 此命令提示字元公用程式的使用者介面版本稱為 **DTExecUI**，它會啟動「執行封裝公用程式」。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[dtutil 公用程式](../integration-services/dtutil-utility.md)|用來管理 SSIS 封裝。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[使用部署公用程式的部署模型方案](../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|用以將 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的執行個體。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VShell\Common7\IDE|  
|[mssql scripter （公開預覽）](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/17/try-new-sql-server-command-line-tools-to-generate-t-sql-scripts-and-monitor-dynamic-management-views/)|用來產生 SQL Server、 Azure SQL Database 和 Azure SQL 資料倉儲中的資料庫物件的建立及插入 T-SQL 指令碼。|請參閱我們[GitHub 儲存機制](https://github.com/Microsoft/sql-xplat-cli)下載和使用方式資訊。| 
|[osql 公用程式](../tools/osql-utility.md)|可讓您在命令提示字元之下，輸入 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式、系統程序和指令碼檔案。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Profiler 公用程式](../tools/profiler-utility.md)|用來從命令提示字元啟動 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[RS.exe 公用程式 &#40;SSRS&#41;](../reporting-services/tools/rs-exe-utility-ssrs.md)|用以執行為了管理 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表伺服器而設計的指令碼。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rsconfig 公用程式 &#40;SSRS&#41;](../reporting-services/tools/rsconfig-utility-ssrs.md)|用來設定報表伺服器連接。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rskeymgmt 公用程式 &#40;SSRS&#41;](../reporting-services/tools/rskeymgmt-utility-ssrs.md)|用來管理報表伺服器的加密金鑰。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 應用程式](../tools/sqlagent90-application.md)|用來從命令提示字元啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent。|\<磁碟機 >: SQL Server \Program Files\Microsoft\\<*instance_name*> \MSSQL\Binn|  
|[sqlcmd 公用程式](../tools/sqlcmd-utility.md)|可讓您在命令提示字元之下，輸入 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式、系統程序和指令碼檔案。|\<*磁碟機*: > \Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[SQLdiag 公用程式](../tools/sqldiag-utility.md)|用以收集可供 [!INCLUDE[msCoName](../includes/msconame-md.md)] 客戶服務與支援部門使用的診斷資訊。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqllogship 應用程式](../tools/sqllogship-application.md)|應用程式用來對記錄傳送組態執行備份、複製和還原作業以及相關的清除工作，而無須執行備份、複製和還原作業。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SqlLocalDB 公用程式](../tools/sqllocaldb-utility.md)|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行模式，專供程式開發人員使用。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\|  
|[sqlmaint 公用程式](../tools/sqlmaint-utility.md)|用來執行舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]所建立的資料庫維護計畫。|\<磁碟機 >: \Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\MSSQL\Binn|  
|[sqlps 公用程式](../tools/sqlps-utility.md)|用來執行 PowerShell 命令和指令碼。 載入並註冊 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 提供者和 cmdlet。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr 應用程式](../tools/sqlservr-application.md)|用來從命令提示字元啟動和停止 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體，以進行疑難排解。|\<磁碟機 >: \Program Files\Microsoft SQL Server\MSSQL13。MSSQLSERVER\MSSQL\Binn|  
|[Ssms 公用程式](../tools/sql-server-management-studio/ssms-utility.md)|用來從命令提示字元啟動 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VSShell\Common7\IDE|  
|[tablediff 公用程式](../tools/tablediff-utility.md)|用來比較兩份資料表，以找出非聚合狀況，當進行複寫拓撲的疑難排解時，它尤其有用。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]COM|  

## <a name="command-prompt-utilities-syntax-conventions"></a>命令提示字元公用程式語法慣例  
  
|**慣例**|**用於**|  
|--------------------|------------------|  
|大寫|作業系統層級所用的陳述式和詞彙。|  
|`monospace`|命令和程式碼範例。|  
|*斜體*|使用者提供的參數。|  
|**粗體字**|必須完全依照顯示狀況來輸入的命令、參數和其他語法。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫散發代理程式](../relational-databases/replication/agents/replication-distribution-agent.md)   
 [複寫記錄讀取器代理程式](../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [複寫合併代理程式](../relational-databases/replication/agents/replication-merge-agent.md)   
 [複寫佇列讀取器代理程式](../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
