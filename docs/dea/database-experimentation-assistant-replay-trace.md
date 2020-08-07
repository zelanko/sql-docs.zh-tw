---
title: 重新執行 SQL Server 升級的追蹤
description: 瞭解如何使用資料庫測試助理來重新執行已捕獲的追蹤，以進行 SQL Server 升級。
ms.custom: seo-lt-2019
ms.date: 12/12/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: rajsell
ms.reviewer: mathoma
ms.openlocfilehash: ae88f4473414e83a2ffbddee5c47fa40c552115a
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823363"
---
# <a name="replay-a-trace-in-database-experimentation-assistant"></a>在資料庫測試助理中重新執行追蹤

在資料庫測試助理 (DEA) 中，您可以針對已升級的測試環境重新執行已捕獲的追蹤檔案。 例如，請考慮在 SQL Server 2008 R2 上執行的生產工作負載。 工作負載的追蹤檔案必須重新執行兩次：一次在生產環境中執行的相同版本 SQL Server，而第二次在具有升級目標 SQL Server 版本的環境上，例如 SQL Server 2016。

> [!NOTE]
> 重新執行追蹤時，您必須手動設定虛擬機器或實體電腦 Distributed Replay 追蹤。 如需詳細資訊，請參閱[Configure Distributed Replay for 資料庫測試助理](database-experimentation-assistant-configure-replay.md)。
>

## <a name="configure-a-trace-replay-for-target-1"></a>設定目標1的追蹤重新執行

首先，您必須針對目標1執行追蹤重新執行，這代表您現有的生產環境。

1. 在 DEA 的左側導覽列上，選取箭號圖示，然後在 [**所有**重新執行] 頁面上，選取 [**新增**重新執行]。

    ![在 DEA 中建立重新執行](./media/database-experimentation-assistant-replay-trace/dea-create-replay.png)

    > [!NOTE]
    > Distributed Replay 控制器電腦需要您用來遠端連線之使用者帳戶的許可權。

2. 在 [**新增**重新執行] 頁面的 [重新執行**詳細資料**] 下，輸入或選取下列資訊：

    - 重新執行**名稱**：輸入追蹤重新執行的名稱。
    - **來源追蹤格式**：指定來源追蹤檔案 (追蹤或 XEvents) 的格式。
    - **來源檔案的完整路徑**：指定來源追蹤檔案的完整路徑。 如果使用 DReplay，檔案必須存在於作為 DReplay 控制器的電腦上，而且使用者帳戶需要存取檔案和資料夾。
    - 重新執行**工具**：指定 (DReplay 或內建) 的重新執行工具。
    - **控制器電腦名稱稱**：指定做為 Distributed Replay 控制器的電腦名稱稱。
    - 重新執行**追蹤位置**：指定路徑來儲存與追蹤重新執行相關聯的追蹤檔案/XEvents。

        > [!NOTE]
        > 針對 Azure SQL Database 或 Azure SQL 受控執行個體，您必須提供 Azure blob 儲存體帳戶的 SAS URI。

3. 選取 [**是，我已手動還原資料庫 () ]** 核取方塊，確認您已 (s) 還原資料庫。

4. 在 [ **SQL Server 連接詳細資料**] 下，輸入或選取下列資訊：

    - **伺服器類型**：指定 SQL Server (**SqlServer**、 **AzureSqlDb**、 **AzureSqlManagedInstance**) 的類型。
    - **伺服器名稱**：指定 SQL Server 的伺服器名稱或 IP 位址。
    - **驗證類型**：針對 [驗證類型]，選取 [ **Windows**]。
    - **資料庫名稱**：輸入要在其上啟動伺服器端追蹤之資料庫的名稱。 如果您未指定資料庫，則會在伺服器上的所有資料庫上捕捉追蹤。

5. 根據您的案例，選取或取消選取 [**加密連接**] 和 [**信任伺服器憑證**] 核取方塊。

    ![新增重新執行頁面](./media/database-experimentation-assistant-replay-trace/dea-new-replay.png)

## <a name="start-the-trace-replay-on-target-1"></a>在目標1上啟動追蹤重新執行

- 在您輸入或選取所需的資訊之後，請選取 [**啟動**] 以起始追蹤重新執行。

  如果您輸入的資訊有效，就會啟動 Distributed Replay 進程。 否則，含有不正確資訊的文字方塊會以紅色反白顯示。 請確定您輸入的值正確無誤，然後選取 [**啟動**]。

  ![針對目標1的重新執行進度](./media/database-experimentation-assistant-replay-trace/dea-run-replay-target1.png)

  您可以視需要監視進程。 當重新執行完成執行時，DEA 會將結果儲存在您指定之位置的檔案中。

  ![針對目標1的重新執行完成](./media/database-experimentation-assistant-replay-trace/dea-replay-target1-complete.png)

## <a name="perform-the-trace-replay-against-target-2"></a>針對目標2執行追蹤重新執行

當您完成針對目標1執行追蹤重新執行之後，您必須針對第二個目標（代表預定的升級環境）執行相同的動作。

1. 設定追蹤重新執行，這次使用與您的目標2環境相關聯的詳細資料。
2. 在目標2上啟動追蹤重新執行。

   您可以視需要監視進程。 當重新執行完成執行時，DEA 會將結果儲存在您指定之位置的檔案中。

## <a name="frequently-asked-questions-about-trace-replay"></a>關於追蹤重新執行的常見問題

**問：我需要哪些安全性許可權才能在我的目標伺服器上啟動重新執行 capture？**

- 在 DEA 應用程式中執行追蹤作業的 Windows 使用者，在執行 SQL Server 的目的電腦上，必須具備 sysadmin 許可權。 需要這些使用者權限才能啟動追蹤。
- 執行 SQL Server 的目的電腦所用的服務帳戶，必須具有指定之追蹤檔案路徑的寫入權限。
- 執行 Distributed Replay 用戶端服務所用的服務帳戶必須具有使用者權限，才能連接到執行 SQL Server 的目的電腦，以及執行查詢。

**問：我可以在同一個會話中啟動多個重新執行嗎？**

是，您可以開始多次重新執行，並在相同的會話中追蹤完成。

**問：我可以平行啟動多個重新執行嗎？**

是，但不是在 [**控制器] 和 [用戶端**] 中選取的一組相同電腦。 控制器和用戶端將會忙碌。 在**控制器加上用戶端**底下設定一組不同的電腦，以啟動平行重新執行。

**問：重新執行通常需要多久的時間才能完成？**

重新執行通常會耗用與來源追蹤相同的時間量，加上前置處理來源追蹤所需的時間量。 不過，如果向控制器註冊的用戶端電腦不足以管理從重新執行產生的負載，則重新執行可能需要較長的時間才能完成。 您最多可以向控制器註冊16部用戶端電腦。

**問：目標追蹤檔案有多大？**

目標追蹤檔案可以介於來源追蹤大小的5到15倍之間。 檔案大小是根據執行的查詢數目而定。 例如，查詢計劃 blob 可能會很大。 如果這些查詢的統計資料經常變更，則會捕捉更多事件。

**問：為什麼我需要還原資料庫？**

SQL Server 是可設定狀態的關係資料庫管理系統。 若要正確執行 A/B 測試，必須隨時保留資料庫的狀態。 否則，您可能會在不會出現在生產環境中的重新執行期間，看到查詢發生錯誤。 若要避免這些錯誤，建議您在來源捕獲之前進行備份。 同樣地，您必須在執行 SQL Server 的目的電腦上還原備份，才能在重新執行期間避免發生錯誤。

**問：「重新執行」頁面上的「pass%」是什麼意思？**

**Pass%** 表示只傳遞了一個百分比的查詢。 您可以診斷是否預期發生錯誤數目。 可能是預期的錯誤，或錯誤可能是因為資料庫遺失其完整性所造成。 如果 [**傳遞%** ] 的值不是您所預期，您可以停止追蹤，並查看 SQL Profiler 中的追蹤檔案，以查看哪些查詢不成功。

**問：如何查看重新執行期間所收集的追蹤事件？**

開啟目標追蹤檔案，並在 SQL Profiler 中加以查看。 或者，如果您想要修改重新執行捕獲，所有的 SQL Server 腳本都可以在 C： \\ Program Files (x86) \\ Microsoft Corporation \\ 資料庫測試助理 \\ 腳本 \\ StartReplayCapture 中取得。

**問： DEA 會在重新執行時收集哪些追蹤事件？**

DEA 會捕捉包含效能相關資訊的追蹤事件。 Capture 設定位於 StartReplayCaptureTrace 腳本中。 這些事件是[sp_trace_setevent (transact-sql) 參考檔](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)中所列的一般 SQL Server 追蹤事件。

## <a name="troubleshoot-trace-replay"></a>針對追蹤重新執行進行疑難排解

**問：為什麼我無法連接到執行 SQL Server 的電腦？**

- 確認執行 SQL Server 的電腦名稱稱是有效的。 若要確認，請使用 SQL Server Management Studio (SSMS) 嘗試連接到伺服器。
- 確認防火牆設定不會封鎖與執行 SQL Server 之電腦的連線。
- 確認使用者具有必要的使用者權限。
- 確認 Distributed Replay 用戶端的服務帳戶可以存取執行 SQL Server 的電腦。

您可以在% temp% DEA 的記錄檔中取得更多詳細資料 \\ 。 如果問題持續發生，請洽詢產品小組。

**問：為什麼我無法連接到 Distributed Replay 控制器？**

- 確認 Distributed Replay 控制器服務正在控制器機器上執行。 若要確認，請使用 Distributed Replay 管理工具 (執行命令 `dreplay.exe status -f 1`) 。
- 如果從遠端啟動重新執行：
  - 確認執行 DEA 的電腦可以順利 ping 控制器。 根據 [設定重新執行**環境**] 頁面上的指示，確認防火牆設定是否允許連線。 如需詳細資訊，請參閱[SQL Server Distributed Replay](https://docs.microsoft.com/sql/tools/distributed-replay/sql-server-distributed-replay?view=sql-server-2017)文章。
  - 請確定 Distributed Replay 控制器的使用者可以使用 DCOM 遠端啟動和遠端啟用。
  - 請確定 Distributed Replay 控制器的使用者可以使用 DCOM 遠端存取使用者權限。

**問：追蹤檔案路徑存在於我的電腦上。為什麼無法 Distributed Replay 控制器找到它？**

Distributed Replay 只能存取本機磁片資源。 您必須先將來源追蹤檔案複製到 Distributed Replay 控制器電腦，才能開始重新執行。 此外，您必須在 [DEA**新**的重新執行] 頁面上提供路徑。

UNC 路徑與 Distributed Replay 不相容。 Distributed Replay 路徑必須是第一個來源追蹤檔案的本機絕對路徑，包括副檔名。

**問：為什麼我無法在新的重新執行頁面上流覽檔案？**

因為我們無法流覽遠端電腦上的資料夾，所以流覽檔案並不實用。 複製並貼上絕對路徑會更有效率。

**問：我已開始使用追蹤重新執行，但 Distributed Replay 不會重新執行任何事件。因此?**

發生此問題的原因可能是追蹤檔案沒有可重新事件或具有如何重新執行事件的相關資訊。 確認所提供的追蹤檔案路徑是否指向來源追蹤檔案。 來源追蹤檔案是使用 StartCaptureTrace 腳本中提供的設定來建立的。

**問：我在嘗試使用 SQL Server 2017 Distributed Replay 控制器來前置處理追蹤檔案時看到「發生未預期的錯誤！」。因此?**

這個問題在 RTM 版本的 SQL Server 2017 中是已知的。 如需詳細資訊，請參閱[當您使用 DReplay 功能在 SQL Server 2017 中重新執行已捕捉的追蹤時，發生未預期的錯誤](https://support.microsoft.com/help/4045678/fix-unexpected-error-when-you-use-the-dreplay-feature-to-replay-a)。  
  
SQL Server 2017 的最新累計更新1已解決此問題。 下載最新版本的[累計更新1（適用于 SQL Server 2017](https://support.microsoft.com/help/4038634/cumulative-update-1-for-sql-server-2017)）。

## <a name="see-also"></a>另請參閱

- 若要建立可協助您取得所提議變更見解的分析報表，請參閱[建立報表](database-experimentation-assistant-create-report.md)。
