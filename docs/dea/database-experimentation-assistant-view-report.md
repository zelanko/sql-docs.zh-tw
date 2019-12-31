---
title: 查看 SQL Server 升級的分析報表
description: 查看資料庫測試助理中的分析報表
ms.custom: seo-lt-2019
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: b72d49e691311104481637ff49d6c1e09ae0c230
ms.sourcegitcommit: 9e026cfd9f2300f106af929d88a9b43301f5edc2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74317746"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>查看資料庫測試助理中的分析報表

當您使用資料庫測試助理（DEA）[建立分析報表](database-experimentation-assistant-create-report.md)之後，請使用下列步驟來根據您的 A/B 測試來檢查效能深入解析的報表。

## <a name="select-a-server"></a>選取伺服器

在 [DEA] 中，選取功能表圖示。 在展開的功能表中，選取檢查清單圖示旁的 [**分析報表**]，開啟 [分析報表] 視窗。

在 [**分析報表**] 底下，輸入執行 SQL Server 具有分析資料庫的電腦名稱稱，然後選取 **[連接]**。

![連接到現有的報表](./media/database-experimentation-assistant-view-report/dea-view-report-connect.png)

如果您遺漏任何相依性，[**必要條件**] 頁面會提示您安裝它們的連結。 如有必要，請安裝必要條件，然後選取 [**再試一次**]。

![必要條件頁面](./media/database-experimentation-assistant-view-report/dea-view-report-prereq.png)

## <a name="select-an-analysis-report-to-view"></a>選取要查看的分析報表

在分析報表清單中，按兩下報表加以開啟。

![查看現有的報表](./media/database-experimentation-assistant-view-report/dea-view-report-view-existing.png)

您可以深入瞭解您的工作負載的呈現程度，如下列範例圖表所示：

![工作負載代表圖表](./media/database-experimentation-assistant-view-report/dea-view-report-workload-compare.png)

## <a name="view-and-understand-the-analysis-report"></a>查看並瞭解分析報表

本節會引導您完成分析報告。

### <a name="query-categories"></a>查詢類別目錄

選取左側圓形圖的不同配量，僅顯示落在該類別之下的查詢。

![報表圓形圖磁區](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

- **降級的查詢**：在中執行效能較佳的查詢，而不是 B。  
- **錯誤**：顯示實例 B 中的錯誤，但不在實例 A 中的查詢。  
- **改良的查詢**：在實例 B 中執行效能比在實例 A 中更好的查詢。  
- **不定查詢**：具有不定效能變更的查詢。  
- **相同**：實例 A 和 B 之間的效能維持不變的查詢。

### <a name="individual-query-drill-down"></a>個別查詢向下切入

您可以選取查詢範本連結，以查看更多關於特定查詢的詳細資訊。

![查詢向下切入](./media/database-experimentation-assistant-view-report/dea-view-report-drilldown.png)

選取特定的查詢，以開啟查詢的比較摘要。

![比較摘要](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

您可以看到查詢執行所在的 A 和 B 實例。 您也可以看到查詢可能的樣子範本。 資料表會顯示實例 A 和 B 特有的查詢資訊。

### <a name="error-queries"></a>錯誤查詢

比較摘要報表具有可擴充的**錯誤資訊**和**查詢計劃資訊**區段。 這些區段會顯示這兩個實例的錯誤和計畫資訊。

選取 [錯誤（紅色）] 圓形圖以顯示這些類型的錯誤：

- **現有的錯誤**：中的錯誤。
- **新的錯誤**： B 中的錯誤。
- **已解決的錯誤**：中的錯誤，但不在 B 中。

![錯誤圖表](./media/database-experimentation-assistant-view-report/dea-view-report-error-charts.png)

## <a name="see-also"></a>另請參閱

- 若要瞭解如何在命令提示字元中產生分析報告，請參閱[在命令提示](database-experimentation-assistant-run-command-prompt.md)字元中執行。
