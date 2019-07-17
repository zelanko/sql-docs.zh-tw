---
title: 擷取 SQL Server 升級資料庫測試助理 」 裡的追蹤
description: 擷取追蹤資料庫測試助理
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
ms.openlocfilehash: ab361c4e83ae5e2b2bb6614bdc4a513e0bdd77ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058998"
---
# <a name="capture-a-trace-in-database-experimentation-assistant"></a>擷取追蹤資料庫測試助理

您可以使用追蹤擷取的資料庫測試助理 (DEA)，來建立追蹤檔案中，已擷取的伺服器事件記錄檔。 擷取的伺服器事件是在特定時間週期內特定伺服器發生的事件。 追蹤擷取必須執行每一部伺服器的一次。

在開始追蹤擷取之前，請務必先備份所有的目標資料庫。

SQL Server 中的查詢快取可能會影響評估結果。 我們建議您重新啟動 SQL Server 服務 (MSSQLSERVER) 中的服務應用程式，以改善評估結果的一致性。

## <a name="create-a-trace-capture"></a>建立追蹤擷取

1. 在 DEA，選取左側功能表中的功能表圖示。 在展開的功能表中，選取**擷取追蹤**相機圖示旁邊。

    ![在功能表中選取擷取的追蹤](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-capture.png)

1. 底下**新擷取**、 輸入或選取下列資訊：

    - **SQL Server 執行個體名稱**:輸入執行您想要擷取伺服器追蹤在其的 SQL Server 之電腦的名稱。
    - **資料庫名稱**:輸入要啟動資料庫追蹤資料庫的名稱。 如果您未指定資料庫，則會將追蹤擷取的伺服器上的所有資料庫。
    - **追蹤檔案名稱**:輸入您擷取的追蹤檔案的名稱。
    - **最大檔案大小 (MB)** :選取的換用檔案。 視需要在您選取的檔案大小，會建立新的檔案。 建議的換用大小為 200 MB。
    - **持續時間 （分鐘）** :選取您想要追蹤擷取執行的時間 （以分鐘為單位） 的長度。
    - **若要儲存輸出追蹤檔的路徑**:選取 追蹤檔案的目的地路徑。 

    > [!NOTE]
    > 追蹤檔案的檔案路徑必須是執行 SQL Server 的電腦上。 如果 SQL Server 服務未設定特定帳戶，服務可能需要寫入權限可寫入的追蹤檔案指定的資料夾。
    >
    >

    ![新的 [擷取] 頁面](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-inputs.png)

## <a name="start-the-trace-capture"></a>啟動追蹤擷取

您輸入或選取所需的資訊之後，請選取**啟動**若要開始擷取追蹤。 如果您輸入的資訊是有效的便會開始追蹤擷取程序。 否則，有無效的項目文字方塊中會反白顯示紅色。 

請確定您已選取或輸入的值都正確無誤，然後選取**啟動**。

追蹤擷取完成時執行，將新的追蹤檔案置於您在中指定的檔案位置**路徑來儲存輸出追蹤檔**。 選取鈴鐺圖示來監視進度，擷取的左側功能表的底部。

![擷取追蹤進度](./media/database-experimentation-assistant-capture-trace/dea-capture-trace-progress.png)

### <a name="trace-file"></a>追蹤檔案

追蹤擷取寫出.trc 檔案中指定的位置。 追蹤檔案包含 SQL Server 資料庫的活動的追蹤結果。 TRC 檔案專為提供詳細資訊，偵測到 SQL Server 所報告的錯誤。

## <a name="frequently-asked-questions-about-trace-capture"></a>追蹤擷取的相關常見問題的解答

以下是一些常見問題 DEA 中追蹤擷取的相關。

### <a name="what-events-are-captured-when-i-run-a-trace-capture-on-a-production-database"></a>我在生產資料庫上執行的追蹤擷取時，會擷取哪些事件？

下表提供的事件和對應的資料行資料，我們會收集追蹤的清單：
  
|事件名稱|文字資料 (1)|二進位資料 (2)|資料庫識別碼 (3)|主機名稱 (8)|應用程式名稱 (10)|登入名稱 (11)|SPID (12)|開始時間 (14)|結束時間 (15)|資料庫名稱 (35)|事件序列 (51)|IsSystem (60)|  
|---|---|---|---|---|---|---|---|---|---|---|---|---|  
|**RPC： 完成 (10)**||*|*|*|*|*|*|*|*|*|*|*|  
|**RPC： 啟動 (11)**||*|*|*|*|*|*|*||*|*|*|  
|**RPC Output Parameter (100)**|*||*|*|*|*|*|*||*|*|*|  
|**Sql: batchcompleted (12)**|*||*|*|*|*|*|*|*|*|*|*|  
|**Sql: batchstarting (13)**|*||*|*|*|*|*|*||*|*|*|  
|**稽核登入 (14)**|*|*|*|*|*|*|*|*||*|*|*|  
|**Audit Logout (15)**|*||*|*|*|*|*|*|*|*|*|*|  
|**ExistingConnection (17)**|*|*|*|*|*|*|*|*||*|*|*|  
|**CursorOpen (53)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorPrepare (70)**|*||*|*|*|*|*|*||*|*|*|  
|**Prepare SQL (71)**|||*|*|*|*|*|*||*|*|*|  
|**Exec Prepared SQL (72)**|||*|*|*|*|*|*||*|*|*|  
|**CursorExecute (74)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorUnprepare (77)**|*||*|*|*|*|*|*||*|*|*|  
|**CursorClose (78)**|*||*|*|*|*|*|*||*|*|*|  

### <a name="is-there-a-performance-effect-on-my-production-server-when-trace-capture-is-running"></a>是否有影響我的實際執行伺服器的效能時追蹤擷取正在執行？
    
是，在追蹤收集期間沒有最少的效能影響。 在我們的測試，我們會發現有關 3%的記憶體不足的壓力。
    
### <a name="what-kind-of-permissions-are-required-for-capturing-traces-on-a-production-workload"></a>需要擷取追蹤，在生產環境工作負載上的何種權限？
    
- DEA 應用程式中執行追蹤作業的 Windows 使用者必須在執行 SQL Server 的電腦上具備 sysadmin 權限。
- 使用執行 SQL Server 的電腦上的服務帳戶必須具有指定的追蹤檔案路徑的寫入權限。

### <a name="can-i-capture-traces-for-the-entire-server-or-only-on-a-single-database"></a>我是否可以擷取追蹤整個伺服器，或只在單一資料庫？
    
您可以使用 DEA 擷取伺服器中的所有資料庫或單一資料庫的追蹤。
    
### <a name="i-have-a-linked-server-configured-in-my-production-environment-do-those-queries-show-up-in-the-traces"></a>我有連結的伺服器，在我的生產環境中設定。 這些查詢顯示在追蹤中？
    
如果您執行整個伺服器的追蹤擷取，則追蹤會擷取所有的查詢，包括連結的伺服器查詢。 若要執行整個伺服器的追蹤擷取，離開**資料庫名稱**下方**新擷取**空白。
    
### <a name="whats-the-minimum-recommended-time-for-production-workload-traces"></a>生產工作負載追蹤的最小的建議的時間為何？
    
我們建議您選擇最能代表您的工作負載的全部內容一次。 如此一來，在您的工作負載中的所有查詢會執行分析。
    
### <a name="how-important-is-to-take-a-database-backup-right-before-i-start-a-trace-capture"></a>重要性是進行資料庫備份正確，之後再開始追蹤擷取？
    
在開始追蹤擷取之前，請務必先備份您的所有目標資料庫。 目標 1 和目標 2 中擷取的追蹤是重新執行。 如果資料庫狀態不相同，則不準實驗的結果。

### <a name="can-i-collect-xevents-instead-of-traces-and-can-i-replay-xevents"></a>可以收集 XEvents 而不是追蹤，並可以重新執行 XEvents 嗎？
    
是的。 DEA 支援 Xevent。 下載最新版的 DEA，試試看。

## <a name="troubleshoot-trace-captures"></a>疑難排解追蹤擷取

如果當您執行的追蹤擷取時，您會看到錯誤，請檢閱下列先決條件：

- 確認執行 SQL Server 之電腦的名稱有效。 若要確認，請嘗試連線到使用 SQL Server Management Studio (SSMS) 執行 SQL Server 的電腦。
- 請確認您的防火牆設定不會封鎖連線到執行 SQL Server 的電腦。
- 確認使用者有部落格文章中所列的權限[Replay 常見問題集](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-replay-faq/)。
- 確認 追蹤名稱並未遵循標準的換用慣例 (擷取\_1)。 相反地，請嘗試追蹤的名稱，例如擷取\_1A 或 Capture1。

以下是一些您可能會看到可能的錯誤和解決問題的解決方案：

|可能的錯誤|方案|  
|---|---|  
|無法啟動目標 SQL Server 上的追蹤檢查是否有必要的權限和 SQL Server 帳戶具有寫入權限，Sql Error Code (53) 之指定的追蹤檔案路徑|執行 DEA 工具的使用者必須具有執行 SQL Server 電腦的存取權。 使用者必須被指派為 sysadmin 角色。|  
|無法啟動目標 SQL Server 上的追蹤檢查是否有必要的權限和 SQL Server 帳戶具有寫入權限，Sql Error Code (19062) 之指定的追蹤檔案路徑|指定的追蹤路徑可能不存在，或資料夾沒有寫入權限帳戶下的 SQL Server 服務正在執行 （例如，網路服務）。 路徑必須存在，而且必須具有要啟動追蹤的必要權限。|  
|DEA 追蹤目前在目標伺服器上執行。|作用中的追蹤已在目標伺服器上執行。 當伺服器範圍追蹤已在執行時，您無法啟動新的追蹤。|  
|無法開啟要求的資料庫擷取追蹤。 此錯誤可能不正確的資料庫名稱。|指定的資料庫不存在，或無法存取目前的使用者。 使用正確的資料庫名稱。|  

如果您看到標示為 任何其他錯誤*Sql 錯誤碼*，請參閱[系統錯誤訊息](https://docs.microsoft.com/previous-versions/sql/sql-server-2008-r2/cc645603(v=sql.105))詳細的描述和解決方式。
    
## <a name="next-steps"></a>後續步驟

- 若要了解如何設定 SQL Server 中的 Distributed Replay 的工具，重新執行擷取的追蹤之前，請參閱[設定重新執行](database-experimentation-assistant-configure-replay.md)。

- 如需 19 分鐘簡介 DEA 和示範，觀看下列影片：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
