---
title: 捕捉 SQL Server 升級的追蹤
description: SQL Server 升級的資料庫測試助理中捕捉追蹤
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
ms.openlocfilehash: 999fd3f6caca13ecd768a9560915c53c732af27c
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258528"
---
# <a name="capture-a-trace-in-database-experimentation-assistant"></a>在資料庫測試助理中捕捉追蹤

您可以使用資料庫測試助理（DEA）來建立含有已捕捉的伺服器事件記錄檔的追蹤檔案。 「已捕捉的伺服器事件」是在特定時間週期內，于特定伺服器上發生的事件。 每一部伺服器必須執行一次追蹤捕捉。

開始追蹤捕捉之前，請確定您已備份所有目標資料庫。

SQL Server 中的查詢快取可能會影響評估結果。 我們建議您重新開機服務應用程式中的 SQL Server 服務（MSSQLSERVER），以改善評估結果的一致性。

## <a name="configure-a-trace-capture"></a>設定追蹤捕獲

1. 在 DEA 的左側導覽列上，選取相機圖示，然後在 [**所有捕捉**] 頁面上，選取 [**新增 Capture**]。

    ![在 DEA 中建立 capture](./media/database-experimentation-assistant-capture-trace/dea-initiate-capture.png)

2. 在 [**新增捕捉**] 頁面的 [ **Capture details**] 底下，輸入或選取下列資訊：

    - **Capture name**：輸入您的 capture 追蹤檔的名稱。
    - **格式**：指定 capture 的格式（Trace 或 XEvents）。
    - **持續時間**：選取您想要執行追蹤捕捉的時間長度（以分鐘為單位）。
    - [**捕捉位置**]：選取追蹤檔案的目的地路徑。

        > [!NOTE]
        > 追蹤檔案的檔案路徑必須在執行 SQL Server 的電腦上。 如果未針對特定帳戶設定 SQL Server 服務，則服務可能需要寫入指定資料夾的寫入權限，才能撰寫追蹤檔案。

3. 選取 [**是，我已手動取得備份 ...]，** 確認您已建立備份 .。。 核取方塊。

4. 在 [ **Capture details**] 底下，輸入或選取下列資訊：

    - **伺服器類型**：指定 SQL Server 的類型（**SqlServer**、 **AzureSqlDb**、 **AzureSqlManagedInstance**）。
    - **伺服器名稱**：指定 SQL Server 的伺服器名稱或 IP 位址。
    - **驗證類型**：針對 [驗證類型]，選取 [ **Windows**]。
    - **資料庫名稱**：輸入要在其上啟動資料庫追蹤之資料庫的名稱。 如果您未指定資料庫，則會在伺服器上的所有資料庫上捕捉追蹤。

5. 根據您的案例，選取或取消選取 [**加密連接**] 和 [**信任伺服器憑證**] 核取方塊。

    ![新增捕捉頁](./media/database-experimentation-assistant-capture-trace/dea-new-capture.png)

## <a name="start-the-trace-capture"></a>啟動追蹤捕獲

1. 在您輸入或選取所需的資訊之後，請選取 [**啟動**] 以起始追蹤捕捉。

    如果您輸入的資訊有效，就會開始追蹤 capture 進程。 否則，含有無效專案的文字方塊會以紅色反白顯示。 如果您遇到錯誤，請更正所有必要的專案，然後再次選取 [**啟動**]。

    當追蹤捕獲正在執行時，在 [ **capture details**] 底下，會顯示追蹤捕捉處理常式的狀態和進度。

    ![監視捕捉進度](./media/database-experimentation-assistant-capture-trace/dea-capture-running.png)

2. 當追蹤捕獲完成執行時，新的追蹤（. .trc）檔案會儲存在您在初始設定期間所指定的**capture 位置**。

    ![已完成追蹤捕獲](./media/database-experimentation-assistant-capture-trace/dea-capture-complete.png)

    追蹤檔案包含 SQL Server 資料庫活動的追蹤結果。 .trc 檔案的設計目的，是為了提供有關 SQL Server 偵測到並回報之錯誤的詳細資訊。

## <a name="frequently-asked-questions-about-trace-capture"></a>關於追蹤捕捉的常見問題

以下是 DEA 中的追蹤捕捉的一些常見問題。

**問：當我在生產資料庫上執行追蹤捕捉時，會捕捉哪些事件？**

下表列出 DEA 為追蹤收集的事件和對應的資料行資料：
  
|活動名稱|文字資料（1）|二進位資料（2）|資料庫識別碼（3）|主機名稱（8）|應用程式名稱（10）|登入名稱（11）|SPID （12）|開始時間（14）|結束時間（15）|資料庫名稱（35）|事件順序（51）|IsSystem （60）|  
|---|---|---|---|---|---|---|---|---|---|---|---|---|  
|**RPC：已完成（10）**||*|*|*|*|*|*|*|*|*|*|*|  
|**RPC：啟動（11）**||*|*|*|*|*|*|*||*|*|*|  
|**RPC 輸出參數（100）**|*||*|*|*|*|*|*||*|*|*|  
|**SQL： BatchCompleted （12）**|*||*|*|*|*|*|*|*|*|*|*|  
|**SQL： BatchStarting （13）**|*||*|*|*|*|*|*||*|*|*|  
|**Audit Login （14）**|*|*|*|*|*|*|*|*||*|*|*|  
|**Audit 登出（15）**|*||*|*|*|*|*|*|*|*|*|*|  
|**ExistingConnection （17）**|*|*|*|*|*|*|*|*||*|*|*|  
|**CursorOpen （53）**|*||*|*|*|*|*|*||*|*|*|  
|**CursorPrepare （70）**|*||*|*|*|*|*|*||*|*|*|  
|**準備 SQL （71）**|||*|*|*|*|*|*||*|*|*|  
|**Exec 備妥的 SQL （72）**|||*|*|*|*|*|*||*|*|*|  
|**CursorExecute （74）**|*||*|*|*|*|*|*||*|*|*|  
|**CursorUnprepare （77）**|*||*|*|*|*|*|*||*|*|*|  
|**CursorClose （78）**|*||*|*|*|*|*|*||*|*|*|  

**問：當追蹤捕獲正在執行時，我的生產伺服器是否會有效能影響？**

是，在追蹤收集期間，效能會有最小的影響。 在我們的測試中，我們發現大約有3% 的記憶體壓力。

**問：在生產工作負載上捕獲追蹤需要何種許可權？**

- 在 DEA 應用程式中執行追蹤作業的 Windows 使用者，必須在執行 SQL Server 的電腦上具有 sysadmin 許可權。
- 在執行 SQL Server 的電腦上所使用的服務帳戶，必須具有指定之追蹤檔案路徑的寫入權限。

**問：我可以為整個伺服器，還是只能在單一資料庫上捕捉追蹤？**

您可以使用 DEA 來為伺服器中的所有資料庫或單一資料庫，捕獲追蹤。

**問：我已在生產環境中設定連結伺服器。這些查詢是否會顯示在追蹤中？**

如果您正在執行整部伺服器的追蹤捕捉，追蹤就會捕捉所有查詢，包括連結的伺服器查詢。 若要執行整部伺服器的追蹤捕捉，請將 [**新的 capture** ] 底下的 [**資料庫名稱**] 方塊保留空白。

**問：生產工作負載追蹤的最低建議時間為何？**

我們建議您選擇最能代表整個工作負載的時間。 如此一來，分析就會在您工作負載中的所有查詢上執行。

**問：在開始追蹤捕捉之前，要採用資料庫備份的重要性為何？**

開始追蹤捕捉之前，請確定您已備份所有目標資料庫。 會重新執行目標1和目標2中的已捕獲追蹤。 如果資料庫狀態不相同，實驗的結果會扭曲。

**問：我可以收集 XEvents 而不是追蹤，我可以重新執行 XEvents 嗎？**

可以。 DEA 支援 XEvents。 下載最新版本的 DEA，並試試看。

## <a name="troubleshoot-trace-captures"></a>疑難排解追蹤捕獲

如果您在執行追蹤捕捉時看到錯誤，請確認：

- 執行 SQL Server 的電腦名稱稱是有效的。 若要確認，請使用 SQL Server Management Studio （SSMS）嘗試連接到執行 SQL Server 的電腦。
- 您的防火牆設定不會封鎖與執行 SQL Server 之電腦的連線。
- 使用者具有 [blog 張貼重新執行][常見問題](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-replay-faq/)中所列的許可權。
- 追蹤名稱不會遵循標準變換慣例（Capture\_1）。 相反地，請嘗試追蹤名稱\_，例如 Capture 1A 或 Capture1。

以下是您可能會看到的一些可能的錯誤，以及解決這些問題的解決方案：

|可能的錯誤|方案|  
|---|---|  
|無法在目標 SQL Server 上啟動追蹤，請檢查您是否擁有必要的許可權，以及 SQL Server 帳戶是否具有指定之追蹤檔案路徑的寫入權限 Sql 錯誤碼（53）|執行 DEA 工具的使用者必須具有執行 SQL Server 之電腦的存取權。 必須將系統管理員（sysadmin）角色指派給使用者。|  
|無法在目標 SQL Server 上啟動追蹤，請檢查您是否擁有必要的許可權，以及 SQL Server 帳戶是否具有指定之追蹤檔案路徑的寫入權限 Sql 錯誤碼（19062）|指定的追蹤路徑可能不存在，或資料夾沒有執行 SQL Server 服務之帳戶的寫入權限（例如 NETWORK SERVICE）。 路徑必須存在，而且必須具有啟動追蹤所需的許可權。|  
|目前正在目標伺服器上執行的 DEA 追蹤。|目標伺服器上已有作用中的追蹤正在執行。 當伺服器範圍的追蹤已在執行時，您無法啟動新的追蹤。|  
|無法開啟要求的資料庫來捕捉追蹤。 此錯誤可能是因為資料庫名稱不正確所造成。|指定的資料庫不存在，或目前的使用者無法存取。 請使用正確的資料庫名稱。|  

如果您看到標示為 *[Sql 錯誤碼*] 的其他任何錯誤，請參閱[資料庫引擎錯誤](https://docs.microsoft.com/sql/relational-databases/errors-events/database-engine-events-and-errors)以取得詳細說明。

## <a name="see-also"></a>另請參閱

- 若要瞭解如何在重新執行已捕捉的追蹤之前，先在 SQL Server 中設定 Distributed Replay 工具，請參閱[設定資料庫測試助理的 Distributed Replay](database-experimentation-assistant-configure-replay.md)。
