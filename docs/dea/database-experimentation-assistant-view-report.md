---
title: 檢視分析中的報告資料庫測試助理 」 進行 SQL Server 升級
description: 檢視分析報告，在 資料庫測試助理
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
manager: jroth
ms.openlocfilehash: da99a24ab6729e78220aeed3d18819e7b075603f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794438"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>檢視分析報告，在 資料庫測試助理

之後您[建立您的分析報表](database-experimentation-assistant-create-report.md)中資料庫測試助理 (DEA)，完成本文，以檢視報表，並獲得您的所提供的效能深入解析中所述的步驟 / B 測試。

## <a name="select-a-server"></a>選取伺服器

在 DEA，選取 [功能表] 圖示。 在展開的功能表中，選取**分析報表**檢查清單圖示，以開啟分析報告 視窗旁邊。

底下**分析報表**，輸入執行分析的資料庫的 SQL Server 的電腦名稱。 選取 [連接]  。 

![連接到現有的報表](./media/database-experimentation-assistant-view-report/dea-view-report-connect.png)

如果遺失的任何相依性**必要條件**頁面會提示您安裝它們的連結。 安裝的必要條件，然後按**再試一次**。

![元件頁面](./media/database-experimentation-assistant-view-report/dea-view-report-prereq.png)

## <a name="select-an-analysis-report-to-view"></a>選取要檢視分析報告

在分析報表清單中，按兩下以開啟報表。

![檢視現有的報表](./media/database-experimentation-assistant-view-report/dea-view-report-view-existing.png)

您可以深入程度即代表您的工作負載，此圖表的範例所示：

![工作負載 Rep 圖表](./media/database-experimentation-assistant-view-report/dea-view-report-workload-compare.png)

## <a name="view-and-understand-the-analysis-report"></a>檢視並了解分析報表

本節將引導您透過 [分析] 報表。

### <a name="query-categories"></a>查詢類別目錄

選取不同的配量的左邊的圓形圖，可顯示屬於該類別的查詢。

![報表圓形圖配量](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

- **降低查詢**:優良，A 在 b 中的查詢  
- **錯誤**:顯示錯誤，在執行個體 B，但不是在執行個體 a 中的查詢  
- **改善查詢**:好在執行與的執行個體 B 執行個體 a 中的查詢  
- **不確定查詢**:查詢具有不定的效能變更。  
- **相同**:查詢中的效能條件維持相同執行個體 A 和 b。

### <a name="individual-query-drill-down"></a>個別查詢向下鑽研

您可以選取查詢範本會連結以查看特定查詢的詳細的資訊。

![查詢向下鑽研](./media/database-experimentation-assistant-view-report/dea-view-report-drilldown.png)

選取特定的查詢，以開啟摘要查詢的比較。

![比較摘要](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

您可以看到 A 和 B 的執行個體上執行的查詢。 您也可以查看的查詢可能如下所示的範本。 資料表會顯示查詢資訊的特定執行個體 A 和 b。

### <a name="error-queries"></a>錯誤查詢

比較摘要報表中包含可展開**錯誤資訊**並**查詢計劃資訊**區段。 區段會顯示錯誤，並規劃這兩個執行個體的資訊。

選取要顯示這些錯誤類型的錯誤 （紅色） 圓形圖：
- **現有錯誤**:已在 a 中的錯誤
- **新的錯誤**:已在 b 中的錯誤
- **解決錯誤**:已 A 中，但不是在 b 中的錯誤

![錯誤圖表](./media/database-experimentation-assistant-view-report/dea-view-report-error-charts.png)

## <a name="next-steps"></a>後續步驟

- 若要了解如何產生分析報表的命令提示字元，請參閱[命令提示字元執行](database-experimentation-assistant-run-command-prompt.md)。

- 如需 19 分鐘簡介 DEA 和示範，觀看下列影片：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
