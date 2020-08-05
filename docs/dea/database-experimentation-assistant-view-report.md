---
title: 查看 SQL Server 升級的分析報表
description: 瞭解如何在資料庫測試助理 (DEA) 中查看及瞭解效能深入解析的分析報表。
ms.custom: seo-lt-2019
ms.date: 02/04/2020
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.openlocfilehash: 5850f3f78590b5ceccea49033b401055180d715e
ms.sourcegitcommit: b80364e31739d7b08cc388c1f83bb01de5dd45c1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87565487"
---
# <a name="view-analysis-reports-in-database-experimentation-assistant"></a>查看資料庫測試助理中的分析報表

當您使用資料庫測試助理 (DEA) [建立分析報表](database-experimentation-assistant-create-report.md)之後，就可以根據您執行的 A/B 測試來檢查效能深入解析的報表。

## <a name="open-an-existing-analysis-report"></a>開啟現有的分析報表

1. 在 [DEA] 中，選取清單圖示、指定伺服器名稱和驗證類型、選取或取消選取適用于您案例的 [**加密**連線] 和 [**信任伺服器憑證**] 核取方塊，然後選取 **[連線]**。

   ![使用報表連接到伺服器](./media/database-experimentation-assistant-view-report/dea-connect-to-server-with-report-files.png)

2. 在 [**分析報表**] 畫面左側，選取您想要查看的報表專案。

   ![開啟現有的報表檔案](./media/database-experimentation-assistant-view-report/dea-select-report-to-view.png)

## <a name="view-and-understand-the-analysis-report"></a>查看並瞭解分析報表

本節會引導您完成分析報告。

在報表的第一頁上，會顯示執行實驗之目標伺服器的版本和組建資訊的相關資訊。 閾值可讓您調整 A/B 測試分析的敏感度或承受度。 預設會將閾值設為 5%;任何 >= 5% 的效能改進都會分類為「改良」。  下拉式清單可讓您以不同的效能閾值評估報表。

您可以將報表中的資料匯出至 CSV 檔案，然後選取 [**匯出**] 按鈕。  在 [分析] 報表的任何頁面上，您可以選取 [**列印**]，以列印當時畫面上可見的內容。

### <a name="query-distribution"></a>查詢散發

- 選取圓形圖的不同配量，只顯示屬於該類別目錄的查詢。

   ![以圓形圖配量形式的報表類別](./media/database-experimentation-assistant-view-report/dea-view-report-pie-slices.png)

  - **降級**：在目標2上執行比目標1更差的查詢。
  - **錯誤**：在至少一個目標上顯示至少有一次錯誤的查詢。
  - **改良**：在目標2上執行的查詢比目標1更好。
  - **無法評估**：取樣大小太小的查詢，無法進行統計分析。 針對 A/B 測試分析，DEA 需要相同的查詢，才能在每個目標上至少執行15次。
  - **相同**：目標1和目標2之間沒有統計差異的查詢。

  錯誤查詢（如果有的話）會顯示在不同的圖表中;橫條圖會依類型分類錯誤，並以圓形圖分類錯誤識別碼的圖表。

   ![錯誤查詢圖表](./media/database-experimentation-assistant-view-report/dea-error-query-charts.png)

  有四種可能的錯誤類型：

  - **現有的錯誤**：存在於目標1和目標2的錯誤。
  - **新的錯誤**：目標2上的新錯誤。
  - **已解決的錯誤**：目標1上存在但在目標2上的錯誤已解決。
  - **升級**封鎖程式：封鎖升級至目標伺服器的錯誤。

  按一下圖表中的任何橫條或圓形圖區段會向下切入類別目錄，並顯示效能計量，即使 [**無法評估**] 類別也一樣。

  此外，儀表板會顯示前五個改良和下降的查詢，以提供快速的效能總覽。

### <a name="individual-query-drill-down"></a>個別查詢向下切入

您可以選取 [查詢範本] 連結，以取得特定查詢的詳細資訊。

![向下切入到特定查詢](./media/database-experimentation-assistant-view-report/dea-query-drill-down-report.png)

- 選取特定的查詢，以開啟相關的比較摘要。

   ![比較摘要](./media/database-experimentation-assistant-view-report/dea-view-report-comparison-summary.png)

   您可以尋找該查詢的摘要統計資料，例如執行次數、平均持續時間、平均 CPU、平均讀取/寫入和錯誤計數。  如果查詢是錯誤查詢，[**錯誤資訊**] 索引標籤會顯示有關錯誤的詳細資料。  在 [**查詢計劃資訊**] 索引標籤上，您可以找到用於 [目標 1] 和 [目標 2] 查詢之查詢計劃的相關資訊。

   > [!NOTE]
   > 如果您要分析擴充事件 (。.XEL) 檔案，不會收集查詢計劃資訊來限制使用者電腦上的記憶體壓力。

## <a name="see-also"></a>另請參閱

- 若要瞭解如何在命令提示字元中產生分析報告，請參閱[在命令提示](database-experimentation-assistant-run-command-prompt.md)字元中執行。
