---
title: 限制與已知的問題適用於 Linux 上的 SSIS |Microsoft Docs
description: 這篇文章描述的限制與已知的問題 SQL Server Integration Services (SSIS) 在 Linux 電腦上
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
manager: craigg
ms.date: 06/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: fdf6542f64549233dd5d4ef15dc39a53fefa49a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66712832"
---
# <a name="limitations-and-known-issues-for-ssis-on-linux"></a>限制與已知的問題適用於 Linux 上的 SSIS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

這篇文章描述的限制與已知的問題 SQL Server Integration Services (SSIS) 在 Linux 上。

## <a name="general-limitations-and-known-issues"></a>一般限制與已知的問題

在這一版的 Linux 上的 SSIS 不支援下列功能：
  - SSIS 目錄資料庫
  - SQL Agent 排程的封裝執行
  - Windows 驗證
  - 第三方元件
  - 異動資料擷取 (CDC)
  - SSIS 相應放大
  - Azure Feature Pack for SSIS
  - Hadoop 和 HDFS 支援
  - Microsoft Connector for SAP BW

如需其他限制和使用 SSIS 在 Linux 上的已知的問題，請參閱[版本資訊](sql-server-linux-release-notes.md#ssis)。

## <a name="components"></a> 支援和不支援的元件

在 Linux 上支援下列內建的 Integration Services 元件。 其中一些 Linux 平台上有限制。 此處未列出的內建元件不支援在 Linux 上。

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

## <a name="control-flow-tasks-supported-with-limitations"></a>支援有限制的控制流程工作

| 工作 | 限制 |
|------------|---|
| 執行處理工作 | 僅支援同處理序模式。 |
| 檔案系統工作 | *移動目錄*並*設定檔屬性*不支援動作。 |
| 指令碼工作 | 只支援標準的.NET Framework Api。 |
| 傳送郵件工作 | 僅支援匿名使用者模式。 |
| 傳送資料庫工作 | 不支援 UNC 路徑。 |
| | |

## <a name="supported-and-unsupported-maintenance-plan-tasks"></a>支援和不支援的維護計畫工作

在 SQL Server 維護計畫中，您通常可以使用各種不同的 SSIS 工作。

在 Linux 上不支援下列的維護計畫工作：
- 通知操作員
- 執行 SQL Server Agent 作業

在 Linux 上支援下列的維護計畫工作：
- 檢查資料庫完整性
- 壓縮資料庫
- 重新組織索引
- 重建索引
- 更新統計資料
- 清除記錄
- 備份資料庫
- T-SQL 陳述式

## <a name="supported-control-flow-containers"></a>支援控制流程容器
- 時序容器
- For 迴圈容器
- Foreach 迴圈容器

## <a name="supported-data-flow-sources-and-destinations"></a>支援的資料流來源和目的地
- 原始檔案來源和目的地
- XML 來源

## <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>資料流程來源和目的地支援有限制

| 元件 | 限制 |
|------------|---|
| ADO.NET 來源和目的地 | 僅支援 SQLClient 資料提供者。 |
| 一般檔案來源和目的地 | 只支援 Windows 型檔案路徑，要套用的預設路徑對應規則。 比方說`D:\home\ssis\travel.csv`會變成`/home/ssis/travel.csv`。 |
| OData 來源 | 僅支援基本驗證。 |
| ODBC 來源和目的地 | 支援在 Linux 上的 64 位元 Unicode ODBC 驅動程式。 取決於 Linux 上的 UnixODBC 驅動程式管理員。 |
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
- 合併式
- 合併聯結
- 多點傳送
- 樞紐
- 資料列計數
- 緩時變維度
- 排序
- 詞彙查閱
- 聯集全部
- 取消樞紐

## <a name="data-flow-transformations-supported-with-limitations"></a>資料流程轉換支援有限制

| 元件 | 限制 |
|------------|---|
| OLE DB 命令轉換 | 與 OLE DB 來源和目的地有相同的限制。 |
| 指令碼元件 | 只支援標準的.NET Framework Api。 |
| | |

## <a name="supported-and-unsupported-log-providers"></a>支援和不支援的記錄提供者
Windows 事件記錄檔提供者以外所有的內建的 SSIS 記錄提供者支援在 Linux 上。

SQL Server 記錄提供者僅支援 SQL 驗證;它不支援 Windows 驗證。

文字檔、 XML 檔案，以及 SQL Server Profiler 的 SSIS 記錄提供者會將其輸出寫入您指定的檔案。 下列考量適用於檔案路徑：
-   如果您沒有提供路徑，記錄提供者就會寫入目前的目錄中的主應用程式。 如果目前使用者沒有寫入目前的目錄主機的權限，記錄提供者會引發錯誤。
-   您無法使用環境變數中的檔案路徑。 如果您指定環境變數，您指定的常值文字會出現在檔案路徑中。 例如，如果您指定`%TMP%/log.txt`，記錄提供者會將附加的常值文字`/%TMP%/log.txt`到目前的主應用程式目錄。

## <a name="related-content-about-ssis-on-linux"></a>關於 Linux 上的 SSIS 的相關的內容
-   [擷取、 轉換和載入與 SSIS Linux 上的資料](sql-server-linux-migrate-ssis.md)
-   [在 Linux 上安裝 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [在 Linux 上設定 SQL Server Integration Services 使用 ssis conf](sql-server-linux-configure-ssis.md)
-   [排程 SQL Server Integration Services 封裝執行在 Linux 上的使用 cron](sql-server-linux-schedule-ssis-packages.md)
