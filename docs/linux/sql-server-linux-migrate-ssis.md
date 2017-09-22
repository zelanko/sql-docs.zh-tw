---
title: "擷取、 轉換和載入資料上使用 SSIS Linux |Microsoft 文件"
description: 
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9dab69c7-73af-4340-aef0-de057356b791
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 736b7e0744a95d859bd25a6c7974dc13e79d4bb7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/21/2017

---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>擷取、 轉換和載入與 SSIS Linux 上的資料

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

本主題描述如何在 Linux 上執行 SQL Server Integration Services (SSIS) 封裝。 SSIS 能夠載入多個來源或資料格式，解決複雜的資料整合問題轉換並清理資料，及更新多個目的地。 

在 Linux 上執行 SSIS 封裝可以連接到 Microsoft SQL Server 在 Windows 內部部署或在雲端中，在 Linux 上或在 Docker 中執行。 它們也可以連接到 Azure SQL Database、 Azure SQL 資料倉儲、 和 ODBC 資料來源。

您可以使用 SSIS 在 Linux 上執行封裝時，您也可以建立和維護封裝的 Windows 電腦。 SSIS 設計和管理工具是 Windows 應用程式。 

## <a name="prerequisites"></a>必要條件

若要在 Linux 電腦上執行 SSIS 封裝，您需要先安裝 SQL Server Integration Services。 如需安裝指示，請參閱[安裝 SQL Server Integration Services](sql-server-linux-setup-ssis.md)。

## <a name="run-an-ssis-package"></a>執行 SSIS 封裝

若要在 Linux 電腦上執行 SSIS 封裝，執行下列動作：

1.  將 SSIS 封裝複製至 Linux 電腦。
2.  執行下列命令：
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="more-about-ssis-on-linux"></a>深入了解在 Linux 上的 SSIS

**ODBC 連接**。 在重新整理 Linux CTP 2.1 和更新版本的 SSIS，SSIS 封裝可以使用 ODBC 連接 on Linux。 這項功能經過測試可與 SQL Server 及 MySQL ODBC 驅動程式，但也應該使用 ODBC 規格會觀察到的任何 Unicode ODBC 驅動程式。 在設計階段，您可以提供 DSN 或連接字串連接至 ODBC 資料;您也可以使用 Windows 驗證。 如需詳細資訊，請參閱[部落格文章發表的 ODBC 支援在 Linux 上](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)。

**路徑**。 在 Linux 上的 SSIS 不支援 Linux 樣式路徑，但在執行階段，將 Windows 樣式路徑對應至 Linux 樣式路徑。 提供 SSIS 封裝中的視窗樣式路徑。 然後，例如，在 Linux 上的 SSIS 對應 Windows 樣式路徑`C:\test`Linux 樣式路徑`/test`。

**部署封裝**。 您只可以將封裝儲存在 Linux 上的檔案系統，在此版本中。 SSIS 目錄資料庫和舊版 SSIS 服務無法使用。 在 Linux 上的封裝部署和儲存體

**排程封裝**。 您無法使用 Linux 上的 SQL 代理程式排程在此版本中的封裝執行。

**其他的限制與已知的問題**。 當您在 Linux 上執行 SSIS 封裝時，下列功能不支援此版本中：
  - SSIS 目錄資料庫
  - SQL Agent 排程的封裝執行
  - Windows 驗證
  - 第三方元件
  - 異動資料擷取 (CDC)
  - SSIS 向外延展
  - 適用於 SSIS 的 azure 功能套件
  - Hadoop 和 HDFS 的支援
  - Microsoft Connector for SAP BW

如需其他限制和 SSIS 在 Linux 上的已知的問題，請參閱[版本資訊](sql-server-linux-release-notes.md#ssis)。

如需在 Linux 上的 SSIS 的詳細資訊，請參閱下列部落格文章：

-   [在 Linux 上的 SSIS 可用於 SQL Server 2017 CTP2.1](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [ODBC 支援 Linux （SQL Server 2017 CTP 2.1 重新整理） 上的 SSIS](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-about-ssis"></a>深入了解 SSIS

Microsoft SQL Server Integration Services (SSIS) 是一個建立高效能資料整合方案，包括擷取、 轉換和載入 (ETL) 封裝資料倉儲的平台。 如需 SSIS 的詳細資訊，請參閱 [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services.md)。

SSIS 包含下列功能：
- 圖形工具和精靈，來建置和偵錯在 Windows 上的封裝
- 各種工作的執行工作流程函式，例如 FTP 作業、 執行 SQL 陳述式，並傳送電子郵件訊息
- 各種不同的資料來源和目的地來擷取及載入資料
- 各種不同的轉換清除、 彙總、 合併和複製資料
- 應用程式開發介面 (Api)，與您自己的自訂指令碼元件擴充 SSIS

若要開始使用 SSIS，下載最新版[SQL Server Data Tools (SSDT)](/sql-docs/docs/integration-services/ssis-how-to-create-an-etl-package)。

## <a name="see-also"></a>另請參閱
- [深入了解 SQL Server Integration Services](/sql-docs/docs/integration-services/sql-server-integration-services)
- [SQL Server Integration Services (SSIS) 開發和管理工具](/sql-docs/docs/integration-services/integration-services-ssis-development-and-management-tools)
- [SQL Server Integration Services 教學課程](/sql-docs/docs/integration-services/integration-services-tutorials)

