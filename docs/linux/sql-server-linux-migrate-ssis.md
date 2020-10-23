---
title: 使用 SSIS 在 Linux 上擷取、轉換和載入資料
description: 了解如何在 Linux 上執行 SQL Server Integration Services (SSIS) 套件。 同時了解哪裡可以找到有關 SSIS 功能的詳細資訊。
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: e513f6783e827617a8c0cc4a1fa0ea4644dcb6e7
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115839"
---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>使用 SSIS 在 Linux 上擷取、轉換和載入資料

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

本文說明如何在 Linux 上執行 SQL Server Integration Services (SSIS) 套件。 SSIS 可擷取來自多個來源和格式的資料、轉換和清理資料，然後將資料載入多個目的地，藉此解決複雜的資料整合問題。 

在 Linux 上執行的 SSIS 套件可以連接到在 Windows 內部部署或雲端、在 Linux 上或是在 Docker 中執行的 Microsoft SQL Server。 其也可以連線到 Azure SQL Database、Azure Synapse Analytics、ODBC 資料來源、一般檔案及其他資料來源，包括 ADO.NET 來源、XML 檔案和 OData 服務。

如需 SSIS 功能的詳細資訊，請參閱 [SQL Server Integration Services](../integration-services/sql-server-integration-services.md)。

## <a name="prerequisites"></a>必要條件

若要在 Linux 電腦上執行 SSIS 套件，您必須先安裝 SQL Server Integration Services。 安裝於 Linux 電腦的 SQL Server 中不包含 SSIS。 如需安裝指示，請參閱[安裝 SQL Server Integration Services](sql-server-linux-setup-ssis.md)。

您也必須有 Windows 電腦才能建立和維護套件。 SSIS 設計和管理工具是目前不適用於 Linux 電腦的 Windows 應用程式。 

## <a name="run-an-ssis-package"></a>執行 SSIS 套件

若要在 Linux 電腦上執行 SSIS 套件，請執行下列動作：

1.  將 SSIS 套件複製到 Linux 電腦。
2.  執行下列命令：
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="run-an-encrypted-password-protected-package"></a>執行加密 (受密碼保護) 的套件
執行使用密碼加密的 SSIS 套件有三種方式：

1.  設定環境變數 `SSIS_PACKAGE_DECRYPT` 的值，如下列範例所示：

    ```
    SSIS_PACKAGE_DECRYPT=test /opt/ssis/bin/dtexec /f package.dtsx
    ```

2.  指定 `/de[crypt]` 選項以互動方式輸入密碼，如下列範例所示：

    ```
    /opt/ssis/bin/dtexec /f package.dtsx /de
    
    Enter decryption password:
    ```

3.  指定 `/de` 選項，在命令列上提供密碼，如下列範例所示。 不建議使用這個方法，因為會將解密密碼與命令一起儲存在命令歷程記錄中。

    ```
    opt/ssis/bin/dtexec /f package.dtsx /de test
    
    Warning: Using /De[crypt] <password> may store decryption password in command history.
    
    You can use /De[crypt] instead to enter interactive mode,
    or use environment variable SSIS_PACKAGE_DECRYPT to set decryption password.
    ```

## <a name="design-packages"></a>設計套件

**連接到 ODBC 資料來源**。 透過 Linux CTP 2.1 Refresh 和更新版本上的 SSIS，SSIS 套件可以在 Linux 上使用 ODBC 連接。 此功能已經過 SQL Server 和 MySQL ODBC 驅動程式的測試，但也應該能夠與任何遵循 ODBC 規格的 Unicode ODBC 驅動程式搭配使用。 在設計階段，您可以提供 DSN 或連接字串來連接到 ODBC 資料；您也可以使用 Windows 驗證。 如需詳細資訊，請參閱[宣佈在 Linux 上提供 ODBC 支援的部落格文章](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/) \(英文\)。

**路徑**。 在 SSIS 套件中提供 Windows 樣式路徑。 Linux 上的 SSIS 不支援 Linux 樣式路徑，但會在執行階段將 Windows 樣式路徑對應至 Linux 樣式路徑。 例如，Linux 上的 SSIS 會將 Windows 樣式路徑 `C:\test` 對應至 Linux 樣式路徑 `/test`。

## <a name="deploy-packages"></a>部署套件
在此版本中，您只能將套件儲存在 Linux 上的檔案系統中。 您無法在 Linux 上使用 SSIS 目錄資料庫和舊版 SSIS 服務去部署和儲存套件。

## <a name="schedule-packages"></a>排程套件
您可以使用 Linux 系統排程工具 (例如 `cron`) 來排程套件。 在此版本中，您無法使用 Linux 上的 SQL Agent 排程套件執行。 如需詳細資訊，請參閱[使用 cron 排程 Linux 上的 SSIS 套件](sql-server-linux-schedule-ssis-packages.md)。

## <a name="limitations-and-known-issues"></a>限制與已知問題

如需 Linux 上 SSIS 限制和已知問題的詳細資訊，請參閱 [Linux 上的 SSIS 限制和已知問題](sql-server-linux-ssis-known-issues.md)。

## <a name="more-info-about-ssis-on-linux"></a>Linux 上 SSIS 的詳細資訊

如需 Linux 上 SSIS 的詳細資訊，請參閱下列部落格文章：

-   [SSIS on Linux is available in SQL Server CTP2.1](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/) (SQL Server CTP2.1 已推出 Linux 上的 SSIS)
-   [ODBC is supported in SSIS on Linux (SQL Server CTP 2.1 refresh)](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/) (Linux (SQL Server CTP 2.1 Refresh) 上的 SSIS 支援 ODBC)

## <a name="more-info-about-ssis"></a>SSIS 的詳細資訊

Microsoft SQL Server Integration Services (SSIS) 是一種用於建置高效能資料整合解決方案的平台，其中包括資料倉儲的擷取、轉換和載入 (ETL) 套件。 如需 SSIS 的詳細資訊，請參閱 [SQL Server Integration Services](../integration-services/sql-server-integration-services.md)。

SSIS 包含下列功能：
- 用於在 Windows 上建置和偵錯套件的圖形化工具和精靈
- 用於執行工作流程函數的各種工作，例如 FTP 作業、執行 SQL 陳述式和傳送電子郵件訊息
- 用於擷取和載入資料的各種資料來源和目的地
- 用於清理、彙總、合併和複製資料的各種轉換
- 現有 SSIS 的應用程式開發介面 (API)，其中包含您自己的自訂指令碼和元件

若要開始使用 SSIS，請下載最新版本的 [SQL Server Data Tools (SSDT)](../integration-services/ssis-how-to-create-an-etl-package.md)。

如需 SSIS 的詳細資訊，請參閱下列文章：
- [深入了解 SQL Server Integration Services](../integration-services/sql-server-integration-services.md)
- [SQL Server Integration Services (SSIS) 開發和管理工具](../integration-services/integration-services-ssis-development-and-management-tools.md)
- [SQL Server Integration Services 教學課程](../integration-services/integration-services-tutorials.md)

## <a name="related-content-about-ssis-on-linux"></a>Linux 上的 SSIS 相關內容
-   [在 Linux 上安裝 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [使用 ssis-conf 設定 Linux 上的 SQL Server Integration Services](sql-server-linux-configure-ssis.md)
-   [Linux 上的 SSIS 限制和已知問題](sql-server-linux-ssis-known-issues.md)
-   [使用 cron 排程 Linux 上的 SQL Server Integration Services 套件執行](sql-server-linux-schedule-ssis-packages.md)