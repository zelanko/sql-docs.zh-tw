---
title: 重新執行追蹤以進行 SQL Server 升級
description: 瞭解如何使用資料庫測試助理來重新執行已捕捉的追蹤，以進行 SQL Server 升級。
ms.custom: seo-lt-2019
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: pochiraju
ms.author: rajpo
ms.reviewer: mathoma
ms.openlocfilehash: b91385f587668b17bd9cde9f173cebacce48dc91
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489542"
---
# <a name="replay-a-trace-in-database-experimentation-assistant"></a>在資料庫測試助理中重新執行追蹤

在資料庫測試助理 (DEA) 中，您可以針對已升級的測試環境重新執行已捕捉的追蹤檔案。 例如，請考慮在 SQL Server 2008 R2 上執行的生產工作負載。 工作負載的追蹤檔必須重新執行兩次：一次在具有相同 SQL Server 版本的環境中執行，而第二次是在具有升級目標 SQL Server 版本的環境中執行，例如 SQL Server 2016。

> [!NOTE]
> 重新執行追蹤需要您手動設定虛擬機器或實體電腦，以執行 Distributed Replay 追蹤。 如需詳細資訊，請參閱 [設定資料庫測試助理的 Distributed Replay](database-experimentation-assistant-configure-replay.md)。
>

## <a name="configure-a-trace-replay-for-target-1"></a>設定目標1的追蹤重新執行

首先，您需要對目標1執行追蹤重新執行，這代表您現有的生產環境。

1. 在 DEA 的左側導覽列中，選取箭號圖示，然後在 [ **所有** 重新執行] 頁面上，選取 [ **新增** 重新執行]。

    ![在 DEA 中建立重新執行](./media/database-experimentation-assistant-replay-trace/dea-create-replay.png)

    > [!NOTE]
    > Distributed Replay 控制器電腦需要您用來遠端連線的使用者帳戶許可權。

2. 在 [ **新** 的重新執行] 頁面的 [重新執行 **詳細資料**] 下，輸入或選取下列資訊：

    - 重新執行 **名稱**：輸入追蹤重新執行的名稱。
    - **來源追蹤格式**：指定來源追蹤檔案 (追蹤或 XEvents) 的格式。
    - **來源檔案的完整路徑**：指定來源追蹤檔案的完整路徑。 如果使用 DReplay，則檔案必須存在於做為 DReplay 控制器的電腦上，而且使用者帳戶需要存取檔案和資料夾。
    - 重新執行 **工具**：指定重新執行工具 (DReplay 或內建) 。
    - **控制器電腦名稱稱**：指定做為 Distributed Replay 控制器的電腦名稱稱。
    - 重新執行 **追蹤位置**：指定儲存追蹤檔/XEvents 與追蹤重新執行相關聯的路徑。

        > [!NOTE]
        > 針對 Azure SQL Database 或 Azure SQL 受控執行個體，您需要提供 Azure blob 儲存體帳戶的 SAS URI。

3. 選取 [ **是，我已手動還原資料庫 () ]** 核取方塊，以確認您已將資料庫 (s) 還原。

4. 在 [ **SQL Server 連接詳細資料**] 底下，輸入或選取下列資訊：

    - **伺服器類型**：指定 SQL Server (**SqlServer**、 **AzureSqlDb**、 **AzureSqlManagedInstance**) 的類型。
    - **伺服器名稱**：指定 SQL Server 的伺服器名稱或 IP 位址。
    - **驗證類型**：在 [驗證類型] 中，選取 [ **Windows**]。
    - **資料庫名稱**：輸入用來啟動伺服器端追蹤之資料庫的名稱。 如果您未指定資料庫，則會在伺服器上的所有資料庫上捕獲追蹤。

5. 選取或取消選取 [ **加密** 連線] 和 [ **信任伺服器憑證** ] 核取方塊，適用于您的案例。

    ![新的重新執行頁面](./media/database-experimentation-assistant-replay-trace/dea-new-replay.png)

## <a name="start-the-trace-replay-on-target-1"></a>在目標1上啟動追蹤重新執行

- 當您輸入或選取所需的資訊之後，請選取 [ **開始** ] 以起始追蹤重新執行。

  如果您輸入的資訊是有效的，則會啟動 Distributed Replay 進程。 否則，會以紅色反白顯示包含不正確資訊的文字方塊。 請確定您輸入的值正確無誤，然後選取 [ **啟動**]。

  ![針對目標1的重新執行進度](./media/database-experimentation-assistant-replay-trace/dea-run-replay-target1.png)

  您可以視需要監視流程。 當重新執行執行完成時，DEA 會將結果儲存在您指定位置的檔案中。

  ![完成目標1的重新執行](./media/database-experimentation-assistant-replay-trace/dea-replay-target1-complete.png)

## <a name="perform-the-trace-replay-against-target-2"></a>針對目標2執行追蹤重新執行

當您完成對目標1執行追蹤重新執行作業之後，您必須針對第二個目標執行相同動作，這表示預定的升級環境。

1. 設定追蹤重新執行，這次使用與您的目標2環境相關的詳細資料。
2. 在目標2上啟動追蹤重新執行。

   您可以視需要監視流程。 當重新執行執行完成時，DEA 會將結果儲存在您指定位置的檔案中。

## <a name="frequently-asked-questions-about-trace-replay"></a>追蹤重新執行的常見問題

**問：我需要哪些安全性許可權才能在目標伺服器上啟動重新執行捕獲？**

- 在 DEA 應用程式中執行追蹤作業的 Windows 使用者，必須具有執行 SQL Server 之目的電腦上的 sysadmin 許可權。 需要這些使用者權限才能啟動追蹤。
- 執行 SQL Server 的目的電腦所用的服務帳戶，必須具有所指定追蹤檔案路徑的寫入權限。
- 執行 Distributed Replay 用戶端服務的服務帳戶必須具有使用者權限，才能連接到執行 SQL Server 的目的電腦，以及執行查詢。

**問：我可以在同一個會話中啟動多個重新執行嗎？**

是的，您可以啟動多個重新開機，並在相同的會話中追蹤它們完成。

**問：我可以平行方式啟動一個以上的重新執行嗎？**

是，但不是使用 **控制器 Plus 用戶端** 中選取的同一組電腦。 控制器和用戶端將會忙碌。 在 [ **控制器 Plus 用戶端** ] 下設定一組不同的電腦，以啟動平行重新執行。

**問：重新執行通常需要多久的時間才能完成？**

重新執行通常會花費與來源追蹤相同的時間量加上前置處理來源追蹤所需的時間量。 但是，如果向控制器註冊的用戶端電腦不足以管理重新執行所產生的負載，則重新執行可能需要較長的時間才能完成。 您最多可以向控制器註冊16部用戶端電腦。

**問：目標追蹤檔案有多大？**

目標追蹤檔案的大小可介於來源追蹤的5到15倍之間。 檔案大小是以執行的查詢數目為基礎。 例如，查詢計劃 blob 可能很大。 如果這些查詢的統計資料經常變更，則會捕捉更多事件。

**問：為什麼需要還原資料庫？**

SQL Server 是具狀態的關係資料庫管理系統。 若要適當地執行 A/B 測試，必須隨時保留資料庫的狀態。 否則，您可能會在重新執行期間，看到不會出現在生產環境中的錯誤。 若要避免這些錯誤，建議您在來源抓取之前進行備份。 同樣地，您必須在執行 SQL Server 的目的電腦上還原備份，以防止在重新執行期間發生錯誤。

**問：「重新執行」頁面上的「傳遞%」是什麼意思？**

**Pass%** 表示只有經過的查詢百分比。 您可以診斷是否有預期的錯誤數目。 可能會發生錯誤，或可能因為資料庫遺失其完整性而發生錯誤。 如果 **pass%** 的值不是您預期的值，您可以停止追蹤並查看 SQL Profiler 中的追蹤檔案，以查看哪些查詢不成功。

**問：如何查看重新執行期間所收集的追蹤事件？**

開啟目標追蹤檔案，並在 SQL Profiler 中加以查看。 或者，如果您想要修改重新執行捕捉，則所有 SQL Server 腳本都可以在 C： \\ Program Files (x86) \\ Microsoft Corporation 資料庫測試助理 script \\ \\ \\ StartReplayCapture 中取得。

**問：在重新執行期間，DEA 會收集哪些追蹤事件？**

DEA 會捕捉包含效能相關資訊的追蹤事件。 Capture 設定位於 StartReplayCaptureTrace .sql 腳本中。 這些事件是 [sp_trace_setevent (transact-sql) 參考檔](../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)中所列的一般 SQL Server 追蹤事件。

## <a name="troubleshoot-trace-replay"></a>針對追蹤重新執行進行疑難排解

**問：為什麼我無法連接到執行 SQL Server 的電腦？**

- 確認執行 SQL Server 的電腦名稱稱有效。 若要確認，請使用 SQL Server Management Studio (SSMS) 來嘗試連接到伺服器。
- 確認防火牆設定不會封鎖與執行 SQL Server 之電腦的連線。
- 確認使用者具有必要的使用者權限。
- 確認 Distributed Replay 用戶端的服務帳戶具有執行 SQL Server 之電腦的存取權。

您可以在% temp% DEA 的記錄中取得更多詳細資料 \\ 。 如果問題持續發生，請洽詢產品團隊。

**問：為什麼我無法連接到 Distributed Replay 控制器？**

- 確認控制器電腦上正在執行 Distributed Replay 控制器服務。 若要確認，請使用 Distributed Replay 管理工具 (執行命令 `dreplay.exe status -f 1`) 。
- 如果從遠端啟動重新執行：
  - 確認執行 DEA 的電腦可以成功 ping 控制器。 確認 [設定重新執行 **環境** ] 頁面上的 [防火牆設定允許每個指示的連接]。 如需詳細資訊，請參閱 [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md)的文章。
  - 請確定 Distributed Replay 控制器的使用者可以使用 DCOM 遠端啟動和遠端啟用。
  - 請確定 Distributed Replay 控制器的使用者可以使用 DCOM 遠端存取使用者權限。

**問：追蹤檔案路徑存在於我的電腦上。為什麼無法 Distributed Replay 控制器找到它？**

Distributed Replay 只能存取本機磁片資源。 在開始重新執行之前，您必須先將來源追蹤檔案複製到 Distributed Replay 控制器電腦。 此外，您必須在 [DEA **新** 的重新執行] 頁面上提供路徑。

UNC 路徑與 Distributed Replay 不相容。 Distributed Replay 路徑必須是本機的路徑，也就是第一個來源追蹤檔案的絕對路徑，包括副檔名。

**問：為什麼無法在新的重新執行頁面上流覽檔案？**

因為無法流覽遠端電腦上的資料夾，所以流覽檔案並不實用。 複製並貼上絕對路徑會更有效率。

**問：我已開始使用追蹤重新執行，但 Distributed Replay 不會重新執行任何事件。為什麼？**

發生此問題的原因可能是追蹤檔案沒有可重新事件，或有關于如何重新執行事件的資訊。 確認所提供的追蹤檔案路徑是否指向來源追蹤檔案。 來源追蹤檔案是使用 StartCaptureTrace 中提供的設定來建立。

**問：當我嘗試使用 SQL Server 2017 Distributed Replay 控制器來前置處理追蹤檔時，我看到「發生意外的錯誤！」。為什麼？**

此問題在 RTM 版的 SQL Server 2017 中是已知的。 如需詳細資訊，請參閱在 [SQL Server 2017 中使用 DReplay 功能重新執行已捕捉的追蹤時發生非預期的錯誤](https://support.microsoft.com/help/4045678/fix-unexpected-error-when-you-use-the-dreplay-feature-to-replay-a)。  
  
SQL Server 2017 的最新累計更新1中已解決此問題。 下載 [SQL Server 2017 的累計更新 1](https://support.microsoft.com/help/4038634/cumulative-update-1-for-sql-server-2017)最新版本。

## <a name="see-also"></a>另請參閱

- 若要建立分析報表以協助您深入瞭解建議的變更，請參閱 [建立報表](database-experimentation-assistant-create-report.md)。
