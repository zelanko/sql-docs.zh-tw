---
title: 開始使用資料庫測試助理 （jlca） for SQL Server 升級
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
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 7630aee7ab39f98f372af7c33f277e7272042f43
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59963274"
---
# <a name="get-started-with-database-experimentation-assistant"></a>開始使用資料庫測試助理

資料庫測試助理 (DEA) 是 A / B 測試解決方案的變更在 SQL Server 環境中，例如升級或新的索引。 DEA 可協助您評估如何在新環境中執行您的來源伺服器 （在您目前的環境中） 上的工作負載。 DEA 會引導您完成執行 A / B 測試完成三個步驟： 

- 擷取
- 重新執行
- 分析

這篇文章會引導您完成這些步驟。

## <a name="capture"></a>擷取

第一個步驟的 SQL Server A / B 測試是擷取您的來源伺服器上的追蹤。 來源伺服器通常會是實際執行伺服器。 追蹤檔案會擷取該伺服器，包括時間戳記的整個查詢工作負載。 更新版本中，這項追蹤重新執行分析的目標伺服器上。 [分析] 報表中的工作負載的效能差異，這兩個目標伺服器之間提供深入解析。

考量因素：

- 在開始將追蹤擷取之前，請務必先備份您要從中擷取追蹤資料庫。
- DEA 使用者必須設定為使用 Windows 驗證連接到資料庫中。
- SQL Server 服務帳戶需要存取權的來源追蹤檔案路徑。

若要擷取您的來源伺服器上的追蹤：

1. DEA，在移至**所有擷取**左側功能表中選取 [相機] 圖示。

   ![左的導覽功能表](./media/database-experimentation-assistant-get-started/dea-get-started-leftnav.png)

1. 輸入或選取下列資訊：

   - **追蹤名稱**:您建立新的追蹤檔案的檔案名稱。 避免使用的換用檔案命名慣例，例如 CaptureName 追蹤名稱\_NNN。
   - **持續時間**:擷取持續時間。
   - **SQL Server 執行個體名稱**:您要從中擷取追蹤 SQL Server 執行個體。
   - **資料庫名稱**:要擷取的追蹤執行 SQL Server 的電腦上的資料庫名稱。 如果保留空白，就會從伺服器上的所有資料庫擷取追蹤。
   - **若要儲存 SQL Server 電腦上的來源追蹤檔案的路徑**:您要儲存追蹤檔案的資料夾路徑。

1. 請確定目標資料庫備份。 然後，選取 [資料庫] 核取方塊。
1. 選取 **啟動**開始擷取。

您可以檢視您的擷取，包括開始時間、 持續時間，以及剩餘時間的進度。 您也可以啟動新的擷取當您等候此完成的擷取。 擷取完成時，使用輸出追蹤檔來啟動第二個階段： 重新執行追蹤檔案，在您的目標伺服器上。

追蹤擷取的相關的一般問題，請參閱[擷取常見問題集](database-experimentation-assistant-capture-trace.md#frequently-asked-questions-about-trace-capture)。

## <a name="replay"></a>重新執行

SQL Server 的第二個步驟 / B 測試可重新執行追蹤檔案已擷取至目標伺服器。 然後，從分析重新執行收集大量的追蹤。 

重新執行追蹤檔案在兩個目標伺服器上： 一個，以模擬您的來源伺服器 (目標 1)，會模擬您提議的變更 (目標 2) 的一個。 目標 1 與目標 2 的硬體組態應盡可能相似，因此 SQL Server 可以精確地分析效能的影響建議變更。

考量因素：

- 若要執行重新執行，必須將您的機器設定來執行 Distributed Replay (DReplay) 追蹤。 如需詳細資訊，請參閱 < [Distributed Replay controller 和 client 安裝程式](https://blogs.msdn.microsoft.com/datamigration/distributed-replay-controller-and-client-setup/)。
- 請確定您的目標伺服器上還原資料庫，使用從來源伺服器的備份。
- SQL Server 中的查詢快取可能會影響評估結果。 我們建議您重新啟動 SQL Server 服務 (MSSQLSERVER) 中的服務應用程式，以改善評估結果的一致性。

若要重新執行追蹤檔案：

1. 在 DEA，選取 移至左側功能表中的播放圖示**所有的重新執行**。 過去的重新執行期間所執行的工作階段中，如果任何項目，出現的清單。 若要啟動新的重新執行，請選取**新的重新執行**。

1. 輸入或選取下列資訊：

   - **重新執行名稱**:重新執行追蹤檔案名稱。
   - **控制器電腦名稱**:Distributed Replay 控制器電腦名稱。
   - **控制站上的來源追蹤檔案的路徑**:從來源追蹤檔案的檔案路徑[擷取](#capture)。
   - **SQL Server 執行個體名稱**:要重新執行來源追蹤的 SQL Server 執行個體名稱。
   - **將目標 SQL Server 電腦上的追蹤檔案的路徑**:產生的重新執行追蹤檔案資料夾路徑。

1. 選取核取方塊，將備份還原第一個步驟。

1. 選取 **啟動**開始重新執行。 

您可以檢視您的重新執行的狀態。 如果要在重新執行來源追蹤這兩個目標伺服器上的之後，您即可產生分析報告。

常見疑問重新執行的詳細資訊，請參閱 <<c0> [ 重新執行常見問題集](database-experimentation-assistant-replay-trace.md#frequently-asked-questions-about-trace-replay)。

## <a name="analysis"></a>分析

最後一個步驟是使用重新執行追蹤產生分析報告。 [分析] 報表可協助您深入了解有關效能含意的提議的變更。

考量因素：

- 如果遺漏一個或多個元件，以產生新的分析報告 （需要網際網路連線） 時，也會出現的必要條件頁面連結的下載項目。
- 若要檢視的報表，產生在舊版的工具中，您必須先更新結構描述。

若要產生分析報告：

1. 在左側功能表中，移至**分析報表**。 連接到執行您用來儲存您的報表資料庫的 SQL 伺服器的電腦。 在伺服器中的所有報表的清單隨即出現。 若要建立新的報表，請選取**新的報表**。

1. 輸入或選取所需來產生報告的資訊：

   - **報表名稱**:若要建立的 [分析] 報表的名稱。
   - **目標 1 SQL Server 追蹤**:從目標 1 上重新執行追蹤檔案的路徑。
   - **目標 2 SQL Server 追蹤**:從目標 2 上重新執行追蹤檔案的路徑。

1. 選取 **啟動**來產生報告。 新的報表會顯示在清單頂端。 在產生報告時，報表旁邊的圖示會變成綠色的核取記號。

現在，檢視 [分析] 報表，以更深入提供您 A / B 測試。

常見疑問分析報表的詳細資訊，請參閱 <<c0> [ 分析常見問題集](database-experimentation-assistant-create-report.md#frequently-asked-questions-about-analysis-reports)。

### <a name="analysis-report"></a>分析報表

在報表的第一頁，會顯示在其上執行實驗的目標伺服器的版本與組建資訊。 您可用來調整您的容錯度的敏感度閾值 / B 測試分析。 根據預設，會將閾值設定 5%。 任何比較或等於 5%的效能改進分為**改良**。 若要使用不同的效能臨界值評估報表下拉式選單中選取選項。

![閾值](https://msdnshared.blob.core.windows.net/media/2017/03/threshold.jpg)

兩個圓形圖會示範在您的工作負載的兩個目標伺服器之間的差異的效能含意。 在左圖根據執行計數。 正確的圖表會根據不同的查詢。 有五個可能的類別：

- **改善**:在統計上，查詢比目標 1 上的目標 2 上執行更好。
- **降級**:在統計上，查詢比目標 1 上的目標 2 上執行較差。
- **相同**:並無差別統計查詢目標 1 與目標 2 之間。
- **無法評估**:取樣大小的查詢是統計的分析而言太小。 A / B 測試分析，DEA 所需的每個目標上有至少 30 次執行相同的查詢。
- **錯誤**：發生錯誤的其中一個目標上至少一次的查詢。

![圓形圖](./media/database-experimentation-assistant-get-started/dea-get-started-piechart.png)

選取向下切入至特定分類，並取得效能計量，包括配量**無法評估**圓形圖配量。

向下鑽研頁面上，效能變更類別目錄會顯示一份該類別中的查詢。 **錯誤**頁面有三個索引標籤：

- **新的錯誤**:出現在目標 2，但不是能在目標 1 的錯誤。
- **現有錯誤**:目標 1 和 2 目標出現的錯誤。
- **解決錯誤**:出現在目標 1，但不是能在目標 2 的錯誤。

   ![錯誤頁面](./media/database-experimentation-assistant-get-started/dea-get-started-errorpage.png)

選取要移至的查詢**比較摘要**該查詢的頁面。

**比較摘要**頁面會顯示該查詢的摘要統計資料。 此摘要包括執行數目、 平均持續時間、 平均 CPU，平均讀取/寫入，以及錯誤計數。

![摘要統計資料](./media/database-experimentation-assistant-get-started/dea-get-started-summarystats.png)

如果查詢是查詢時發生錯誤**錯誤資訊**索引標籤會顯示錯誤的詳細資訊。 **查詢計劃資訊**索引標籤會顯示用來在目標 1 與目標 2 上查詢的查詢計劃的相關資訊。

![查詢計劃](./media/database-experimentation-assistant-get-started/dea-get-started-queryplan.png)

在 [分析] 報表的任何頁面上，選取**列印**在頂端的按鈕列印權限的所有項目可見。

## <a name="next-steps"></a>後續步驟

- 若要了解如何產生具有在伺服器發生的事件記錄檔的追蹤檔案，請參閱[追蹤擷取](database-experimentation-assistant-capture-trace.md)。

- 如需 19 分鐘簡介 DEA 和示範，觀看下列影片：

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
