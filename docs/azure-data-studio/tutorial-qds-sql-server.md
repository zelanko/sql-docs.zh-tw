---
title: 教學課程： 啟用 5 名最慢的查詢範例小工具-Azure Data Studio |Microsoft Docs
description: 本教學課程會示範如何啟用資料庫儀表板上的五個最慢的查詢範例 widget。
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 75886c26b7ceff9df9e2fc96f76038e8d6e70dd0
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356239"
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>教學課程： 新增*五個最慢的查詢*資料庫儀表板的範例小工具

本教學課程會示範將其中一個程序[!INCLUDE[name-sos](../includes/name-sos-short.md)]的內建範例的 widget *database 儀表板*快速檢視資料庫的五個最慢的查詢。 您也了解如何檢視查詢速度緩慢的詳細資料和查詢計劃使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]的功能。 在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 在資料庫上啟用查詢存放區
> * 將預先建置的深入解析小工具新增至資料庫儀表板
> * 檢視資料庫的最慢的查詢的詳細資料
> * 檢視查詢速度緩慢的查詢執行計畫

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 包含數個深入解析小工具--蜪鎏。 本教學課程示範如何新增*查詢的資料-存放區-db-深入了解* widget 中，但步驟都基本上是相同的新增任何小工具。

## <a name="prerequisites"></a>必要條件

本教學課程需要 SQL Server 或 Azure SQL Database *TutorialDB*。 若要建立 *TutorialDB* 資料庫，請完成下列其中一項快速入門教學：

- [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連接及查詢 SQL Server](quickstart-sql-server.md)
- [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連接及查詢 Azure SQL Database](quickstart-sql-database.md)



## <a name="turn-on-query-store-for-your-database"></a>開啟查詢存放區，為您的資料庫

在此範例中的小工具需要*查詢存放區*啟用。

1. 以滑鼠右鍵按一下**TutorialDB**資料庫 (在**伺服器**資訊看板)，然後選取**新查詢**。
2. 在查詢編輯器中貼上下列 TRANSACT-SQL (T-SQL) 陳述式，然後按一下**執行**:

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>將查詢速度緩慢的小工具新增至資料庫儀表板

新增*緩慢查詢 widget*到您的儀表板中，編輯*dashboard.database.widgets*中設定您*使用者設定*檔案。

1. 藉由按下 **Ctrl + Shift + P** 來開啟*命令選擇區*，以開啟*使用者設定*。
2. 在搜尋方塊中輸入 *settings* 並選取**喜好設定： 開啟使用者設定**。

   ![開啟使用者設定 命令](./media/tutorial-qds-sql-server/open-user-settings.png)

2. 型別*儀表板*在設定搜尋 方塊，然後找出**dashboard.database.widgets**。

   ![搜尋設定](./media/tutorial-qds-sql-server/search-settings.png)

3. 若要自訂 **dashboard.database.widgets** 設定，您需要在**使用者設定**區段中 (在右側資料欄) 編輯 **dashboard.database.widgets** 項目。 如果沒有任何 **dashboard.database.widgets** 在**使用者設定**區段內，請將滑鼠停留在預設設定欄中的 **dashboard.database.widgets** 文字上，按一下顯示在文字左邊的鉛筆圖示，然後按一下**複製到設定**。 如果快顯視窗中顯示**在設定中取代**，請不要按！ 移至右邊的**使用者設定**欄並找出 **dashboard.database.widgets** 區段，然後前進至下一個步驟。

4. 在  **dashboard.database.widgets**區段中，新增下列：

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

1. 按下**Ctrl + S**若要儲存已修改**使用者設定**。

6. 開啟*資料庫儀表板*瀏覽至**TutorialDB**中**伺服器**提要欄位中，按一下滑鼠右鍵，然後選取**管理**。

   ![開啟儀表板](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. 深入解析小工具會出現在儀表板： 

   ![QDS 小工具](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>如需詳細資訊的 檢視深入解析詳細資料

1. 若要檢視深入解析小工具的其他資訊，請按一下 省略符號 (**...**)，然後選取右上角**顯示詳細資料**。
2. 若要顯示的項目更多詳細資料，請選取 中的任何項目**圖表資料**清單。

   ![了解詳細資料 對話方塊](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. 以滑鼠右鍵按一下右邊的儲存格**query_sql_txt**中**項目詳細資料**然後按一下**複製儲存格**。

4. 關閉**Insights**窗格。

## <a name="view-the-query-plan"></a>檢視查詢計劃 

1. 按下 **Ctrl + N** 開啟新的查詢編輯器。

2. 先前步驟中的查詢文字貼入編輯器中。

3. 按一下 **說明**。

   ![深入解析 QDS 說明](./media/tutorial-qds-sql-server/insight-qds-explain.png)

4. 檢視查詢的執行計畫：

   ![執行程序表](./media/tutorial-qds-sql-server/showplan.png)

## <a name="save-and-open-a-query-plan"></a>儲存並開啟的查詢計劃 

1. 開啟深入解析的詳細資料 對話方塊。
2. 選取其中一個查詢項目。
2. 以滑鼠右鍵按一下**query_plan**值並選取**複製儲存格**

   ![Insights QDS 計劃](./media/tutorial-qds-sql-server/insight-qds-plan.png)

3. 按下**Ctrl + N**開啟新的編輯器。

4. 貼到編輯器中複製的計劃。

5. 按下**Ctrl + S**儲存檔案，並變更副檔名 *.sqlplan*。 *.sqlplan*未出現在檔案延伸模組的下拉式清單中，因此只要輸入中。 本教學課程中，將檔案命名*slowquery.sqlplan*。

6. 在中開啟的查詢計劃[!INCLUDE[name-sos](../includes/name-sos-short.md)]的查詢計劃檢視器：

   ![Insights QDS 計劃](./media/tutorial-qds-sql-server/sqlplan.png)


## <a name="next-steps"></a>後續的步驟
在本教學課程中，您已了解如何：
> [!div class="checklist"]
> * 在資料庫上啟用查詢存放區
> * 將深入解析小工具新增至資料庫儀表板
> * 檢視資料庫的最慢的查詢的詳細資料
> * 檢視查詢速度緩慢的查詢執行計畫


若要了解如何啟用**資料表空間使用量**範例深入解析，請完成下一個教學課程：

> [!div class="nextstepaction"]
> [啟用資料表空間範例深入解析小工具](tutorial-table-space-sql-server.md)
