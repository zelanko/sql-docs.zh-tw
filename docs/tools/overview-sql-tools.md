---
title: 適用于 SQL Server、Azure SQL （Azure sql 資料庫、Azure SQL 受控實例、SQL 虛擬機器）和 Azure SQL 資料倉儲的 SQL 查詢和管理工具 |Microsoft Docs
description: 適用于 SQL Server、Azure SQL （Azure SQL database、Azure SQL 受控實例、SQL 虛擬機器）和 Azure SQL 資料倉儲的 SQL 查詢與管理工具
ms.custom: ''
ms.date: 09/11/2019
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ''
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 56ed7a0cf53a026b470c90c36b37da95f02ac5bc
ms.sourcegitcommit: 3bd813ab2c56b415a952e5fbd5cfd96b361c72a2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/11/2019
ms.locfileid: "70913571"
---
# <a name="sql-query-and-management-tools-for-sql-server-azure-sql-azure-sql-database-azure-sql-managed-instance-sql-virtual-machines-and-azure-sql-data-warehouse"></a>適用于 SQL Server、Azure SQL （Azure SQL database、Azure SQL 受控實例、SQL 虛擬機器）和 Azure SQL 資料倉儲的 SQL 查詢與管理工具
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

若要管理 (查詢、監視等等) 您的資料庫, 您需要工具。 當您的資料庫可以在雲端、Windows 或[Linux](../linux/sql-server-linux-overview.md)上執行時, 您的工具不需要在與資料庫相同的平臺上執行。 

有許多資料庫工具可供使用, 因此本文提供一些適用于使用 SQL 資料庫之可用工具的說明和指標。 如果您需要協助來決定所需的工具, 請參閱[應該使用哪一種工具？](#which-tool-should-i-choose)。

如需其他資訊，以及下載工具，請在下表中選取 [工具] 欄中的連結。 若要下載 SQL Server，請參閱[安裝 SQL Server](../database-engine/install-windows/install-sql-server.md)。 

## <a name="gui-tools-to-manage-databases"></a>用來管理資料庫的 GUI 工具  

下列工具提供圖形化使用者介面（GUI）：

| 工具 | Description | 執行于 |
|:--|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)]是免費的輕量工具, 可用於管理其執行位置的資料庫。 此預覽版本提供資料庫管理功能, 包括擴充的 Transact-sql 編輯器, 以及可自訂的資料庫操作狀態深入解析。 | **[!INCLUDE[name-sos](../includes/name-sos-short.md)] 可在 Windows、macOS 與 Linux 上執行**.|
| [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) | 使用 SQL Server Management Studio (SSMS) 來查詢、設計和管理您的 SQL Server、Azure SQL Database 和 Azure SQL 資料倉儲。 | **SSMS 在 Windows 上執行**。|
| [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md) | 針對 SQL Server、Azure SQL Database 和 Azure SQL 資料倉儲, 將 Visual Studio 轉換為功能強大的開發環境。| **SSDT 在 Windows 上執行**。|
| [Visual Studio Code](https://code.visualstudio.com/)| 安裝 Visual Studio Code 之後, 請安裝[mssql 擴充](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)功能以開發 Microsoft SQL Server、Azure SQL Database 和 SQL 資料倉儲。| **Visual Studio Code 會在 Windows、macOS 和 Linux 上執行**。|


## <a name="command-line-tools-to-manage-databases"></a>用來管理資料庫的命令列工具

下列是主要的命令列工具:

| 工具 | Description | 執行于 |
|:--|:--|:--|
|[**mssql-cli (預覽)** ](mssql-cli.md)|**mssql-cli**是用來查詢 SQL Server 的互動式命令列工具。 | Windows、macOS 和 Linux|
| [**sqlpackage**](sqlpackage.md) |**sqlpackage**是命令列公用程式, 可將數個資料庫開發工作自動化。 sqlpackage 的 macOS 和 Linux 版本目前為預覽狀態。 | Windows、macOS 和 Linux|
|[**SQL Server PowerShell**](../powershell/sql-server-powershell.md)| **SQL Server PowerShell**提供使用 SQL 的 Cmdlet| Windows、macOS 和 Linux|
| [**sqlcmd**](sqlcmd-utility.md) |**sqlcmd**公用程式可讓您在命令提示字元中輸入 transact-sql 語句、系統程式和腳本檔案。 | Windows、macOS 和 Linux|
|[**bcp**](https://docs.microsoft.com/sql/tools/bcp-utility?view=sql-server-2014)|**b**ulk **c**opy **p**rogram 公用程式 (**bcp**) 會以使用者指定格式，在 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體與資料檔案之間大量複製資料。|Windows、macOS 和 Linux|
|[**mssql-腳本 (預覽)** ](https://github.com/Microsoft/mssql-scripter)|**mssql-** 腳本撰寫 SQL Server 資料庫的多平臺命令列體驗|Windows、macOS 和 Linux|
|[**mssql-conf**](../linux/sql-server-linux-configure-mssql-conf.md)|**mssql-會議**會設定在 Linux 上執行的 SQL Server。|Linux|



## <a name="which-tool-should-i-choose"></a>我應該選擇哪一種工具？

- 您要以 Windows、Linux 或 Mac 上的輕量編輯器來管理 SQL Server 實例或資料庫嗎？ 選擇 [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md)
- 您想要在具有完整 GUI 支援的 Windows 上管理 SQL Server 實例或資料庫嗎？ 選擇 [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)
- 您想要在 Windows 上建立或維護資料庫程式碼, 包括編譯時間驗證、重構和設計工具支援嗎？ 選擇 [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
- 您是否想要使用命令列工具查詢 SQL Server, 其具備 IntelliSense、語法高光源等功能？ 選擇[mssql-cli](mssql-cli.md)
- 您想要在 Windows、Linux 或 Mac 上以輕量編輯器撰寫 T-sql 腳本嗎？ 選擇[Visual Studio Code](https://code.visualstudio.com/)和[mssql 擴充](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)功能



## <a name="additional-tools"></a>其他工具

| 工具 | Description |
|:--|:--|
| [組態管理員](../tools/configuration-manager/sql-server-configuration-manager-help.md) | 使用 SQL Server 組態管理員來設定 SQL Server 服務並設定網路連線能力。 在 Windows 上執行 Configuration Manager|
| [SQL Server 移轉小幫手](../ssma/sql-server-migration-assistant.md) | 使用 SQL Server 移轉小幫手將從 Microsoft Access、DB2、MySQL、Oracle 及 Sybase 到 SQL Server 的資料庫移轉作業自動化。|
| [資料庫測試助理](../dea/database-experimentation-assistant-overview.md) | 使用資料庫測試助理, 針對指定的工作負載評估 SQL 的目標版本。 |
| [Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md) | 使用 Distributed Replay 功能, 協助您評估未來 SQL Server 升級的影響。 也請使用 Distributed Replay 協助評估硬體和作業系統升級的影響, 以及 SQL Server 調整。 |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | Ssbdiagnose 公用程式會報告 Service Broker 交談或 Service Broker 服務設定中的問題。 |

如果您要尋找此頁面未提及的其他工具, 請參閱[SQL 命令提示字元公用程式](command-prompt-utility-reference-database-engine.md)。

