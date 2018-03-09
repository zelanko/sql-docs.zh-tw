---
title: "教學課程： 啟用 5 名最慢的查詢範例 widget-SQL 作業 Studio （預覽） |Microsoft 文件"
description: "本教學課程會示範如何啟用資料庫儀表板上的五個最慢的查詢範例 widget。"
ms.custom: tools|sos
ms.date: 11/16/2017
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
ms.openlocfilehash: fc30051dff2bef07ac3e7d06aa98d92d4e05e79e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>教學課程： 將*5 名最慢的查詢*範例資料庫儀表板的小工具

本教學課程示範的程序加入的其中一個[!INCLUDE[name-sos](../includes/name-sos-short.md)]的內建範例的 widget*資料庫儀表板*快速檢視資料庫的五個最慢的查詢。 您也了解如何檢視慢速查詢的詳細資料，以及查詢計劃使用[!INCLUDE[name-sos](../includes/name-sos-short.md)]的功能。 在此教學課程中，您學到如何：

> [!div class="checklist"]
> * 在資料庫上啟用查詢存放區
> * 將預先建立的深入解析 widget 加入資料庫儀表板
> * 檢視資料庫的最慢的查詢的詳細資料
> * 檢視查詢執行緩慢的查詢計劃

[!INCLUDE[name-sos](../includes/name-sos-short.md)]包含數個深入了解 widget--現成。 本教學課程示範如何加入*查詢的資料-存放區-db-深入解析* widget 中，但步驟都基本上是相同的新增任何小工具。

## <a name="prerequisites"></a>Prerequisites

本教學課程需要 SQL Server 或 Azure SQL Database *TutorialDB*。 若要建立*TutorialDB*資料庫，請完成下列快速入門的其中一個：

- [連接及查詢 SQL Server 使用[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [連接及查詢使用 Azure SQL Database[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)



## <a name="turn-on-query-store-for-your-database"></a>針對您的資料庫開啟查詢存放區

在此範例中的 widget 需要*查詢存放區*来啟用，執行下列 TRANSACT-SQL (T-SQL) 陳述式是否符合您的資料庫：

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-an-insight-widget-to-your-database-dashboard"></a>將深入了解 widget 加入儀表板資料庫

若要深入了解 widget 加入儀表板，請編輯*dashboard.database.widgets*中設定您*使用者設定*檔案。

1. 開啟*使用者設定*按**Ctrl + Shift + P**開啟*命令選擇區*。
2. 型別*設定*[搜尋] 方塊中，從可用的設定檔選取**喜好設定： 開啟使用者設定**。

   ![開啟使用者設定命令](./media/tutorial-qds-sql-server/open-user-settings.png)

2. 型別*儀表板*在設定搜尋 方塊，然後找出**dashboard.database.widgets**。

   ![搜尋設定](./media/tutorial-qds-sql-server/search-settings.png)

3. 若要自訂**dashboard.database.widgets**設定，將鉛筆圖示左邊的滑鼠停留**dashboard.database.widgets**文字、 按一下**編輯** > **複製到設定**。

4. 複製的設定之後**dashboard.database.widgets**，將游標置於行尾，左括號，按下之後**Enter**，並將類似下列的大括號 （右大括號會自動顯示）：

   ```json
   "dashboard.database.widgets": [
   {}
   ```
5. 您在大括號內的資料指標，然後按**Ctrl + 空格鍵**選取**名稱**。 
6. 完成設定小工具，讓它看起來如下：

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
        }
    ...
    ```

5. 按**Ctrl + S**儲存已修改**使用者設定**。

6. 開啟*資料庫儀表板*瀏覽至**TutorialDB**中*伺服器*[資訊看板] 中，按一下滑鼠右鍵，並選取**管理**。

   ![開啟儀表板](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. 深入了解 widget 會顯示在儀表板： 

   ![QDS widget](./media/tutorial-qds-sql-server/insight-qds-result.png)


## <a name="view-insight-details-for-more-information"></a>如需詳細資訊的 檢視深入了解詳細資料

1. 若要檢視深入了解小工具的其他資訊，請按一下 省略符號 (**...**) 正確，然後選取右上角**顯示詳細資料**。
2. 顯示多個項目的詳細資料，請選取任何項目中的**圖表資料**清單。

   ![深入了解詳細資料 對話方塊](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. 以滑鼠右鍵按一下**query_sql_txt**中**項目詳細資料**按一下**複製儲存格**。

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

5. 按**Ctrl + S**儲存檔案，並變更的檔案副檔名*.sqlplan*。 此教學課程中，將檔案命名*slowquery.sqlplan*。

6. 在中開啟的查詢計劃[!INCLUDE[name-sos](../includes/name-sos-short.md)]的查詢計劃檢視器：

   ![Insights QDS 計劃](./media/tutorial-qds-sql-server/sqlplan.png)


## <a name="next-steps"></a>後續步驟
在此教學課程中，您學會如何：
> [!div class="checklist"]
> * 在資料庫上啟用查詢存放區
> * 資料庫儀表板將深入了解 widget
> * 檢視資料庫的最慢的查詢的詳細資料
> * 檢視查詢執行緩慢的查詢計劃


若要了解如何啟用**資料表空間使用量**範例深入資訊，請完成下一個教學課程：

> [!div class="nextstepaction"]
> [啟用資料表空間範例深入了解 widget](tutorial-table-space-sql-server.md)