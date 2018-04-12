---
title: 教學課程： 建立自訂的 insight widget 中 SQL Operations Studio (preview) |Microsoft 文件
description: 本教學課程會示範如何建置自訂的 insight widget，並將它們加入 SQL Operations Studio (preview) 中的資料庫和伺服器儀表板。
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: erickangMSFT
ms.author: erickang
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 344cf021a4a0abc13fc8c531875c604095c8c0d1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="tutorial-build-a-custom-insight-widget"></a>教學課程： 建立自訂的 insight widget

本教學課程會示範如何使用您自己的深入剖析查詢來建置自訂的 insight widget。

在本教學課程期間您了解如何：
> [!div class="checklist"]
> * 執行您自己的查詢和檢視圖表中
> * 建置自訂的 insight widget 圖
> * 將圖表加入到伺服器或資料庫儀表板
> * 加入自訂的 insight widget 的詳細資料

## <a name="prerequisites"></a>必要條件

本教學課程需要 SQL Server 或 Azure SQL Database *TutorialDB*。 若要建立*TutorialDB*資料庫，請完成下列快速入門的其中一個：

- [連接及查詢 SQL Server 使用[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [連接及查詢使用 Azure SQL Database[!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="run-your-own-query-and-view-the-result-in-a-chart-view"></a>執行您自己的查詢，並在圖表檢視中檢視結果
在此步驟中，執行 sql 指令碼來查詢目前作用中工作階段。

1. 若要開啟新的編輯器，請按**Ctrl + N**。 

2. 變更的連接內容**TutorialDB**。

3. 下列查詢貼入查詢編輯器中：

   ```sql
   SELECT count(session_id) as [Active Sessions]
   FROM sys.dm_exec_sessions
   WHERE status = 'running'
   ```

4. 儲存查詢編輯器 中\*.sql 檔案。 此教學課程中，儲存為指令碼*activeSession.sql*。

5. 若要執行查詢時，請按**F5**。

6. 顯示查詢結果之後，請按一下**以圖表方式檢視**，然後按一下 [**圖表檢視器**] 索引標籤。

7. 變更**圖表類型**至**計數**。 這些設定會呈現計數圖表。

## <a name="add-the-custom-insight-to-the-database-dashboard"></a>資料庫儀表板中加入自訂的深入解析

1. 若要開啟 深入了解小工具設定，請按一下**建立深入了解**上*圖表檢視器*:

   ![組態](./media/tutorial-build-custom-insight-sql-server/create-insight.png)
   
2. 深入了解設定 （JSON 資料） 複製。 

3. 按**Ctrl + 逗號**開啟*使用者設定*。

4. 型別*儀表板*中*搜尋設定*。

5. 按一下**編輯**如*dashboard.database.widgets*。

   ![儀表板設定](./media/tutorial-build-custom-insight-sql-server/dashboard-settings.png)

6. 深入了解組態 JSON 貼上到*dashboard.database.widgets*。 資料庫儀表板設定如下：

   ```json
    "dashboard.database.widgets": [
        {
            "name": "My-Widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "insights-widget": {
                    "type": {
                        "count": {
                            "dataDirection": "vertical",
                            "dataType": "number",
                            "legendPosition": "none",
                            "labelFirstColumn": false,
                            "columnsAsLabels": false
                        }
                    },
                    "queryFile": "{your file folder}/activeSession.sql"
                }
            }
        }
    ]
   ```

7. 儲存*使用者設定*檔案，並開啟*TutorialDB*資料庫儀表板，以查看作用中工作階段 widget:

   ![activesession 深入解析](./media/tutorial-build-custom-insight-sql-server/insight-activesession-dashboard.png)

## <a name="add-details-to-custom-insight"></a>加入自訂的深入資訊的詳細資料

1. 若要開啟新的編輯器，請按**Ctrl + N**。

2. 變更的連接內容**TutorialDB**。

3. 下列查詢貼入查詢編輯器中：

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. 儲存查詢編輯器 中\*.sql 檔案。 此教學課程中，儲存為指令碼*activeSessionDetail.sql*。

5. 按**Ctrl + 逗號**開啟*使用者設定*。

6. 編輯現有*dashboard.database.widgets*設定檔案中的節點：

   ```json
    "dashboard.database.widgets": [
        {
            "name": "My-Widget",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "insights-widget": {
                    "type": {
                        "count": {
                            "dataDirection": "vertical",
                            "dataType": "number",
                            "legendPosition": "none",
                            "labelFirstColumn": false,
                            "columnsAsLabels": false
                        }
                    },
                    "queryFile": "{your file folder}/activeSession.sql",
                    "details": {
                        "queryFile": "{your file folder}/activeSessionDetail.sql",
                        "label": "SID",
                        "value": "Login Name"
                    }
                }
            }
        }
    ]
   ```

7. 儲存*使用者設定*檔案，並開啟*TutorialDB*資料庫儀表板。 按一下省略符號 （...） 按鈕旁的 *我 Widget*以顯示詳細資料：

    ![activesession 深入解析](./media/tutorial-build-custom-insight-sql-server/insight-activesession-detail.png)

## <a name="next-steps"></a>後續步驟
在此教學課程中，您學會如何：
> [!div class="checklist"]
> * 執行您自己的查詢和檢視圖表中
> * 建置自訂的 insight widget 圖表
> * 將圖表加入到伺服器或資料庫儀表板
> * 加入自訂的 insight widget 的詳細資料

若要瞭解如何備份和還原資料庫，請完成下一個教學課程：

> [!div class="nextstepaction"]
> [備份和還原資料庫](tutorial-backup-restore-sql-server.md)。