---
title: 偵錯及診斷 Spark 應用程式
titleSuffix: SQL Server Big Data Clusters
description: 使用 Spark 歷程記錄伺服器來偵錯及診斷在 SQL Server 2019 巨量資料叢集上執行的 Spark 應用程式。
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a2e1297ee6d32adc59810f3a4f9379e600f1464f
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606500"
---
# <a name="debug-and-diagnose-spark-applications-on-big-data-clusters-2019-in-spark-history-server"></a>在 Spark 歷程記錄伺服器中偵測並診斷 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]上的 Spark 應用程式

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文提供指引，說明如何使用延伸的 Spark 歷程記錄伺服器來偵測並診斷 SQL Server 巨量資料叢集中的 Spark 應用程式。 這些偵錯和診斷功能內建於 Spark 歷程記錄伺服器中，並由 Microsoft 提供技術支援。 延伸模組包含 [資料] 索引標籤、[圖表] 索引標籤和 [診斷] 索引標籤。在 [資料] 索引標籤中，使用者可以檢查 Spark 作業的輸入和輸出資料。 在 [圖表] 索引標籤中，使用者可以檢查資料流程，並重新執行作業圖表。 在 [診斷] 索引標籤中，使用者可以參考資料扭曲、時間扭曲和執行程式使用狀況分析。

## <a name="get-access-to-spark-history-server"></a>取得 Spark 歷程記錄伺服器的存取權

來自開放原始碼的 Spark 歷程記錄伺服器使用者體驗已透過資訊加以增強，其中包括作業特定資料以及作業圖表的互動式視覺效果，以及適用於巨量資料叢集的資料流程。 

### <a name="open-the-spark-history-server-web-ui-by-url"></a>依 URL 開啟 Spark 歷程記錄伺服器 Web UI
藉由瀏覽至下列 URL 來開啟 Spark 歷程記錄伺服器，並將 `<Ipaddress>` 和 `<Port>` 取代為巨量資料叢集特定資訊。 請注意，在基本驗證 (使用者名稱/密碼) 巨量資料叢集中，當提示您登入閘道 (Knox) 端點時，您必須提供使用者 **root**。 如需詳細資訊，可以參考：[部署 SQL Server 巨量資料叢集](quickstart-big-data-cluster-deploy.md)

```
https://<Ipaddress>:<Port>/gateway/default/sparkhistory
```

Spark 歷程記錄伺服器 Web UI 如下所示：

![Spark 歷程記錄伺服器](./media/apache-azure-spark-history-server/spark-history-server.png)


## <a name="data-tab-in-spark-history-server"></a>Spark 歷程記錄伺服器中的 [資料] 索引標籤
選取 [作業識別碼]，然後按一下工具功能表上的 [資料] 以取得資料檢視。

+ 個別選取索引標籤，以檢查 [輸入]、[輸出] 和 [資料表作業]。

    ![Spark 歷程記錄伺服器 [資料] 索引標籤](./media/apache-azure-spark-history-server/sparkui-data-tabs.png)

+ 按一下 [複製] 按鈕來複製所有資料列。

    ![複製所有資料列](./media/apache-azure-spark-history-server/sparkui-data-copy.png)

+ 按一下 [csv] 按鈕，將所有資料儲存為 CSV 檔案。

    ![將資料儲存為 CSV 檔案](./media/apache-azure-spark-history-server/sparkui-data-save.png)

+ 在 [搜尋] 欄位中輸入關鍵字來進行搜尋，搜尋結果會立即顯示。

    ![使用關鍵字搜尋](./media/apache-azure-spark-history-server/sparkui-data-search.png)

+ 按一下資料行標頭來排序資料表，按一下加號展開資料列以顯示更多詳細資料，或按一下減號來摺疊列。

    ![資料表功能](./media/apache-azure-spark-history-server/sparkui-data-table.png)

+ 若要下載單一檔案，請按一下右邊的 [部分下載] 按鈕，然後將選取的檔案下載到本機位置。 如果檔案不存在，則會開啟新的索引標籤來顯示錯誤訊息。

    ![下載資料列](./media/apache-azure-spark-history-server/sparkui-data-download-row.png)

+ 複製完整路徑或相對路徑，方法是選取從下載功能表展開的 [複製完整路徑]、[複製相對路徑]。 針對 Azure 資料湖儲存體檔案，[在 Azure 儲存體總管中開啟] 將會啟動 Azure 儲存體總管。 並在登入時找出正確的資料夾。

    ![複製完整或相對路徑](./media/apache-azure-spark-history-server/sparkui-data-copy-path.png)

+ 當在一個頁面中顯示太多資料列時，請按一下資料表下方的數字以瀏覽頁面。 

    ![資料頁面](./media/apache-azure-spark-history-server/sparkui-data-page.png)

+ 將滑鼠停留在 [資料] 旁的問號以顯示工具提示，或按一下問號以取得詳細資訊。

    ![資料詳細資訊](./media/apache-azure-spark-history-server/sparkui-data-more-info.png)

+ 按一下 [提供意見反應] 以傳送有關問題的意見反應。

    ![圖表意見反應](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)

## <a name="graph-tab-in-spark-history-server"></a>Spark 歷程記錄伺服器中的 [圖表] 索引標籤

選取作業識別碼，然後按一下工具功能表上的 [圖表] 以取得作業圖表檢視。

+ 透過產生的作業圖表檢查作業概觀。 

+ 根據預設，它會顯示所有作業，而且可以依 [作業識別碼] 進行篩選。

    ![圖表作業識別碼](./media/apache-azure-spark-history-server/sparkui-graph-jobid.png)

+ 我們將 [進度] 保留為預設值。 使用者可以在 [顯示] 的下拉式清單中選取 [讀取] 或 [寫入] 來檢查資料流程。

    ![圖表顯示](./media/apache-azure-spark-history-server/sparkui-graph-display.png)

    圖表節點會以顯示熱度圖的色彩顯示。

    ![圖表熱度圖](./media/apache-azure-spark-history-server/sparkui-graph-heatmap.png)

+ 按一下 [播放] 按鈕來播放作業，並按一下 [停止] 按鈕隨時停止。 播放時，工作會以色彩顯示以顯示不同的狀態：

    + 綠色表示成功：作業已成功完成。
    + 橘色表示重試：失敗但不會影響作業最終結果的工作執行個體。 這些工作具有稍後可能會成功的重複或重試執行個體。
    + 藍色表示執行中：工作正在執行。
    + 白色表示正在等候或略過：工作正在等候執行，或已略過該階段。
    + 紅色表示失敗：工作失敗。

    ![圖表色彩樣本、執行中](./media/apache-azure-spark-history-server/sparkui-graph-color-running.png)
 
    略過的階段會以白色顯示。
    ![圖表色彩樣本、略過](./media/apache-azure-spark-history-server/sparkui-graph-color-skip.png)

    ![圖表色彩樣本、失敗](./media/apache-azure-spark-history-server/sparkui-graph-color-failed.png)
 
    > [!NOTE]
    > 允許播放每個工作。 針對不完整的作業，不支援播放。


+ 滑鼠會滾動以放大/縮小作業圖表，或按一下　[縮放至適當比例]，使其符合螢幕大小。
 
    ![圖表縮放至適當比例](./media/apache-azure-spark-history-server/sparkui-graph-zoom2fit.png)

+ 當工作失敗時，將滑鼠停留在圖表節點上以查看工具提示，然後按一下 [階段] 以開啟 [階段] 頁面。

    ![圖表工具提示](./media/apache-azure-spark-history-server/sparkui-graph-tooltip.png)

+ 在 [作業圖表] 索引標籤中，如果階段的工作符合下列條件，則會顯示工具提示和小型圖示：
    + 資料扭曲：資料讀取大小 > 此階段中所有工作的平均資料讀取大小 * 2 和資料讀取大小 > 10 MB
    + 時間扭曲：此階段中所有工作的執行時間 > 平均執行時間 * 2，而執行時間 > 2 分鐘

    ![圖表扭曲圖示](./media/apache-azure-spark-history-server/sparkui-graph-skew-icon.png)

+ [作業圖表] 節點會顯示每個階段的下列資訊：
    + 識別碼。
    + 名稱或描述。
    + 總工作數。
    + 讀取的資料：輸入大小和隨機讀取大小的總和。
    + 資料寫入：輸出大小和隨機寫入大小的總和。
    + 執行時間：第一次嘗試的開始時間與最後一次嘗試的完成時間之間的時間。
    + 資料列計數：輸入記錄、輸出記錄、隨機讀取記錄和隨機寫入記錄的總和。
    + 進度。

    > [!NOTE]
    > 根據預設，[作業圖表] 節點會顯示每個階段的最後一次嘗試的資訊 (階段執行時間除外)，但在播放圖表節點期間，會顯示每次嘗試的資訊。

    > [!NOTE]
    > 對於讀取和寫入的資料大小，我們使用 1MB = 1000 KB = 1000 * 1000 個位元組。

+ 按一下 [提供意見反應] 以傳送有關問題的意見反應。

    ![圖表意見反應](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)


## <a name="diagnosis-tab-in-spark-history-server"></a>Spark 歷程記錄伺服器中的 [診斷] 索引標籤
選取作業識別碼，然後按一下工具功能表上的 [診斷] 以取得作業診斷檢視。 [診斷] 索引標籤包括 [資料扭曲]、[時間扭曲] 和 [執行程式使用狀況分析]。
    
+ 透過個別選取索引標籤，檢查 [資料扭曲]、[時間扭曲] 和 [執行程式使用狀況分析]。

    ![[診斷] 索引標籤](./media/apache-azure-spark-history-server/sparkui-diagnosis-tabs.png)

### <a name="data-skew"></a>資料扭曲
按一下[資料扭曲] 索引標籤，就會根據指定的參數顯示對應的扭曲工作。 

+ **指定參數** -第一個區段會顯示用來偵測資料扭曲的參數。 內建規則是：工作資料讀取大於平均工作資料讀取的 3 倍，而工作資料讀取超過 10 MB。 如果您想要為扭曲的工作定義自己的規則，您可以選擇您的參數 ([扭曲階段])，[扭曲字元] 區段將會據此重新整理。 

+ **扭曲階段** -第二個區段會顯示階段，其中有扭曲的工作符合上面指定的準則。 如果某個階段中有一個以上的扭曲工作，扭曲階段資料表只會顯示最扭曲的工作 (例如，資料扭曲的最大資料)。 

    ![資料扭曲 section2](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section2.png)

+ **扭曲圖表** - 選取扭曲階段資料表中的資料列時，扭曲圖表會根據讀取和執行時間的資料，顯示更多工作分佈詳細資料。 扭曲的工作會以紅色標示，而一般工作則會以藍色標示。 基於效能考量，圖表最多只會顯示 100 個樣本工作。 工作詳細資料會顯示在右下方面板中。

    ![資料扭曲 section3](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section3.png)

### <a name="time-skew"></a>時間扭曲
[時間扭曲] 索引標籤會根據工作執行時間顯示扭曲的工作。 

+ **指定參數** - 第一個區段會顯示用來偵測時間扭曲的參數。 偵測時間扭曲的預設準則是：工作執行時間大於平均執行時間的三倍，而工作執行時間大於 30 秒。 您可以根據您的需求變更參數。 [扭曲階段] 和 [扭曲圖表] 會顯示對應的階段和工作資訊，就像上面的 [資料扭曲] 索引標籤一樣。

+ 按一下 [時間扭曲]，然後根據 [指定參數] 區段中所設定的參數，在 [扭曲階段] 區段中顯示篩選的結果。 按一下 [扭曲階段] 區段中的一個專案，然後對應的圖表會在 section3 中繪製，而且工作詳細資料會顯示在右下方面板中。

    ![時間扭曲 section2](./media/apache-azure-spark-history-server/sparkui-diagnosis-timeskew-section2.png)

### <a name="executor-usage-analysis"></a>執行程式使用狀況分析
執行程式使用狀況圖表會將 Spark 作業的實際執行程式配置和執行狀態視覺化。  

+ 按一下 [執行程式使用狀況分析]，然後繪製與執行程式使用方式相關的四種曲線類型。 其中包括 [已配置的執行程式]、[執行中的執行程式]、[閒置的執行程式] 以及 [最大執行程式執行個體]。 關於已配置的執行程式，每個「已新增執行程式」或「已移除執行程式」事件都會增加或減少配置的執行程式。 您可以檢查 [作業] 索引標籤中的 [事件時間軸] 以進行比較。

    ![[執行程式] 索引標籤](./media/apache-azure-spark-history-server/sparkui-diagnosis-executors.png)

+ 按一下色彩圖示，以選取或取消選取所有草稿中的對應內容。

    ![選取圖表](./media/apache-azure-spark-history-server/sparkui-diagnosis-select-chart.png)


## <a name="known-issues"></a>已知問題
Spark 歷程記錄伺服器具有下列已知問題：

+ 目前，它僅適用於 Spark 2.3 叢集。

+ 使用 RDD 的輸入/輸出資料不會顯示在 [資料] 索引標籤中。

## <a name="next-steps"></a>後續步驟

* [開始使用 SQL Server 巨量資料叢集](../big-data-cluster/deploy-get-started.md)
* 設定 Spark 設定
* [設定 Spark 設定](/azure/hdinsight/spark/apache-spark-settings/)
