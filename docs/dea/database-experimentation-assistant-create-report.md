---
title: 建立分析報表
description: 在資料庫測試助理中建立分析報表
ms.date: 01/24/2020
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: f82aba87632abea4ac5fbc8b54daa6dfd0eb5b4a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "79289836"
---
# <a name="create-analysis-reports-in-database-experimentation-assistant-sql-server"></a>在資料庫測試助理中建立分析報表（SQL Server）

在兩個目標伺服器上重新執行來源追蹤之後，您可以在資料庫測試助理（DEA）中產生分析報表。 分析報表可協助您深入瞭解建議變更的效能影響。

## <a name="create-an-analysis-report"></a>建立分析報表

1. 在 [DEA] 中，選取清單圖示、指定伺服器名稱和驗證類型、選取或取消選取適用于您案例的 [**加密**連線] 和 [**信任伺服器憑證**] 核取方塊，然後選取 **[連線]**。

   ![使用追蹤檔案連接到伺服器](./media/database-experimentation-assistant-create-report/dea-connect-to-server-with-trace-files.png)

2. 在 [**分析報表**] 畫面上，選取 [**新增分析報表**]。

   ![建立新的分析報表](./media/database-experimentation-assistant-create-report/dea-create-an-analysis-report.png)

3. 在 [**新增分析報表**] 畫面上，指定報表的名稱、目標1和目標2追蹤檔案的儲存位置和路徑，然後選取 [**啟動**]。

   ![指定新的分析報表詳細資料](./media/database-experimentation-assistant-create-report/dea-new-analysis-report-details.png)

   如果您輸入的資訊有效，就會建立分析報表。

   ![新建立的分析報表](./media/database-experimentation-assistant-create-report/dea-newly-created-analysis-report.png)

      > [!NOTE]
      > 如果您輸入的資訊中有任何一項無效，則包含不正確資訊的文字方塊會以紅色反白顯示。 進行任何必要的更正，然後再次選取 [**啟動**]。

## <a name="frequently-asked-questions-about-analysis-reports"></a>分析報告的相關常見問題

**問：我的分析報表會告訴我什麼？**

DEA 會使用統計測試來分析您的工作負載，並判斷每個查詢從目標1到目標2的執行方式。 它會提供每個查詢的效能詳細資料。 深入瞭解[開始](database-experimentation-assistant-get-started.md)使用中的 DEA。

**問：是否可以在產生另一個報表時，建立新的分析報表？**

不可以。  目前，一次只能產生一份報表，以避免發生衝突。 不過，您可以同時執行一個以上的 capture 和 replay。

**問：我可以使用命令提示字元產生分析報告嗎？**

是。 您可以在命令提示字元中產生分析報表。 然後您可以在 UI 中查看報表。 如需詳細資訊，請參閱[在命令提示](database-experimentation-assistant-run-command-prompt.md)字元中執行。

## <a name="troubleshoot-analysis-reports"></a>分析報表的疑難排解

**問：我需要哪些安全性許可權，才能在我的伺服器上產生及查看分析報表？**

登入 DEA 的使用者必須具有 analysis server 的 sysadmin 許可權。 如果使用者是群組的一部分，請確定該群組具有 sysadmin 許可權。

|可能的錯誤|解決方法|  
|---|---|  
|無法連接到資料庫。 請確定您具有系統管理員許可權，可分析及查看報表。|您可能沒有伺服器或資料庫的存取權或系統管理員（sysadmin）許可權。 請確認您的登入許可權，然後再試一次。|  
|無法在伺服器**伺服器名稱**上產生**報告名稱**。 如需詳細資訊，請參閱**報表名稱**報表。|您可能沒有產生新報告所需的系統管理員許可權。 若要查看詳細錯誤，請選取錯誤時報告，並檢查% temp%\\DEA 中的記錄。|  
|目前的使用者沒有執行此作業所需的許可權。 請確定您擁有執行追蹤和分析報告的 sysadmin 許可權。|您沒有產生新報告所需的系統管理員（sysadmin）許可權。|  

**問 .. 我無法連接到執行 SQL Server 的電腦**

- 確認執行 SQL Server 的電腦名稱稱是有效的。 若要確認，請使用 SQL Server Management Studio （SSMS）嘗試連接到伺服器。
- 確認您的防火牆設定不會封鎖與執行 SQL Server 之電腦的連線。
- 確認使用者具有必要的使用者權限。

您可以在% temp%\\DEA 的記錄中查看更多詳細資料。 如果問題持續發生，請洽詢產品小組。

**問：我在產生分析報表時看到錯誤**

在安裝 DEA 之後，第一次產生分析報表時，需要存取網際網路。 需要有網際網路存取權，才能下載統計分析所需的套件。

如果在建立報表時發生錯誤，[進度] 頁面會顯示分析產生失敗的特定步驟。 您可以在% temp%\\DEA 的記錄中查看更多詳細資料。 請確認您具有所需使用者權限的有效連接伺服器，然後重試。 如果問題持續發生，請洽詢產品小組。

|可能的錯誤|解決方法|  
|---|---|  
|RInterop 在啟動時遇到錯誤。 請檢查 RInterop 記錄，然後再試一次。|DEA 需要有網際網路存取權，才能下載相依的 R 套件。 檢查% temp%\\RInterop 中的 RInterop 記錄和% temp%\\DEA 中的 DEA 記錄。 如果 RInterop 未正確地初始化，或如果沒有正確的 R 封裝進行初始化，您可能會在 DEA 記錄中的 InitializeRInterop 步驟之後看到「無法產生新的分析報表」例外狀況。<br><br>RInterop 記錄也可能會顯示類似「沒有可用的 jsonlite 套件」的錯誤。 如果您的電腦無法存取網際網路，您可以手動下載必要的 jsonlite R 套件：<br><br><li>移至電腦檔案系統上\\的% userprofile% DEARPackages 資料夾。 此資料夾包含 R 用於 DEA 的封裝。</li><br><li>如果已安裝的套件清單中遺漏 jsonlite 資料夾，您需要具有網際網路存取權的電腦，才能從\_ [https://cran.r-project.org/web/packages/jsonlite/index.html](https://cran.r-project.org/web/packages/jsonlite/index.html)下載 jsonlite 1.4 的發行版本。</li><br><li>將 .zip 檔案複製到您正在執行 DEA 的電腦。  解壓縮 jsonlite 資料夾，並將它複製到% userprofile\\% DEARPackages。 此步驟會自動在 R 中安裝 jsonlite 套件。資料夾應命名為**jsonlite** ，而內容應直接放在資料夾內，而不是以下的一個層級。</li><br><li>關閉 DEA，重新開啟，然後再試一次分析。</li><br>您也可以使用 RGUI.EXE。 移至 [**從 zip 安裝****套件** > ]。 移至您稍早下載的套件並安裝。<br><br>如果 RInterop 已初始化並正確設定，您應該會在 RInterop 記錄檔中看到「正在安裝相依 R 封裝 jsonlite」。|  
|無法連接到 SQL Server 實例，請確定伺服器名稱正確，並檢查是否有登入的使用者所需的存取權。|您可能沒有伺服器的存取權或使用者權限，或伺服器名稱可能不正確。|
|RInterop 進程超時。檢查 DEA 和 RInterop 記錄檔，在 [工作管理員] 中停止 RInterop 進程，然後再試一次。<br><br>或<br><br>RInterop 處於錯誤狀態。 在 [工作管理員] 中停止 RInterop 進程，然後再試一次。|請檢查% temp%\\RInterop 中的記錄檔，以確認錯誤。 請先從 [工作管理員] 中移除 RInterop 進程，然後再試一次。 如果問題持續發生，請洽詢產品小組。|

**問：報表已產生，但資料似乎遺失**

檢查執行 SQL Server 的分析電腦上的資料庫，以確認資料存在。 檢查分析資料庫是否存在，並檢查其資料表。 例如，請檢查下列資料表： TblBatchesA、TblBatchesB 和 TblSummaryStats。

如果資料不存在，則資料可能未正確複製，或資料庫可能已損毀。 如果只有部分資料遺失，則在 [capture] 或 [重新執行] 中建立的追蹤檔案可能不會正確地捕捉您的工作負載。 如果資料位於該處，請檢查% temp%\\DEA 中的記錄檔，以查看是否已記錄任何錯誤。 然後，再試一次以產生分析報告。

有其他問題或意見反應嗎？ 選擇左下角的笑臉圖示，透過 DEA 工具提交意見反應。

## <a name="see-also"></a>另請參閱

- 若要瞭解如何查看分析報表，請參閱[view reports](database-experimentation-assistant-view-report.md)。
