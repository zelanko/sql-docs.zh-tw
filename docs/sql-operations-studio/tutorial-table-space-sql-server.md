---
title: 教學課程： 啟用資料表空間使用方式範例深入了解 widget 中 SQL Operations Studio (preview) |Microsoft 文件
description: 本教學課程會示範如何啟用的資料表空間使用方式範例深入了解 widget SQL Operations Studio (preview) 資料庫儀表板上。
ms.custom: tools|sos
ms.date: 03/19/2018
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
ms.openlocfilehash: 09a1ebe6fda1baf546923887f28b51d416a80b59
ms.sourcegitcommit: 6bd21109abedf64445bdb3478eea5aaa7553fa46
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2018
---
# <a name="tutorial-enable-the-table-space-usage-sample-insight-widget-using-includename-sosincludesname-sos-shortmd"></a>教學課程： 使用情況下啟用資料表的空間使用方式範例深入了解 widget [!INCLUDE[name-sos](../includes/name-sos-short.md)]

本教學課程會示範如何啟用資料庫儀表板上，提供在摘要檢視的空間使用量的相關資料庫中的所有資料表深入了解 widget。 在此教學課程中，您學到如何：

> [!div class="checklist"]
> * 快速開啟使用內建的深入解析 widget 範例深入了解 widget
> * 檢視資料表空間使用量的詳細資料
> * 篩選資料，以及檢視標籤詳細資料，深入了解圖表上

## <a name="prerequisites"></a>必要條件

本教學課程需要 SQL Server 或 Azure SQL Database *TutorialDB*。 若要建立*TutorialDB*資料庫，請完成下列快速入門的其中一個：

- [連接及查詢 SQL Server 使用 [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-server.md)
- [連接及查詢使用 Azure SQL Database [!INCLUDE[name-sos-short](../includes/name-sos-short.md)]](quickstart-sql-database.md)


## <a name="turn-on-a-management-insight-on-includename-sosincludesname-sos-shortmds-database-dashboard"></a>開啟管理 insight 上[!INCLUDE[name-sos](../includes/name-sos-short.md)]的資料庫儀表板
[!INCLUDE[name-sos](../includes/name-sos-short.md)] 具有內建範例小工具來監視資料庫中的資料表所使用的空間。

1. 開啟*使用者設定*按**Ctrl + Shift + P**開啟*命令選擇區*。
2. 型別*設定*搜尋方塊中選取**喜好設定： 開啟使用者設定**。
2. 型別*儀表板*中設定搜尋輸入方塊，並找出**dashboard.database.widgets**。

3. 若要自訂**dashboard.database.widgets**設定您需要編輯**dashboard.database.widgets**中的項目**使用者設定**> 一節 (中的資料行右側）。 如果沒有任何**dashboard.database.widgets**中**使用者設定**區段中，將滑鼠停留在**dashboard.database.widgets**中 預設設定資料行，然後按一下文字會顯示在左邊的文字，然後按一下鉛筆圖示**複製到設定**。 如果快顯視窗中顯示**設定中取代**，但不要按 ！ 移至**使用者設定**右邊資料行並找出**dashboard.database.widgets**區段和前進至下一個步驟。

4. 在**dashboard.database.widgets**區段中，加入下列：

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
**Dashboard.database.widgets**區段看起來應該類似以下的映像：

   ![搜尋設定](./media/tutorial-table-space-sql-server/insight-table-space.png)

5. 按**Ctrl + S**儲存設定。

6. 以滑鼠右鍵按一下資料庫開啟儀表板**TutorialDB**按一下**管理**。

7. 檢視*資料表空間*深入了解 widget 圖所示： 

   ![小工具](./media/tutorial-table-space-sql-server/insight-table-space-result.png)


## <a name="working-with-the-insight-chart"></a>使用深入了解圖表

[!INCLUDE[name-sos](../includes/name-sos-short.md)]深入資訊圖提供篩選和滑鼠停留的詳細資料。 嘗試下列步驟：

1. 按一下，並切換*row_count*圖例在圖表上的。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 顯示和隱藏資料數列，如同您切換開啟或關閉圖例。
    
2. 將滑鼠指標停留在圖表中。 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 顯示資料數列標籤以及其值，如下列螢幕擷取畫面所示的詳細資訊。

   ![圖表切換和圖例](./media/tutorial-table-space-sql-server/insight-table-space-toggle.png)


## <a name="next-steps"></a>後續的步驟
在此教學課程中，您學會如何：
> [!div class="checklist"]
> * 快速開啟使用內建的深入解析 widget 範例深入了解 widget。
> * 檢視資料表空間使用量的詳細資料。
> * 篩選資料，以及檢視標籤詳細資料，深入了解圖表上

若要深入了解如何建置自訂的見解 widget，完成下一個教學課程：

> [!div class="nextstepaction"]
> [建置自訂的見解 widget](tutorial-build-custom-insight-sql-server.md)。