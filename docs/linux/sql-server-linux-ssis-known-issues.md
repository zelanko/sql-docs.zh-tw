---
title: "限制與已知的問題適用於 Linux 上的 SSIS |Microsoft 文件"
description: "這篇文章描述限制與已知的問題 SQL Server Integration Services (SSIS) 在 Linux 電腦上"
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: c366afc1b8755a22b13fa6224ec117db045c8dd3
ms.sourcegitcommit: 9d0467265e052b925547aafaca51e5a5e93b7e38
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/02/2018
---
# <a name="limitations-and-known-issues-for-ssis-on-linux"></a>限制與已知的問題適用於 Linux 上的 SSIS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文說明目前的限制與已知的問題 SQL Server Integration Services (SSIS) 在 Linux 上。

## <a name="general-limitations-and-known-issues"></a>一般的限制與已知的問題

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

## <a name="components"></a> 支援和不支援的元件

Linux 支援下列的內建 Integration Services 元件。 下表中所述，其中部分可以具有 Linux 平台上的限制。

此處未列出的內建元件不支援在 Linux 上。

### <a name="supported-control-flow-tasks"></a>支援的控制流程工作
- 大量插入工作
- 資料流程工作
- 資料分析工作
- 執行 SQL 工作
- 執行 T-SQL 陳述式工作
- 運算式工作
- FTP 工作
- Web 服務工作
- XML Task

### <a name="control-flow-tasks-supported-with-limitations"></a>支援有限制的控制流程工作

| 工作 | 限制 |
|------------|---|
| 執行處理工作 | 只支援同處理序模式。 |
| 檔案系統工作 | *移動目錄*和*設定檔案屬性*不支援動作。 |
| 指令碼工作 | 只支援標準的.NET Framework Api。 |
| 傳送郵件工作 | 僅支援匿名使用者模式。 |
| 傳送資料庫工作 | 不支援 UNC 路徑。 |
| | |

### <a name="supported-control-flow-containers"></a>支援的控制流程容器
- 時序容器
- For 迴圈容器
- Foreach 迴圈容器

### <a name="supported-data-flow-sources-and-destinations"></a>支援的資料流來源和目的地
- 原始檔案來源和目的地
- XML 來源

### <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>資料流程來源和目的地支援有限制

| 元件 | 限制 |
|------------|---|
| ADO.NET 來源和目的地 | 僅支援 SQLClient 資料提供者。 |
| 一般檔案來源和目的地 | 只支援 Windows 型檔案路徑，要套用的預設路徑對應規則。 例如`D:\home\ssis\travel.csv`變成`/home/ssis/travel.csv`。 |
| OData 來源 | 只支援基本驗證。 |
| ODBC 來源和目的地 | 在 Linux 上支援 64 位元 Unicode ODBC 驅動程式。 取決於 on Linux 的 UnixODBC 驅動程式管理員。 |
| OLE DB 來源和目的地 | 只支援 SQL Server Native Client 11.0 和 Microsoft OLE DB Provider for SQL Server。 |
| | |

### <a name="supported-data-flow-transformations"></a>支援的資料流程轉換
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

### <a name="data-flow-transformations-supported-with-limitations"></a>資料流程轉換支援有限制

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

## <a name="related-content-about-ssis-on-linux"></a>有關 SSIS 在 Linux 上的相關的內容
-   [擷取、 轉換和載入與 SSIS Linux 上的資料](sql-server-linux-migrate-ssis.md)
-   [Linux 上安裝 SQL Server Integration Services (SSIS)](sql-server-linux-setup-ssis.md)
-   [使用 ssis conf，設定 Linux 上的 SQL Server Integration Services](sql-server-linux-configure-ssis.md)
-   [排程 SQL Server Integration Services 封裝執行 Linux 上的 cron](sql-server-linux-schedule-ssis-packages.md)
