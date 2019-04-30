---
title: 升級的 SQL Server 的資料庫測試助理解決方案概觀
description: 資料庫測試助理的概觀
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 1c2a28a5dc83d22a327bf797358d5edae69eb82b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63200692"
---
# <a name="overview-of-database-experimentation-assistant"></a>資料庫測試助理的概觀

資料庫測試助理 (DEA) 是 SQL Server 升級的測試解決方案。 DEA 可協助您評估特定的工作負載的目標的版本的 SQL Server。 已從舊版的 SQL Server 版本 （從 2005年開始） 升級至較新版本的 SQL Server 客戶可以使用此工具會提供分析計量。 

DEA 分析計量包括：
- 具有相容性錯誤的查詢
- 降級的查詢和查詢計劃
- 其他工作負載的比較資料

比較資料可能會導致信賴度更高及成功升級的使用體驗。

如需 19 分鐘簡介 DEA 及示範，觀看下列影片：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]

## <a name="get-dea"></a>取得 DEA

若要安裝 DEA，[下載](https://www.microsoft.com/download/details.aspx?id=54090)工具的最新版本。 然後，執行**DatabaseExperimentationAssistant.exe**檔案。

## <a name="solution-architecture-for-comparing-workloads"></a>比較工作負載的解決方案架構

下圖顯示的工作負載比較的方案架構。 工作負載的比較會在從 SQL Server 2008 升級至 SQL Server 2016 中使用 DEA 和 Distributed Replay。

![工作負載比較解決方案架構](./media/database-experimentation-assistant-overview/dea-overview-compare-solution-architecture.png)

## <a name="dea-prerequisites"></a>DEA 必要條件

以下是執行 DEA 某些必要條件：
- 最低硬體需求：在單一核心的機器為 3.5 GB 的 RAM。
- 理想的硬體需求：八核心 CPU (3.5 GB 的 RAM 或以上)。 有超過八個核心的處理器不能改善 DEA 執行階段。
- 需要額外的 33%的效能追蹤大小 A、 B 和報表分析資料庫。

## <a name="configure-dea"></a>設定 DEA

在必要條件環境架構中，我們建議您安裝 DEA *Distributed Replay controller 與相同的電腦上*。 這種做法可以避免跨電腦呼叫，並可簡化組態。

### <a name="required-configuration-for-workload-comparison-by-using-dea"></a>所需的組態工作負載使用 DEA 的比較

DEA 會連接到資料庫伺服器使用 Windows 驗證。 請務必執行 DEA 的使用者可以連接到資料庫伺服器 （來源、 目標和分析），藉由使用 Windows 驗證。

**擷取組態需求**:

*   執行 DEA 使用者可以使用 Windows 驗證連接到來源資料庫伺服器。
*   執行 DEA 使用者具有來源資料庫伺服器上的 sysadmin 權限。
*   執行來源資料庫伺服器服務帳戶具有寫入權限至追蹤資料夾路徑。

如需詳細資訊，請參閱[擷取常見問題集](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)

**重新執行組態需求**: 

*   執行 DEA 使用者可以使用 Windows 驗證連接到目標資料庫伺服器。
*   執行 DEA 使用者具有在目標資料庫伺服器上的 sysadmin 權限。
*   執行目標資料庫伺服器服務帳戶具有寫入權限至追蹤資料夾路徑。
*   執行 Distributed Replay client 服務帳戶可以使用 Windows 驗證連接到目標資料庫伺服器。
*   DEA 使用 COM 介面會與 Distributed Replay controller 通訊。 確定 TCP 連接埠已開啟 Distributed Replay controller 上的傳入要求。

如需詳細資訊，請參閱[重新執行常見問題集](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)

**分析組態需求**: 

*   執行 DEA 使用者可以使用 Windows 驗證連接到分析資料庫伺服器。
*   執行 DEA 使用者具有來源資料庫伺服器上的 sysadmin 權限。

如需詳細資訊，請參閱[分析常見問題集](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)

## <a name="set-up-telemetry"></a>設定遙測

DEA 具有啟用網際網路的功能，可以將遙測資訊傳送給 Microsoft。 Microsoft 會收集遙測來強化產品體驗。 遙測是選擇性的。 所收集的資訊也會儲存在您的本機稽核的電腦上。 您可以隨時查看收集項目的。 從 DEA 的所有記錄檔會都儲存在 %temp%\\DEA 資料夾。

您可以決定收集哪些事件。 您也可以決定是否要將收集的事件傳送給 Microsoft。 有四種類型的事件：

*   **TraceEvent**:應用程式 （例如，"觸發的停止擷取 」） 的使用量事件。
*   **例外狀況**:在應用程式使用期間擲回的例外狀況。
*   **DiagnosticEvent**:事件記錄檔以協助診斷發生問題時 (*不*傳送給 Microsoft)。
*   **FeedbackEvent**:透過應用程式送出的使用者意見反應。

下列步驟說明如何以選擇要收集哪些事件，是否將事件傳送給 Microsoft:

1.  移至 DEA 安裝所在的位置 (例如 c:\\Program Files (x86)\\Microsoft Corporation\\資料庫測試助理)。
2.  開啟兩個.config 檔案：DEA.exe.config （適用於應用程式） 和 DEACmd.exe.config （適用於 CLI)。
3.  若要停止收集事件的類型，請將設定的值*事件*(例如**TraceEvent**) 來**false**。 若要開始收集事件一次，將值設為 **，則為 true**。
4.  若要停止儲存事件的本機副本，設定的值**TraceLoggerEnabled**要**false**。 若要啟動一次儲存本機複本，請將值設定為 **，則為 true**。
5.  若要停止將事件傳送至 Microsoft，設定的值**AppInsightsLoggerEnabled**要**false**。 若要啟動一次將事件傳送至 Microsoft，請將值設定為 **，則為 true**。

DEA 受到[Microsoft 隱私權聲明](https://aka.ms/dea-privacy)。

## <a name="next-steps"></a>後續步驟

[開始使用](database-experimentation-assistant-get-started.md)逐步引導您擷取、 重新執行，並分析追蹤所需的步驟。
