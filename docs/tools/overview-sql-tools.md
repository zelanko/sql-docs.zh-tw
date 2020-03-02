---
title: SQL 工具概觀
description: SQL Server、Azure SQL (Azure SQL database、Azure SQL 受控執行個體、SQL 虛擬機器) 和 Azure SQL 資料倉儲的 SQL 查詢和管理工具。
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ''
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 02/04/2020
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 3f457b485994d2619e68b4315a308e66a05715cb
ms.sourcegitcommit: cf8db6330be0d89bbec362e4c7e187b5461026f0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/06/2020
ms.locfileid: "77051668"
---
# <a name="sql-tools-overview"></a>SQL 工具概觀

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

若要管理您的資料庫，您需要工具。 不論您的資料庫是在雲端、Windows、macOS 或 [Linux](../linux/sql-server-linux-overview.md) 上執行，工具不一定要在與資料庫相同的平台上執行。

您可以在下表中檢視不同 SQL 工具的連結。

> [!Note]
> 若要下載 SQL Server，請參閱[安裝 SQL Server](../database-engine/install-windows/install-sql-server.md)。

## <a name="recommended-tools"></a>建議工具

下列工具提供圖形化使用者介面 (GUI)。

| 工具 | 描述 | 作業系統 |
|:--|:--|:--|
| [ **![ADS 影像](../tools/media/overview-sql-tools/azure-data-studio.svg)</br></br>Azure Data Studio**](../azure-data-studio/download.md) | 一種可執行隨選 SQL 查詢、檢視結果並將其儲存為文字、JSON 或 Excel 的輕量編輯器。 在熟悉的物件瀏覽體驗中編輯資料、管理您慣用的資料庫連線，以及瀏覽資料庫物件。 | **Windows</br>macOS</br>Linux** |
| [ **![SSMS 影像](../tools/media/overview-sql-tools/ssms.svg)</br></br>SQL Server Management Studio (SSMS)** ](../ssms/download-sql-server-management-studio-ssms.md) | 管理具有完整 GUI 支援的 SQL Server 執行個體或資料庫。 存取、設定、管理、掌管和開發 SQL Server、Azure SQL Database 和 SQL 資料倉儲的所有元件。 可提供單一的完整公用程式，其結合廣泛圖形工具和豐富的指令碼編輯器，使開發人員和資料庫管理員 (不管他們的技術水準如何) 都能夠存取 SQL。 | **Windows** |
| [ **![SSDT 影像](../tools/media/overview-sql-tools/ssdt.svg)</br>SQL Server Data Tools (SSDT)** ](../ssdt/download-sql-server-data-tools-ssdt.md) | 一個新式開發工具，可用來建置 SQL Server 關聯式資料庫、Azure SQL 資料庫、Analysis Services (AS) 資料模型、Integration Services (IS) 套件和 Reporting Services (RS) 報表。 有了 SSDT，您即可設計和部署任何 SQL Server 內容類型，如同在 **[Visual Studio](https://visualstudio.microsoft.com/downloads/)** 中開發應用程式一樣容易。 | **Windows** |
| [ **![VS Code 影像](../tools/media/overview-sql-tools/visual-studio-code.svg)</br></br>Visual Studio Code**](https://code.visualstudio.com/) | Visual Studio Code 的 **[mssql 延伸模組](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)** 是正式的 SQL Server 延伸模組，可在 Visual Studio Code 中支援對 SQL Server 的連線，以及豐富的 T-SQL 編輯體驗。 在輕量編輯器中撰寫 T-SQL 指令碼。 | **Windows</br>macOS</br>Linux** |

## <a name="command-line-tools"></a>命令列工具

以下工具是主要的命令列工具。

| 工具 | 描述 | 作業系統 |
|:--|:--|:--|
|[**bcp**](bcp-utility.md)|**b**ulk **c**opy **p**rogram 公用程式 (**bcp**) 會以使用者指定的格式在 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體與資料檔案之間大量複製資料。| **Windows</br>macOS</br>Linux** |
|[**mssql-cli (預覽)** ](mssql-cli.md)|**mssql-cli** 是用於查詢 SQL Server 的互動式命令列查詢工具。 此外，請使用具備 IntelliSense、語法醒目提示等功能的命令列工具來查詢 SQL Server。 | **Windows</br>macOS</br>Linux** |
|[**mssql-conf**](../linux/sql-server-linux-configure-mssql-conf.md) | **mssql-conf** 可設定在 Linux 上執行的 SQL Server。 | **Linux** |
|[**mssql-scripter (預覽)** ](https://github.com/Microsoft/mssql-scripter) | **mssql-scripter** 是多平台命令列體驗，用於撰寫 SQL Server 資料庫的指令碼。 | **Windows</br>macOS</br>Linux** |
| [**sqlcmd**](sqlcmd-utility.md) |**sqlcmd** 公用程式可讓您在命令列提示字元中輸入 Transact-SQL 陳述式、系統程序和指令檔。 | **Windows</br>macOS</br>Linux** |
| [**sqlpackage**](sqlpackage.md) |**sqlpackage** 是命令列公用程式，可將數種資料庫開發工作自動化。 |**Windows</br>macOS</br>Linux** |
|[**SQL Server PowerShell**](../powershell/sql-server-powershell.md)| **SQL Server PowerShell** 提供可用於 SQL 的 Cmdlet。 | **Windows</br>macOS</br>Linux** |

## <a name="migration-and-other-tools"></a>移轉和其他工具

這些工具用來移轉、設定及提供 SQL 資料庫的其他功能。

| 工具 | 描述 |
|:--|:--|
| **[組態管理員](../tools/configuration-manager/sql-server-configuration-manager-help.md)** | 使用 SQL Server 組態管理員來設定 SQL Server 服務以及設定網路連線能力。 組態管理員在 Windows 上執行|
| **[資料庫測試助理](../dea/database-experimentation-assistant-overview.md)** | 使用資料庫測試助理來評估指定工作負載的 SQL 目標版本。 |
| **[Data Migration Assistant](../dma/dma-overview.md)** | Data Migration Assistant 工具可藉由偵測可能對您新版 SQL Server or Azure SQL Database 中資料庫功能造成影響的相容性問題，以協助您升級至新式資料平台。 |
| **[Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md)** | 使用 Distributed Replay 功能來協助您評定未來 SQL Server 升級的影響。 您也可以使用 Distributed Replay 來協助評定硬體和作業系統升級以及 SQL Server 微調的影響。 |
| **[ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)** | ssbdiagnose 公用程式會報告 Service Broker 交談或 Service Broker 服務組態中的問題。 |
| **[SQL Server 移轉小幫手](../ssma/sql-server-migration-assistant.md)** | 使用 SQL Server 移轉小幫手將從 Microsoft Access、DB2、MySQL、Oracle 及 Sybase 到 SQL Server 的資料庫移轉作業自動化。|

如果您要尋找此頁面未提及的其他工具，請參閱 [SQL 命令提示字元公用程式](command-prompt-utility-reference-database-engine.md)和[下載 SQL Server 擴充功能及工具](download-sql-feature-packs.md)