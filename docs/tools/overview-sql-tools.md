---
title: SQL 工具和公用程式 SQL Server、 Azure SQL Database 和 Azure SQL 資料倉儲 |Microsoft Docs
ms.custom: ''
ms.date: 02/22/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.component: misc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: 0
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: a8f31d6479a0a2ba5e5f19f6a0739ab6322de92b
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 08/02/2018
ms.locfileid: "39458982"
---
# <a name="sql-tools-and-utilities-for-sql-server-azure-sql-database-and-azure-sql-data-warehouse"></a>SQL 工具和公用程式 SQL Server、 Azure SQL Database 和 Azure SQL 資料倉儲
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

若要管理 （查詢、 監視等） 您的資料庫需要的工具。 有數個資料庫的工具。 雖然可以在雲端，Windows，或上執行您的資料庫[Linux](../linux/sql-server-linux-overview.md)，您的工具不需要與資料庫相同的平台上執行。 

本文提供可用的工具，使用您的 SQL database 的相關資訊。 


## <a name="tools-to-run-queries-and-manage-databases"></a>若要執行查詢及管理資料庫的工具  

| 工具 | Description |
|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)] 是免費、 輕量級工具，管理資料庫，只要它們執行。 此預覽版本中提供資料庫管理功能，包括擴充的 TRANSACT-SQL 編輯器和可自訂的深入了解您的資料庫的操作狀態。 **[!INCLUDE[name-sos](../includes/name-sos-short.md)] 在 Windows、 macOS 和 Linux 上執行**。|
| [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) | 您可以使用 SQL Server Management Studio (SSMS) 來查詢、 設計和管理 SQL Server、 Azure SQL Database 和 Azure SQL 資料倉儲。 **在 Windows 上執行 SSMS**。|
| [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md) | 將 Visual Studio 打造為強大的開發環境，SQL Server、 Azure SQL Database 和 Azure SQL 資料倉儲。 **Windows 上執行的 SSDT**。|
|[mssql-cli](mssql-cli.md)|mssql cli 是查詢 SQL Server 的互動式命令列工具。 **執行 Windows、 macOS 和 Linux 上的 mssql-cli**|
| [Visual Studio Code](https://code.visualstudio.com/)| 安裝 Visual Studio Code 之後, 安裝[mssql 擴充功能](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)開發 Microsoft SQL Server、 Azure SQL Database 和 SQL 資料倉儲。 **在 Windows、 macOS 和 Linux 上的 visual Studio Code 執行**。|

## <a name="which-tool-should-i-choose"></a>我應該選擇哪一種工具？

- 管理 SQL Server 執行個體或資料庫，在 Windows、 Linux 或 Mac 上的輕量級編輯器嗎？ 選擇 [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md)
- 若要管理 SQL Server 執行個體或在 Windows 上的資料庫使用完整的 GUI 支援嗎？ 選擇 [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)
- 執行您想要建立或維護資料庫程式碼，包括編譯時間驗證、 重構和設計工具支援在 Windows 上嗎？ 選擇 [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
- 您要使用命令列工具，特色 IntelliSense、 語法高-光源，查詢 SQL Server 和更多功能？ 選擇[mssql-cli](mssql-cli.md)
- 若要在 Windows、 Linux 或 Mac 上的輕量級編輯器中撰寫 T-SQL 指令碼嗎？ 選擇[Visual Studio Code](https://code.visualstudio.com/)而[mssql 擴充功能](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)

## <a name="additional-tools"></a>其他工具

| 工具 | Description |
|:--|:--|
| [組態管理員](../tools/configuration-manager/sql-server-configuration-manager-help.md) | 使用 SQL Server 組態管理員來設定 SQL Server 服務和設定網路連線。 Configuration Manager 在 Windows 上執行|
|[mssql conf](../linux/sql-server-linux-configure-mssql-conf.md)|使用 mssql conf 設定在 Linux 上執行的 SQL Server。|
| [SQL Server 移轉小幫手](../ssma/sql-server-migration-assistant.md) | 使用 SQL Server 移轉小幫手將從 Microsoft Access、DB2、MySQL、Oracle 及 Sybase 到 SQL Server 的資料庫移轉作業自動化。|
| [Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md) | 使用 Distributed Replay 功能可協助您評估未來的 SQL Server 升級的影響。 也可以使用 Distributed Replay 幫助您評估硬體和作業系統升級，以及 SQL Server 微調的影響。 |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | Ssbdiagnose 公用程式會報告 Service Broker 交談或 Service Broker 服務的組態中的問題。 |


## <a name="command-line-utilities"></a>命令列公用程式

  命令列公用程式可編寫 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 作業指令碼。 下表列出 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]隨附的命令提示字元公用程式清單。  
  
|**公用程式**|**說明**|**安裝位置**|  
|-----------------|---------------------|----------------------|  
|[bcp 公用程式](../tools/bcp-utility.md)|在 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體和使用者指定之格式的資料檔案之間，用來複製資料。|\<*磁碟機*:>\Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[dta 公用程式](../tools/dta/dta-utility.md)|用來分析工作負載和建議實體設計結構，以最佳化這項工作負載的伺服器效能。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[dtexec 公用程式](../integration-services/packages/dtexec-utility.md)|用以設定及執行 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。 此命令提示字元公用程式的使用者介面版本稱為 **DTExecUI**，它會啟動「執行封裝公用程式」。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[dtutil 公用程式](../integration-services/dtutil-utility.md)|用來管理 SSIS 封裝。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[使用部署公用程式的部署模型方案](../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|用以將 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 專案部署到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的執行個體。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VShell\Common7\IDE|  
|[mssql scripter （公開預覽）](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/17/try-new-sql-server-command-line-tools-to-generate-t-sql-scripts-and-monitor-dynamic-management-views/)|用來產生 SQL Server、 Azure SQL Database 和 Azure SQL 資料倉儲中的資料庫物件的建立及插入 T-SQL 指令碼。|請參閱我們[GitHub 存放庫](https://github.com/Microsoft/sql-xplat-cli)如需下載和使用方式資訊。| 
|[osql 公用程式](../tools/osql-utility.md)|可讓您在命令提示字元之下，輸入 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式、系統程序和指令碼檔案。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Profiler 公用程式](../tools/profiler-utility.md)|用來從命令提示字元啟動 [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] 。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[RS.exe 公用程式 &#40;SSRS&#41;](../reporting-services/tools/rs-exe-utility-ssrs.md)|用以執行為了管理 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 報表伺服器而設計的指令碼。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rsconfig 公用程式 &#40;SSRS&#41;](../reporting-services/tools/rsconfig-utility-ssrs.md)|用來設定報表伺服器連接。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rskeymgmt 公用程式 &#40;SSRS&#41;](../reporting-services/tools/rskeymgmt-utility-ssrs.md)|用來管理報表伺服器的加密金鑰。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 應用程式](../tools/sqlagent90-application.md)|用來從命令提示字元啟動 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent。|\<磁碟機>:\Program Files\Microsoft SQL Server\\<*執行個體名稱*>\MSSQL\Binn|  
|[sqlcmd 工用程式](../tools/sqlcmd-utility.md)|可讓您在命令提示字元之下，輸入 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式、系統程序和指令碼檔案。|\<*磁碟機*:>\Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[SQLdiag 公用程式](../tools/sqldiag-utility.md)|用以收集可供 [!INCLUDE[msCoName](../includes/msconame-md.md)] 客戶服務與支援部門使用的診斷資訊。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqllogship 應用程式](../tools/sqllogship-application.md)|應用程式用來對記錄傳送組態執行備份、複製和還原作業以及相關的清除工作，而無須執行備份、複製和還原作業。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SqlLocalDB 公用程式](../tools/sqllocaldb-utility.md)|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 的執行模式，專供程式開發人員使用。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\|  
|[sqlmaint 公用程式](../tools/sqlmaint-utility.md)|用來執行舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]所建立的資料庫維護計畫。|\<磁碟機>:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn|  
|[sqlps 公用程式](../tools/sqlps-utility.md)|用來執行 PowerShell 命令和指令碼。 載入並註冊 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 提供者和 cmdlet。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr 應用程式](../tools/sqlservr-application.md)|用來從命令提示字元啟動和停止 [!INCLUDE[ssDE](../includes/ssde-md.md)] 執行個體，以進行疑難排解。|\<磁碟機>:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn|  
|[Ssms 公用程式](../tools/sql-server-management-studio/ssms-utility.md)|用來從命令提示字元啟動 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VSShell\Common7\IDE|  
|[tablediff 公用程式](../tools/tablediff-utility.md)|用來比較兩份資料表，以找出非聚合狀況，當進行複寫拓撲的疑難排解時，它尤其有用。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]COM|  

## <a name="sql-command-prompt-utilities-syntax-conventions"></a>SQL 命令提示字元公用程式語法慣例  
  
|**慣例**|**用於**|  
|--------------------|------------------|  
|大寫|作業系統層級所用的陳述式和詞彙。|  
|`monospace`|命令和程式碼範例。|  
|*斜體*|使用者提供的參數。|  
|**粗體字**|必須完全依照顯示狀況來輸入的命令、參數和其他語法。|  



