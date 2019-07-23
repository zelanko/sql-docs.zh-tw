---
title: 使用 SQL Server Management Studio (SSMS) 的提示和訣竅
description: 了解如何使用 SQL Server Management Studio 對程式碼進行註解和取消註解、對文字進行縮排、在物件總管中篩選物件、存取 SQL Server 錯誤記錄檔，以及尋找 SQL Server 執行個體名稱。
ms.topic: tutorial
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
author: MashaMSFT
ms.author: mathoma
ms.reviewer: sstein
helpviewer_keywords:
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
- Find SQL Server Instance
- find instance name
- find sql server instance name
ms.custom: ''
ms.date: 03/13/2018
ms.openlocfilehash: d5b52a35bce720e3985a8191335491c50e43c50e
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267577"
---
# <a name="tips-and-tricks-for-using-sql-server-management-studio-ssms"></a>使用 SQL Server Management Studio (SSMS) 的提示和訣竅

此文章提供使用 SQL Server Management Studio (SSMS) 的一些提示和訣竅。 本文示範如何： 

> [!div class="checklist"]
> * 註解與取消註解 TRANSACT-SQL (T-SQL) 文字
> * 縮排文字
> * 在 [物件總管] 中檢篩選物件
> * 存取您的 SQL Server 錯誤記錄檔
> * 尋找您的 SQL Server 執行個體名稱

## <a name="prerequisites"></a>Prerequisites

若要測試此文章所提供的步驟，您需要 SQL Server Management Studio、SQL 伺服器的存取權，以及 AdventureWorks 資料庫。 

* 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
* 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
* 下載 [AdventureWorks 範例資料庫](https://github.com/Microsoft/sql-server-samples/releases)。 若要了解如何在 SSMS 中還原資料庫，請參閱[還原資料庫](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。 

## <a name="commentuncomment-your-t-sql-code"></a>註解與取消註解您的 T-SQL 程式碼

透過使用工具列中的 [註解]  按鈕，可以對部分文字進行註解與取消註解。 標記為註解的文字將不會執行。

1. 開啟 SQL Server Management Studio。

2. 連線到 SQL Server。

3. 開啟 [新增查詢] 視窗。

4. 將下列 T-SQL 程式碼貼入文字視窗中。

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

5. 反白顯示文字中的 **Alter Database** 部分，然後選取工具列上的 [註解]  按鈕： 

    ![[註解] 按鈕](media/ssms-tricks/comment.png)
6. 選取 [執行]  來執行文字中未註解的部分。 

7. 反白顯示除了 **Alter Database** 命令的所有項目，然後選取 [註解]  按鈕：

    ![註解所有項目](media/ssms-tricks/commenteverything.png)

    > [!NOTE]
    > 加上文字註解的鍵盤快速鍵為 **CTRL + K、CTRL + C**。

8. 反白顯示文字中的 **Alter Database** 部分，然後選取 [取消註解]  按鈕，將它取消註解：

    ![取消註解文字](media/ssms-tricks/uncomment.png)

    > [!NOTE]
    > 取消文字註解的鍵盤快速鍵為 **CTRL + K、CTRL + U**。

9. 選取 [執行]  來執行文字中未註解的部分。

## <a name="indent-your-text"></a>縮排文字

您可以使用工具列上的縮排按鈕，增加或減少文字的縮排。

1. 開啟 [新增查詢] 視窗。

2. 將下列 T-SQL 程式碼貼入文字視窗中：

    ```sql
    USE master
      GO

      --Drop the database if it already exists
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

3. 反白文字中的 **Alter Database** 部分，然後選取工具列上的 [增加縮排]  按鈕，將這段文字向前移動：

    ![增加縮排](media/ssms-tricks/increaseindent.png)

4. 再一次反白顯示文字中的 **Alter Database** 部分，然後選取 [減少縮排]  按鈕，將這段文字向後移動。

    ![減少縮排](media/ssms-tricks/decreaseindent.png)

## <a name="filter-objects-in-object-explorer"></a>在 [物件總管] 中檢篩選物件

在含有許多物件的資料庫中，您可以使用篩選來搜尋特定資料表、檢視等。本節描述如何篩選資料表，但是您可以在 [物件總管] 中的任何其他節點使用下列步驟：

1. 連線到 SQL Server。

2. 展開 [資料庫]   > [AdventureWorks]   > [資料表]  。 資料庫中的所有資料表都會出現。

3. 以滑鼠右鍵按一下 [資料表]  ，然後選取 [篩選]   > [篩選設定]  ：

    ![篩選設定](media/ssms-tricks/filtersettings.png)

4. 在 [篩選設定]  視窗中，您可以修改下列部分篩選設定：
    * 依名稱篩選： 

      ![依名稱篩選](media/ssms-tricks/filterbyname.png)

    * 依結構描述篩選： 

      ![依結構描述篩選](media/ssms-tricks/filterbyschema.png)

5. 若要清除篩選，以滑鼠右鍵按一下 [資料表]  然後選取 [移除篩選]  。

    ![移除篩選](media/ssms-tricks/removefilter.png)

## <a name="access-your-sql-server-error-log"></a>存取您的 SQL Server 錯誤記錄檔

錯誤記錄檔是含有在 SQL Server 執行個體中發生事項之詳細資料的檔案。 您可以在 SSMS 中瀏覽和查詢錯誤記錄檔。 錯誤記錄檔是位於您磁碟上的 .log 檔案。

### <a name="open-the-error-log-in-ssms"></a>在 SSMS 中開啟錯誤記錄檔

1. 連線到 SQL Server。  

2. 展開 [管理]   > [SQL Server 記錄檔]  。 

3. 以滑鼠右鍵按一下 [目前]  錯誤記錄檔，然後選取 [檢視 SQL Server 記錄檔]  ：

    ![在 SSMS 中檢視錯誤記錄檔](media/ssms-tricks/viewerrorloginssms.png)

### <a name="query-the-error-log-in-ssms"></a>在 SSMS 中查詢錯誤記錄檔

1. 連線到 SQL Server。

2. 開啟 [新增查詢] 視窗。

3. 將下列 T-SQL 程式碼貼入查詢視窗中：

     ```sql
       sp_readerrorlog 0,1,'Server process ID'
      ```

4. 將單引號中之文字修改為您想要搜尋的文字。

5. 執行查詢，然後檢視結果：

    ![查詢錯誤記錄檔](media/ssms-tricks/queryerrorlog.png)

### <a name="find-the-error-log-location-if-youre-connected-to-sql-server"></a>若您已連線到 SQL Server，請尋找錯誤記錄檔的位置

1. 連線到 SQL Server。

2. 開啟 [新增查詢] 視窗。

3. 在查詢視窗中貼上以下 T-SQL 程式碼，然後選取 [執行]  ：

     ```sql
        SELECT SERVERPROPERTY('ErrorLogFileName') AS 'Error log file location'  
      ```

4. 結果會顯示檔案系統中錯誤記錄檔的位置： 

    ![透過查詢尋找錯誤記錄檔](media/ssms-tricks/finderrorlogquery.png)

### <a name="find-the-error-log-location-if-you-cant-connect-to-sql-server"></a>若您無法連線到 SQL Server，尋找錯誤記錄檔的位置

視您的組態設定而定。SQL Server 錯誤記錄路徑可能會不同。 您可以在 SQL Server 組態管理員內的啟動參數中找到錯誤記錄位置的路徑。 依照下面的步驟尋找指出 SQL Server 錯誤記錄檔位置的相關啟動參數。 *您的路徑可能與下面的路徑不同*。

1. 開啟 [SQL Server 設定管理員]。

2. 展開 [服務]  。

3. 以滑鼠右鍵按一下您的 SQL Server 執行個體，然後選取 [屬性]  ：

    ![設定管理員伺服器屬性](media/ssms-tricks/serverproperties.PNG)

4. 選取 [啟動參數]  索引標籤。

5. 在 [現有參數]  區域中，"-e" 後面的路徑是錯誤記錄檔位置： 

    ![錯誤記錄檔](media/ssms-tricks/errorlog.png)

    這個位置中有數個 errorlog.* 檔案。 結尾為 *.log 的檔案名稱是目前的錯誤記錄檔。 結尾為數字的檔案名稱是先前的記錄檔。 每次 SQL Server 重新啟動時，會建立新的記錄檔。

6. 在 [記事本] 中開啟 errorlog.log 檔案。 

## <a name="determine-sql-server-name"></a>尋找 SQL Server 執行個體名稱

您有一些選項可用來在連線到 SQL Server 之前和之後尋找您的 SQL Server 名稱。  

### <a name="before-you-connect-to-sql-server"></a>連線到 SQL Server 之前

1. 請遵循下列步驟找出[磁碟上的 SQL Server 錯誤記錄檔](#find-the-error-log-location-if-you-cant-connect-to-sql-server)。 您的路徑可能與下圖中的路徑不同。

2. 在 [記事本] 中開啟 errorlog.log 檔案。

3. 搜尋文字「伺服器名稱是」  。

    在單引號中列出的任何內容，就是您將要連線到的 SQL Server 執行個體名稱：

    ![在錯誤記錄檔中尋找伺服器名稱](media/ssms-tricks/servernameinlog.png)

    名稱的格式是 HOSTNAME\INSTANCENAME。 若您只看到主機名稱，則代表您已安裝預設執行個體，而執行個體的名稱為 MSSQLSERVER。 當連線到預設執行個體時，在連線到 SQL Server 時只需要輸入主機名稱。  

### <a name="when-youre-connected-to-sql-server"></a>當您連線到 SQL Server 時

當您連線到 SQL Server 時，您可以在三個位置中找到伺服器名稱： 

1. 伺服器名稱將會列在 [物件總管] 中：

    ![[物件總管] 中的 SQL Server 執行個體名稱](media/ssms-tricks/nameinobjectexplorer.png)
2. 伺服器名稱將會列在查詢視窗中：

    ![查詢視窗中的 SQL Server 執行個體名稱](media/ssms-tricks/nameinquerywindow.png)
3. 伺服器名稱將會列在 [屬性]  中。
    * 在 [檢視]  功能表，選取 [屬性視窗]  。

      ![屬性視窗中的 SQL Server 執行個體名稱](media/ssms-tricks/nameinproperties.png)

### <a name="if-youre-connected-to-an-alias-or-availability-group-listener"></a>如果您已連線到別名或可用性群組接聽程式

如果您已連線到別名或可用性群組接聽程式，該資訊會顯示在 [物件總管] 和 [屬性]。 在此情況下，SQL Server 名稱可能不明顯，且必須進行查詢：

1. 連線到 SQL Server。

2. 開啟 [新增查詢] 視窗。

3. 將下列 T-SQL 程式碼貼入視窗中：

      ```sql
       select @@Servername
     ```

4. 檢視查詢結果以識別您連線的 SQL Server 執行個體名稱： 

    ![查詢 SQL 伺服器名稱](media/ssms-tricks/queryservername.png)

## <a name="next-steps"></a>後續步驟

熟悉 SSMS 的最佳方式是實際練習。 這些「教學課程」  與「操作方式」  文章可協助您使用 SSMS 內所提供的各種功能。  這些文章會告訴您如何管理 SSMS 的元件及如何尋找您經常使用的功能。

* [連線至執行個體並對其進行查詢](connect-query-sql-server.md)
* [指令碼](scripting-ssms.md)
* [在 SSMS 中使用範本](../template/templates-ssms.md)
* [SSMS 組態](ssms-configuration.md)
