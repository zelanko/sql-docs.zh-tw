---
title: 教學課程：啟用資料表空間使用量範例深入解析小工具
titleSuffix: Azure Data Studio
description: 本教學課程示範如何在 Azure Data Studio 資料庫儀表板上，啟用資料表空間使用量範例深入解析小工具。
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/10/2019
ms.openlocfilehash: 4b44fc9dbee773e7bc88daecf9142c1f826d65a0
ms.sourcegitcommit: dacf6c57f6a2e3cf2005f3268116f3c609639905
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/11/2019
ms.locfileid: "70878633"
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>教學課程：使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 啟用資料表空間使用量範例深入解析小工具

本教學課程示範如何在資料庫儀表板上啟用深入解析小工具，提供資料庫中所有資料表空間使用量的摘要檢視。 在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 使用內建深入解析小工具範例，快速開啟深入解析小工具
> * 檢視資料表空間使用量的詳細資料
> * 在深入解析圖表上篩選資料並檢視標籤詳細資料

## <a name="prerequisites"></a>Prerequisites

本教學課程需要 SQL Server 或 Azure SQL Database *TutorialDB*。 若要建立 *TutorialDB* 資料庫，請完成下列任一項快速入門：

* [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連線及查詢 SQL Server](quickstart-sql-server.md)
* [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連線及查詢 Azure SQL Database](quickstart-sql-database.md)

## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>在 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 的資料庫儀表板上開啟管理深入解析

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 內建範例小工具，可監視資料庫中資料表所使用的空間。

1. 按 **Ctrl+Shift+P** 開啟 [命令選擇區]  ，以開啟 [使用者設定]  。

2. 在搜尋方塊中鍵入 *settings*，然後選取 [Preferences:**Open User Settings] \(喜好設定: 開啟使用者設定\)** 。

3. 在 [設定搜尋] 輸入方塊中鍵入 *dashboard*，然後尋找 **dashboard.database.widgets**。

4. 若要自訂 **dashboard.database.widgets** 設定，您需要編輯 [使用者設定]  區段中的 **dashboard.database.widgets** 項目。

   ![搜尋設定](media/tutorial-table-space-sql-server/search-settings.png)

   如果 [使用者設定]  區段中沒有 **dashboard.database.widgets**，請將滑鼠移至 [預設設定] 資料行中的 **dashboard.database.widgets** 文字上方，然後按一下出現在文字左邊的*齒輪*圖示，並按一下 [複製為設定 JSON]  。 如果快顯視窗顯示 [在設定中取代]  ，請勿點選！ 移至右方的 [使用者設定]  資料行並尋找 **dashboard.database.widgets** 區段，然後繼續進行下一個步驟。

5. 在 **dashboard.database.widgets** 區段中，新增下列幾行：

   ```json
        {
            "name": "Space Used by Tables",
            "gridItemConfig": {
                "sizex": 2,
                "sizey": 1
            },
            "widget": {
                "table-space-db-insight": null
            }
        },
    ```

   **dashboard.database.widgets** 區段應該如下圖所示：

    ![搜尋設定](./media/tutorial-table-space-sql-server/insight-table-space.png)

6. 按 **Ctrl+S** 儲存設定。

7. 以滑鼠右鍵按一下 [TutorialDB]  ，然後按一下 [管理]  ，開啟資料庫儀表板。

8. 檢視「資料表空間」  深入解析小工具，如下圖所示：

   ![小工具](./media/tutorial-table-space-sql-server/insight-table-space-result.png)

## <a name="working-with-the-insight-chart"></a>運用深入解析圖表

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 的深入解析圖表提供篩選和滑鼠暫留詳細資料。 若要嘗試下列步驟：

1. 按一下並切換圖表上的 *row_count* 圖例。 當您開啟或關閉圖例時，[!INCLUDE[name-sos](../includes/name-sos-short.md)] 會顯示和隱藏資料數列。

2. 將滑鼠指標移至圖表上方。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 顯示資料數列標籤及其值的詳細資訊，如以下螢幕擷取畫面所示。

   ![圖表切換和圖例](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：
> [!div class="checklist"]
> * 使用內建深入解析小工具範例，快速開啟深入解析小工具。
> * 檢視資料表空間使用量的詳細資料。
> * 在深入解析圖表上篩選資料並檢視標籤詳細資料

若要了解如何建置自訂深入解析小工具，請完成下一個教學課程：

> [!div class="nextstepaction"]
> [建置自訂深入解析小工具](tutorial-build-custom-insight-sql-server.md)
