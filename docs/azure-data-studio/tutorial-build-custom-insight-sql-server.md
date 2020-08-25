---
title: 教學課程：建置自訂深入解析小工具
description: 本教學課程示範如何建置自訂深入解析小工具，並新增至 Azure Data Studio 中的資料庫和伺服器儀表板。
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: efe6473dc716b8e8a2c70349b98e6433105d401a
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/21/2020
ms.locfileid: "88745751"
---
# <a name="tutorial-build-a-custom-insight-widget"></a>教學課程：建置自訂深入解析小工具

本教學課程示範如何使用您自己的深入解析查詢，建置自訂深入解析小工具。

在本教學課程中，您將了解如何：
> [!div class="checklist"]
> * 執行您自己的查詢並在圖表中檢視
> * 從圖表建置自訂深入解析小工具
> * 將圖表新增至伺服器或資料庫儀表板
> * 將詳細資料新增至您的自訂深入解析小工具

## <a name="prerequisites"></a>Prerequisites

本教學課程需要 SQL Server 或 Azure SQL Database *TutorialDB*。 若要建立 *TutorialDB* 資料庫，請完成下列任一項快速入門：

- [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連線及查詢 SQL Server](quickstart-sql-server.md)
- [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連線及查詢 Azure SQL Database](quickstart-sql-database.md)


## <a name="run-your-own-query-and-view-the-result-in-a-chart-view"></a>執行您自己的查詢並在圖表檢視中檢視結果
在此步驟中，您會執行 SQL 指令碼查詢目前使用中的工作階段。

1. 若要開啟新的編輯器，請按 **Ctrl+N**。 

2. 將連線內容變更為 **TutorialDB**。

3. 將下列查詢貼到查詢編輯器：

   ```sql
   SELECT count(session_id) as [Active Sessions]
   FROM sys.dm_exec_sessions
   WHERE status = 'running'
   ```

4. 在編輯器中將查詢儲存為 \*.sql 檔案。 在本教學課程中，將指令碼儲存為 *activeSession.sql*。

5. 若要執行查詢，請按 **F5**。

6. 顯示查詢結果之後，按一下 [View as Chart] \(以圖表檢視\)  ，然後按一下 [Chart Viewer] \(圖表檢視器\)  索引標籤。

7. 將 [圖表類型]  變更為 [計數]  。 這些設定會呈現計數圖表。

## <a name="add-the-custom-insight-to-the-database-dashboard"></a>將自訂深入解析新增至資料庫儀表板

1. 若要開啟深入解析小工具設定，請在 [Chart Viewer] \(圖表檢視器\)  上按一下 [Create Insight] \(建立深入解析\)  ：

   ![組態](./media/tutorial-build-custom-insight-sql-server/create-insight.png)
   
2. 複製深入解析設定 (JSON 資料)。 

3. 按 **Ctrl+Comma** 開啟 [使用者設定]  。

4. 在 [搜尋設定]  中鍵入 *dashboard*。

5. 對 *dashboard.database.widgets* 按一下 [編輯]  。

   ![儀表板設定](./media/tutorial-build-custom-insight-sql-server/dashboard-settings.png)

6. 將深入解析設定 JSON 貼到 *dashboard.database.widgets*。 資料庫儀表板設定如下所示：

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

7. 儲存 [使用者設定]  檔案，然後開啟 *TutorialDB* 資料庫儀表板，查看使用中的工作階段小工具：

   ![使用中的工作階段深入解析](./media/tutorial-build-custom-insight-sql-server/insight-activesession-dashboard.png)

## <a name="add-details-to-custom-insight"></a>將詳細資料新增至自訂深入解析

1. 若要開啟新的編輯器，請按 **Ctrl+N**。

2. 將連線內容變更為 **TutorialDB**。

3. 將下列查詢貼到查詢編輯器：

   ```sql
    SELECT session_id AS [SID], login_time AS [Login Time], host_name AS [Host Name], program_name AS [Program Name], login_name AS [Login Name]
    FROM sys.dm_exec_sessions
    WHERE status = 'running'
   ```

4. 在編輯器中將查詢儲存為 \*.sql 檔案。 在本教學課程中，將指令碼儲存為 *activeSessionDetail.sql*。

5. 按 **Ctrl+Comma** 開啟 [使用者設定]  。

6. 在您的設定檔中編輯現有的 *dashboard.database.widgets* 節點：

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

7. 儲存 [使用者設定]  檔案，然後開啟 *TutorialDB* 資料庫儀表板。 按一下 *My-Widget* 旁的省略符號 (...) 按鈕，顯示詳細資料：

    ![使用中的工作階段深入解析](./media/tutorial-build-custom-insight-sql-server/insight-activesession-detail.png)

## <a name="next-steps"></a>後續步驟
在本教學課程中，您已了解如何：
> [!div class="checklist"]
> * 執行您自己的查詢並在圖表中檢視
> * 從圖表建置自訂深入解析小工具
> * 將圖表新增至伺服器或資料庫儀表板
> * 將詳細資料新增至您的自訂深入解析小工具

若要了解如何備份及還原資料庫，請完成下一個教學課程：

> [!div class="nextstepaction"]
> [備份及還原資料庫](tutorial-backup-restore-sql-server.md)。
