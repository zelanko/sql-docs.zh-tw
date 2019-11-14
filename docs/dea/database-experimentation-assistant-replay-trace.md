---
title: 重新執行 SQL Server 升級的追蹤
description: 使用資料庫測試助理 SQL Server 升級重新執行追蹤
ms.custom: seo-lt-2019
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
ms.openlocfilehash: b1607aefdc8495f374b2586b0b896f20e87f62d1
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056701"
---
# <a name="replay-a-trace-in-database-experimentation-assistant"></a>在資料庫測試助理中重新執行追蹤

在資料庫測試助理（DEA）中，您可以針對已升級的測試環境重新執行已捕獲的追蹤檔案。 例如，請考慮在 SQL Server 2008 R2 上執行的生產工作負載。 工作負載的追蹤檔案必須重新執行兩次：一次在具有相同版本之 SQL Server 的環境中執行，而且在具有升級目標 SQL Server 版本的環境上，如 SQL Server 2016。

> [!NOTE]
> 若要執行此動作，您必須手動設定虛擬機器或實體機器，以執行 Distributed Replay 追蹤。 如需詳細資訊，請參閱[Distributed Replay 控制器和用戶端設定](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/)。
>
>

## <a name="create-a-trace-replay"></a>建立追蹤重新執行

在 [DEA] 中，選取功能表圖示。 在展開的功能表中，選取 [播放] 圖示旁的 [重新執行**追蹤**]。

![選取功能表中的 [重新執行追蹤]](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-open.png)

> [!NOTE]
> Distributed Replay 控制器電腦需要您用來遠端存取許可權的使用者帳戶。
>

### <a name="grant-access-to-the-distributed-replay-controller"></a>授與 Distributed Replay 控制器的存取權

1. 在命令提示字元中，輸入**dcomcnfg.exe**以開啟 [**元件服務**] 介面。
1. 展開 **元件服務** >  > **我的電腦** > **DCOM Config** > **DReplayController**的**電腦**。
1. 以滑鼠右鍵按一下 [ **DReplayController**]，然後選取 [**屬性**]。
1. 在 [**安全性**] 索引標籤上，選取 [**編輯**] 以新增使用者帳戶。
1. 選取 [確定]。

### <a name="verify-setup"></a>驗證設定

1.  **SQL Server 安裝路徑**：輸入 SQL Server 安裝所在的路徑。 例如，C：\\Program Files （x86）\\Microsoft SQL Server\\120。
1.  **控制器電腦名稱稱**：輸入已設定為控制器的電腦名稱稱。 這部電腦正在執行名為 SQL Server Distributed Replay 控制器的 Windows 服務。 Distributed Replay 控制器會協調 Distributed Replay 用戶端的動作。 每個 Distributed Replay 環境都只能有一個 Controller 執行個體。
1.  **用戶端電腦名稱稱**：輸入每部用戶端電腦的名稱，並以逗號分隔。 範例： client1、client2。 您最多可以有五個用戶端控制器。 用戶端是一部或多部執行 Windows 服務的電腦（實體或虛擬），SQL Server Distributed Replay 用戶端。 Distributed Replay Client 會共同運作以模擬 SQL Server 執行個體的工作負載。 每個 Distributed Replay 環境中可以有一個或多個用戶端。
1.  選取 **[下一步]** 。

### <a name="select-a-trace"></a>選取追蹤

1.  **追蹤**檔案的路徑：輸入輸入追蹤（. .trc）檔案的路徑。
1.  儲存重新執行前置處理**輸出的路徑**：  
    \- 如果您還沒有 IRF 檔案，請輸入您要儲存 IRF 檔案和其他前置處理輸出位置的路徑。  
    \- 如果您已經有 IRF 檔案，請輸入 IRF 檔案的路徑。
1. 選取 **[下一步]** 。

### <a name="replay-a-trace"></a>重新執行追蹤

1.  **追蹤檔案名**：輸入追蹤檔名稱。
1.  檔案**大小上限（MB）** ：輸入追蹤檔案變換大小的值。 預設值為 200 MB。 您可以輸入自訂值。
1.  **儲存重新執行追蹤輸出的路徑**：輸入 .trc 檔案的路徑。
1.  **SQL Server 實例名稱**：輸入要重新執行追蹤之 SQL Server 實例的名稱。
1.  選取 [開始]。

如果您輸入的資訊有效，就會啟動 Distributed Replay 進程。 否則，含有不正確資訊的文字 boses 會以紅色反白顯示。 請確定您輸入的值正確無誤，然後選取 [**啟動**]。

等待重新執行完成，以查看您指定的位置。 選取左側功能表底部的 [鐘] 圖示，以監視重新執行進度。

![重新執行追蹤進度](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-progress.png)

## <a name="frequently-asked-questions-about-trace-replay"></a>關於追蹤重新執行的常見問題

### <a name="what-security-permissions-do-i-need-to-start-a-replay-capture-on-my-target-server"></a>我需要哪些安全性許可權才能在我的目標伺服器上啟動重新執行 capture？

- 在 DEA 應用程式中執行追蹤作業的 Windows 使用者，在執行 SQL Server 的目的電腦上，必須具備 sysadmin 許可權。 需要這些使用者權限才能啟動追蹤。
- 執行 SQL Server 的目的電腦所用的服務帳戶，必須具有指定之追蹤檔案路徑的寫入權限。
- 執行 Distributed Replay 用戶端服務所用的服務帳戶必須具有使用者權限，才能連接到執行 SQL Server 的目的電腦，以及執行查詢。

### <a name="can-i-start-more-than-one-replay-in-the-same-session"></a>我可以在同一個會話中啟動多個重新執行嗎？

是，您可以開始多次重新執行，並在相同的會話中追蹤完成。

### <a name="can-i-start-more-than-one-replay-in-parallel"></a>我可以平行啟動多個重新執行嗎？

是，但不是在 [**控制器] 和 [用戶端**] 中選取的一組相同電腦。 控制器和用戶端將會忙碌。 在**控制器加上用戶端**底下設定一組不同的電腦，以啟動平行重新執行。

### <a name="how-long-does-a-replay-typically-take-to-finish"></a>重新執行通常需要多久的時間才能完成？

重新執行通常會耗用與來源追蹤相同的時間量，加上前置處理來源追蹤所需的時間量。 不過，如果向控制器註冊的用戶端電腦不足以管理從重新執行產生的負載，則重新執行可能需要較長的時間才能完成。 您最多可以向控制器註冊16部用戶端電腦。

### <a name="how-large-do-target-trace-files-get"></a>目標追蹤檔案的取得大小為何？

目標追蹤檔案的來源追蹤大小可能介於5到15倍之間。 檔案大小是根據執行的查詢數目而定。 例如，查詢計劃 blob 可能會很大。 如果這些查詢的統計資料經常變更，則會捕捉更多事件。

### <a name="why-do-i-need-to-restore-databases"></a>為什麼需要還原資料庫？

SQL Server 是可設定狀態的關係資料庫管理系統。 若要正確執行 A/B 測試，必須隨時保留資料庫的狀態。 否則，您可能會在不會出現在生產環境中的重新執行期間，看到查詢發生錯誤。 若要避免這些錯誤，建議您在來源捕獲之前進行備份。 同樣地，您必須在執行 SQL Server 的目的電腦上還原備份，才能在重新執行期間避免發生錯誤。

### <a name="what-does-pass--on-the-replay-page-mean"></a>「重新執行」頁面上的「pass%」是什麼意思？

**Pass%** 表示只傳遞了一個百分比的查詢。 您可以診斷是否預期發生錯誤數目。 可能是預期的錯誤，或錯誤可能是因為資料庫遺失其完整性所造成。 如果 [**傳遞%** ] 的值不是您所預期，您可以停止追蹤，並查看 SQL Profiler 中的追蹤檔案，以查看哪些查詢不成功。

### <a name="how-can-i-look-at-the-trace-events-that-were-collected-during-replay"></a>如何查看重新執行期間所收集的追蹤事件？

開啟目標追蹤檔案，並在 SQL Profiler 中加以查看。 或者，如果您想要修改重新執行捕捉，所有 SQL Server 腳本都可以在 C：\\Program Files （x86）\\Microsoft Corporation\\資料庫測試助理\\腳本\\StartReplayCapture 中取得。

### <a name="what-trace-events-does-dea-collect-during-replay"></a>DEA 會在重新執行時收集哪些追蹤事件？

DEA 會捕捉包含效能相關資訊的追蹤事件。 Capture 設定位於 StartReplayCaptureTrace 腳本中。 這些事件是[sp_trace_setevent （transact-sql）參考檔](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)中所列的一般 SQL Server 追蹤事件。

## <a name="troubleshoot-trace-replay"></a>針對追蹤重新執行進行疑難排解

### <a name="i-cant-connect-to-the-computer-thats-running-sql-server"></a>我無法連接到執行 SQL Server 的電腦

- 確認執行 SQL Server 的電腦名稱稱是有效的。 若要確認，請使用 SQL Server Management Studio （SSMS）嘗試連接到伺服器。
- 確認防火牆設定不會封鎖與執行 SQL Server 之電腦的連線。
- 確認使用者具有必要的使用者權限。
- 確認 Distributed Replay 用戶端的服務帳戶可以存取執行 SQL Server 的電腦。

您可以在% temp%\\DEA 的記錄中取得更多詳細資料。 如果問題持續發生，請洽詢產品小組。

### <a name="i-cant-connect-to-the-distributed-replay-controller"></a>我無法連接到 Distributed Replay 控制器

- 確認 Distributed Replay 控制器服務正在控制器機器上執行。 若要確認，請使用 Distributed Replay 管理工具（執行 `dreplay.exe status -f 1`的命令）。
- 如果從遠端啟動重新執行：
  - 確認執行 DEA 的電腦可以成功 ping 控制器。 根據 [設定重新執行**環境**] 頁面上的指示，確認防火牆設定是否允許連線。 如需詳細資訊，請參閱[SQL Server Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/sql-server-distributed-replay?view=sql-server-2017)文章。
  - 請確定 Distributed Replay 控制器的使用者可以使用 DCOM 遠端啟動和遠端啟用。
  - 請確定 Distributed Replay 控制器的使用者可以使用 DCOM 遠端存取使用者權限。

### <a name="the-trace-file-path-exists-on-my-machine-why-cant-distributed-replay-controller-find-it"></a>追蹤檔案路徑存在於我的電腦上。 為什麼無法 Distributed Replay 控制器找到它？

Distributed Replay 只能存取本機磁片資源。 您必須先將來源追蹤檔案複製到 Distributed Replay 控制器電腦，才能開始重新執行。 此外，您必須在 [DEA**新**的重新執行] 頁面上提供路徑。 

UNC 路徑與 Distributed Replay 不相容。 Distributed Replay 路徑必須是第一個來源追蹤檔案的本機絕對路徑，包括副檔名。

### <a name="why-cant-i-browse-for-files-on-the-new-replay-page"></a>為什麼我無法在新的重新執行頁面上流覽檔案？

因為我們無法流覽遠端電腦的資料夾，所以流覽檔案並不實用。 複製和貼上絕對路徑會更有效率。

### <a name="i-started-replay-with-a-trace-but-distributed-replay-didnt-replay-any-events"></a>我開始以追蹤重新執行，但 Distributed Replay 不會重新執行任何事件

發生此問題的原因可能是追蹤檔案沒有可重新事件，或是沒有如何重新執行事件的相關資訊。 確認所提供的追蹤檔案路徑是否為來源追蹤檔案。 來源追蹤檔案是使用 StartCaptureTrace 腳本中提供的設定來建立的。

### <a name="i-see-unexpected-error-occurred-when-i-try-to-preprocess-my-trace-files-by-using-the-sql-server-2017-distributed-replay-controller"></a>我看到「發生未預期的錯誤！」 當我嘗試使用 SQL Server 2017 Distributed Replay 控制器來前置處理追蹤檔案時

這個問題在 RTM 版本的 SQL Server 2017 中是已知的。 如需詳細資訊，請參閱[當您使用 DReplay 功能在 SQL Server 2017 中重新執行已捕捉的追蹤時，發生未預期的錯誤](https://support.microsoft.com/help/4045678/fix-unexpected-error-when-you-use-the-dreplay-feature-to-replay-a)。  
  
SQL Server 2017 的最新累計更新1已解決此問題。 下載最新版本的[累計更新1（適用于 SQL Server 2017](https://support.microsoft.com/help/4038634/cumulative-update-1-for-sql-server-2017)）。

## <a name="next-steps"></a>後續的步驟

- 若要建立可協助您取得所提議變更見解的分析報表，請參閱[建立報表](database-experimentation-assistant-create-report.md)。

- 如需 DEA 和示範的19分鐘簡介，請觀看下列影片：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
