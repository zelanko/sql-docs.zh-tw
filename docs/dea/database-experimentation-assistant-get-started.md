---
title: SQL Server 升級的資料庫測試助理入門
description: 開始使用資料庫測試助理
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
ms.openlocfilehash: 9fe162b2a9bc0db4a2a49648eecb76c5802f57c0
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381766"
---
# <a name="get-started-with-database-experimentation-assistant"></a>開始使用資料庫測試助理

資料庫測試助理（DEA）是一個/B 測試解決方案，適用于 SQL Server 環境中的變更，例如升級或新的索引。 DEA 可協助您評估來源伺服器上的工作負載（在目前的環境中）如何在您的新環境中執行。 DEA 會藉由完成三個步驟，引導您執行 A/B 測試： 

- 擷取
- 重播
- 分析

本文會引導您完成這些步驟。

## <a name="capture"></a>擷取

SQL Server A/B 測試的第一個步驟是在來源伺服器上捕捉追蹤。 來源伺服器通常是實際執行伺服器。 追蹤檔案會在該伺服器上捕捉整個查詢工作負載，包括時間戳記。 之後，會在目標伺服器上重新執行此追蹤以進行分析。 分析報表可讓您深入瞭解兩個目標伺服器之間工作負載的效能差異。

考量因素：

- 開始追蹤捕捉之前，請確定您已備份要從中捕獲追蹤的資料庫。
- DEA 使用者必須設定為使用 Windows 驗證連接到資料庫。
- SQL Server 的服務帳戶需要存取來源追蹤檔案路徑。
- 若要讓 DEA 判斷查詢的效能是否已改善或降級，該查詢在捕獲期間至少必須執行15次。  

若要在來源伺服器上捕獲追蹤：

1. 在 DEA 中，選取左側功能表中的相機圖示，以移至 [**所有**]。

   ![左側導覽功能表](./media/database-experimentation-assistant-get-started/dea-get-started-leftnav.png)

1. 輸入或選取下列資訊：

   - **追蹤名稱**：您正在建立之新追蹤檔案的檔案名。 避免使用變換檔案命名慣例的追蹤名稱，例如，CaptureName \_NNN。
   - **持續時間**：捕捉的持續時間。
   - **SQL Server 實例名稱**：您要從中捕獲追蹤的 SQL Server 實例。
   - **資料庫名稱**：電腦上執行的資料庫名稱，您想要在其中捕獲追蹤的 SQL Server。 如果保留空白，則會從伺服器上的所有資料庫中捕獲追蹤。
   - **在 SQL Server 機上儲存來源追蹤**檔案的路徑：您要儲存追蹤檔案的資料夾路徑。

1. 請確定已備份目標資料庫。 然後，選取 [資料庫] 核取方塊。
1. 選取 [**啟動**] 以開始捕獲。

您可以查看您的 capture 進度，包括開始時間、持續時間和剩餘時間。 您也可以在等候此 capture 完成時，啟動新的 capture。 當您的 capture 完成時，請使用輸出追蹤檔案來啟動第二個階段：在目標伺服器上重新執行追蹤檔案。

如需追蹤 capture 的常見問題，請參閱[CAPTURE 常見問題](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)。

## <a name="replay"></a>重播

SQL Server A/B 測試的第二個步驟是重新執行已捕獲到目標伺服器的追蹤檔案。 然後，從重新執行收集大量追蹤以進行分析。 

您會在兩個目標伺服器上重新執行追蹤檔案：一個模擬來源伺服器（目標1），另一個則是模擬您提議的變更（目標2）。 [目標 1] 和 [目標 2] 的硬體設定應該盡可能類似，讓 SQL Server 可以正確地分析建議變更的效能影響。

考量因素：

- 您的電腦必須設定為執行 Distributed Replay （DReplay）追蹤，才能執行重新播放。 如需詳細資訊，請參閱[Distributed Replay 控制器和用戶端設定](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/)。
- 請務必使用來源伺服器的備份來還原目標伺服器上的資料庫。
- SQL Server 中的查詢快取可能會影響評估結果。 我們建議您重新開機服務應用程式中的 SQL Server 服務（MSSQLSERVER），以改善評估結果的一致性。

若要重新執行追蹤檔案：

1. 在 [DEA] 中，選取左側功能表中的 [播放] 圖示，以移至 [**所有**重新執行]。 會話期間（如果有的話）執行的過去重新執行清單隨即出現。 若要開始新的重新執行，請選取 [**新增**重新執行]。

1. 輸入或選取下列資訊：

   - **Replay name**：重新執行追蹤的檔案名。
   - **控制器電腦名稱稱**： Distributed Replay 控制器電腦的名稱。
   - **控制器上來源追蹤**檔案的路徑： [Capture](#capture)的來源追蹤檔案的檔案路徑。
   - **SQL Server 實例名稱**：要重新執行來源追蹤之 SQL Server 實例的名稱。
   - 將**目標追蹤檔案儲存在 SQL Server 機上的路徑**：產生的重新執行追蹤檔案的資料夾路徑。

1. 選取核取方塊以從第一個步驟還原備份。

1. 選取 [**啟動**] 以開始重新執行。 

您可以查看重新執行的狀態。 在兩部目標伺服器上重新執行來源追蹤之後，您就可以開始產生分析報告。

如需重新執行的相關常見問題，請參閱[REPLAY 常見問題](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)。

## <a name="analysis"></a>分析

最後一個步驟是使用重新執行追蹤來產生分析報表。 分析報表可協助您深入瞭解建議變更的效能影響。

考量因素：

- 如果遺失一或多個元件，當您嘗試產生新的分析報告（需要網際網路連線）時，就會出現包含下載連結的必要條件頁面。
- 若要查看使用舊版工具產生的報表，您必須先更新架構。

若要產生分析報表：

1. 在左側功能表中，移至 [**分析報表**]。 連接到執行 SQL Server 的電腦，您可以在其中儲存報表資料庫。 伺服器中的所有報表清單隨即出現。 若要建立新的報表，請選取 [**新增報表**]。

1. 輸入或選取產生報告所需的資訊：

   - **報表名稱**：要建立的分析報表名稱。
   - **目標 1 SQL Server 的追蹤**：在目標1上重新執行之追蹤檔案的路徑。
   - **目標 2 SQL Server 的追蹤**：在目標2上重新執行之追蹤檔案的路徑。

1. 選取 [**啟動**] 以產生報表。 新的報表會顯示在清單頂端。 產生報表時，報表旁的圖示會變成綠色核取記號。

現在，請查看分析報表，以取得 A/B 測試所提供的見解。

如需分析報告的常見問題，請參閱[分析常見問題](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)。

### <a name="analysis-report"></a>分析報表

在報表的第一頁上，會顯示執行實驗之目標伺服器的版本和組建資訊。 您可以使用臨界值來調整 A/B 測試分析的敏感度或容錯。 根據預設，閾值設定為 5%。 任何大於或等於 5% 的效能改進都會分類為**改良**。 選取下拉式功能表中的 [選項]，以使用不同的效能閾值來評估報表。

![臨界值](https://msdnshared.blob.core.windows.net/media/2017/03/threshold.jpg)

兩個圓形圖會針對您的工作負載，示範兩部目標伺服器之間差異的效能影響。 左側圖表是根據執行計數。 右圖表是以不同的查詢為基礎。 共有五種可能的類別：

- 已**改善**：統計的查詢在目標2上執行的速度比目標1更好。
- 已**降級**：統計的情況下，查詢在目標2上執行的效能比目標1更糟。
- **相同**：目標1和目標2之間的查詢沒有任何統計差異。
- **無法評估**：查詢的取樣大小太小，無法進行統計分析。 針對 A/B 測試分析，DEA 需要相同的查詢，才能在每個目標上至少有30個執行。
- **錯誤**：查詢在其中一個目標上至少錯誤一次。

![圓形圖](./media/database-experimentation-assistant-get-started/dea-get-started-piechart.png)

選取配量以向下切入至特定類別並取得效能計量，包括 [**無法評估**圓形圖] 配量。

[效能變更] 分類的向下切入頁面會顯示該類別中的查詢清單。 [**錯誤**] 頁面有三個索引標籤：

- **新的錯誤**：出現在目標2但不在目標1上的錯誤。
- **現有的錯誤**：出現在目標1和目標2上的錯誤。
- **已解決的錯誤**：出現在目標1但不在目標2上的錯誤。

   ![錯誤頁面](./media/database-experimentation-assistant-get-started/dea-get-started-errorpage.png)

選取查詢，以移至該查詢的**比較摘要**頁面。

[**比較摘要**] 頁面會顯示該查詢的摘要統計資料。 摘要包含執行次數、平均持續時間、平均 CPU、平均讀取/寫入和錯誤計數。

![摘要統計資料](./media/database-experimentation-assistant-get-started/dea-get-started-summarystats.png)

如果查詢是錯誤查詢，[**錯誤資訊**] 索引標籤會顯示有關錯誤的詳細資訊。 [**查詢計劃資訊**] 索引標籤會顯示在目標1和目標2上用於查詢之查詢計劃的相關資訊。

![查詢計劃](./media/database-experimentation-assistant-get-started/dea-get-started-queryplan.png)

在分析報表的任何頁面上，選取右上方的 [**列印**] 按鈕，以列印顯示的所有內容。

## <a name="next-steps"></a>後續的步驟

- 若要瞭解如何產生具有伺服器上所發生事件記錄檔的追蹤檔案，請參閱[Capture trace](database-experimentation-assistant-capture-trace.md)。

- 如需 DEA 和示範的19分鐘簡介，請觀看下列影片：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
