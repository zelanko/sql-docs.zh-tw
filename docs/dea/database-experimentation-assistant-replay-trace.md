---
title: 重新執行 SQL Server 升級之追蹤透過資料庫測試助理
description: 重新執行追蹤，以透過資料庫測試助理
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
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 09c3ffe6897107d2b3db0f53b0fdc895ee437efd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273964"
---
# <a name="replay-a-trace-in-database-experimentation-assistant"></a>重新執行追蹤，以在資料庫測試助理

在 資料庫測試助理 (DEA)，您可以重新執行擷取的追蹤檔案，針對已升級的測試環境。 例如，假設 SQL Server 2008 R2 執行生產工作負載。 必須兩次重新執行追蹤檔案工作負載： 一次上具有相同版本的 SQL Server，在執行生產環境，一次在已經升級的目標 SQL Server 版本，例如 SQL Server 2016 的環境的環境。

> [!NOTE]
> 若要執行此動作，您必須手動設定虛擬機器或實體機器來執行 Distributed Replay 追蹤。 如需詳細資訊，請參閱 < [Distributed Replay controller 和用戶端安裝程式](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/)。
>
>

## <a name="create-a-trace-replay"></a>建立重新執行追蹤

在 DEA，選取 [功能表] 圖示。 在展開的功能表中，選取**重新執行追蹤**旁邊的播放圖示。

![選取功能表中的 重新執行追蹤](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-open.png)

> [!NOTE]
> Distributed Replay 控制器電腦需要遠端連線到您所使用的使用者帳戶的權限。
>

### <a name="grant-access-to-the-distributed-replay-controller"></a>Distributed Replay controller 授與存取權

1. 在命令提示字元中，輸入**dcomcnfg**來開啟**元件服務**介面。
1. 依序展開**Microsoft.biztalk.deployment.deployercomponent** > **電腦** > **我的電腦** > **DCOM 設定** >  **DReplayController**。
1. 以滑鼠右鍵按一下**DReplayController**，然後選取**屬性**。
1. 在 **安全性**索引標籤上，選取**編輯**來新增使用者帳戶。
1. 選取 [確定]。

### <a name="verify-setup"></a>確認設定

1.  **SQL Server 安裝路徑**:若要安裝 SQL Server 中輸入的路徑。 例如，c:\\Program Files (x86)\\Microsoft SQL Server\\120。
1.  **控制器電腦名稱**:輸入已為控制器設定機器的名稱。 這部電腦執行名為 SQL Server Distributed Replay controller 的 Windows 服務。 Distributed Replay controller 會協調 Distributed Replay client 的動作。 每個 Distributed Replay 環境都只能有一個 Controller 執行個體。
1.  **用戶端的電腦名稱**:輸入每個用戶端電腦，並以逗號分隔的名稱。 範例： client1，client2。 您可以有最多五個用戶端控制站。 用戶端會將一或多個機器，不論是實體或虛擬的執行名為 SQL Server Distributed Replay 用戶端的 Windows 服務。 Distributed Replay Client 會共同運作以模擬 SQL Server 執行個體的工作負載。 每個 Distributed Replay 環境中可以有一個或多個用戶端。
1.  選取 **[下一步]**。

### <a name="select-a-trace"></a>選取 [追蹤]

1.  **追蹤檔案的路徑**:輸入輸入的追蹤 (.trc) 檔案的路徑。
1.  **路徑來儲存重新執行前置處理輸出**:  
    \- 如果您還沒有 IRF 檔案，請輸入您想要用來儲存 IRF 檔案的位置的路徑和其他前置處理輸出。  
    \- 如果您已經有 IRF 檔案中，輸入 IRF 檔案的路徑。
1. 選取 **[下一步]**。

### <a name="replay-a-trace"></a>重新執行追蹤

1.  **追蹤檔案名稱**:輸入追蹤檔案名稱。
1.  **最大檔案大小 (MB)**:輸入追蹤檔案換用大小值。 預設值為 200 MB。 您可以輸入自訂值。
1.  **路徑來儲存重新執行追蹤輸出**:輸入輸出.trc 檔案的路徑。
1.  **SQL Server 執行個體名稱**:輸入用來重新執行追蹤的 SQL Server 執行個體的名稱。
1.  選取 [開始]。

如果您輸入的資訊是有效的會啟動 Distributed Replay 程序。 否則，有不正確的資訊文字 boses 會反白顯示紅色。 請確定您輸入的值都正確無誤，然後選取**啟動**。

等候重新執行完成執行，以查看您所指定的位置。 選取底部的左側功能表以監視重新執行進度的鈴鐺圖示。

![重新執行追蹤進度](./media/database-experimentation-assistant-replay-trace/dea-replay-trace-progress.png)

## <a name="frequently-asked-questions-about-trace-replay"></a>重新執行追蹤的相關常見問題的解答

### <a name="what-security-permissions-do-i-need-to-start-a-replay-capture-on-my-target-server"></a>我要在目標伺服器上啟動重新執行擷取安全性權限？

- DEA 應用程式中執行追蹤作業的 Windows 使用者必須具備執行 SQL Server 的目標電腦上的 sysadmin 權限。 這些使用者權限，才能啟動追蹤。
- 執行 SQL Server 的目標電腦執行的服務帳戶必須具有指定的追蹤檔案路徑的寫入權限。
- 用以執行 Distributed Replay Client 服務的服務帳戶必須具有使用者權限來連接到執行 SQL Server 的目標電腦以及執行查詢。

### <a name="can-i-start-more-than-one-replay-in-the-same-session"></a>可以啟動多個重新執行相同工作階段嗎？

是，您可以啟動多個重新執行，並完成相同工作階段時追蹤它們。

### <a name="can-i-start-more-than-one-replay-in-parallel"></a>可以啟動多個重新執行以平行方式？

是，但不是具有相同設定中已選取的機器**控制器，再加上用戶端**。 在控制器和用戶端會很忙碌。 設定一組個別的機器底下**控制器與用戶端**開始平行的重新執行。

### <a name="how-long-does-a-replay-typically-take-to-finish"></a>重新執行通常需要花費多久時間才能完成？

相同數量的來源追蹤時間再加上前置處理來源追蹤所花費的時間量，通常只需要重新執行。 不過，如果控制器已向用戶端機器不足，無法從重新執行管理所產生的負載，重新執行可能需要較長的時間完成。 您可以註冊最多 16 個用戶端電腦與控制器。

### <a name="how-large-do-target-trace-files-get"></a>大目標追蹤檔案會變得？

大小的來源追蹤的目標追蹤檔案可能是介於 5 到 15 倍。 檔案大小根據執行查詢。 比方說，查詢計劃 blob 可能很大。 如果這些查詢的統計資料經常變更，則會擷取更多的事件。

### <a name="why-do-i-need-to-restore-databases"></a>為何需要還原資料庫？

SQL Server 是一個可設定狀態的關聯式資料庫管理系統。 若要正確執行 A / B 測試，資料庫的狀態必須保留在所有的時間。 否則，您可能會看到在查詢中的錯誤，就不會出現在生產環境中的重新執行期間。 若要避免這些錯誤，我們建議您進行備份之前擷取的來源。 同樣地，還原執行 SQL Server 的目標電腦上的備份，才能避免重新執行期間發生錯誤。

### <a name="what-does-pass--on-the-replay-page-mean"></a>什麼會 「 成功 %」 上重新執行頁面平均？

**傳遞 %** 傳遞查詢的百分比表示。 您可以診斷是否在預期的錯誤數目。 可能會預期的錯誤，或可能會發生錯誤，因為資料庫已經失去其完整性。 如果值**pass %** 不不如預期，您可以停止追蹤，並看看 SQL Profiler，以查看哪些查詢不成功的追蹤檔。

### <a name="how-can-i-look-at-the-trace-events-that-were-collected-during-replay"></a>如何查看在重新執行期間所收集的追蹤事件？

開啟目標追蹤檔案，並在 SQL Profiler 中檢視它。 或者，如果您想要修改重新執行擷取時，所有 SQL Server 指令碼都位於 c:\\Program Files (x86)\\Microsoft Corporation\\資料庫測試助理\\的指令碼\\StartReplayCapture.sql。

### <a name="what-trace-events-does-dea-collect-during-replay"></a>在重新執行期間將 DEA 收集在哪些追蹤事件？

DEA 擷取包含與效能相關資訊的追蹤事件。 擷取組態是 StartReplayCaptureTrace.sql 指令碼中。 這些事件是一般的 SQL Server 追蹤事件中所列[sp_trace_setevent & Amp;#40;transact-SQL&AMP;#41; 參考文件](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)。

## <a name="troubleshoot-trace-replay"></a>疑難排解 重新執行追蹤

### <a name="i-cant-connect-to-the-computer-thats-running-sql-server"></a>我無法連線到執行 SQL Server 的電腦

- 確認執行 SQL Server 之電腦的名稱有效。 若要確認，請嘗試使用 SQL Server Management Studio (SSMS) 連接到伺服器。
- 確認防火牆設定不會封鎖連線到執行 SQL Server 的電腦。
- 確認使用者具有必要的使用者權限。
- 確認 Distributed Replay client 服務帳戶具有執行 SQL Server 電腦的存取權。

您可以在記錄中取得更多詳細資料，在 %temp%\\DEA。 如果問題持續發生，請連絡產品小組。

### <a name="i-cant-connect-to-the-distributed-replay-controller"></a>我無法連接至 Distributed Replay controller

- 確認 Distributed Replay controller 服務在控制器電腦上執行。 若要確認，請使用 Distributed Replay 管理工具 (執行命令`dreplay.exe status -f 1`)。
- 如果從遠端啟動重新執行：
  - 確認執行 DEA 的電腦可以成功 ping 控制器。 確認防火牆設定，允許在每個指示的連線**設定重新執行環境**頁面。 如需詳細資訊，請參閱文章[SQL Server Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/sql-server-distributed-replay?view=sql-server-2017)。
  - 請確定 Distributed Replay controller 使用者允許 DCOM 遠端啟動 」 和 「 遠端啟用。
  - 請確定 DCOM 遠端存取使用者的權限會允許 Distributed Replay controller 使用者。

### <a name="the-trace-file-path-exists-on-my-machine-why-cant-distributed-replay-controller-find-it"></a>追蹤檔案路徑存在，我的電腦上。 為什麼無法 Distributed Replay controller 找到它？

Distributed 的 Replay 只能存取本機的磁碟資源。 開始重新執行之前，您必須將來源追蹤檔案複製至 Distributed Replay 控制器電腦中。 此外，您必須提供的路徑上 DEA**新的重新執行**頁面。 

UNC 路徑不相容於 Distributed Replay。 分散式重新執行路徑必須是本機的絕對路徑的第一次的來源追蹤檔案，包括副檔名。

### <a name="why-cant-i-browse-for-files-on-the-new-replay-page"></a>為什麼無法 vyhledat 在新的重新執行 頁面上的檔案？

因為我們無法瀏覽遠端電腦的資料夾，瀏覽檔案，並不實用。 複製並貼上的絕對路徑會更有效率。

### <a name="i-started-replay-with-a-trace-but-distributed-replay-didnt-replay-any-events"></a>我開始重新執行與追蹤，但 Distributed Replay 不重新執行任何事件

因為追蹤檔案可能沒有可重新執行事件，或不具有如何重新執行事件的相關資訊，可能會發生此問題。 請確認提供的追蹤檔案路徑是否為來源追蹤檔案。 來源追蹤檔案會建立使用 StartCaptureTrace.sql 指令碼中提供的組態。

### <a name="i-see-unexpected-error-occurred-when-i-try-to-preprocess-my-trace-files-by-using-the-sql-server-2017-distributed-replay-controller"></a>我看到 「 發生非預期的錯誤 ！ 」 當我嘗試前置我追蹤的檔案處理使用 SQL Server 2017 Distributed Replay controller

此問題稱為在 RTM 版本的 SQL Server 2017。 如需詳細資訊，請參閱 <<c0> [ 未預期的錯誤，當您使用 DReplay 功能來重新執行擷取的追蹤，在 SQL Server 2017](https://support.microsoft.com/help/4045678/fix-unexpected-error-when-you-use-the-dreplay-feature-to-replay-a)。  
  
SQL Server 2017，已在最新的累計更新 1 中處理這個問題。 下載最新版[Cumulative Update 1 for SQL Server 2017](https://support.microsoft.com/help/4038634/cumulative-update-1-for-sql-server-2017)。

## <a name="next-steps"></a>後續步驟

- 若要建立分析報表，可協助您深入了解建議的變更，請參閱[建立報表](database-experimentation-assistant-create-report.md)。

- 如需 19 分鐘簡介 DEA 和示範，觀看下列影片：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
