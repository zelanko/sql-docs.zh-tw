---
title: "教學課程： 啟用 5 名最慢的查詢範例 widget-SQL 作業 Studio （預覽） |Microsoft 文件"
description: "本教學課程會示範如何啟用資料庫儀表板上的五個最慢的查詢範例 widget。"
ms.custom: tools|sos
ms.date: 03/15/2018
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 78c6ad929a3eea55669e9ebdcef149e605d594ef
ms.sourcegitcommit: 3ed9be04cc7fb9ab1a9ec230c298ad2932acc71b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/17/2018
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>教學課程： 將*5 名最慢的查詢*範例資料庫儀表板的小工具

本教學課程示範的程序加入的其中一個[!INCLUDE[name-sos](../includes/name-sos-short.md)]的內建範例的 widget*資料庫儀表板*快速檢視資料庫的五個最慢的查詢。 您也了解如何檢視慢速查詢的詳細資料，以及查詢計劃使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]的功能。 在此教學課程中，您學到如何：

> [!div class="checklist"]
> * 在資料庫上啟用查詢存放區
> * 將預先建立的深入解析 widget 加入資料庫儀表板
> * 檢視資料庫的最慢的查詢的詳細資料
> * 檢視查詢執行緩慢的查詢計劃

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 包含數個深入了解 widget--現成。 本教學課程示範如何加入*查詢的資料-存放區-db-深入解析* widget 中，但步驟都基本上是相同的新增任何小工具。

## <a name="prerequisites"></a>필수 구성 요소

本教學課程需要 SQL Server 或 Azure SQL Database *TutorialDB*。 若要建立*TutorialDB*資料庫，請完成下列快速入門的其中一個：

- [連接及查詢 SQL Server 使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [連接及查詢使用 Azure SQL Database [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)



## <a name="turn-on-query-store-for-your-database"></a>針對您的資料庫開啟查詢存放區

在此範例中的 widget 需要*查詢存放區*啟用。

1. 以滑鼠右鍵按一下**TutorialDB**資料庫 (在**伺服器**[資訊看板]) 並選取**新查詢**。
2. 在查詢編輯器中，貼上下列 TRANSACT-SQL (T-SQL) 陳述式，然後按一下**執行**:

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>慢速查詢 widget 加入儀表板資料庫

若要加入*緩慢的查詢 widget*儀表板，編輯*dashboard.database.widgets*中設定您*使用者設定*檔案。

1. 開啟*使用者設定*按**Ctrl + Shift + P**開啟*命令選擇區*。
2. 型別*設定*搜尋方塊中選取**喜好設定： 開啟使用者設定**。

   ![開啟使用者設定命令](./media/tutorial-qds-sql-server/open-user-settings.png)

2. 型別*儀表板*在設定搜尋 方塊，然後找出**dashboard.database.widgets**。

   ![搜尋設定](./media/tutorial-qds-sql-server/search-settings.png)

3. 若要自訂**dashboard.database.widgets**設定您需要編輯**dashboard.database.widgets**中的項目**使用者設定**> 一節 (中的資料行右側）。 如果沒有任何**dashboard.database.widgets**中**使用者設定**區段中，將滑鼠停留在**dashboard.database.widgets**中 預設設定資料行，然後按一下文字會顯示在左邊的文字，然後按一下鉛筆圖示**複製到設定**。 如果快顯視窗中顯示**設定中取代**，但不要按 ！ 移至**使用者設定**右邊資料行並找出**dashboard.database.widgets**區段和前進至下一個步驟。

4. 在**dashboard.database.widgets**區段中，加入下列：

   ```json
        {
            "name": "slow queries widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "query-data-store-db-insight": null
            }
        },
    ```

1. 如果這是加入新的 widget 中，第一次**dashboard.database.widgets**區段應該看起來像這樣：

   ```json
   "dashboard.database.widgets": [
       {
           "name": "slow queries widget",
           "gridItemConfig": {
               "sizex": 2,
               "sizey": 1
           },
           "widget": {
               "query-data-store-db-insight": null
           }
       },
       {
           "name": "Tasks",
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 1
           },
           "widget": {
               "tasks-widget": {}
           }
       },
       {
           "gridItemConfig": {
               "sizex": 1,
               "sizey": 2
           },
           "widget": {
               "explorer-widget": {}
           }
       }
   ]
   ```

1. 按**Ctrl + S**儲存已修改**使用者設定**。

6. 開啟*資料庫儀表板*瀏覽至**TutorialDB**中**伺服器**[資訊看板] 中，按一下滑鼠右鍵，並選取**管理**。

   ![開啟儀表板](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. 深入了解 widget 會顯示在儀表板： 

   ![QDS widget](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>如需詳細資訊的 檢視深入了解詳細資料

1. 若要檢視深入了解小工具的其他資訊，請按一下 省略符號 (**...**) 正確，然後選取右上角**顯示詳細資料**。
2. 顯示多個項目的詳細資料，請選取任何項目中的**圖表資料**清單。

   ![深入了解詳細資料 對話方塊](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. 以滑鼠右鍵按一下右邊的儲存格**query_sql_txt**中**項目詳細資料**按一下**複製儲存格**。

4. 關閉**Insights**窗格。

## <a name="view-the-query-plan"></a>檢視查詢計劃 

1. 按下開啟新的查詢編輯器**Ctrl + N**。

2. 將先前步驟中的查詢文字貼到編輯器。

3. 按一下**說明**。

   ![深入了解 QDS 說明](./media/tutorial-qds-sql-server/insight-qds-explain.png)

4. 檢視查詢執行計畫：

   ![執行程序表](./media/tutorial-qds-sql-server/showplan.png)

## <a name="save-and-open-a-query-plan"></a>儲存並開啟查詢計劃 

1. 開啟 [深入了解詳細資料] 對話方塊。
2. 選取其中一個查詢項目。
2. 以滑鼠右鍵按一下**query_plan**值，並選取**複製儲存格**

   ![Insights QDS 計劃](./media/tutorial-qds-sql-server/insight-qds-plan.png)

3. 按**Ctrl + N**開啟新的編輯器。

4. 將複製的計劃貼到編輯器。

5. 按**Ctrl + S**儲存檔案，並變更的檔案副檔名*.sqlplan*。 *.sqlplan*未出現的檔案副檔名下拉式清單中，因此只要輸入中。 此教學課程中，將檔案命名*slowquery.sqlplan*。

6. 在中開啟的查詢計劃[!INCLUDE[name-sos](../includes/name-sos-short.md)]的查詢計劃檢視器：

   ![Insights QDS 計劃](./media/tutorial-qds-sql-server/sqlplan.png)


## <a name="next-steps"></a>後續的步驟
在此教學課程中，您學會如何：
> [!div class="checklist"]
> * 在資料庫上啟用查詢存放區
> * 資料庫儀表板將深入了解 widget
> * 檢視資料庫的最慢的查詢的詳細資料
> * 檢視查詢執行緩慢的查詢計劃


若要了解如何啟用**資料表空間使用量**範例深入資訊，請完成下一個教學課程：

> [!div class="nextstepaction"]
> [啟用資料表空間範例深入了解 widget](tutorial-table-space-sql-server.md)