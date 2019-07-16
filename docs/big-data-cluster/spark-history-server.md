---
title: 偵錯/診斷的 Spark 應用程式
titleSuffix: SQL Server big data clusters
description: 若要偵錯和診斷在 SQL Server 2019 巨量資料叢集上執行的 Spark 應用程式中使用 Spark 歷程記錄伺服器。
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5659de24ed9cc0a61290d055049c804c6709b2a5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67957856"
---
# <a name="debug-and-diagnose-spark-applications-on-sql-server-big-data-clusters-in-spark-history-server"></a>偵錯和診斷在 SQL Server 在 Spark 歷程記錄伺服器中的巨量資料叢集上的 Spark 應用程式

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文章提供有關如何使用擴充的 Spark 歷程記錄伺服器偵錯和診斷中的 SQL Server 2019 （預覽） 的巨量資料叢集的 Spark 應用程式的指引。 這些偵錯和診斷功能會內建於 Spark 歷程記錄伺服器，並由 Microsoft 所提供。 擴充功能包括資料 索引標籤和 graph 索引標籤和診斷 索引標籤。在 資料 索引標籤中，使用者可以檢查的輸入和輸出資料的 Spark 作業。 圖表索引標籤中，使用者可以檢查資料流，並重新執行工作圖形。 在 [診斷] 索引標籤中，使用者可以參考資料扭曲 」、 「 時間偏差和 「 執行程式使用情況分析。

## <a name="get-access-to-spark-history-server"></a>存取 Spark 歷程記錄伺服器

從開放原始碼 Spark 歷程記錄伺服器使用者體驗已增強式的詳細資訊，其中包含作業特定的資料和巨量資料叢集的作業圖表和資料流程的互動式視覺效果。 

### <a name="open-the-spark-history-server-web-ui-by-url"></a>開啟 Spark 歷程記錄伺服器 Web UI URL
開啟 Spark 歷程記錄伺服器，瀏覽至下列 URL，取代`<Ipaddress>`和`<Port>`巨量資料叢集特定資訊。 可參考的詳細資訊：[部署 SQL Server 的巨量資料叢集](quickstart-big-data-cluster-deploy.md)

```
https://<Ipaddress>:<Port>/gateway/default/sparkhistory
```

Spark 記錄伺服器 」 web UI 看起來像：

![Spark 歷程記錄伺服器](./media/apache-azure-spark-history-server/spark-history-server.png)


## <a name="data-tab-in-spark-history-server"></a>在 [Spark 歷程記錄伺服器中的資料] 索引標籤
選取的作業識別碼，然後按一下 **資料**在工具功能表上，若要取得資料檢視。

+ 請檢查**輸入**，**輸出**，並**資料表作業**個別選取索引標籤。

    ![Spark 歷程記錄伺服器資料索引標籤](./media/apache-azure-spark-history-server/sparkui-data-tabs.png)

+ 按一下按鈕來複製所有資料列**複製**。

    ![複製所有資料列](./media/apache-azure-spark-history-server/sparkui-data-copy.png)

+ 將所有資料都儲存為 CSV 檔案中，按一下按鈕**csv**。

    ![將資料儲存為 CSV 檔案](./media/apache-azure-spark-history-server/sparkui-data-save.png)

+ 搜尋欄位中輸入關鍵字**搜尋**，將會立即顯示搜尋結果。

    ![使用關鍵字搜尋](./media/apache-azure-spark-history-server/sparkui-data-search.png)

+ 按一下資料行標頭來排序資料表，按一下加號，展開 資料列來顯示更多詳細資料，或按一下減號摺疊資料列。

    ![資料的資料表功能](./media/apache-azure-spark-history-server/sparkui-data-table.png)

+ 下載單一檔案按鈕，即可**部分下載**，放在右側，然後選取的檔案下載至本機位置。 如果檔案不存在任何其他，即會開啟新索引標籤，以顯示錯誤訊息。

    ![下載資料列](./media/apache-azure-spark-history-server/sparkui-data-download-row.png)

+ 選取 複製完整路徑或相對路徑**複製完整路徑**，**複製相對路徑**將它展開並從 下載 功能表。 Azure data lake 儲存體檔案，如**在 Azure 儲存體總管中開啟**會啟動 Azure 儲存體總管。 並在登入時，找出要完全相同的資料夾。

    ![複製的完整或相對路徑](./media/apache-azure-spark-history-server/sparkui-data-copy-path.png)

+ 按一下資料表下方的編號，瀏覽頁面時太多資料列在一個網頁中顯示。 

    ![資料頁面](./media/apache-azure-spark-history-server/sparkui-data-page.png)

+ 將滑鼠停留在資料顯示工具提示中，旁邊的問號，或按一下問號，以取得詳細資訊。

    ![資料的詳細資訊](./media/apache-azure-spark-history-server/sparkui-data-more-info.png)

+ 按一下 傳送意見反應與議題**向我們反應意見**。

    ![圖形的意見反應](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)

## <a name="graph-tab-in-spark-history-server"></a>在 Spark 歷程記錄伺服器中的 圖表 索引標籤

選取的作業識別碼，然後按一下  **Graph**在工具功能表上，若要取得工作的 圖表 檢視。

+ 產生的作業圖表來檢查您的工作的概觀。 

+ 根據預設，它會顯示所有作業，以及它可以藉由使用篩選**的作業識別碼**。

    ![圖形作業識別碼](./media/apache-azure-spark-history-server/sparkui-graph-jobid.png)

+ 我們將保留**進度**做為預設值。 使用者可以選取來檢查資料流**讀取**或 寫入 * * * 在下拉式清單中的**顯示**。

    ![圖形顯示](./media/apache-azure-spark-history-server/sparkui-graph-display.png)

    圖形節點以顯示熱度圖的色彩顯示。

    ![圖形熱度圖](./media/apache-azure-spark-history-server/sparkui-graph-heatmap.png)

+ 按一下播放作業**播放**按鈕，並隨時停止，依序按一下 [停止] 按鈕。 工作中的顯示色彩來顯示不同的狀態時播放：

    + 綠色的成功：作業已順利完成。
    + 橘色的重試：工作失敗，但不會影響作業的最終結果的執行個體。 這些工作會有重複或重試稍後可能會成功的執行個體。
    + 藍色執行：工作正在執行。
    + 等候的白色或略過：工作在等候執行，或已略過階段。
    + 紅色表示失敗：工作已失敗。

    ![圖形的色彩範例中執行](./media/apache-azure-spark-history-server/sparkui-graph-color-running.png)
 
    已略過的階段以白色顯示。
    ![圖形的色彩範例，請略過](./media/apache-azure-spark-history-server/sparkui-graph-color-skip.png)

    ![圖形的色彩範例中失敗](./media/apache-azure-spark-history-server/sparkui-graph-color-failed.png)
 
    > [!NOTE]
    > 允許為每個工作的播放。 針對未完成的工作，不支援播放。


+ 捲動至縮放輸入/輸出作業圖表，或按一下的滑鼠**縮放以符合**容易調整成螢幕。
 
    ![圖表縮放以符合](./media/apache-azure-spark-history-server/sparkui-graph-zoom2fit.png)

+ 將滑鼠停留在圖形節點以查看工具提示時有失敗的工作，然後按一下以開啟階段頁面上的階段。

    ![圖形工具提示](./media/apache-azure-spark-history-server/sparkui-graph-tooltip.png)

+ 工作圖表 索引標籤中，階段會有工具提示和小圖示顯示有工作符合以下條件：
    + 資料扭曲： 讀取的資料大小 > 平均資料讀取的這個階段內的所有工作的大小 * 2 和讀取的資料大小 > 10 MB
    + 時間誤差： 執行時間 > 的這個階段內的所有工作的平均執行時間 * 2 和執行時間 > 2 分鐘

    ![圖形扭曲圖示](./media/apache-azure-spark-history-server/sparkui-graph-skew-icon.png)

+ 作業圖形節點會顯示每個階段的下列資訊：
    + 識別碼。
    + 名稱或描述。
    + 總工作數。
    + 讀取的資料： 輸入的大小的 shuffle 加總讀取的大小。
    + 資料寫入： 輸出大小的 shuffle 總和寫入大小。
    + 執行時間： 第一次嘗試開始時間和上次嘗試的完成時間之間的時間。
    + 資料列計數： 輸入記錄的加總輸出記錄、 隨機讀取的記錄和隨機寫入記錄。
    + 進度。

    > [!NOTE]
    > 根據預設，作業圖形節點會顯示從上一次嘗試的 （除了階段執行時間），每個階段的資訊，但是在播放圖形節點會顯示每一次嘗試的資訊。

    > [!NOTE]
    > 資料大小的讀取和寫入，我們會使用 1 MB = 1000 KB = 1000 * 1000 個位元組。

+ 按一下 傳送意見反應與議題**向我們反應意見**。

    ![圖形的意見反應](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)


## <a name="diagnosis-tab-in-spark-history-server"></a>在 [Spark 歷程記錄伺服器] 診斷索引標籤
選取的作業識別碼，然後按一下 **診斷**在工具功能表上，以取得診斷檢視的作業。 [診斷] 索引標籤包含**資料扭曲**，**時間誤差**，並**執行程式使用情況分析**。
    
+ 請檢查**資料扭曲**，**時間誤差**，並**執行程式使用情況分析**分別選取索引標籤。

    ![診斷索引標籤](./media/apache-azure-spark-history-server/sparkui-diagnosis-tabs.png)

### <a name="data-skew"></a>資料扭曲
按一下 **資料扭曲**索引標籤上，對應扭曲的工作才會顯示根據指定的參數。 

+ **指定參數**-第一部分顯示的參數，用來偵測資料扭曲。 內建的規則是：讀取的工作資料大於三次的平均工作資料讀取，且讀取的工作資料會超過 10 MB。 如果您想要定義您自己的規則，扭曲的工作，您可以選擇您的參數**扭曲階段**，並**扭曲 Char**區段將會據以重新整理。 

+ **扭曲階段**-第二個區段會顯示包含了扭曲符合上述準則的工作階段。 是否有多個扭曲的工作階段中，扭曲的暫存資料表只會顯示最扭曲的工作 （例如，資料扭曲的最大資料）。 

    ![資料扭曲 section2](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section2.png)

+ **扭曲圖表**-選取扭曲的暫存資料表中的資料列時，詳細的工作分佈根據讀取的資料和執行時間誤差的圖表顯示。 扭曲的工作會標示為紅色，和一般工作會以藍色標示。 基於效能考量，圖表只會顯示最多 100 個範例工作。 工作詳細資料會顯示在右邊的下方面板。

    ![資料扭曲 section3](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section3.png)

### <a name="time-skew"></a>時間扭曲
**時間誤差**索引標籤會顯示扭曲的工作執行時間為基礎的工作。 

+ **指定參數**-第一部分顯示的參數，用來偵測時間誤差。 預設準則，來偵測時間誤差是： 工作執行時間大於三次的平均執行時間，且工作執行時間大於 30 秒。 您可以變更您的需求為基礎的參數。 **扭曲階段**並**扭曲圖表**一樣顯示的對應階段和工作資訊**資料扭曲**上述 索引標籤。

+ 按一下 **時間誤差**，然後篩選的結果會顯示在**扭曲階段**根據區段中設定的參數區段**指定參數**。 按一下一個項目**扭曲階段**區段，則相對應的圖表草稿中 section3，並在右邊的下方面板中顯示工作詳細資料。

    ![時間誤差 section2](./media/apache-azure-spark-history-server/sparkui-diagnosis-timeskew-section2.png)

### <a name="executor-usage-analysis"></a>執行程式的使用量分析
在執行程式的使用量圖表會視覺化 Spark 作業實際執行程式配置和執行狀態。  

+ 按一下 **執行程式使用情況分析**，則我們編寫有關執行者使用量的四個型別曲線。 其中包括**配置執行程式**，**執行的執行程式**，**閒置的執行程式**，以及**最大可執行程式執行個體**。 有關配置的執行程式，每個 「 執行程式已新增 」 或 「 執行程式已移除 」 的事件會增加或減少配置執行程式。 如需詳細的比較 [作業] 索引標籤中，您可以檢查 」 事件時間軸 」。

    ![執行程式 索引標籤](./media/apache-azure-spark-history-server/sparkui-diagnosis-executors.png)

+ 按一下色彩圖示以選取或取消選取所有 [草稿] 中的對應內容。

    ![選取的圖表](./media/apache-azure-spark-history-server/sparkui-diagnosis-select-chart.png)


## <a name="known-issues"></a>已知問題
「 Spark 記錄伺服器具有下列已知的問題：

+ 目前，它只適用於 Spark 2.3 叢集。

+ 在 [資料] 索引標籤中，將不會顯示使用 RDD 的輸入/輸出資料。

## <a name="next-steps"></a>後續步驟

* [管理 HDInsight 上的 Spark 叢集的資源](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-resource-manager)
* [設定 Spark 設定](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-settings)
