---
title: "擷取、 轉換和載入資料上使用 SSIS Linux |Microsoft 文件"
description: 
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9dab69c7-73af-4340-aef0-de057356b791
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: aa4ac0cca739ea57a28beb399325d55b38502217
ms.contentlocale: zh-tw
ms.lasthandoff: 10/02/2017

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

### <a name="general-limitations-and-known-issues"></a>一般的限制與已知的問題

在這個版本的 Linux 上的 SSIS 不支援下列功能：
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

### <a name="components"></a>支援和不支援的元件

Linux 支援下列的內建 Integration Services 元件。 下表中所述，其中部分可以具有 Linux 平台上的限制。

此處未列出的內建元件不支援在 Linux 上。

#### <a name="supported-control-flow-tasks"></a>支援的控制流程工作
- 大量插入工作
- 資料流程工作
- 資料分析工作
- 執行 SQL 工作
- 執行 T-SQL 陳述式工作
- 運算式工作
- FTP 工作
- Web 服務工作
- XML 工作

#### <a name="control-flow-tasks-supported-with-limitations"></a>支援有限制的控制流程工作

| 工作 | 限制 |
|------------|---|
| 執行處理工作 | 只支援同處理序模式。 |
| 檔案系統工作 | *移動目錄*和*設定檔案屬性*不支援動作。 |
| 指令碼工作 | 只支援標準的.NET Framework Api。 |
| 傳送郵件工作 | 僅支援匿名使用者模式。 |
| 傳送資料庫工作 | 不支援 UNC 路徑。 |
| | |

#### <a name="supported-control-flow-containers"></a>支援的控制流程容器
- 時序容器
- For 迴圈容器
- Foreach 迴圈容器

#### <a name="supported-data-flow-sources-and-destinations"></a>支援的資料流來源和目的地
- 原始檔案來源和目的地
- XML 來源

#### <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>資料流程來源和目的地支援有限制

| 元件 | 限制 |
|------------|---|
| ADO.NET 來源和目的地 | 僅支援 SQLClient 資料提供者。 |
| 一般檔案來源和目的地 | 只支援 Windows 型檔案路徑，要套用的預設路徑對應規則。 例如`D:\home\ssis\travel.csv`變成`/home/ssis/travel.csv`。 |
| OData 來源 | 只支援基本驗證。 |
| ODBC 來源和目的地 | 在 Linux 上支援 64 位元 Unicode ODBC 驅動程式。 取決於 on Linux 的 UnixODBC 驅動程式管理員。 |
| OLE DB 來源和目的地 | 只支援 SQL Server Native Client 11.0 和 Microsoft OLE DB Provider for SQL Server。 |
| | |

#### <a name="supported-data-flow-transformations"></a>支援的資料流程轉換
- Aggregate
- 稽核
- 平衡型資料散發者
- 字元對應
- 條件式分割
- 複製資料行
- 資料轉換
- 衍生的資料行
- 匯出資料行
- 模糊群組 (Fuzzy Grouping)
- 模糊查閱
- 匯入資料行
- 查閱
- 合併式
- 合併聯結
- 多點傳送
- 樞紐
- 資料列計數
- 緩時變維度
- 排序
- 詞彙查閱
- Union All
- 取消樞紐

#### <a name="data-flow-transformations-supported-with-limitations"></a>資料流程轉換支援有限制

| 元件 | 限制 |
|------------|---|
| OLE DB 命令轉換 | OLE DB 來源和目的地相同的限制。 |
| 指令碼元件 | 只支援標準的.NET Framework Api。 |
| | |

### <a name="supported-and-unsupported-log-providers"></a>支援和不支援的記錄提供者
Windows 事件記錄檔提供者以外所有 Linux 上支援的內建的 SSIS 記錄提供者。

SQL Server 記錄提供者僅支援 SQL 驗證。不支援 Windows 驗證。

文字檔、 XML 檔案和 SQL Server Profiler 的 SSIS 記錄提供者會將其輸出寫入您指定的檔案。 下列考量適用於檔案路徑：
-   如果您沒有提供路徑，記錄提供者會寫入目前的目錄中的主機。 如果目前使用者沒有主應用程式的目前目錄的寫入權限，記錄提供者會引發錯誤。
-   您無法使用環境變數中的檔案路徑。 如果您指定的環境變數，您指定的常值文字會出現在檔案路徑。 例如，如果您指定`%TMP%/log.txt`，記錄提供者會將常值的文字附加`/%TMP%/log.txt`為目前的主機目錄。

## <a name="more-info-about-ssis-on-linux"></a>在 Linux 上的 SSIS 的詳細資訊

如需在 Linux 上的 SSIS 的詳細資訊，請參閱下列部落格文章：

-   [在 Linux 上的 SSIS 可用於 SQL Server 2017 CTP2.1](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [ODBC 支援 Linux （SQL Server 2017 CTP 2.1 重新整理） 上的 SSIS](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-info-about-ssis"></a>SSIS 的詳細資訊

Microsoft SQL Server Integration Services (SSIS) 是一個建立高效能資料整合方案，包括擷取、 轉換和載入 (ETL) 封裝資料倉儲的平台。 如需 SSIS 的詳細資訊，請參閱 [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services.md)。

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

