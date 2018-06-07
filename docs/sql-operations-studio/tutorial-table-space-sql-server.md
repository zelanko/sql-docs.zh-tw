---
title: 教學課程：在 SQL Operations Studio (預覽) 中啟用資料表空間使用量範例 insight widget | Microsoft 文件
description: 本教學課程會示範如何在 SQL Operations Studio (預覽) 資料庫儀表板上啟用資料表空間使用量範例 insight widget。 
ms.custom: tools|sos
ms.date: 03/19/2018
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
ms.openlocfilehash: 3a09dd273bb005432eaf638bb88c55ff35a5bd90
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/17/2018
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>教學課程：使用 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 啟用資料表空間使用量範例 insight widget

本教學課程會示範如何在資料庫儀表板上啟用 insight widget，提供有關資料庫中所有資料表空間使用情況的概覽檢視。 在此教學課程中，您學到如何：

> [!div class="checklist"]
> * 使用內建 insight widget 範例，以快速開啟 insight widget
> * 檢視資料表空間使用量的詳細資料
> * 在 insight 圖表上篩選資料與檢視標籤詳細資料

## <a name="prerequisites"></a>必要條件

本教學課程需要 SQL Server 或 Azure SQL Database *TutorialDB*。 若要建立 *TutorialDB* 資料庫，請完成下列其中一項快速入門教學：

- [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連接及查詢 SQL Server](quickstart-sql-server.md)
- [使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] 連接及查詢 Azure SQL Database](quickstart-sql-database.md)


## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a> 在[!INCLUDE[name-sos](../includes/name-sos-short.md)] 資料庫儀表板上開啟管理 insight 
[!INCLUDE[name-sos](../includes/name-sos-short.md)] 具有內建範例小工具來監視資料庫中資料表所使用的空間。

1. 藉由按下 **Ctrl + Shift + P** 來開啟*命令選擇區*，以開啟*使用者設定*。
2. 在搜尋方塊中輸入 *settings* 並選取**喜好設定： 開啟使用者設定**。
2. 在設定搜尋輸入方塊中輸入 *dashboard*，並找出 **dashboard.database.widgets**。

3. 若要自訂 **dashboard.database.widgets** 設定，您需要在**使用者設定**區段中 (在右側資料欄) 編輯 **dashboard.database.widgets** 項目。如果沒有任何 **dashboard.database.widgets** 在**使用者設定**區段內，請將滑鼠停留在預設設定欄中的 **dashboard.database.widgets** 文字上，按一下顯示在文字左邊的鉛筆圖示，然後按一下**複製到設定**。如果快顯視窗中顯示**在設定中取代**，請不要按！移至右邊的**使用者設定**欄並找出 **dashboard.database.widgets** 區段，然後前進至下一個步驟。

4. 在**dashboard.database.widgets** 區段中，加入下列：

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
**Dashboard.database.widgets**區段看起來應該與下面的圖片相似：

   ![搜尋設定](./media/tutorial-table-space-sql-server/insight-table-space.png)

5. 按**Ctrl + S**儲存設定。

6. 以滑鼠右鍵按一下 **TutorialDB**，然後按一下**管理**，以開啟資料庫開啟儀表板。

7. 檢視如下圖所示的*資料表空間* insight widget： 

   ![小工具](./media/tutorial-table-space-sql-server/insight-table-space-result.png)


## <a name="working-with-the-insight-chart"></a>使用深入了解圖表

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 的 insight 圖表提供篩選和滑鼠停留顯示詳細資料功能。嘗試下列步驟：

1. 按一下並切換在圖表上的 *row_count* 圖例。當您切換開啟或關閉圖例時，[!INCLUDE[name-sos](../includes/name-sos-short.md)] 會顯示和隱藏資料數列。
    
2. 將滑鼠指標停留在圖表上。[!INCLUDE[name-sos](../includes/name-sos-short.md)] 會顯示如下列螢幕擷取畫面所示的資料數列標籤及其值的詳細資訊。

   ![圖表切換和圖例](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)


## <a name="next-steps"></a>後續的步驟
在此教學課程中，您學會如何：
> [!div class="checklist"]
> * 使用內建 insight widget 範例，快速開啟 insight widget。
> * 檢視資料表空間使用量的詳細資料
> * 在 insight 圖表上篩選資料與檢視標籤詳細資料

若要深入了解如何建置自訂的 insight widget，請完成下一個教學課程：

> [!div class="nextstepaction"]
> [建置自訂的 insight widget](tutorial-build-custom-insight-sql-server.md)。
