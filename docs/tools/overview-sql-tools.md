---
title: SQL 工具和公用程式 SQL Server、 Azure SQL Database 和 Azure SQL 資料倉儲 |Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ''
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 0a0a46fb27c8695ead3cc68e17677ccdcf7cb6fc
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2018
ms.locfileid: "51292974"
---
# <a name="sql-tools-and-utilities-for-sql-server-azure-sql-database-and-azure-sql-data-warehouse"></a>SQL 工具和公用程式 SQL Server、 Azure SQL Database 和 Azure SQL 資料倉儲
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

若要管理 （查詢、 監視等） 您的資料庫需要的工具。 雖然可以在雲端，Windows，或上執行您的資料庫[Linux](../linux/sql-server-linux-overview.md)，您的工具不需要與資料庫相同的平台上執行。 

有許多資料庫工具，因此這篇文章提供說明和可用的工具中的部分的指標來使用您的 SQL database。 如果您需要協助以決定哪一種工具您需要請參閱[應該使用哪一種工具？](#which-tool-should-i-choose)。


## <a name="gui-tools-to-manage-databases"></a>若要管理資料庫的 GUI 工具  

以下是主要的圖形化使用者介面 (GUI) 工具：

| 工具 | Description | 在上執行 |
|:--|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)] 是免費、 輕量級工具，管理資料庫，只要它們執行。 此預覽版本中提供資料庫管理功能，包括擴充的 TRANSACT-SQL 編輯器和可自訂的深入了解您的資料庫的操作狀態。 | **[!INCLUDE[name-sos](../includes/name-sos-short.md)] 在 Windows、 macOS 和 Linux 上執行**。|
| [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) | 您可以使用 SQL Server Management Studio (SSMS) 來查詢、 設計和管理 SQL Server、 Azure SQL Database 和 Azure SQL 資料倉儲。 | **SSMS 在 Windows 上執行**。|
| [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md) | 將 Visual Studio 打造為強大的開發環境，SQL Server、 Azure SQL Database 和 Azure SQL 資料倉儲。| **SSDT 在 Windows 上執行**。|
| [Visual Studio Code](https://code.visualstudio.com/)| 安裝 Visual Studio Code 之後, 安裝[mssql 擴充功能](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)開發 Microsoft SQL Server、 Azure SQL Database 和 SQL 資料倉儲。| **在 Windows、 macOS 和 Linux 上的 visual Studio Code 執行**。|


## <a name="command-line-tools-to-manage-databases"></a>命令列工具來管理資料庫

以下是主要的命令列工具：

| 工具 | Description | 在上執行 |
|:--|:--|:--|
|[**mssql-cli (預覽)**](mssql-cli.md)|**mssql cli**是查詢 SQL Server 的互動式命令列工具。 | Windows、 macOS 和 Linux|
| [**sqlpackage**](sqlpackage.md) |**sqlpackage**是命令列公用程式會自動執行數個資料庫開發工作。 macOS 和 Linux 版本的 sqlpackage 目前目前為預覽版。 | Windows、 macOS 和 Linux|
|[**SQL Server PowerShell**](../powershell/sql-server-powershell.md)| **SQL Server PowerShell**提供 cmdlet 讓您使用 SQL| Windows、 macOS 和 Linux|
| [**sqlcmd**](sqlcmd-utility.md) |**sqlcmd**公用程式可讓您輸入 TRANSACT-SQL 陳述式、 系統程序和指令碼檔案，在命令提示字元。 | Windows、 macOS 和 Linux|
|[**bcp**](../2014/tools/bcp-utility.md)|**b**ulk **c**opy **p**rogram 公用程式 (**bcp**) 會以使用者指定格式，在 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體與資料檔案之間大量複製資料。|Windows、 macOS 和 Linux|
|[**mssql scripter （預覽）**](https://github.com/Microsoft/mssql-scripter)|**mssql scripter**是一種多平台命令列體驗來編寫指令碼 SQL Server 資料庫|Windows、 macOS 和 Linux|
|[**mssql conf**](../linux/sql-server-linux-configure-mssql-conf.md)|**mssql conf**設定在 Linux 上執行的 SQL Server。|Linux|



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
| [SQL Server 移轉小幫手](../ssma/sql-server-migration-assistant.md) | 使用 SQL Server 移轉小幫手將從 Microsoft Access、DB2、MySQL、Oracle 及 Sybase 到 SQL Server 的資料庫移轉作業自動化。|
| [資料庫測試助理](../dea/database-experimentation-assistant-overview.md) | 使用資料庫測試助理 來評估指定的工作負載的目標的版本的 SQL。 |
| [Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md) | 使用 Distributed Replay 功能可協助您評估未來的 SQL Server 升級的影響。 也可以使用 Distributed Replay 幫助您評估硬體和作業系統升級，以及 SQL Server 微調的影響。 |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | Ssbdiagnose 公用程式會報告 Service Broker 交談或 Service Broker 服務的組態中的問題。 |

如果您想要尋求未提及此頁面的其他工具，請參閱[SQL 命令提示字元公用程式](command-prompt-utility-reference-database-engine.md)。

