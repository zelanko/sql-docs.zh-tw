---
Title: 'Tutorial: Additional Tips and Tricks for using SSMS'
description: '涵蓋 SSMS 使用上的一些其他祕訣與訣竅之教學課程。 '
keywords: SQL Server、SSMS、SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
ms.openlocfilehash: e358fb73ff4f248b7de368364b8bb758f70018ff
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="tutorial-additional-tips-and-tricks-for-using-ssms"></a>教學課程：使用 SSMS 的其他祕訣與訣竅
本文將提供 SQL Server Management Studio 使用上的一些其他祕訣。 本文將告訴您如何： 

> [!div class="checklist"]
> * 註解與取消註解 TRANSACT-SQL (T-SQL) 文字
> * 縮排文字
> * 在物件總管中檢篩選物件
> * 存取您的 SQL Server 錯誤記錄檔
> * 尋找您的 SQL Server 執行個體名稱

## <a name="prerequisites"></a>Prerequisites
若要完成本教學課程，您需要 SQL Server Management Studio、SQL Server 存取權，以及 AdventureWorks 資料庫。 

- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
- 下載 [AdventureWorks 範例資料庫](https://github.com/Microsoft/sql-server-samples/releases)。 此處可以找到在 SSMS 中還原資料庫的說明：[還原資料庫](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。 

## <a name="comment--uncomment-your-t-sql-code"></a>註解/取消註解您的 T-SQL 程式碼
透過使用工具列中的註解按鈕，可以對部分文字進行註解與取消註解。 標記為註解的文字將不會執行。 

1. 開啟 SQL Server Management Studio。 
2. 連接到 SQL Server。
3. 開啟 [新增查詢] 視窗。 
4. 將下列 T-SQL 程式碼貼入文字視窗中： 

  ```sql
    USE master
    GO

    -- Drop the database if it already exists
    IF  EXISTS (
        SELECT name 
            FROM sys.databases 
            WHERE name = N'TutorialDB'
            )

    DROP DATABASE TutorialDB
    GO

    CREATE DATABASE TutorialDB
    GO

    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
 ``` 


5. 反白顯示文字中的 **Alter Database** 部分，按一下工具列中的 [註解]： 

    ![註解](media/ssms-tricks/comment.png)
6. 按一下 [執行] 來執行文字中未註解的部分。 
7. 反白顯示 **Alter Database** 命令以外的所有項目，然後按一下工具列中的 [註解]：

    ![註解所有項目](media/ssms-tricks/commenteverything.png)

8. 反白顯示 **Alter Database** 部分，並按一下 [取消註解] 以將其取消註解：

    ![取消註解](media/ssms-tricks/uncomment.png)
    
9. 按一下 [執行] 來執行文字中未註解的部分。 

## <a name="indent-your-text"></a>縮排文字
縮排按鈕可讓您增加和減少文字的縮排。 

1. 開啟 [新增查詢] 視窗。 
2. 將下列 T-SQL 程式碼貼入文字視窗中： 

  ```sql
    USE master
    GO

    -- Drop the database if it already exists
    IF  EXISTS (
        SELECT name 
            FROM sys.databases 
            WHERE name = N'TutorialDB'
            )

    DROP DATABASE TutorialDB
    GO

    CREATE DATABASE TutorialDB
    GO

    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
 ``` 
 
3. 反白文字中的 **Alter Database** 部分，然後按工具列中的 [增加縮排] 將這段文字向前移動：

    ![增加縮排](media/ssms-tricks/increaseindent.png)

4. 再一次反白顯示文字中的 **Alter Database** 部分，這次按一下 [減少縮排] 將文字向後移動。 
    ![減少縮排](media/ssms-tricks/decreaseindent.png)


## <a name="filter-objects-in-object-explorer"></a>在物件總管中檢篩選物件
當資料庫有許多物件時，尋找特定的物件可能很困難。 若要更容易進行，您可以篩選物件。 本節說明如何篩選資料表，但同樣的步驟也可套用於**物件總管**中的任何其他節點

1. 連接到 SQL Server。
2. 展開您的 [資料庫] 節點。
3. 展開您的 [AdventureWorks] 資料庫節點。 
4. 展開您的 [資料表] 節點。 
   - 您會注意到您可以查看出現在資料庫中的所有資料表。
5. 以滑鼠右鍵按一下 [資料表] 節點 > [篩選] > [篩選設定]：

    ![篩選設定](media/ssms-tricks/filtersettings.png)

6. 在 [篩選設定] 視窗中，您可以修改篩選設定。 一些範例：
    - 依名稱篩選：![依名稱篩選](media/ssms-tricks/filterbyname.png)
    - 依結構描述篩選：![依結構描述篩選](media/ssms-tricks/filterbyschema.png)

7. 若要清除篩選，以滑鼠右鍵按一下 [資料表] > [移除篩選]

    ![移除篩選](media/ssms-tricks/removefilter.png)
    


## <a name="access-your-sql-server-error-log"></a>存取您的 SQL Server 錯誤記錄檔
錯誤記錄檔是含有在 SQL Server 中發生事項之詳細資訊的檔案。 可以在 SSMS 中瀏覽和查詢。 也可以作為 .log 檔案在磁碟上找到。

### <a name="open-error-log-within-ssms"></a>在 SSMS 中開啟錯誤記錄檔
1. 連接到 SQL Server。
2. 展開 **[管理]** 節點。 
3. 展開 [SQL Server 記錄檔] 節點。 
4. 以滑鼠右鍵按一下 [目前的] 錯誤記錄檔 > [檢視 SQL Server 記錄檔]：

    ![在 SSMS 中檢視錯誤記錄檔](media/ssms-tricks/viewerrorloginssms.png)

### <a name="query-error-log-within-ssms"></a>在 SSMS 中查詢錯誤記錄檔
1. 連接到 SQL Server。
2. 開啟 [新增查詢] 視窗。
3. 將下列 T-SQL 程式碼貼入查詢視窗中：

 ```sql
   sp_readerrorlog 0,1,'Server process ID' 
  ``` 
4. 將單引號中之文字修改為您想要的文字。
5. 執行查詢並檢視結果：
   
    ![查詢錯誤記錄檔](media/ssms-tricks/queryerrorlog.png)


### <a name="find-error-log-location-if-youre-connected-to-sql"></a>若您已連線至 SQL，請尋找錯誤記錄檔的位置
1. 連線到 SQL Server。
2. 開啟 [新增查詢] 視窗。
3. 將下列 T-SQL 程式碼貼入查詢視窗中，然後按一下 [執行]：

 ```sql
    SELECT SERVERPROPERTY('ErrorLogFileName') AS 'Error log file location'  
  ``` 

4. 結果會顯示檔案系統中錯誤記錄檔的位置： 

    ![透過查詢尋找錯誤記錄檔](media/ssms-tricks/finderrorlogquery.png)

### <a name="find-error-log-location-if-you-cannot-connect-to-sql"></a>若您無法連線至 SQL，請尋找錯誤記錄檔的位置
1. 開啟您的 SQL Server 設定管理員。 
2. 展開 [服務] 節點。
3. 以滑鼠右鍵按一下您的 SQL Server 執行個體 > [屬性]：

    ![設定管理員伺服器屬性](media/ssms-tricks/serverproperties.PNG)

4. 選取 [啟動參數] 索引標籤。
5. 在**現有參數**區域中，"-e" 後面的路徑是錯誤記錄檔位置： 
    
    ![錯誤記錄檔](media/ssms-tricks/errorlog.png)
    - 您會注意到這個位置中有數個 errorlog.*。 以 *.log 結尾之檔案是目前的記錄檔。 以數字結尾之檔案是先前的記錄檔，因為每次 SQL Server 重新啟動時都會建立一個新紀錄檔。 
6. 在記事本中開啟這個檔案。 

## <a name="determine-sql-server-name"></a>判斷 SQL Server 名稱...
在連線至 SQL Server 的前後，有多種判斷 SQL Server 名稱的方式。  

### <a name="when-you-dont-know-it"></a>不知道執行個體名稱時
1. 請遵循下列步驟找出[磁碟上的 SQL Server 錯誤記錄檔](#finding-your-error-log-if-you-cannot-connect-to-sql)。 
2. 在記事本中開啟 errorlog.log。 
3. 巡覽至您找到 "Server name is" 文字為止：
  - 任何在單引號中列出的，就是 SQL Server 名稱和您將要連線的：![錯誤記錄檔中的伺服器名稱](media/ssms-tricks/servernameinlog.png) 名稱的格式為「主機名稱\執行個體名稱」。 若您只看到主機名稱，則代表您安裝了預設執行個體，而執行個體的名稱為 'MSSQLSERVER'。 當連線至預設執行個體時，在連線至 SQL Server 時只需要鍵入主機名稱。  

### <a name="once-youre-connected-to-sql"></a>...一旦您連線至 SQL 
有三個地方可以尋找您已連線到哪一個 SQL Server。 

1. 伺服器名稱將會列在**物件總管**中：

    ![物件總管中的執行個體名稱](media/ssms-tricks/nameinobjectexplorer.png)
2. 伺服器名稱將會列在查詢視窗中：

    ![查詢視窗中的名稱](media/ssms-tricks/nameinquerywindow.png)
3. 伺服器名稱也將列在**屬性視窗**中。
    - 若要加以存取，請開啟 [檢視] 功能表 > [屬性視窗]：

    ![在屬性中的名稱](media/ssms-tricks/nameinproperties.png)

### <a name="if-youre-connected-to-an-alias-or-availability-group-listener"></a>如果您已連線到別名或可用性群組接聽程式 
當您已連線到別名或可用性群組接聽程式時，那麼將會顯示**物件總管**和**屬性**。 在此情況下，SQL Server 名稱可能不明顯，且必須進行查詢。 

1. 連接到 SQL Server。
2. 開啟 [新增查詢] 視窗。
3. 將下列 T-SQL 程式碼貼入視窗中： 

  ```sql
   select @@Servername 
 ``` 
4. 檢視查詢結果以識別您連線的 SQL Server 名稱： 
    
    ![查詢伺服器名稱](media/ssms-tricks/queryservername.png)


