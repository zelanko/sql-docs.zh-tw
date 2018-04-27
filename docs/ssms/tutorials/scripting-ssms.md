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
ms.openlocfilehash: a931ddb3cf3229970de4b301e18002484acbaf53
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-script-objects-in-sql-server-management-studio"></a>教學課程：在 SQL Server Management Studio 中撰寫物件指令碼
本教學課程將教導您如何為 SQL Server Management Studio 中的各種物件產生 Transact-SQL (T-SQL) 指令碼。  在本教學課程中，您將找到如何撰寫以下物件指令碼的範例： 

> [!div class="checklist"]
> * 在 GUI 中執行動作時查詢
> * 使用兩種不同方式 (「撰寫指令碼為」和「產生指令碼」) 的資料庫
> * 資料表
> * 預存程序
> * 擴充事件

本教學課程的摘要是**物件總管**中的任何物件都可以透過按一下滑鼠右鍵並選取 [Script Object As] \(編寫物件指令碼為\) 選項來編寫指令碼。 


## <a name="prerequisites"></a>Prerequisites
若要完成本教學課程，您需要 SQL Server Management Studio、SQL Server 存取權，以及 AdventureWorks 資料庫。 

- 安裝 [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms)。
- 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)。
- 下載 [AdventureWorks2016 範例資料庫](https://github.com/Microsoft/sql-server-samples/releases)。 此處可以找到在 SSMS 中還原資料庫的說明：[還原資料庫](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。 


## <a name="script-queries-from-gui"></a>從 GUI 撰寫查詢指令碼
每當您使用 SSMS 中的 GUI 執行工作時，您也可以產生與該工作建立關聯的 T-SQL 程式碼。 下列範例顯示在執行資料庫備份和壓縮交易紀錄時如何進行此操作。  這些相同的步驟可以套用於任何透過 GUI 完成的動作。 

### <a name="script-t-sql-when-backing-up-a-database"></a>在備份資料庫時撰寫 T-SQL 指令碼
1. 連接到 SQL Server。
2. 展開 **[資料庫]** 節點。
3. 以滑鼠右鍵按一下 [**Adventureworks2016** 資料庫] > [工作] > [備份]：

    ![備份資料庫](media/scripting-ssms/backupdb.png)

4. 以您想要的方式設定備份。 為了本教學課程目的，所有項目都會保留預設。 不過，在視窗中所做的任何變更也會反映在指令碼中。 
5. 按一下選項 [指令碼] > [Script Action to Query Window] \(編寫動作的指令碼至查詢視窗)：
 
    ![撰寫資料庫備份指令碼](media/scripting-ssms/scriptdbbackup.PNG)
6. 檢視填入於查詢視窗的 T-SQL： 

    ![撰寫資料庫備份指令碼](media/scripting-ssms/dbbackupscript.PNG)
7. 選取 [執行] 來執行查詢以透過 T-SQL 備份資料庫。 


### <a name="script-t-sql-when-shrinking-the-transaction-log"></a>壓縮交易紀錄時撰寫 T-SQL 指令碼
1. 以滑鼠右鍵按一下 [**AdventureWorks2016** 資料庫] > [工作] > [壓縮] > [檔案]：

     ![壓縮檔案](media/scripting-ssms/shrinkfiles.png)

2. 從 [檔案類型] 下拉式清單中選擇 [記錄]：

    ![壓縮交易記錄](media/scripting-ssms/shrinktlog.png)

3. 選取選項 [指令碼] 和 [Script Action to Clipboard] \(編寫動作的指令碼至剪貼簿\)：

    ![編寫指令碼至剪貼簿](media/scripting-ssms/scriptactiontoclipboard.png)

4. 開啟 [新增查詢] 視窗並貼上 (在視窗中以滑鼠右鍵按一下 > [貼上])：

    ![貼上指令碼](media/scripting-ssms/paste.png)
5. 選取 [執行] 來執行查詢並壓縮交易記錄。 


## <a name="script-databases"></a>撰寫資料庫指令碼
下一節將教導您如何使用 [撰寫指令碼為] 選項和 [產生指令碼] 選項來撰寫資料庫指令碼。  [撰寫指令碼為] 選項將會重新建立資料庫及其設定選項。 [產生指令碼] 選項可讓您為結構描述與資料編寫指令碼。 在本節中，您將建立兩個新的資料庫，*AdventureWorks2016a* 會透過使用 [Script As] \(建立指令碼為\) 選項建立。 而 *AdventureWorks2016b* 則會使用 [產生指令碼] 選項建立。 


### <a name="script-database-using-script-option"></a>使用撰寫指令碼選項來撰寫資料庫指令碼
1. 連接到 SQL Server。
2. 展開 **[資料庫]** 節點。
3. 以滑鼠右鍵按一下 [**AdventureWorks2016** 資料庫] > [Script Database As] \(編寫資料庫的指令碼為\) > [Create To] \(建立至\) > [New Query Window] \(新增查詢視窗\)：

    ![撰寫資料庫指令碼](media/scripting-ssms/scriptdb.png)

4. 在視窗中檢閱資料庫的建立查詢： 

    ![已撰寫指令碼的資料庫](media/scripting-ssms/scriptedoutdb.png)
    - 此選項只會撰寫資料庫設定選項的指令碼。
5. 在您的鍵盤上選取 **Ctrl + F** 開啟 [尋找] 對話方塊，並選取向下鍵開啟 [取代] 選項。 在上方的 [尋找] 行鍵入 *AdventureWorks2016*，並在下方的 [取代] 行鍵入 *AdventureWorks2016a*。 
6. 選取 [全部取代] 以將所有 *AdventureWorks2016* 的執行個體取代為 *AdventureWorks2016a*。 

    ![尋找和取代](media/scripting-ssms/findandreplace.png)

1. 選取 [執行] 執行查詢並建立新的 *AdventureWorks2016a* 資料庫。 

### <a name="script-database-using-generate-scripts-option"></a>使用 [產生指令碼] 選項來撰寫資料庫指令碼
1. 連接到 SQL Server。
2. 展開 **[資料庫]** 節點。
3. 以滑鼠右鍵按一下 [**AdventureWorks2016** 資料庫] > [工作] > [產生指令碼]：

    ![產生資料庫指令碼](media/scripting-ssms/generatescriptsfordb.png)

4. [簡介] 頁面會隨即開啟，請選取 [下一步] 開啟 [選擇物件] 頁面。 您可以選取整個資料庫或資料庫中的特定物件。 選取選項 [Script entire database and all database objects] \(編寫整個資料庫與所有資料庫物件的指令碼\) 
 
    ![產生資料庫指令碼](media/scripting-ssms/scriptobjects.png)
 
5. 選取 [下一步] 開啟 [Set Scripting Options] \(設定指令碼編寫選項\) 頁面，您可在其中設定指令碼的存放位置，以及設定其他進階選項。 

    A. 選取選項 [儲存至新增查詢視窗]。 

    B. 選取 [進階] 並確認這些選項均以設定： 

      - [Script Statistics] \(編寫統計資料的指令碼\) 設定為 *Script Statistics*
      - [Types of data to script] \(要編寫指令碼的資料類型\) 設定為 *Schema only*
      - [Script Indexes] \(編寫索引的指令碼\) 設定為 *true*

   ![Script Objects (指令碼物件)](media/scripting-ssms/advancedscripts.png)

   > [!NOTE]
   > 當您選取 [Types of data to script] \(要編寫指令碼的資料類型\) 選項的 *Schema and data* 時，可以為資料庫的資料編寫指令碼。 但是，因為大型資料庫使用的記憶體可能會超過 SSMS 所能配置的數量，所以對大型資料庫來說並不適合。 對於小型資料庫而言這樣做是沒問題的，但若您想將資料移至更大的資料庫，則建議您使用[匯入與匯出精靈](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard)。



1. 依序選取 [確定] 和 [下一步]。 
2. 選取 [摘要] 上的 [下一步]，然後再次選取 [下一步] 將指令碼產生到 [New Query] \(新增查詢\) 視窗。  
3. 在您的鍵盤上選取 **Ctrl + F** 開啟 [尋找] 對話方塊，並選取向下鍵開啟 [取代] 選項。 在上方的 [尋找] 行鍵入 *AdventureWorks2016*，並在下方的 [取代] 行鍵入 *AdventureWorks2016b*。 
    A. 選取 [全部取代] 以將所有 *AdventureWorks2016* 的執行個體取代為 *AdventureWorks2016b*。 

    ![AdventureWorks2016b](media/scripting-ssms/adventureworks2016b.png)
7. 選取 [執行] 執行查詢並建立新的 *AdventureWorks2016b* 資料庫。 
 
## <a name="script-tables"></a>撰寫資料表指令碼
本節說明如何從您的資料庫撰寫資料表指令碼。 您可使用此選項來建立資料表，或是卸除及建立資料表。 您也可以使用此選項來為與修改資料表相關聯的 T-SQL 編寫指令碼，例如對其插入或對其更新。 在本節中，您將卸除資料表並予以重新建立。 

1. 連接到 SQL Server。
2. 展開您的 [資料庫] 節點。
3. 展開您的 [AdventureWorks] 資料庫節點。 
4. 展開您的 [資料表] 節點。
5. 以滑鼠右鍵按一下 [dbo.ErrorLog] >  [Script Table as] \(編寫資料表的指令碼為\) > [Drop and Create To] \(卸除並建立至\) > [New Query Editor Window] \(新增查詢編輯器視窗\)：
    
    ![編寫資料表的指令碼](media/scripting-ssms/scripttable.png)

6. 選取 [執行]執行查詢 - 這會卸除 *Errorlog* 資料表並予以重新建立。 

    >[!NOTE]
    > *Errorlog* 資料表在 AdventureWorks2016 資料庫中預設為空，因此您不會因為卸除資料表而失去任何資料。 但是，在具有資料的資料表上進行這些步驟則可能會導致資料遺失。 
 
## <a name="script-stored-procedures"></a>撰寫預存程序的指令碼
在本節中，您會學到如何卸除及建立預存程序。  

1. 連接到 SQL Server。
2. 展開您的 [資料庫] 節點。
3. 展開您的 [可程式性] 節點。 
4. 展開您的 [預存程序] 節點。
5. 以滑鼠右鍵按一下預存程序 [dbo.uspGetBillOfMaterials]> [Script Stored Procedure As] \(編寫預存程序的指令碼為\) > [Drop and Create to] \(卸除並建立至\) > [New Query Window] \(新增查詢視窗\)：
    
    ![撰寫預存程序的指令碼](media/scripting-ssms/scriptstoredprocedure.PNG)

## <a name="script-extended-events"></a>撰寫擴充事件的指令碼
本節說明如何撰寫[擴充事件](https://docs.microsoft.com/en-us/sql/relational-databases/extended-events/extended-events)的指令碼。 

1. 連接到 SQL Server。
2. 展開您的 [管理] 節點。
3. 展開您的 [擴充事件] 節點。
4. 展開您的 [工作階段] 節點。
5. 以滑鼠右鍵按一下您想要的延伸工作階段 > [Script Session As] \(編寫工作階段的指令碼為\) > [New Query Editor Window] \(新增查詢編輯器視窗\)：

    ![撰寫 xEvents 指令碼](media/scripting-ssms/scriptxevents.png) 
6. 在 [New Query Window] \(新增查詢視窗\) 中，將工作階段的新名稱從 *system_health* 修改為 *system_health2*，並選取 [執行] 執行查詢。 

    A. 以滑鼠右鍵按一下**物件總管**中的 [工作階段]，並選取 [重新整理] 查看新的延伸事件工作階段。 工作階段旁的綠色圖示代表工作階段正在執行，而紅色圖示則代表工作階段已停止。 

    ![新增 xEvent](media/scripting-ssms/newxevent.png)

    >[!NOTE]
    > 您可以滑鼠右鍵按一下工作階段並選取 [開始] 來開始工作階段。 不過，因為已經有正在執行之 *system_health*工作階段的複本，所以可跳過此步驟。 您可以滑鼠右鍵按一下延伸事件工作階段的複本，並選取 [刪除] 將其刪除。 

## <a name="next-steps"></a>後續步驟
下一篇文章將為您介紹 SSMS 中的預先建立 T-SQL 範本。 

請前往下一篇文章以深入了解：
> [!div class="nextstepaction"]
> [後續步驟](templates-ssms.md)


