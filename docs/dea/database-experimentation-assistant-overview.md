---
title: 資料庫測試助理的總覽
description: 資料庫測試助理總覽
ms.custom: seo-lt-2019
ms.date: 11/05/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: 7180656f8a4779c43f4c691f583aaaf5fcbf86d0
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056577"
---
# <a name="overview-of-database-experimentation-assistant"></a>資料庫測試助理總覽

資料庫測試助理（DEA）是 SQL Server 升級的試驗解決方案。 DEA 可協助您評估特定工作負載的目標 SQL Server 版本。 從舊版 SQL Server （從2005開始）升級為較新版本之 SQL Server 的客戶，可以使用工具提供的分析計量。

DEA 分析計量包括：

- 具有相容性錯誤的查詢
- 降級的查詢和查詢計劃
- 其他工作負載比較資料

比較資料可能會導致更高的信賴度，以及成功的升級體驗。

## <a name="get-dea"></a>取得 DEA

若要安裝 DEA，請[下載](https://www.microsoft.com/download/details.aspx?id=54090)最新版本的工具。 然後，執行**DatabaseExperimentationAssistant**檔案。

## <a name="solution-architecture-for-comparing-workloads"></a>用於比較工作負載的解決方案架構

下圖顯示工作負載比較的方案架構。 從 SQL Server 2008 升級至 SQL Server 2016 時，工作負載比較會使用 DEA 和 Distributed Replay。

![工作負載比較解決方案架構](./media/database-experimentation-assistant-overview/dea-overview-compare-solution-architecture.png)

## <a name="dea-prerequisites"></a>DEA 必要條件

以下是執行 DEA 的一些必要條件：

- 最低硬體需求：具有 3.5 GB RAM 的單核心電腦。
- 理想的硬體需求：八核心 CPU （具有 3.5 GB RAM 或更多）。 具有8個以上核心的處理器不會改善 DEA 執行時間。
- 需要額外的33% 效能追蹤大小，才能儲存 A、B 和 report 分析資料庫。

## <a name="configure-dea"></a>設定 DEA

在必要條件環境架構中，我們建議您將 DEA 安裝*在與 Distributed Replay 控制器相同的電腦上*。 這種作法可避免跨電腦的呼叫，並簡化設定。

### <a name="required-configuration-for-workload-comparison-by-using-dea"></a>使用 DEA 進行工作負載比較所需的設定

DEA 會使用 Windows 驗證連接到資料庫伺服器。 請確定執行 DEA 的使用者可以使用 Windows 驗證連接到資料庫伺服器（來源、目標和分析）。

**捕捉設定需求**：

- 執行 DEA 的使用者可以使用 Windows 驗證連接到源資料庫伺服器。
- 執行 DEA 的使用者在源資料庫伺服器上具有 sysadmin 許可權。
- 執行源資料庫伺服器的服務帳戶具有追蹤資料夾路徑的寫入權限。

如需詳細資訊，請參閱[CAPTURE 常見問題](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)

重新執行設定**需求**： 

- 執行 DEA 的使用者可以使用 Windows 驗證連接到目標資料庫伺服器。
- 執行 DEA 的使用者具有目標資料庫伺服器上的系統管理員（sysadmin）許可權。
- 執行目標資料庫伺服器的服務帳戶具有追蹤資料夾路徑的寫入權限。
- 執行 Distributed Replay 用戶端的服務帳戶，可以使用 Windows 驗證連接到目標資料庫伺服器。
- DEA 會使用 COM 介面與 Distributed Replay 控制器通訊。 請確定已針對 Distributed Replay 控制器上的連入要求開啟 TCP 通訊埠。

如需詳細資訊，請參閱重新執行[常見問題](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)

**分析設定需求**：

- 執行 DEA 的使用者可以使用 Windows 驗證連接到分析資料庫伺服器。
- 執行 DEA 的使用者在源資料庫伺服器上具有 sysadmin 許可權。

如需詳細資訊，請參閱[分析常見問題](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)

## <a name="set-up-telemetry"></a>設定遙測

DEA 具有已啟用網際網路的功能，可將遙測資訊傳送至 Microsoft。 Microsoft 會收集遙測資料，以增強產品體驗。 遙測是選擇性的。 所收集的資訊也會儲存在您的電腦上進行本機審核。 您一律可以查看所收集的內容。 來自 DEA 的所有記錄檔會儲存在% temp%\\DEA 資料夾中。

您可以決定要收集的事件。 您也可以決定是否要將收集的事件傳送給 Microsoft。 有四種類型的事件：

- **TraceEvent**：應用程式的使用事件（例如，「已觸發停止捕獲」）。
- **Exception**：應用程式使用期間擲回例外狀況。
- **DiagnosticEvent**：事件記錄檔，可在發生問題時協助診斷（*未*傳送至 Microsoft）。
- **FeedbackEvent**：透過應用程式提交的使用者意見反應。

這些步驟會示範如何選擇要收集哪些事件，以及是否要將事件傳送給 Microsoft：

1. 移至安裝 DEA 的位置（例如 C：\\Program Files （x86）\\Microsoft Corporation\\資料庫測試助理）。
2. 開啟兩個 .config 檔案： DEA （適用于應用程式）和 DEACmd （適用于 CLI）。
3. 若要停止收集事件種類，請將*事件*的值（例如， **TraceEvent**）設定為**false**。 若要再次開始收集事件，請將值設定為**true**。
4. 若要停止儲存事件的本機複本，請將**TraceLoggerEnabled**的值設定為**false**。 若要再次開始儲存本機複本，請將值設定為**true**。
5. 若要停止將事件傳送至 Microsoft，請將**AppInsightsLoggerEnabled**的值設定為**false**。 若要再次開始將事件傳送至 Microsoft，請將值設定為**true**。

DEA 受[Microsoft 隱私權聲明](https://aka.ms/dea-privacy)所規範。

## <a name="next-steps"></a>後續的步驟

[[開始](database-experimentation-assistant-get-started.md)使用] 會引導您完成捕獲、重新執行和分析追蹤所需的步驟。
