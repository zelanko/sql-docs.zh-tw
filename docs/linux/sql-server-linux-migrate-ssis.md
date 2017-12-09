---
title: "擷取、 轉換和載入資料上使用 SSIS Linux |Microsoft 文件"
description: "本文說明的 Linux 電腦的 SQL Server Integration Services (SSIS)"
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: 2b09251cae6b89dd742d685f9405155a7b674a3d
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>擷取、 轉換和載入與 SSIS Linux 上的資料

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本主題描述如何在 Linux 上執行 SQL Server Integration Services (SSIS) 封裝。 SSIS 可從多個來源和格式，擷取資料來解決複雜的資料整合問題轉換並清理資料，並將資料載入到多個目的地。 

在 Linux 上執行 SSIS 封裝可以連接到 Microsoft SQL Server 在 Windows 內部部署或在雲端中，在 Linux 上或在 Docker 中執行。 它們也可以連接到 Azure SQL Database、 Azure SQL 資料倉儲、 ODBC 資料來源、 一般檔案和其他資料來源，包括 ADO.NET 來源、 XML 檔案和 OData 服務。

如需詳細的 SSIS 功能的詳細資訊，請參閱[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)。

## <a name="prerequisites"></a>必要條件

若要在 Linux 電腦上執行 SSIS 封裝，您需要先安裝 SQL Server Integration Services。 SSIS 不隨附於 SQL Server 安裝的 Linux 電腦。 如需安裝指示，請參閱[安裝 SQL Server Integration Services](sql-server-linux-setup-ssis.md)。

您還必須提供建立和維護封裝的 Windows 電腦。 SSIS 設計和管理工具是不是目前可用的 Linux 電腦的 Windows 應用程式。 

## <a name="run-an-ssis-package"></a>執行 SSIS 封裝

若要在 Linux 電腦上執行 SSIS 封裝，執行下列動作：

1.  將 SSIS 封裝複製至 Linux 電腦。
2.  執行下列命令：
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="other-common-ssis-tasks"></a>其他常見的 SSIS 工作

-   **設計封裝**。

    -   **連接至 ODBC 資料來源**。 在重新整理 Linux CTP 2.1 和更新版本的 SSIS，SSIS 封裝可以使用 ODBC 連接 on Linux。 這項功能經過測試可與 SQL Server 及 MySQL ODBC 驅動程式，但也應該使用 ODBC 規格會觀察到的任何 Unicode ODBC 驅動程式。 在設計階段，您可以提供 DSN 或連接字串連接至 ODBC 資料;您也可以使用 Windows 驗證。 如需詳細資訊，請參閱[部落格文章發表的 ODBC 支援在 Linux 上](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。

    -   **路徑**。 提供 SSIS 封裝中的視窗樣式路徑。 在 Linux 上的 SSIS 不支援 Linux 樣式路徑，但在執行階段，將 Windows 樣式路徑對應至 Linux 樣式路徑。 然後，例如，在 Linux 上的 SSIS 對應 Windows 樣式路徑`C:\test`Linux 樣式路徑`/test`。

-   **部署封裝**。 您只可以將封裝儲存在 Linux 上的檔案系統，在此版本中。 SSIS 目錄資料庫和舊版 SSIS 服務無法使用。 在 Linux 上的封裝部署和儲存體

-   **排程封裝**。 您可以使用這類排程工具的 Linux 系統`cron`排程封裝。 您無法使用 Linux 上的 SQL 代理程式排程在此版本中的封裝執行。 如需詳細資訊，請參閱[排程 SSIS 封裝在 Linux 上的 cron](sql-server-linux-schedule-ssis-packages.md)。

## <a name="limitations-and-known-issues"></a>限制與已知的問題

如需限制和 SSIS 在 Linux 上的已知的問題的詳細資訊，請參閱[限制與已知的問題適用於 Linux 上的 SSIS](sql-server-linux-ssis-known-issues.md)。

## <a name="more-info-about-ssis-on-linux"></a>在 Linux 上的 SSIS 的詳細資訊

如需在 Linux 上的 SSIS 的詳細資訊，請參閱下列部落格文章：

-   [在 Linux 上的 SSIS 可用於 SQL Server 2017 CTP2.1](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [ODBC 支援 Linux （SQL Server 2017 CTP 2.1 重新整理） 上的 SSIS](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-info-about-ssis"></a>SSIS 的詳細資訊

Microsoft SQL Server Integration Services (SSIS) 是一個建立高效能資料整合方案，包括擷取、 轉換和載入 (ETL) 封裝資料倉儲的平台。 如需 SSIS 的詳細資訊，請參閱 [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services)。

SSIS 包含下列功能：
- 圖形工具和精靈，來建置和偵錯在 Windows 上的封裝
- 各種工作的執行工作流程函式，例如 FTP 作業、 執行 SQL 陳述式，並傳送電子郵件訊息
- 各種不同的資料來源和目的地來擷取及載入資料
- 各種不同的轉換清除、 彙總、 合併和複製資料
- 應用程式開發介面 (Api)，與您自己的自訂指令碼元件擴充 SSIS

若要開始使用 SSIS，下載最新版[SQL Server Data Tools (SSDT)](../integration-services/ssis-how-to-create-an-etl-package.md)。

## <a name="see-also"></a>另請參閱
- [深入了解 SQL Server Integration Services](../integration-services/sql-server-integration-services.md)
- [SQL Server Integration Services (SSIS) 開發和管理工具](../integration-services/integration-services-ssis-development-and-management-tools.md)
- [SQL Server Integration Services 教學課程](../integration-services/integration-services-tutorials.md)
