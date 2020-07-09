---
title: Linux 上的 SSIS 限制和已知問題
description: 本文描述 Linux 電腦上的 SQL Server Integration Services (SSIS) 限制和已知問題
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
ms.date: 06/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: ff8b3953961a6d3a8f13ceec262df5fea079ced8
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85897233"
---
# <a name="limitations-and-known-issues-for-ssis-on-linux"></a>Linux 上的 SSIS 限制和已知問題

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

本文描述 Linux 上的 SQL Server Integration Services (SSIS) 限制和已知問題。

## <a name="general-limitations-and-known-issues"></a>一般限制與已知問題

Linux 上的此版本 SSIS 不支援下列功能：
  - SSIS 類別目錄資料庫
  - SQL Agent 排定的套件執行
  - Windows 驗證
  - 協力廠商元件
  - 異動資料擷取 (CDC)
  - SSIS Scale Out
  - 適用於 SSIS 的 Azure Feature Pack
  - Hadoop 和 HDFS 支援
  - Microsoft Connector for SAP BW

如需 Linux 上的 SSIS 其他限制和已知問題，請參閱[版本資訊](sql-server-linux-release-notes.md#ssis)。

## <a name="supported-and-unsupported-components"></a><a name="components"></a> 支援和不支援的元件

Linux 支援下列內建 Integration Services 元件。 其中有些元件對 Linux 平台有所限制。 Linux 不支援此處未列出的內建元件。

## <a name="supported-control-flow-tasks"></a>支援的控制流程工作
- 大量插入工作
- 資料流程工作
- 資料分析工作
- 執行 SQL 工作
- 執行 T-SQL 陳述式工作
- 運算式工作
- FTP 工作
- Web 服務工作
- XML 工作

## <a name="control-flow-tasks-supported-with-limitations"></a>有限支援的控制流程工作

| Task | 限制 |
|------------|---|
| 執行處理工作 | 僅支援同處理序模式。 |
| 檔案系統工作 | 不支援「移動目錄」  *和「設定檔案屬性」* 動作。 |
| 指令碼工作 | 僅支援標準 .NET Framework API。 |
| 傳送郵件工作 | 僅支援匿名使用者模式。 |
| 傳輸資料庫工作 | 不支援 UNC 路徑。 |
| | |

## <a name="supported-and-unsupported-maintenance-plan-tasks"></a>支援和不支援的維護計畫工作

在 SQL Server 維護計畫中，您通常可以使用各種 SSIS 工作。

Linux 不支援下列維護計畫工作：
- 通知操作員
- 執行 SQL Server Agent 作業

Linux 支援下列維護計畫工作：
- 檢查資料庫完整性
- 壓縮資料庫
- 重新組織索引
- 重建索引
- 更新統計資料
- 清除記錄
- 備份資料庫
- T-SQL 陳述式

## <a name="supported-control-flow-containers"></a>支援的控制流程容器
- 時序容器
- For 迴圈容器
- Foreach 迴圈容器

## <a name="supported-data-flow-sources-and-destinations"></a>支援的資料流程來源和目的地
- 原始檔案來源和目的地
- XML 來源

## <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>有限支援的資料流程來源和目的地

| 元件 | 限制 |
|------------|---|
| ADO.NET 來源和目的地 | 僅支援 SQLClient 資料提供者。 |
| 一般檔案來源和目的地 | 僅支援套用預設路徑對應規則的 Windows 樣式檔案路徑。 例如 `D:\home\ssis\travel.csv` 會變成 `/home/ssis/travel.csv`。 |
| OData 來源 | 僅支援基本驗證。 |
| ODBC 來源和目的地 | Linux 支援 64 位元 Unicode ODBC 驅動程式。 取決於 Linux 上的 UnixODBC 驅動程式管理員。 |
| OLE DB 來源和目的地 | 僅支援 SQL Server Native Client 11.0 和 Microsoft OLE DB Provider for SQL Server。 |
| | |

## <a name="supported-data-flow-transformations"></a>支援的資料流程轉換
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
- 合併
- 合併聯結
- 多點傳送
- 樞紐
- 資料列計數
- 緩時變維度
- Sort
- 詞彙查閱
- 聯集全部
- 取消樞紐

## <a name="data-flow-transformations-supported-with-limitations"></a>有限支援的資料流程轉換

| 元件 | 限制 |
|------------|---|
| OLE DB 命令轉換 | 其限制與 OLE DB 來源和目的地相同。 |
| 指令碼元件 | 僅支援標準 .NET Framework API。 |
| | |

## <a name="supported-and-unsupported-log-providers"></a>支援和不支援的記錄提供者
除了 Windows 事件記錄提供者以外，Linux 支援所有內建的 SSIS 記錄提供者。

SQL Server 記錄提供者僅支援 SQL 驗證，而不支援 Windows 驗證。

SSIS 記錄提供者 (適用於文字檔、XML 檔案與 SQL Server Profiler) 會將其輸出寫入您指定的檔案。 下列考量適用於檔案路徑：
-   如果您未提供路徑，記錄提供者會寫入主機目前的目錄。 如果目前使用者沒有寫入主機目前目錄的權限，記錄提供者就會引發錯誤。
-   您不能在檔案路徑中使用環境變數。 如果您指定環境變數，則您所指定的常值文字會出現在檔案路徑中。 例如，如果您指定 `%TMP%/log.txt`，則記錄提供者會將常值文字 `/%TMP%/log.txt` 附加到目前的主機目錄。

## <a name="related-content-about-ssis-on-linux"></a>Linux 上的 SSIS 相關內容
-   [使用 SSIS 在 Linux 上擷取、轉換和載入資料](sql-server-linux-migrate-ssis.md)
-   [在 Linux 上安裝 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [使用 ssis-conf 設定 Linux 上的 SQL Server Integration Services](sql-server-linux-configure-ssis.md)
-   [使用 cron 排程 Linux 上的 SQL Server Integration Services 套件執行](sql-server-linux-schedule-ssis-packages.md)
