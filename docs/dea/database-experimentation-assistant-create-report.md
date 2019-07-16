---
title: 在 資料庫測試助理建立分析報告，SQL Server 升級
description: 建立分析報告中資料庫測試助理
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
ms.openlocfilehash: d53d8734e0c01fa2056b9d560f3bc65b7f64d9a9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058959"
---
# <a name="create-analysis-reports-in-database-experimentation-assistant"></a>建立分析報告中資料庫測試助理

重新執行來源追蹤這兩個目標伺服器上的之後，您可以產生分析報告中資料庫測試助理 (DEA)。 分析報表可協助您深入了解建議變更的效能含意。

## <a name="create-an-analysis-report"></a>建立分析報表

在 DEA，選取 [功能表] 圖示。 在展開的功能表中，選取**分析報表**檢查清單圖示旁邊。

![分析 功能表](./media/database-experimentation-assistant-create-report/dea-create-reports-menu.png)

底下**分析報表**，選取**新的分析報告**。

![新的分析報告功能表](./media/database-experimentation-assistant-create-report/dea-create-reports-new-report.png)

輸入或選取下列資訊：

- **報表名稱**:輸入報表的名稱。 會使用的報表名稱的 A 和 B 的資料庫。 範例*A （或 B）*  + *報表名稱* + *唯一識別項*。 
- **伺服器名稱**︰輸入您想要納入的在伺服器電腦的名稱 B 和分析資料庫。
- **SQL Server 執行個體名稱**:輸入要用於報表的 SQL Server 執行個體的名稱。
- **來源伺服器的追蹤**:輸入 SQL Server (2008 R2) 的第一個追蹤 (.trc) 檔案。
- **目標伺服器的追蹤**:輸入目標 SQL Server (2014) 第一個.trc 檔案。

![新的分析報表頁面](./media/database-experimentation-assistant-create-report/dea-create-reports-inputs.png)

## <a name="generate-a-report"></a>產生報告

您輸入或選取所需的資訊，在後**新的分析報告**頁面上，選取**開始**開始建立報表。 如果您輸入的資訊是有效的則會建立 [分析] 報表。 否則，有無效的資訊的文字方塊會反白顯示紅色。 請確定您輸入正確的值，然後選取**啟動**。 

會產生新的分析報告。 分析資料庫遵循的命名配置分析 +*使用者指定的報表名稱* + *唯一識別項*。

## <a name="frequently-asked-questions-about-analysis-reports"></a>分析報表的相關的常見問題集

### <a name="what-does-my-analysis-report-tell-me"></a>我的分析報告告訴我哪些資訊？
    
DEA 會使用統計檢定來分析您的工作負載，並判斷如何每個查詢已執行目標 1 從目標 2。 它會提供每個查詢的效能詳細資料。 深入了解在 DEA[開始](database-experimentation-assistant-get-started.md)。
    
### <a name="can-i-create-a-new-analysis-report-while-another-report-is-being-generated"></a>另一份報表會在產生時可以建立新的分析報表嗎？
    
資料分割  目前，只有一個報表可以產生以防止發生衝突，一次。 不過，您可以執行一個以上的擷取，並重新執行一次。

### <a name="i-upgraded-dea-to-version-20-can-i-still-view-and-use-my-old-reports"></a>DEA 升級到 2.0 版。 我仍然檢視及使用我的舊報表嗎？
    
是的。 若要檢視先前產生的報表，您必須更新報表的結構描述。 如需詳細資訊，請參閱[DEA 2.0:更新資料庫結構描述中 DEA 分析報表的](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-updating-db-schema-for-analysis-report-in-the-database-experimentation-assistant/)。
    
### <a name="can-i-generate-an-analysis-report-by-using-the-command-prompt"></a>可以使用命令提示字元產生分析報告嗎？
    
是的。 您可以產生分析報告，在命令提示字元。 您接著可以在 UI 中檢視報表。 如需詳細資訊，請參閱 <<c0> [ 命令提示字元執行](database-experimentation-assistant-run-command-prompt.md)。
    
## <a name="troubleshoot-analysis-reports"></a>疑難排解分析報表

###  <a name="what-security-permissions-do-i-need-to-generate-and-view-an-analysis-report-on-my-server"></a>我需要產生，並在 我的伺服器上檢視分析報告安全性權限？
    
DEA 來登入的使用者必須具有 analysis server 的 sysadmin 權限。 如果使用者屬於群組的一部分，請確定群組具有 sysadmin 權限。

|可能的錯誤|方案|  
|---|---|  
|無法連接到資料庫。 請確定您具備 sysadmin 權限，來分析及檢視報表。|您可能沒有存取權或系統管理員權限的伺服器或資料庫。 確認您的登入權限，並再試一次。|  
|無法產生**報表名稱**伺服器上**伺服器名稱**。 如需詳細資訊，請**報表名稱**報表。|您可能沒有 sysadmin 權限，才能產生新的報表。 若要查看詳細的錯誤，請選取錯誤放大報表，然後檢查 %temp%中的記錄檔\\DEA。|  
|目前的使用者沒有執行作業的必要權限。 請確定您有適用於執行追蹤及分析報表的 sysadmin 權限。|您不需要產生新的報表所需的系統管理員權限。|  

### <a name="i-cant-connect-to-the-computer-running-sql-server"></a>我無法連線到執行 SQL Server 的電腦
    
- 確認執行 SQL Server 之電腦的名稱有效。 若要確認，請嘗試使用 SQL Server Management Studio (SSMS) 連接到伺服器。
- 請確認您的防火牆設定不會封鎖連線到執行 SQL Server 的電腦。
- 確認使用者具有必要的使用者權限。 

您可以看到在 %temp%中的記錄檔中的更多詳細資料\\DEA。 如果問題持續發生，請連絡產品小組。

### <a name="i-see-an-error-when-i-generate-an-analysis-report"></a>我看到錯誤時產生的分析報表
    
網際網路存取才第一次您安裝 DEA 之後產生分析報告。 若要下載所需的統計分析的封裝需要網際網路存取。

如果建立報表時，就會發生錯誤，[進度] 頁面會顯示特定的分析產生失敗的步驟。 您可以看到在 %temp%中的記錄檔中的更多詳細資料\\DEA。 請確認您已使用必要的使用者權限，伺服器的有效連接，並再試一次。 如果問題持續發生，請連絡產品小組。

|可能的錯誤|方案|  
|---|---|  
|RInterop 叫用在啟動時發生。 檢查 RInterop 記錄檔，並再試一次。|DEA 需要存取網際網路才能下載相依的 R 套件。 檢查 RInterop 記錄在 %temp%\\RInterop 和 DEA 記錄在 %temp%\\DEA。 如果 RInterop 未正確初始化，或者它初始化不正確的 R 封裝，您可能會看到 「 無法產生新的分析報告 」 的例外狀況之後 DEA 記錄檔的 InitializeRInterop 步驟。<br><br>RInterop 記錄也可能會顯示錯誤類似於 「 有 」 沒有 jsonlite 套件可用。 如果您的電腦沒有網際網路存取，您可以手動下載必要的 jsonlite R 套件：<br><br><li>移至 %userprofile%\\DEARPackages 機器的檔案系統上的資料夾。 此資料夾包含用於 DEA R 套件。</li><br><li>在已安裝的套件清單中遺漏 jsonlite 資料夾時，您需要有網際網路存取才可下載 jsonlite 的發行版本的電腦\_從 1.4.zip [ https://cran.r-project.org/web/packages/jsonlite/index.html ](https://cran.r-project.org/web/packages/jsonlite/index.html)。</li><br><li>將.zip 檔案複製到您要在其中執行 DEA 的機器。  擷取 jsonlite 資料夾，並將它複製到 %userprofile%\\DEARPackages。 此步驟會自動安裝 jsonlite 封裝此資料夾應該命名**jsonlite**且內容應直接在資料夾中，未在一個層級。</li><br><li>一次關閉 DEA，再重新開啟，請嘗試分析。</li><br>您也可以使用 RGUI。 移至**封裝** > **從 zip 安裝**。 請移至您稍早下載的封裝，並安裝。<br><br>如果 RInterop 已初始化且已正確設定，您應該會看到 「 正在安裝相依 R 封裝 jsonlite"RInterop 記錄檔中。|  
|無法連接到 SQL Server 執行個體，請確定伺服器名稱正確無誤，並檢查使用者已登入的必要存取權。|您可能沒有存取權，或使用者權限給伺服器或伺服器名稱可能不正確。| 
|RInterop 程序已逾時。請檢查 DEA 和 RInterop 記錄、 停止 RInterop 程序在 [工作管理員] 中，並再試一次。<br><br>或<br><br>RInterop 處於錯誤狀態。 停止 RInterop 程序在 [工作管理員] 中，並再試一次。|請參閱記錄檔在 %temp%\\RInterop 確認錯誤。 移除 RInterop 程序從 工作管理員才能再試一次。 如果問題持續發生，請連絡產品小組。| 

### <a name="the-report-is-generated-but-data-appears-to-be-missing"></a>產生報告時，但資料似乎遺失
    
檢查執行 SQL Server，以確認資料存在的分析電腦上的資料庫。 分析資料庫的存在並檢查其資料表。 例如，檢查這些資料表：TblBatchesA、 TblBatchesB 和 TblSummaryStats。

如果不存在的資料，資料可能不正確複製，或資料庫可能已損毀。 如果只有部分資料遺失，或追蹤檔建立中擷取重新執行可能會無法擷取您的工作負載準確地。 如果有資料，請檢查 %temp%中的記錄檔\\DEA 查看如果記錄任何錯誤。 然後，再試一次產生分析報表。

更多的問題或意見反應嗎？ 選擇左下角的笑臉圖示，以提交意見反應，透過 DEA 工具。  

## <a name="next-steps"></a>後續步驟

- 若要了解如何檢視 [分析] 報表，請參閱[檢視報表](database-experimentation-assistant-view-report.md)。

- 如需 19 分鐘簡介 DEA 和示範，觀看下列影片：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
