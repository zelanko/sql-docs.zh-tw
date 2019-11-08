---
title: 教學課程：在 SQL Server Management Studio 中撰寫物件指令碼
description: 在 SSMS 中撰寫物件指令碼的教學課程
keywords: SQL Server, SSMS, SQL Server Management Studio, 指令碼, 撰寫指令碼
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.reviewer: sstein
helpviewer_keywords:
- projects [SQL Server Management Studio], tutorials
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- solutions [SQL Server Management Studio], tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.openlocfilehash: 36d3b90a9ac1e49af564323c86421216216522a9
ms.sourcegitcommit: d65cef35cdf992297496095d3ad76e3c18c9794a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/28/2019
ms.locfileid: "72988410"
---
# <a name="script-objects-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中撰寫物件指令碼

本教學課程將教導您如何針對能在 SQL Server Management Studio (SSMS) 內找到的各種物件產生 Transact-SQL (T-SQL) 指令碼。 在本教學課程中，您會找到如何撰寫以下物件指令碼的範例：

> [!div class="checklist"]
> * 查詢，當您在 GUI 內執行動作時
> * 資料庫，以兩種不同方式撰寫 (「撰寫指令碼為」和「產生指令碼」)
> * 資料表
> * 預存程序
> * 擴充事件

若要在 [物件總管]  中編寫任何物件的指令碼，請以滑鼠右鍵按一下它，然後選取 [撰寫指令碼為]  選項。 本教學課程會說明此程序。

## <a name="prerequisites"></a>Prerequisites

若要完成本教學課程，您需要 SQL Server Management Studio、執行 SQL Server 伺服器的存取權，以及 AdventureWorks 資料庫。

* 安裝 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。
* 安裝 [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)。
* 下載 [AdventureWorks2016 範例資料庫](https://github.com/Microsoft/sql-server-samples/releases) \(英文\)。

如需在 SSMS 中還原資料庫的指示，請參閱：[還原資料庫](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms)。 

## <a name="script-queries-from-the-gui"></a>從 GUI 撰寫查詢指令碼

每當您使用 SSMS 中的 GUI 來完成工作時，可以為工作產生相關聯的 T-SQL 程式碼。 下列範例說明如何在備份資料庫及壓縮交易記錄時進行此操作。 這些相同的步驟可以套用於任何透過 GUI 完成的動作。

### <a name="script-t-sql-when-you-back-up-a-database"></a>在備份資料庫時撰寫 T-SQL 指令碼

1. 連線至執行 SQL Server 的伺服器。

2. 展開 **[資料庫]** 節點。

3. 以滑鼠右鍵按一下資料庫 [Adventureworks2016]   > [工作]   > [備份]  ：

    ![備份資料庫](media/scripting-ssms/backupdb.png)

4. 以您想要的方式設定備份。 針對本教學課程，所有項目都會保留預設。 不過，在視窗中所做的任何變更也會反映在指令碼中。 

5. 依序選取 [指令碼]   > [將動作指令碼編寫至新增查詢視窗]  ：

    ![編寫資料庫備份指令碼 - 指令碼動作](media/scripting-ssms/scriptdbbackup.PNG)
6. 檢閱填入於查詢視窗的 T-SQL。

    ![編寫資料庫備份指令碼 - 檢閱 T-SQL](media/scripting-ssms/dbbackupscript.PNG)
7. 選取 [執行]  來執行查詢以透過 T-SQL 備份資料庫。 

### <a name="script-t-sql-when-you-shrink-the-transaction-log"></a>在壓縮交易記錄時撰寫 T-SQL 指令碼

1. 以滑鼠右鍵按一下 [AdventureWorks2016]   > [工作]   > [壓縮]   > [檔案]  ：

     ![壓縮檔案](media/scripting-ssms/shrinkfiles.png)

2. 從 [檔案類型]  下拉式清單方塊選取 [記錄]  ：

    ![壓縮交易記錄](media/scripting-ssms/shrinktlog.png)

3. 選取 [指令碼]  和 [將動作指令碼編寫至剪貼簿]  ：

    ![編寫指令碼至剪貼簿](media/scripting-ssms/scriptactiontoclipboard.png)

4. 開啟 [新增查詢]  視窗，然後貼上。 (在視窗中以滑鼠右鍵按一下。 然後選取 [貼上]  )。

    ![貼上指令碼](media/scripting-ssms/paste.png)

5. 選取 [執行]  來執行查詢並壓縮交易記錄。

## <a name="script-databases"></a>撰寫資料庫指令碼

下一節將教導您如何使用 [撰寫指令碼為]  和 [產生指令碼]  選項來撰寫資料庫指令碼。 [撰寫指令碼為]  選項會重新建立資料庫及其設定選項。 您可以使用 [產生指令碼]  選項為結構描述和資料編寫指令碼。 在本節中，您會建立兩個新的資料庫。 您使用 [撰寫指令碼為]  選項來建立 *AdventureWorks2016a*。 您使用 [產生指令碼]  選項來建立 *AdventureWorks2016b*。

### <a name="script-a-database-by-using-the-script-option"></a>使用 [指令碼] 選項來編寫資料庫指令碼

1. 連線至執行 SQL Server 的伺服器。

2. 展開 **[資料庫]** 節點。

3. 以滑鼠右鍵按一下 [AdventureWorks2016]   > [編寫資料庫的指令碼為]   > [建立至]   > [新增查詢編輯器視窗]  ：

    ![編寫資料庫的指令碼](media/scripting-ssms/scriptdb.png)

4. 在視窗中檢閱資料庫的建立查詢：

    ![編寫資料庫指令碼](media/scripting-ssms/scriptedoutdb.png) 這個選項只會編寫資料庫設定選項的指令碼。

5. 在鍵盤上，選取 Ctrl+F 以開啟 [尋找]  對話方塊。 選取向下箭號以開啟 [取代]  選項。 在上方的 [尋找]  行輸入 AdventureWorks2016，並在下方的 [取代]  行輸入 AdventureWorks2016a。

6. 選取 [全部取代]  以將所有 *AdventureWorks2016* 的執行個體取代為 *AdventureWorks2016a*。 

    ![尋找及取代](media/scripting-ssms/findandreplace.png)

7. 選取 [執行]  來執行查詢並建立新的 AdventureWorks2016a 資料庫。 

### <a name="script-a-database-by-using-the-generate-scripts-option"></a>使用 [產生指令碼] 選項來編寫資料庫指令碼

1. 連線至執行 SQL Server 的伺服器。

2. 展開 **[資料庫]** 節點。

3. 以滑鼠右鍵按一下 [AdventureWorks2016]   > [工作]   > [產生指令碼]  ：

    ![產生資料庫的指令碼](media/scripting-ssms/generatescriptsfordb.png)

4. [簡介]  頁面隨即開啟。 選取 [下一步]  來開啟 [選擇物件]  頁面。 您可以選取整個資料庫或資料庫中的特定物件。 選取 [編寫整個資料庫和所有資料庫物件的指令碼]  。

    ![產生物件的指令碼](media/scripting-ssms/scriptobjects.png)

5. 選取 [下一步]  來開啟 [設定指令碼編寫選項]  頁面。 在這裡您可以設定指令碼的儲存位置以及其他進階選項。 

    A. 選取 [儲存至新增查詢視窗]  。

    B. 選取 [進階]  並確認這些選項皆已設定：

      * [編寫統計資料的指令碼]  已設定為 [編寫統計資料的指令碼]  。
      * [要編寫指令碼的資料類型]  已設定為 [僅結構描述]  。
      * [編寫索引的指令碼]  已設定為 [True]  。

   ![編寫物件的指令碼](media/scripting-ssms/advancedscripts.png)

   > [!NOTE]
   > 當您針對 [要編寫指令碼的資料類型]  選項選取 [結構描述及資料]  時，便可以為資料庫的資料編寫指令碼。 不過，這並不適用於大型資料庫。 此工作所需的記憶體，會比 SSMS 所能配置的還要多。 這項限制並不會影響小型資料庫。 如果您想要移動更大型資料庫的資料，請使用 [[匯入和匯出精靈]](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard)。

6. 依序選取 [確定]  和 [下一步]  。

7. 在 [摘要]  上選取 [下一步]  。 然後再次選取 [下一步]  以在 [新增查詢]  視窗中產生指令碼。

8. 在鍵盤上，開啟 [尋找]  對話方塊 (Ctrl+F)。 選取向下箭號以開啟 [取代]  選項。 在上方的 [尋找]  行中，輸入 *AdventureWorks2016*。 在下方的 [取代]  行中，輸入 *AdventureWorks2016b*。

9. 選取 [全部取代]  以將所有 *AdventureWorks2016* 的執行個體取代為 *AdventureWorks2016b*。

    ![AdventureWorks2016b](media/scripting-ssms/adventureworks2016b.png)

10. 選取 [執行]  來執行查詢並建立新的 AdventureWorks2016b 資料庫。

## <a name="script-tables"></a>撰寫資料表的指令碼

本節說明如何從您的資料庫撰寫資料表指令碼。 您可使用此選項來建立資料表，或是卸除並建立資料表。 您也可以使用此選項來針對與修改資料表相關聯的 T-SQL 編寫指令碼。 幾個修改的範例，為針對它進行插入或更新。 在本節中，您會卸除資料表，然後重新建立它。 

1. 連線至執行 SQL Server 的伺服器。

2. 展開您的 [資料庫]  節點。

3. 展開您的 [AdventureWorks2016]  資料庫節點。 

4. 展開您的 [資料表]  節點。

5. 以滑鼠右鍵按一下 **dbo.ErrorLog** > [產生資料表的指令碼為]   > [DROP 並 CREATE 至]   > [新增查詢編輯器視窗]  ：

    ![編寫資料表的指令碼](media/scripting-ssms/scripttable.png)

6. 選取 [執行]  來執行查詢。 這個動作會刪除 *Errorlog* 資料表，然後重新建立它。 

    >[!NOTE]
    > 在 AdventureWorks2016 資料庫中，*Errorlog* 資料表預設是空的。 因此刪除該資料表並不會遺失任何資料。 但是，在具有資料的資料表上執行這些步驟，則可能會導致資料遺失。

## <a name="script-stored-procedures"></a>撰寫預存程序的指令碼

在本節中，您將了解如何卸除並建立預存程序。  

1. 連線至執行 SQL Server 的伺服器。

2. 展開您的 [資料庫]  節點。

3. 展開您的 [可程式性]  節點。 

4. 展開您的 [預存程序]  節點。

5. 以滑鼠右鍵按一下預存程序 **dbo.uspGetBillOfMaterials** > [產生預存程序的指令碼為]   > [DROP 並 CREATE 至]   > [新增查詢編輯器視窗]  ：

    ![撰寫預存程序的指令碼](media/scripting-ssms/scriptstoredprocedure.PNG)

## <a name="script-extended-events"></a>撰寫擴充事件的指令碼

本節說明如何撰寫[擴充事件](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)的指令碼。

1. 連線至執行 SQL Server 的伺服器。

2. 展開您的 [管理]  節點。

3. 展開您的 [擴充事件]  節點。

4. 展開您的 [工作階段]  節點。

5. 以滑鼠右鍵按一下所需的擴充工作階段 > [編寫工作階段的指令碼為]   > [CREATE 至]   > [新增查詢編輯器視窗]  ：

    ![擴充新增查詢編輯器視窗工作階段](media/scripting-ssms/scriptxevents.png)

6. 在 [新增查詢編輯器視窗]  中，將工作階段的名稱從 *system_health* 修改為 *system_health2*。 選取 [執行]  來執行查詢。

7. 以滑鼠右鍵按一下 [物件總管]  中的 [工作階段]  。 選取 [重新整理]  來查看新的擴充事件工作階段。 工作階段旁邊的綠色圖示表示工作階段正在執行中。 紅色圖示表示工作階段已停止。

    ![新的擴充事件工作階段](media/scripting-ssms/newxevent.png)

    >[!NOTE]
    > 您可以滑鼠右鍵按一下工作階段並選取 [開始]  來開始工作階段。 不過，此為已執行 **system_health** 工作階段的複本，所以您可跳過此步驟。 您可以滑鼠右鍵按一下擴充事件工作階段的複本，並選取 [刪除]  來將其刪除。

## <a name="next-steps"></a>後續步驟

熟悉 SSMS 的最佳方式是實際練習。 這些「教學課程」  與「操作方式」  文章可協助您使用 SSMS 內所提供的各種功能。 這些文章會告訴您如何管理 SSMS 的元件及如何尋找您經常使用的功能。

* [連線至執行個體並對其進行查詢](connect-query-sql-server.md)
* [在 SSMS 中使用範本](../template/templates-ssms.md)
* [SSMS 組態](ssms-configuration.md)
* [使用 SSMS 的其他提示與訣竅](ssms-tricks.md)
