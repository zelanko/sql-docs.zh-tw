---
Title: 'Tutorial: Script Objects in SQL Server Management Studio'
description: 在 SSMS 中撰寫物件指令碼的教學課程。
keywords: SQL Server, SSMS, SQL Server Management Studio, 指令碼, 撰寫指令碼
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- projects [SQL Server Management Studio], tutorials
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- solutions [SQL Server Management Studio], tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.openlocfilehash: bc20cc573c6b0890e5b16f4876636534f9fbb916
ms.sourcegitcommit: ccb05cb5a4cccaf7ffa9e85a4684fa583bab914e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
---
# <a name="tutorial-script-objects-in-sql-server-management-studio"></a>教學課程：在 SQL Server Management Studio 中撰寫物件指令碼
本教學課程將教導您如何為 SQL Server Management Studio 中的各種物件產生 Transact-SQL (T-SQL) 指令碼。  在本教學課程中，您將找到如何撰寫以下物件指令碼的範例： 

> [!div class="checklist"]
> * 在 GUI 中執行動作時查詢
> * 使用兩種不同方式 (「撰寫指令碼為」和「產生指令碼」) 的資料庫
> * 資料表
> * 預存程序
> * 擴充事件

本教學課程的摘要是**物件總管**中的任何物件都可以透過按一下滑鼠右鍵並選取 [撰寫物件指令碼為] 選項來撰寫指令碼。 


## <a name="prerequisites"></a>Prerequisites
若要完成本教學課程，您需要 SQL Server Management Studio、SQL Server 存取權，以及 AdventureWorks 資料庫。 

- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)。
- 下載 [AdventureWorks 範例資料庫](https://github.com/Microsoft/sql-server-samples/releases)。 此處可以找到在 SSMS 中還原資料庫的說明：[還原資料庫](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。 


## <a name="script-queries-from-gui"></a>從 GUI 撰寫查詢指令碼
每當您使用 SSMS 中的 GUI 執行工作時，您也可以產生與該工作建立關聯的 T-SQL 程式碼。 下列範例顯示在執行資料庫備份和壓縮交易紀錄時如何進行此操作。  這些相同的步驟可以套用於任何透過 GUI 完成的動作。 

### <a name="script-t-sql-when-backing-up-a-database"></a>在備份資料庫時撰寫 T-SQL 指令碼
1. 連接到 SQL Server。
2. 展開 **[資料庫]** 節點。
3. 以滑鼠右鍵按一下資料庫 > [工作] > [備份]：

    ![備份資料庫](media/scripting-ssms/backupdb.png)

4. 以您想要的方式設定備份。 為了本教學課程目的，所有內容都保留預設。 不過，在視窗中所做的任何變更也會反映在指令碼中。 
5. 按一下選項到 [指令碼] > [撰寫動作至查詢視窗]：
 
    ![撰寫資料庫備份指令碼](media/scripting-ssms/scriptdbbackup.PNG)
6. 檢視填入於查詢視窗的 T-SQL： 

    ![撰寫資料庫備份指令碼](media/scripting-ssms/dbbackupscript.PNG)


### <a name="script-t-sql-when-shrinking-the-transaction-log"></a>壓縮交易紀錄時撰寫 T-SQL 指令碼
1. 以滑鼠右鍵按一下資料庫 > [工作] > [壓縮] > [檔案]：

     ![壓縮檔案](media/scripting-ssms/shrinkfiles.png)

2. 從 [檔案類型] 下拉式清單中選擇 [記錄]：

    ![壓縮交易記錄](media/scripting-ssms/shrinktlog.png)

3. 按一下選項 [撰寫] 和 [撰寫動作指令碼至剪貼簿]：

    ![編寫指令碼至剪貼簿](media/scripting-ssms/scriptactiontoclipboard.png)

4. 開啟 [新增查詢] 視窗並貼上 (在視窗中以滑鼠右鍵按一下 > [貼上])：

    ![貼上指令碼](media/scripting-ssms/paste.png)


## <a name="script-databases"></a>撰寫資料庫指令碼
下一節將教導您如何使用 [撰寫指令碼為] 選項和 [產生指令碼] 選項來撰寫資料庫指令碼。  [撰寫指令碼為] 選項將會重新建立資料庫及其設定選項。 [產生指令碼] 選項將產生資料庫中的所有物件指令碼，但不包含資料。 若要撰寫資料指令碼，您需要使用[匯入和匯出精靈](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/start-the-sql-server-import-and-export-wizard)。  


### <a name="script-database-using-script-option"></a>使用撰寫指令碼選項來撰寫資料庫指令碼
1. 連接到 SQL Server。
2. 展開 **[資料庫]** 節點。
3. 以滑鼠右鍵按一下資料庫 > [撰寫資料庫的指令碼為]：

    ![撰寫資料庫指令碼](media/scripting-ssms/scriptdb.png)

4. 在視窗中檢閱資料庫的建立查詢： 

    ![已撰寫指令碼的資料庫](media/scripting-ssms/scriptedoutdb.png)
    - 此選項只會撰寫資料庫設定選項的指令碼。  

### <a name="script-database-using-generate-scripts-option"></a>使用 [產生指令碼] 選項來撰寫資料庫指令碼
1. 連接到 SQL Server。
2. 展開 **[資料庫]** 節點。
3. 以滑鼠右鍵按一下資料庫 > [工作] > [產生指令碼]：

    ![產生資料庫指令碼](media/scripting-ssms/generatescriptsfordb.png)

4. 選取 [下一步]，您會看到可以選擇撰寫整個資料庫或資料庫中的特定物件： 
 
    ![產生資料庫指令碼](media/scripting-ssms/scriptobjects.png)
 
5. 選取 **[下一步]**。 在這個畫面，您可以設定要將指令碼儲存在哪裡。 
    - 您也可以藉由選取 [進階] 來設定進階的選項：

    ![進階撰寫指令碼選項](media/scripting-ssms/advancedscripts.png)

6. 一旦您準備好繼續，請持續按 [下一步] 直到產生指令碼，然後移至 [完成]。 您的資料庫指令碼會位於在步驟 5 中儲存的位置。 
    - 這將撰寫資料庫中的結構描述和各種物件指令碼，但不包括資料。 
 
## <a name="script-tables"></a>撰寫資料表指令碼
本節說明如何從您的資料庫撰寫資料表指令碼。

1. 連接到 SQL Server。
2. 展開您的 [資料庫] 節點。
3. 展開您的 [AdventureWorks] 資料庫節點。 
4. 展開您的 [資料表] 節點。
5. 以滑鼠右鍵按一下您想要撰寫指令碼的資料表 > [產生資料表的指令碼為]：
    - 從這裡可以看到各種選項，例如建立資料表或將資料插入至資料表中： 
    
    ![編寫資料表的指令碼](media/scripting-ssms/scripttable.png)
 
## <a name="script-stored-procedures"></a>撰寫預存程序的指令碼
本節說明如何撰寫預存程序的指令碼。 

1. 連接到 SQL Server。
2. 展開您的 [資料庫] 節點。
3. 展開您的 [可程式性] 節點。 
4. 展開您的 [預存程序] 節點。
5. 以滑鼠右鍵按一下您想要的預存程序 > [產生預存程序的指令碼為]：
    
    ![撰寫預存程序的指令碼](media/scripting-ssms/scriptstoredprocedure.PNG)

## <a name="script-extended-events"></a>撰寫擴充事件的指令碼
本節說明如何撰寫[擴充事件](https://docs.microsoft.com/en-us/sql/relational-databases/extended-events/extended-events)的指令碼。 

1. 連接到 SQL Server。
2. 展開您的 [管理] 節點。
3. 展開您的 [擴充事件] 節點。
4. 展開您的 [工作階段] 節點。
5. 以滑鼠右鍵按一下您想要的擴充工作階段 > [撰寫工作階段指令碼為]：

    ![撰寫 xEvents 指令碼](media/scripting-ssms/scriptxevents.png) 

## <a name="next-steps"></a>後續步驟
下一篇文章將為您介紹 SSMS 中的預先建立範本。 

請前往下一篇文章來進一步了解
> [!div class="nextstepaction"]
> [按鈕](templates-ssms.md)


