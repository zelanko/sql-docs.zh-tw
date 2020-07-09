---
title: 尋找具有異動複寫的錯誤
description: 描述如何找出並識別異動複寫的錯誤，以及解決複寫問題的疑難排解方法。
ms.custom: seo-lt-2019
ms.date: 07/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: d7c818e48c916a8ad3da7dfda7eaad6230c16ebd
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882281"
---
# <a name="troubleshooter-find-errors-with-sql-server-transactional-replication"></a>疑難排解員：尋找 SQL Server 異動複寫的錯誤 
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

若對異動複寫的運作方式沒有基本的了解，針對複寫錯誤進行疑難排解可能會令人感到沮喪。 建立發行集的第一個步驟是讓快照集代理程式建立快照集，並將它儲存到快照集資料夾。 接下來，散發代理程式會將快照集套用到訂閱者。 

此處理序會建立發行集，並將它置於「同步處理」  狀態。 同步處理將分成三個階段進行：
1. 交易將在複寫的物件上發生，且在交易記錄中會標示為「供複寫」。 
2. 記錄讀取器代理程式會掃描交易記錄，並尋找標示為「供複寫」的交易。 接著，這些交易會儲存到散發資料庫。 
3. 散發代理程式會使用讀取器執行緒來掃描散發資料庫。 接著，此代理程式會使用寫入器執行緒連線至訂閱者，將這些變更套用到該訂閱者。

此處理序的任何步驟都可能會發生錯誤。 尋找這些錯誤可能是同步處理問題疑難排解中最具挑戰性的層面。 幸好使用複寫監視器可簡化此處理序。 

>[!NOTE]
> - 本疑難排解指南旨在教導疑難排解方法。 它的設計目的不是解決您的特定錯誤，而是提供尋找複寫錯誤的一般指導方針。 提供了一些特定範例，但它們的解決方法可能會因環境而有所不同。 
> - 本指南提供作為範例的錯誤是根據[設定異動複寫](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md)教學課程。



## <a name="troubleshooting-methodology"></a>疑難排解方法 

### <a name="questions-to-ask"></a>要詢問的問題
1. 在同步處理過程中的哪個位置複寫失敗？
2. 哪個代理程式發生錯誤？
1. 上次複寫成功執行是什麼時候？ 自那時起有任何變更嗎？  

### <a name="steps-to-take"></a>需採取的步驟
1. 使用複寫監視器來找出複寫發生錯誤的時間點 (哪個代理程式？)：
   - 如果在**發行者到散發者**區段中發生錯誤，則問題出自記錄讀取器代理程式。 
   - 如果在**散發者到訂閱者**區段中發生錯誤，則問題出自散發代理程式。  
2. 查看該代理程式在 [作業活動監視器] 中的作業記錄，以找出錯誤的詳細資料。 如果作業記錄未顯示足夠的詳細資料，您可以在該特定代理程式上[啟用詳細資訊記錄](#enable-verbose-logging-on-any-agent)。
3. 嘗試判斷適用於該錯誤的解決方案。


## <a name="find-errors-with-the-snapshot-agent"></a>尋找快照集代理程式的錯誤
快照集代理程式會產生快照集，並將它寫入至指定的快照集資料夾。 

1. 檢視快照集代理程式的狀態：

    a. 在 [物件總管] 中，展開 [複寫]  下的 [本機發行集]  節點。

    b. 以滑鼠右鍵按一下您的發行集 **AdvWorksProductTrans** > [檢視快照集代理程式的狀態]  。 

    ![捷徑功能表上的 [檢視快照集代理程式的狀態] 命令](media/troubleshooting-tran-repl-errors/view-snapshot-agent-status.png)

1. 如果快照集代理程式狀態回報錯誤，您可在快照集代理程式的作業記錄中找到更多詳細資料：

    a. 展開 [物件總管] 中的 [SQL Server Agent]  ，然後開啟 [作業活動監視器]。 

    b. 依據 [分類]  排序，並依分類 **REPL-Snapshot** 找出快照集代理程式。

    c. 以滑鼠右鍵按一下快照集代理程式，然後選取 [檢視記錄]  。 

   ![開啟快照集代理程式記錄的選取項目](media/troubleshooting-tran-repl-errors/snapshot-agent-history.png)
    
1. 在快照集代理程式記錄中，選取相關的記錄項目。 這通常是報告該錯誤之項目「前」  的一兩行。 (紅色 X 表示錯誤。)請檢閱記錄下方方塊中的訊息文字： 

    ![存取遭拒的快照集代理程式錯誤](media/troubleshooting-tran-repl-errors/snapshot-access-denied.png)

    ```console
    The replication agent had encountered an exception.
    Exception Message: Access to path '\\node1\repldata.....' is denied.
    ```

如果您未正確設定快照集資料夾的 Windows 權限，您會看到快照集代理程式發生「拒絕存取」錯誤。 您必須驗證快照集儲存所在之資料夾的權限，並確定用來執行快照集代理程式的帳戶具有存取該共用的權限。  

## <a name="find-errors-with-the-log-reader-agent"></a>尋找記錄讀取器代理程式的錯誤
記錄讀取器代理程式會連線到您的發行者資料庫，並掃描交易記錄是否有標示為「供複寫」的任何交易。 接著它會將這些交易新增至散發資料庫。 

1.  連線至 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的發行者。 展開伺服器節點，再以滑鼠右鍵按一下 [複寫]  資料夾，然後選取 [啟動複寫監視器]  ：  

    ![快顯功能表上的 [啟動複寫監視器] 命令](media/troubleshooting-tran-repl-errors/launch-repl-monitor.png)
  
    [複寫監視器] 隨即開啟：![複寫監視器](media/troubleshooting-tran-repl-errors/repl-monitor.png) 
   
2. 紅色 X 表示發行集未執行同步處理。 展開左側的 [我的發行者]  ，再展開相關的發行者伺服器。  
  
3.  在左側選取 **AdvWorksProductTrans** 發行集，然後在其中一個索引標籤中尋找紅色 X，以找出問題所在。 在本例中，紅色 X 出現在 [代理程式]  索引標籤上，因此其中一個代理程式發生錯誤： 

    ![[代理程式] 索引標籤上的紅色 X](media/troubleshooting-tran-repl-errors/agent-error.png)

4. 選取 [代理程式]  索引標籤以找出發生錯誤的代理程式： 

    ![失敗的記錄讀取器代理程式上的紅色 X](media/troubleshooting-tran-repl-errors/log-reader-agent-failure.png)


5. 此檢視會向您顯示兩個代理程式：快照集代理程式和記錄讀取器代理程式。 發生錯誤的代理程式會有一個紅色 X。在此情況下，它是記錄讀取器代理程式。 

    在報告錯誤的行上按兩下，以開啟記錄讀取器代理程式的代理程式記錄。 此記錄會提供有關錯誤的詳細資訊： 
    
    ![記錄讀取器代理程式的錯誤詳細資料](media/troubleshooting-tran-repl-errors/log-reader-error.png)

    ```console
    Status: 0, code: 20011, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.
    The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.
    Status: 0, code: 15517, text: 'Cannot execute as the database principal because the principal "dbo" does not exist, this type of principal cannot be impersonated, or you do not have permission.'.
    Status: 0, code: 22037, text: 'The process could not execute 'sp_replcmds' on 'NODE1\SQL2016'.'.        
    ```

6. 若未正確設定發行者資料庫的擁有者，通常會發生這個錯誤。 還原資料庫時也可能會發生此錯誤。 若要驗證這一點，請：

    a. 在 [物件總管] 中展開 [資料庫]  。

    b. 以滑鼠右鍵按一下 **AdventureWorks2012** > [屬性]  。 

    c. 確認擁有者位在 [檔案]  頁面之下。 如果此方塊為空白，這可能就是問題的原因。 

   ![資料庫屬性中的 [檔案] 頁面，其中的 [擁有者] 方塊為空白](media/troubleshooting-tran-repl-errors/db-properties.png)

7. 如果 [檔案]  頁面上的擁有者為空白，請在 AdventureWorks2012 資料庫的內容中開啟 [新增查詢]  視窗。 執行下列 T-SQL 程式碼：

    ```sql
    -- set the owner of the database to 'sa' or a specific user account, without the brackets. 
    EXECUTE sp_changedbowner '<useraccount>'
    -- example for sa: exec sp_changedbowner 'sa'
    -- example for user account: exec sp_changedbowner 'sqlrepro\administrator' 
    ```

8. 您可能需要重新啟動記錄讀取器代理程式：

    a. 展開 [物件總管] 的 [SQL Server Agent]  節點，然後開啟 [作業活動監視器]。

    b. 依據 [分類]  排序，並依 **REPL-LogReader** 分類找出記錄讀取器代理程式。 

    c. 以滑鼠右鍵按一下 [記錄讀取器代理程式]  作業，然後選取 [從下列步驟啟動作業]  。 

    ![要重新啟動記錄讀取器代理程式的選取項目](media/troubleshooting-tran-repl-errors/start-job-at-step.png)

9. 再次開啟複寫監視器，以驗證您的發行集現在正執行同步處理。 如果它尚未開啟，只要以滑鼠右鍵按一下 [物件總管] 中的 [複寫]  即可找到它。 
10. 依序選取 **AdvWorksProductTrans** 發行集和 [代理程式]  索引標籤，並按兩下選取記錄讀取器代理程式來開啟代理程式記錄。 您現在應會看到記錄讀取器代理程式在執行中，且正在複寫命令或其有「無複寫交易」:

    ![執行時無複寫交易的記錄讀取器代理程式](media/troubleshooting-tran-repl-errors/log-reader-running.png)

## <a name="find-errors-with-the-distribution-agent"></a>尋找散發代理程式的錯誤
散發代理程式會在散發資料庫中尋找資料，然後將它套用到訂閱者。 

1. 連線至 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的發行者。 展開伺服器節點，再以滑鼠右鍵按一下 [複寫]  資料夾，然後選取 [啟動複寫監視器]  。  
2. 在**複寫監視器**中選取 [AdvWorksProductTrans]  發行集，然後選取 [所有訂閱]  索引標籤。以滑鼠右鍵按一下訂閱並選取 [檢視詳細資料]  ：

    ![捷徑功能表上的 [檢視詳細資料] 命令](media/troubleshooting-tran-repl-errors/view-details.png)

2. [散發者到訂閱者記錄]  對話方塊隨即開啟，並會釐清代理程式發生哪個錯誤： 

     ![散發代理程式的錯誤詳細資料](media/troubleshooting-tran-repl-errors/dist-history-error.png)

    ```console
    Error messages:
    Agent 'NODE1\SQL2016-AdventureWorks2012-AdvWorksProductTrans-NODE2\SQL2016-7' is retrying after an error. 89 retries attempted. See agent job history in the Jobs folder for more details.
    ```

3. 此錯誤指出散發代理程式正在重試。 若要尋找更多詳細資訊，請檢查散發代理程式作業記錄： 

    a. 展開 [物件總管] 中的 [SQL Server Agent]  > [作業活動監視器]  。 
    
    b. 依**分類**排序作業。 

    c. 依分類 **REPL-Distribution** 找出散發代理程式。 以滑鼠右鍵按一下代理程式，然後選取 [檢視記錄]  。

    ![檢視散發代理程式記錄的選取項目](media/troubleshooting-tran-repl-errors/view-dist-agent-history.png)

5. 選取其中一個錯誤項目，檢視視窗底部的錯誤文字：  

    ![指出散發代理程式密碼錯誤的錯誤文字](media/troubleshooting-tran-repl-errors/dist-pw-wrong.png)

    ```console
    Message:
    Unable to start execution of step 2 (reason: Error authenticating proxy NODE1\repl_distribution, system error: The user name or password is incorrect.)
    ```

6. 這個錯誤指出散發代理程式所使用的密碼不正確。 若要解決此問題，請：

    a. 展開 [物件總管] 中的 [複寫]  節點。
    
    b. 以滑鼠右鍵按一下訂閱 > [屬性]  。
    
    c. 選取**代理程式處理帳戶**旁的省略符號 (...) 並修改密碼。

    ![修改散發代理程式之密碼的選取項目](media/troubleshooting-tran-repl-errors/dist-agent-pw-change.png)

7. 以滑鼠右鍵按一下 [物件總管] 中的 [複寫]  ，再次檢查複寫監視器。 [所有訂閱]  下的紅色 X 指出散發代理程式仍有錯誤。 

    以滑鼠右鍵按一下 [複寫監視器]   > [檢視詳細資料]  中的訂閱，開啟 [發佈到訂閱者]  記錄。 現在錯誤變得不一樣了： 

    ![指出散發代理程式無法連線的錯誤](media/troubleshooting-tran-repl-errors/dist-agent-cant-connect.png)

    ```console
    Connecting to Subscriber 'NODE2\SQL2016'        
    Agent message code 20084. The process could not connect to Subscriber 'NODE2\SQL2016'.
    Number:  18456
    Message: Login failed for user 'NODE2\repl_distribution'.
    ```

8. 此錯誤指出散發代理程式無法連線至訂閱者，因為使用者 **NODE2\repl_distribution** 登入失敗。 若要進一步調查，請連線至訂閱者並開啟 [物件總管] 中 [管理]  節點下「目前的」  SQL Server 錯誤記錄： 

    ![指出訂閱者登入失敗的錯誤](media/troubleshooting-tran-repl-errors/login-failed.png)
    
    如果您看到這個錯誤，則表示訂閱者缺少登入。 若要解決這個錯誤，請參閱[複寫的權限](../../relational-databases/replication/security/security-role-requirements-for-replication.md)。

9. 登入錯誤解決之後，請再次檢查複寫監視器。 如果所有問題都獲得解決，您應該會在**發行集名稱**旁看到一個綠色箭號，而且 [所有訂閱]  下的狀態為 [執行中]  。 

    再以滑鼠右鍵按一下訂閱，以啟動 [散發者到訂閱者]  記錄，確認是否成功。 如果這是散發代理程式第一次執行，您會看到快照集已大量複製到訂閱者： 

     ![具有 [執行中] 狀態和大量複製相關訊息的散發代理程式](media/troubleshooting-tran-repl-errors/dist-agent-success.png)   


## <a name="enable-verbose-logging-on-any-agent"></a>在任何代理程式上啟用詳細資訊記錄
您可以使用詳細資訊記錄，來查看有關複寫拓撲中任何代理程式所發生錯誤的更多詳細資訊。 每個代理程式的步驟都相同。 只要確定您在 [作業活動監視器] 中選取正確的代理程式。 

   >[!NOTE]   
   > 根據代理程式是提取或發送訂閱而定，它可以位在發行者或訂閱者上。 如果在所查看的伺服器中找不到您要尋找的代理程式，請嘗試檢查其他伺服器。  

1. 決定您要儲存詳細資訊記錄的位置，並確保此資料夾已存在。 這個範例會使用 c:\temp。 
2. 展開 [物件總管] 的 [SQL Server Agent]  節點，然後開啟 [作業活動監視器]。 

    ![[作業活動監視器] 之捷徑功能表上的 [檢視作業活動] 命令](media/troubleshooting-tran-repl-errors/job-activity-monitor.png)    

1. 依據 [分類]  排序，並找出您感興趣的代理程式。 這個範例會使用記錄讀取器代理程式。 以滑鼠右鍵按一下您感興趣的代理程式 > [屬性]  。

    ![開啟代理程式屬性的選取項目](media/troubleshooting-tran-repl-errors/log-agent-properties.png)

1. 選取 [步驟]  頁面，然後反白顯示 [執行代理程式]  步驟。 選取 [編輯]  。 

    ![編輯 [執行代理程式] 步驟的選取項目](media/troubleshooting-tran-repl-errors/edit-steps.png)

1. 在 [命令]  方塊中，開始新的一行，輸入下列文字，然後選取 [確定]  ： 

    ```console
    -Output C:\Temp\OUTPUTFILE.txt -Outputverboselevel 3
    ```

    您可以根據自己的喜好修改位置和詳細資訊層級。

    ![作業步驟之屬性中的詳細資訊輸出](media/troubleshooting-tran-repl-errors/verbose.png)

   > [!NOTE]
   > 當您新增詳細資訊輸出參數時，這些事項可能會導致您的代理程式失敗或遺漏輸出檔案：
   > - 有一個格式問題，其中虛線變成連字號。 
   > - 該位置不存在於磁碟上，或執行代理程式的帳戶缺少寫入指定位置的權限。 
   > - 最後一個參數與 `-Output` 參數之間遺漏一個空格。 
   > - 不同的代理程式支援不同層級的詳細資訊。 如果您啟用詳細資訊記錄，但代理程式無法啟動，請嘗試將指定的詳細資訊層級減少 1。 

1. 以滑鼠右鍵按一下代理程式 > [從下列步驟停止作業]  ，重新啟動記錄讀取器代理程式。 選取工具列中的 [重新整理]  圖示以重新整理。 以滑鼠右鍵按一下代理程式 > [從下列步驟啟動作業]  。
2. 檢閱磁碟上的輸出。 

    ![輸出文字檔](media/troubleshooting-tran-repl-errors/output.png)

    
1. 若要停用詳細資訊記錄，請遵循相同的上一個步驟來移除您之前新增的一整行 `-Output`。 

如需詳細資訊，請參閱[啟用複寫代理程式的詳細資訊記錄](https://support.microsoft.com/help/312292/how-to-enable-replication-agents-for-logging-to-output-files-in-sql-se)。 


## <a name="see-also"></a>另請參閱
<br>[異動複寫概觀](../../relational-databases/replication/transactional/transactional-replication.md)
<br>[複寫教學課程](../../relational-databases/replication/replication-tutorials.md)
<br>[ReplTalk 部落格](https://blogs.msdn.microsoft.com/repltalk)

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]

