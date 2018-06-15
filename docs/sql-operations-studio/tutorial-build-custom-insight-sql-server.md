---
title: 教學課程： 在 SQL Operations Studio （預覽）中建立自訂的 insight widget |Microsoft 文件
description: 本教學課程會示範如何建置自訂的 insight widget，並將它們加入 SQL Operations Studio （預覽） 中的資料庫和伺服器儀表板。
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fe4ec372ada626ab1dd05981d9ffa3217eb46bd5
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/17/2018
ms.locfileid: "34235752"
---
# <a name="tutorial-build-a-custom-insight-widget"></a>教學課程： 建立自訂的 insight widget

本教學課程會示範如何使用您自己的 insight 查詢來建置自訂的 insight widget。

在本教學課程期間您了解如何：
> [!div class="checklist"]
> * 執行您自己的查詢和在圖表中檢視
> * 建置自訂的 insight widget 圖表
> * 將圖表加入到伺服器或資料庫儀表板
> * 新增詳細資料至您自訂的 insight widget

## <a name="prerequisites"></a>必要條件

本教學課程需要 SQL Server 或 Azure SQL Database *TutorialDB*。 若要建立 *TutorialDB* 資料庫，請完成下列其中一項快速入門教學：

- [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連接及查詢 SQL Server](quickstart-sql-server.md)
- [連接及查詢使用 Azure SQL Database [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="run-your-own-query-and-view-the-result-in-a-chart-view"></a>執行您自己的查詢，並在圖表檢視中檢視結果
在此步驟中，執行 sql 指令碼來查詢目前作用中工作階段。

1. 若要開啟新的編輯器，請按**Ctrl + N**。 

2. 變更連接內容為 **TutorialDB**。

3. 下列查詢貼入查詢編輯器中：

   ```sql
   SELECT count(session_id) as [Active Sessions]
   FROM sys.dm_exec_sessions
   WHERE status = 'running'
   ```

4. 在查詢編輯器中儲存查詢為 \*.sql 檔案。 此教學課程中，儲存為指令碼*activeSession.sql*。

5. 若要執行查詢時，請按**F5**。

6. 顯示查詢結果之後，請按一下**以圖表方式檢視**，然後按一下 [**圖表檢視器**] 索引標籤。

7. 變更**圖表類型**至**計數**。 這些設定會呈現計數圖表。

## <a name="add-the-custom-insight-to-the-database-dashboard"></a>資料庫儀表板中加入自訂的 insight

1. 若要開啟 insight widget 設定，請在*圖表檢視器*上按一下**建立 insight**:

   ![組態](./media/tutorial-build-custom-insight-sql-server/create-insight.png)
   
2. 複製 insight 設定 （JSON 資料）。 

3. 按**Ctrl + 逗號**開啟*使用者設定*。

4. 在*搜尋設定*中輸入*dashboard*。

5. 在*dashboard.database.widgets* 按一下**編輯**。

   ![儀表板設定](./media/tutorial-build-custom-insight-sql-server/dashboard-settings.png)

6. 將 insight 組態 JSON 貼上至 *dashboard.database.widgets*。 資料庫儀表板設定如下：

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

7. 儲存*使用者設定*檔案，並開啟*TutorialDB*資料庫儀表板。

   ![activesession 深入解析](./media/tutorial-build-custom-insight-sql-server/insight-activesession-dashboard.png)

## <a name="add-details-to-custom-insight"></a>新增詳細資料至自訂的 insight

1. 若要開啟新的編輯器，請按**Ctrl + N**。

2. 變更連接內容為 **TutorialDB**。

3. 下列查詢貼入查詢編輯器中：

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. 在查詢編輯器中儲存查詢為 \*.sql 檔案。 此教學課程中，儲存為指令碼*activeSessionDetail.sql*。

5. 按**Ctrl + 逗號**開啟*使用者設定*。

6. 在您的設定檔案中編輯現有*dashboard.database.widgets*節點：

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

7. 儲存*使用者設定*檔案，並開啟*TutorialDB*資料庫儀表板。 按一下*我的 Widget*旁邊的省略符號（...）按鈕以顯示詳細資料：

    ![activesession 深入解析](./media/tutorial-build-custom-insight-sql-server/insight-activesession-detail.png)

## <a name="next-steps"></a>後續步驟
在此教學課程中，您學會如何：
> [!div class="checklist"]
> * 執行您自己的查詢和在圖表中檢視
> * 建置自訂的 insight widget 圖表
> * 將圖表加入到伺服器或資料庫儀表板
> * 新增詳細資料至您自訂的 insight widget

若要瞭解如何備份和還原資料庫，請完成下一個教學課程：

> [!div class="nextstepaction"]
> [備份和還原資料庫](tutorial-backup-restore-sql-server.md)。