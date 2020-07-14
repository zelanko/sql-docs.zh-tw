---
title: 啟用五個最慢速查詢範例小工具
description: 本教學課程示範如何在資料庫儀表板上啟用五個最慢速查詢範例小工具。
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18; seo-lt-2019
ms.date: 06/01/2020
ms.openlocfilehash: f4e8e76583a90ce64a9f99ef3c94875b2c1fc6dd
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774541"
---
# <a name="tutorial-add-the-five-slowest-queries-sample-widget-to-the-database-dashboard"></a>教學課程：將「五個最慢速查詢」範例小工具新增至資料庫儀表板

此教學課程所示範的程序可將其中一個內建的 Azure Data Studio 範例小工具新增至「資料庫儀表板」，以快速檢視資料庫的五個最慢速查詢。 您也將了解如何使用 Azure Data Studio 功能，來檢視慢速查詢和查詢計劃的詳細資料。 在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 在資料庫上啟用查詢存放區
> * 將預先建置的深入解析小工具新增至資料庫儀表板
> * 檢視資料庫最慢速查詢的詳細資料
> * 檢視慢速查詢的查詢執行計畫

Azure Data Studio 包含數個現成的見解小工具。 本教學課程示範如何新增 *query-data-store-db-insight* 小工具，但步驟基本上與新增所有小工具相同。

## <a name="prerequisites"></a>必要條件

本教學課程需要 SQL Server 或 Azure SQL Database *TutorialDB*。 若要建立 *TutorialDB* 資料庫，請完成下列任一項快速入門：

* [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連線及查詢 SQL Server](quickstart-sql-server.md)

* [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連線及查詢 Azure SQL Database](quickstart-sql-database.md)

## <a name="turn-on-query-store-for-your-database"></a>為資料庫開啟查詢存放區

此範例中的小工具需要啟用 [查詢存放區]。

1. 以滑鼠右鍵按一下 [TutorialDB] 資料庫 (在 [伺服器] 提要欄位中)，然後選取 [新增查詢]。

2. 將下列 Transact-SQL (T-SQL) 陳述式貼到查詢編輯器，然後按一下 [執行]：

   ```sql
    ALTER DATABASE TutorialDB SET QUERY_STORE = ON
   ```

## <a name="add-the-slow-queries-widget-to-your-database-dashboard"></a>將慢速查詢小工具新增至資料庫儀表板

若要將「慢速查詢小工具」新增至儀表板，請編輯 [使用者設定] 檔案中的 *dashboard.database.widgets* 設定。

1. 按 **Ctrl+Shift+P** 開啟 [命令選擇區]，開啟 [使用者設定]。

2. 在搜尋方塊中鍵入 *settings*，然後選取 [Preferences:Open User Settings] \(喜好設定: 開啟使用者設定\)。

   ![開啟使用者設定命令](./media/tutorial-qds-sql-server/open-user-settings.png)

3. 在設定搜尋方塊中鍵入 *dashboard*，然後尋找 **dashboard.database.widgets**，接著按一下 [*在 settings.json 中編輯*]。

   ![搜尋設定](./media/tutorial-qds-sql-server/search-settings.png)

4. 在 settings.json 中新增下列程式碼：

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

5. 按 **Ctrl+S** 儲存修改的 [使用者設定]。

6. 巡覽至 [伺服器] 提要欄位中的 [TutorialDB]，然後選取 [管理]，開啟 [資料庫儀表板]。

   ![開啟儀表板](./media/tutorial-qds-sql-server/insight-open-dashboard.png)

7. 深入解析小工具隨即出現在儀表板上：

   ![QDS 小工具](./media/tutorial-qds-sql-server/insight-qds-result.png)

## <a name="view-insight-details-for-more-information"></a>如需詳細資訊，請檢視深入解析詳細資料

1. 若要檢視深入解析小工具的其他資訊，請按一下右上方的省略符號 ([...])，然後選取 [顯示詳細資料]。

2. 若要顯示項目的更多詳細資料，請選取 [圖表資料] 清單中的任意項目。

   ![深入解析詳細資料對話方塊](./media/tutorial-qds-sql-server/insight-details-dialog.png)

3. 關閉 [深入解析] 窗格。

## <a name="view-the-query-plan"></a>檢視查詢計劃

1. 以滑鼠右鍵按一下 [TutorialDB] 資料庫，然後選取 [管理]

2. 在 [緩慢查詢小工具] 中，若要檢視見解小工具的其他資訊，請按一下右上方的省略符號 ([...])，然後選取 [執行查詢]。

    ![執行查詢](media/tutorial-qds-sql-server/run-query.png)

3. 現在您應該會看到具有結果的新查詢視窗。

    ![執行查詢結果](media/tutorial-qds-sql-server/run-query-results.png)

4. 按一下 [解說]。

   ![深入解析 QDS 解說](./media/tutorial-qds-sql-server/insight-qds-explain.png)

5. 檢視查詢的執行計畫：

   ![執行程序表](./media/tutorial-qds-sql-server/showplan.png)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：
> [!div class="checklist"]
> * 在資料庫上啟用查詢存放區
> * 將深入解析小工具新增至資料庫儀表板
> * 檢視資料庫最慢速查詢的詳細資料
> * 檢視慢速查詢的查詢執行計畫

若要了解如何啟用**資料表空間使用量**範例深入解析，請完成下一個教學課程：

> [!div class="nextstepaction"]
> [啟用資料表空間範例深入解析小工具](tutorial-table-space-sql-server.md)