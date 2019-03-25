---
title: 版本資訊
titleSuffix: Azure Data Studio
description: Azure Data Studio 版本資訊
ms.custom: seodec18
ms.date: 03/22/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 359723a1e2d75b7cbbd3a88c9a0ba7ee89fdf420
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58381586"
---
# <a name="release-notes-for-azure-data-studio"></a>Azure Data Studio 的版本資訊

**[下載並安裝最新版的 ！](download.md)**

## <a name="march-2019-hotfix"></a>年 3 月 2019 (Hotfix)

2019 年 3 月 22 日&nbsp;  /  &nbsp;版本：1.5.2 &nbsp;  /  &nbsp; Hotfix 版本

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| 已修正 1.5.1 中探索到的一些問題。 | 請參閱[三月在 GitHub 上的 Hotfix 版本](https://github.com/Microsoft/azuredatastudio/milestone/28)。<br/> <br/>&bull; &nbsp; 已修正的使用者無法關閉 notebook 開啟儀表板中的 「 開啟筆記本 」 工作的問題 <br/>&bull; &nbsp; 已修正問題，Notebook JSON 有較多} 儲存後 <br/>&bull; &nbsp; 已修正的問題，notebook 方格所未回應佈景主題變更 <br/>&bull; &nbsp; 已修正的問題，其中顯示完整的 notebook 路徑 索引標籤標頭中。 現在會顯示檔案名稱。 |
| &nbsp; | &nbsp; |

## <a name="march-2019"></a>2019 年 3 月

2019 年 3 月 18 日&nbsp;  /  &nbsp;版本：1.5.1

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| 新增[PostgreSQL 擴充功能，適用於 Azure 資料 Studio](postgres-extension.md) | 支援的功能： <br/>&bull; &nbsp; 連接對話方塊 <br/>&bull; &nbsp; 物件總管 <br/>&bull; &nbsp; 查詢編輯器 <br/>&bull; &nbsp; 圖表 <br/>&bull; &nbsp; 儀表板 <br/>&bull; &nbsp; 程式碼片段 <br/>&bull; &nbsp; 編輯資料 <br/>&bull; &nbsp; Notebook |
| 已新增的 SQL Notebook | 已新增的 SQL 核心支援的內建筆記本檢視器： <br/>&bull; &nbsp; 支援的 T-SQL <br/>&bull; &nbsp; 支援 PGSQL |
| 新增的 PowerShell 延伸模組  | 帶來[PowerShell 延伸模組](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell)體驗從 VS Code。  |
| 已新增的 SQL Server dacpac 延伸模組  | 移除 SQL Server 匯入延伸模組的資料層應用程式精靈儲存成新的擴充功能。  |
| 已新增 「 社群 」 延伸模組 QueryPlan.show | 加入以視覺化方式檢視查詢計劃的整合支援  |
| 更新的 SQL Server 2019 Preview 擴充 | &bull; &nbsp; Jupyter Notebook 支援，特別是 Python3 和 Spark 核心，已移至核心 Azure Data Studio 工具。 <br/>&bull; &nbsp; 修正 bug 以外部資料精靈  |
| 已解決的 bug 和問題。 | 請參閱[Bug 和問題，請在 GitHub 上的](https://github.com/Microsoft/azuredatastudio/milestone/25?closed=1)。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知問題
- [#4427](https://github.com/Microsoft/azuredatastudio/issues/4427):按一下 儲存格之前核心上的執行為就緒的 Spark 會導致嚴重的錯誤**因應措施：** 等待核心會載入之前執行任何資料格
- [#4493](https://github.com/Microsoft/azuredatastudio/issues/4493):啟動 SSMS 使用 SQL 驗證-提示使用者輸入密碼的廣告**因應措施：** 現在，使用 Windows 驗證。 
- [#4494](https://github.com/Microsoft/azuredatastudio/issues/4494):無法安裝 SQL notebook 功能 <br/>
**因應措施：** 請依照下列因應措施步驟[此處](https://github.com/Microsoft/azuredatastudio/issues/4494#issuecomment-473043832)。 
- [#4503](https://github.com/Microsoft/azuredatastudio/issues/4503):Azure Data Studio 無法下載] 資料夾 (Mac) 從 [開啟直接 <br />
**因應措施：** 解壓縮應用程式之後，重新啟動電腦。 將調查。 
- [#4539](https://github.com/Microsoft/azuredatastudio/issues/4539):Notebook 另存新檔將會遺失連接內容 <br />
**因應措施：** 將在下一個版本中修正。 
- [#4458](https://github.com/Microsoft/azuredatastudio/issues/4458):Dacpac 擷取損毀 SqlToolsService，如果使用無效的版本 <br/>
**因應措施：** 重新啟動 Azure Data Studio，並確保使用正確的版本。
- 新的 [Notebook] 和 [開啟 Notebook] 圖示將會遺失 <br/> 
**因應措施：** 在舊版的連線類型已被取代。 我們建議您連接到 SQL Server 端點，並如預期般運作，您會收到所有的動作 （新的 Notebook，Spark 作業）。 

## <a name="february-2019"></a>2019 年 2 月

2019 年 2 月 13 日&nbsp;  /  &nbsp;版本：1.4.5

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| 新增**SQL Server 的管理組件**延伸模組套件。 | 這可讓您更輕鬆地安裝 SQL Server 系統管理擴充功能。 這包括：<br/>&bull; &nbsp; [SQL Server 代理程式](sql-server-agent-extension.md?view=sql-server-2017)<br/>&bull; &nbsp; [SQL Server Profiler](https://docs.microsoft.com/sql/azure-data-studio/sql-server-profiler-extension.md?view=sql-server-2017)<br/>&bull; &nbsp; [SQL Server 匯入](sql-server-import-extension.md?view=sql-server-2017) |
| 新增篩選擴充 Profiler 擴充功能中的事件支援。 | &nbsp; |
| 已新增將儲存為 XML 功能，可以將 T-SQL 結果儲存為 XML。 | &nbsp; |
| 已新增的資料層應用程式精靈增強功能。 | &bull; &nbsp; 新增的產生的指令碼 按鈕<br/>&bull; &nbsp; 加入的檢視，以在部署期間提供的資料可能會遺失的警告。 |
| SQL Server 2019 Preview 延伸模組的更新。 | 請參閱[SQL Server 2019 Preview 擴充](sql-server-2019-extension.md?view=sql-server-ver15)。 |
| 結果資料流預設啟用的長時間執行的查詢。 | &nbsp; |
| 已解決的 bug 和問題。 | 請參閱[Bug 和問題，請在 GitHub 上的](https://github.com/Microsoft/azuredatastudio/milestone/23?closed=1)。 |
| &nbsp; | &nbsp; |

## <a name="january-2019-hotfix"></a>2019 年 1 月年 (Hotfix)

2019 年 1 月 16 日&nbsp;  /  &nbsp;版本：1.3.9 &nbsp;  /  &nbsp; Hotfix 版本

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| 已修正 1.3.8 中探索到的一些問題。 | 請參閱[年 1 月 Hotfix 版本中，在 GitHub 上](https://github.com/Microsoft/azuredatastudio/milestone/24?closed=1)。<br/><br/>如需詳細資訊，請參閱：<br/>&bull; &nbsp; [變更記錄檔，在 GitHub 上的](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md)。<br/>&bull; &nbsp; [在 GitHub 上的版本，](https://github.com/Microsoft/azuredatastudio/releases)。 |
| &nbsp; | &nbsp; |

## <a name="january-2019"></a>2019 年 1 月

2019 年 1 月 09 &nbsp;  /  &nbsp;版本：1.3.8

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| 加入新的使用者安裝程式的 Windows。 | 不同於現有的系統安裝程式中，新的使用者安裝程式不需要系統管理員權限。 這也可讓您更輕鬆的升級體驗，非系統管理員。 |
| 已加入的 Azure Active Directory 驗證支援。 | &nbsp; |
| 宣布 Idera SQL DM 效能深入解析 （預覽）。 | &nbsp; |
| SQL Server 匯入延伸模組中的資料層應用程式精靈支援。 | &nbsp; |
| 更新至 SQL Server 2019 Preview 延伸模組。 | 請參閱[SQL Server 2019 Preview 擴充](sql-server-2019-extension.md?view=sql-server-ver15)。 |
| SQL Server Profiler 的功能改進。 | &nbsp; |
| 針對大型查詢 （預覽） 資料流的結果。 | &nbsp; |
| Community extensions: sp_executesql to sql 和新的資料庫。 | &nbsp; |
| 已解決的 bug 和問題。 | 請參閱[Bug 和問題，請在 GitHub 上的](https://github.com/Microsoft/azuredatastudio/milestone/19?closed=1)。 |
| &nbsp; | &nbsp; |

## <a name="november-2018"></a>2018 年 11 月

2018 年 11 月 6 日&nbsp;  /  &nbsp;版本：1.2.4

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| 更新至 SQL Server 2019 Preview 延伸模組。 | 請參閱[SQL Server 2019 Preview 擴充](sql-server-2019-extension.md?view=sql-server-ver15)。 |
| 導入貼上的計劃延伸模組。 | &nbsp; |
| 導入高彩查詢擴充功能，包括 SSMS 編輯器佈景主題。 | &nbsp; |
| 修正 SQL Server Agent、 Profiler、 和匯入延伸模組。 | &nbsp; |
| 修正.Net Core 通訊端 KeepAlive 問題造成被卸除在 macOS 上的非作用中連線。 | &nbsp; |
| 升級至.Net Core 的 SQL 工具服務 2.2 Preview 3 （適用於最終的 AAD 支援）。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-november-2018"></a>Bug 修正，2018 年 11 月

- 修正[發出 # 2933年](https://github.com/Microsoft/azuredatastudio/issues/2933):連接到 Azure SQL DB 遺失
- 修正[發出 # 2914年](https://github.com/Microsoft/azuredatastudio/issues/2914):「 無效的引數 」 例外狀況擴充 OE 資料庫節點
- 修正[發出 # 2935年](https://github.com/Microsoft/azuredatastudio/pull/2935):查詢結果中正確顯示多行訊息
- 修正[發出 # 2906年](https://github.com/Microsoft/azuredatastudio/pull/2906):資料表名稱包含特殊字元時，修正編輯資料文件名稱
- 修正[發出 # 2929年](https://github.com/Microsoft/azuredatastudio/issues/2929):建置延伸模組中的變更記錄指出檢查 VSCode 版本資訊的變更
- 修正[發出 # 2719年](https://github.com/Microsoft/azuredatastudio/issues/2719):高對比佈景主題雙精度浮點數/三合一的圖示
- 修正[發出 #3047](https://github.com/Microsoft/azuredatastudio/pull/3047):新增命令列介面來連接到 SQL Server
- 修正[發出 #3031](https://github.com/Microsoft/azuredatastudio/pull/3031):加入查詢計劃的佈景主題支援

## <a name="october-2018"></a>2018 年 10 月

2018 年 10 月 29 日&nbsp;  /  &nbsp;版本：1.1.4

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| 簡介 Azure 資源總管，瀏覽 Azure SQL Database。 | &nbsp; |
| 改進 物件總管 和 查詢編輯器連線強固性。 | &nbsp; |
| SQL 代理程式擴充功能的改進。 | &nbsp; |
| 更新至 SQL Server 2019 Preview 延伸模組。 | 請參閱[SQL Server 2019 Preview 擴充](sql-server-2019-extension.md?view=sql-server-ver15)。 |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-october-2018"></a>Bug 修正，2018 年 10 月

- 修正[發出 # 2717年](https://github.com/Microsoft/azuredatastudio/issues/2717):XML 資料行結果按一下格式設定
- 修正[發出 # 2993年](https://github.com/Microsoft/azuredatastudio/issues/2993):視窗寬度的結果不完整
- 修正[發出 # 2999年](https://github.com/Microsoft/azuredatastudio/issues/2999):無法載入檔案 System.Diagnostics.Tracing Mac 上的，連接到資料庫時
- 修正[發出 # 2851年](https://github.com/Microsoft/azuredatastudio/issues/2851):TimeSeries 圖表無法正確轉譯
- 修正[發出 # 2996年](https://github.com/Microsoft/azuredatastudio/issues/2996):由於突然出現的工作階段變更的暫存資料表遺失

如需詳細資訊，請參閱 <<c0> [ 變更記錄檔](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md)，並[版本](https://github.com/Microsoft/azuredatastudio/releases)。

## <a name="september-2018-ga-release"></a>2018 年 9 月起 （GA 版本）

2018 年 9 月 24 日&nbsp;  /  &nbsp;版本：1.0 &nbsp;  /  &nbsp; GA 版本

一般可用性版本的 Azure Data Studio (先前稱為 SQL Operations Studio)。

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| 查詢結果方格效能和大量的結果集的 UX 改良功能。 | &nbsp; |
| Visual Studio 程式碼的原始碼重新整理 從 1.23 1.26.1 格線版面配置與改善設定編輯器 （預覽）。 | &nbsp; |
| 螢幕助讀程式、 鍵盤導覽和高對比的協助工具改善。 | &nbsp; |
| 新增`Connection name`選項可以讓您在 [伺服器] 檢視讓替代的顯示名稱。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="announcing-the-sql-server-2019-preview-extension"></a>宣佈 SQL Server 2019 Preview 延伸模組

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| 支援 SQL Server 2019 預覽版功能，包括[巨量資料叢集](../big-data-cluster/big-data-cluster-overview.md)支援。 | 在連SQL Server 2019 預覽版上連線到HDFS/Spark 閘道。<br/><br/>瀏覽 HDFS、 將檔案上傳、 儲存檔案，並啟動例如在 Notebook 中進行分析有用的 CSV 檔案的動作。<br/><br/>提交 Spark 作業，從儀表板，或以滑鼠右鍵按一下物件總管 中的 HDFS/Spark 連接。 |
| Azure Data Studio Notebook。 | 建立或開啟使用整合式的筆記本檢視器的 Notebook。 在此版本中的筆記本檢視器會支援連接到本機的核心和 SQL Server 2019 巨量資料叢集只。<br/><br/>若要了解快速資料準備的檔案格式和資料類型使用在 Notebook 中的文字的程式碼加速器程式庫。 |
| Azure 資源總管。 | Azure 資源總管檢視可讓您瀏覽資料相關的端點，您的 Azure 帳戶，並在 [物件總管] 中建立其連線。 在此版本中都支援 Azure SQL Database 和伺服器。 |
| SQL Server PolyBase 建立外部資料表精靈。 | 使用簡單易用的精靈，建立外部資料表和其支援的中繼資料結構。 在此版本中，支援 SQL Server 和 Oracle 的遠端伺服器。 |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-september-2018"></a>Bug 修正，2018 年 9 月

- 修正[發出 # 2647年](https://github.com/Microsoft/azuredatastudio/issues/143):圖表會回溯花了一大步。
- 修正[發出 # 2648年](https://github.com/Microsoft/azuredatastudio/issues/143):傳回 JSON 的超連結的整個資料行的選取。

如需詳細資訊，請參閱 <<c0> [ 變更記錄檔](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md)，並[版本](https://github.com/Microsoft/azuredatastudio/releases)。

## <a name="august-2018"></a>2018 年 8 月

2018 年 8 月 30 日&nbsp;  /  &nbsp;版本：0.32.8 &nbsp;  /  &nbsp;公開預覽

*年 8 月公開預覽*著重於 bug 修正、 產品穩定和填滿現有案例中的間距。

_0.32.8 包含幾個 0.32.7 中找到的迴歸修正 ([# 1971年](https://github.com/Microsoft/azuredatastudio/issues/1971)， [# 2372年](https://github.com/Microsoft/azuredatastudio/issues/2372))_

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| 宣布 SQL Server 匯入擴充功能。 | &nbsp; |
| SQL Server Profiler 工作階段管理。 | &nbsp; |
| SQL Server Profiler 工作階段範本支援。 | &nbsp; |
| SQL Server Agent 的功能改進。 | &nbsp; |
| 新的社群延伸模組：第一個回應程式套件。 | &nbsp; |
| 生活品質改良：連接字串 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-august-2018"></a>Bug 修正，2018 年 8 月

- 剖析 SQL 查詢編輯器 視窗中的，使用`Parse Syntax`命令。
- 修正[發出 #143](https://github.com/Microsoft/azuredatastudio/issues/143):按兩下 [未選取變數名稱中的]。
- 修正[問題 #387](https://github.com/Microsoft/azuredatastudio/issues/387):SQL 索引標籤 DB 圖示為紅色。
- 修正[發出 #825](https://github.com/Microsoft/azuredatastudio/issues/825):要求：自動連接到目前的伺服器，做為指令碼之後... 
- 修正[問題 1278](https://github.com/Microsoft/azuredatastudio/issues/1278): sqlops.desktop [桌面項目]-名稱和註解的備援值。
- 修正[發出 # 1285年](https://github.com/Microsoft/azuredatastudio/issues/1285):正在更新的原因是在 Windows 中的 移除/取代的應用程式圖示。
- 修正[發出 # 1317年](https://github.com/Microsoft/azuredatastudio/issues/1317):修正在小數點分隔符號。
- 修正[發出 # 1474年](https://github.com/Microsoft/azuredatastudio/issues/1474):取消變更連線會中斷目前的連接。
- 修正[發出 # 1497年](https://github.com/Microsoft/azuredatastudio/issues/1497):選項會被截掉底部的圖表，以檢視。
- 修正[發出 # 1524年](https://github.com/Microsoft/azuredatastudio/issues/1524):殼層/儀表板：主要 viewlet 圖示可拖曳，而且可能會損毀應用程式。
- 修正[發出 # 1578年](https://github.com/Microsoft/azuredatastudio/issues/1578):無法展開/摺疊遠端檔案瀏覽器資料夾名稱，即可。
- 修正[發出 # 1620年](https://github.com/Microsoft/azuredatastudio/issues/1620):功能建議：取得現有連接的連接字串。
- 修正[發出 # 1624年](https://github.com/Microsoft/azuredatastudio/issues/1624):SelectBox 不會變更色彩時停用。
- 修正[發出 amp;#40;sql 1728](https://github.com/Microsoft/azuredatastudio/issues/1728):將儲存為 JSON/EXCEL/CSV 無法工作。
- 修正[發出 # 1744年](https://github.com/Microsoft/azuredatastudio/issues/1744):索引標籤之間切換時，結果窗格會失去其捲動的位置。
- 修正[發出 # 1748年](https://github.com/Microsoft/azuredatastudio/issues/1748):儲存 Excel 檔案，第二個 （及後續） 時間時，出現錯誤訊息。
- 修正[發出 # 1782年](https://github.com/Microsoft/azuredatastudio/issues/1782):編輯資料： 資料格不會還原為原始值按下 Esc 鍵。
- 修正[問題 1836](https://github.com/Microsoft/azuredatastudio/issues/1836)： 與 SQL Operations Studio 無關的.sql 檔案。
- 修正[發出 # 1850年](https://github.com/Microsoft/azuredatastudio/issues/1850):輸入 N '會以 N' '。
- 修正[發出 # 1985年](https://github.com/Microsoft/azuredatastudio/issues/1985):1 個資料行，將從查詢結果方格複製為關閉。
- 修正[發出 # 1998年](htpts://github.com/Microsoft/azuredatastudio/pull/1998):加入至對話方塊相關的 VS Code 版本。
- 修正[發出 # 2042年](https://github.com/Microsoft/azuredatastudio/pull/2042):Agent：已啟用 按鈕，從 sql 檔案匯入查詢。
- 修正[發出 # 2091年](https://github.com/Microsoft/azuredatastudio/issues/2091):無法使用快速鍵 Ctrl + C 複製結果 窗格。
- 修正[發出 # 2099年](https://github.com/Microsoft/azuredatastudio/pull/2099):新增更多的 saveAsCsv 選項。
- 修正[發出 # 2107年](https://github.com/Microsoft/azuredatastudio/issues/2107):更新儀表板和 Profiler 的文件的文件圖示。
- 修正[發出 # 2129年](https://github.com/Microsoft/azuredatastudio/pull/2129):切換索引標籤時，請儲存編輯資料捲軸位置。
- 修正[發出 # 2152年](https://github.com/Microsoft/azuredatastudio/issues/2152):結果方格資料列指標以零為起始。

### <a name="known-issues-august-2018"></a>已知的問題，2018 年 8 月

- [問題 2371](https://github.com/Microsoft/azuredatastudio/issues/2371)儲存為 Excel 僅將第一個資料列的資料
- [問題 # 2150年](https://github.com/Microsoft/azuredatastudio/issues/2150):無法連接到容器中的 SQL 的 Ubuntu 16.04

## <a name="july-2018"></a>2018 年 7 月

2018 年 7 月 19 日&nbsp;  /  &nbsp;版本：0.31.4 &nbsp;  /  &nbsp;公開預覽

*年 7 月公開預覽*著重於下列項目：

- 初始版本的 SQL Server Agent 組態案例。
- SQL Server Profiler 工作階段並檢視範本的增強功能。
- 持續的 bug 修正的客戶回報的 GitHub 問題。

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| [SQL Operations Studio 擴充功能的 SQL Server Agent](sql-server-agent-extension.md)增強功能。 | 在左窗格中的警示、 運算子和 Proxy 和圖示加入的檢視。<br/><br/>已新增新的工作、 新增作業步驟中，新的警示，和 New 運算子的對話方塊。<br/><br/>已新增刪除作業、 刪除警示，以及刪除運算子 （右鍵）。<br/><br/>新增先前執行的視覺效果。<br/><br/>已新增的每個資料行名稱的篩選條件。 |
| [SQL Operations Studio 擴充功能的 SQL Server Profiler](sql-server-profiler-extension.md)增強功能。 | 加入預設的 5 個範本，若要檢視擴充事件。<br/><br/>已新增的伺服器/資料庫連接名稱。<br/><br/>已新增的對 Azure SQL Database 執行個體的詳細資訊。<br/><br/>新增結束時 Profiler 仍在執行時，系統會關閉索引標籤的 Profiler 的詳細建議。 |
| 合併指令碼延伸模組的版本。 | &nbsp; |
| 新增延伸模組作者的精靈和對話方塊擴充性點。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-july-2018"></a>Bug 修正，2018 年 7 月

- 修正[發出 728](https://github.com/Microsoft/azuredatastudio/issues/728):在 macOS 上加入連接沒有回應
- 修正[發出 1612年](https://github.com/Microsoft/azuredatastudio/issues/1612):結果方格中文字顯示亂七八糟國際字元
- 修正[發出 1693年](https://github.com/Microsoft/azuredatastudio/issues/1693):備份的對話方塊：檔案瀏覽器 UI 已中斷
- 修正[發出 1713年](https://github.com/Microsoft/azuredatastudio/issues/1713):受影響的資料列數目
- 修正[發出 1718年](https://github.com/Microsoft/azuredatastudio/issues/1718):無法連線到任何資料來源
- 修正[發出 1719年](https://github.com/Microsoft/azuredatastudio/issues/1719):TypeError 連接到伺服器時
- 修正[發出 1724年](https://github.com/Microsoft/azuredatastudio/issues/1724):延伸模組對話方塊已停止運作
- 修正[發出 1749年](https://github.com/Microsoft/azuredatastudio/issues/1749):BUG:取得解譯資料行中的 HTML 資料
- 修正[發出 1789年](https://github.com/Microsoft/azuredatastudio/issues/1789):擴充性： 如果您新增的連線提供者解除安裝將會永遠不會從清單移除
- 修正[發出 1791年](https://github.com/Microsoft/azuredatastudio/issues/1791):Sqlops 擴充功能： queryeditor.connect() 連接到目標資料庫，但 UI 不會顯示編輯器連接
- 修正[發出 1799年](https://github.com/Microsoft/azuredatastudio/issues/1799):前 10 個 DB 大小圖表在區分大小寫的執行個體上無法運作
- 修正[問題 1814](https://github.com/Microsoft/azuredatastudio/issues/1814): sqlops.d.ts 打字錯誤導致隱含 'any' 類型的定義
- 修正[發出 1817年](https://github.com/Microsoft/azuredatastudio/issues/1817):錯誤 de Ortografia
- 修正[發出 1830年](https://github.com/Microsoft/azuredatastudio/issues/1830):設定 ButtonComponent iconPath component() 呼叫之後，不會變更圖示
- 修正[發出 1843年](https://github.com/Microsoft/azuredatastudio/issues/1843):較佳的資料表組織

## <a name="june-2018"></a>2018 年 6 月

2018 年 6 月 20 日&nbsp;  /  &nbsp;版本：0.30.6 &nbsp;  /  &nbsp;公開預覽

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| **SQL Operations Studio 的 SQL Server Profiler _Preview_** 延伸最初發行版本。 | &nbsp; |
| 新**SQL 資料倉儲**擴充功能包含豐富的可自訂儀表板 widget 呈現到您的資料倉儲的深入解析。 | 這會解除鎖定金鑰管理和調整您的資料倉儲，以確保它適合一致的效能案例。 |
| **編輯資料 」 篩選和排序"** 支援。 | &nbsp; |
| **SQL Operations Studio 的 SQL Server Agent _Preview_** 擴充功能增強作業和作業歷程記錄檢視。 | &nbsp; |
| 改善**精靈和對話方塊 UI 產生器架構**擴充性 Api。 | &nbsp; |
| 更新 VS 程式碼平台的原始程式碼。 | 整合下列版本：<br/>&bull; &nbsp; [2018 年 3 月起 (1.22)](https://code.visualstudio.com/updates/v1_22)<br/>&bull; &nbsp; [2018 年 4 月起 (1.23)](https://code.visualstudio.com/updates/v1_23) |
| &nbsp; | &nbsp; |

### <a name="github-issues-fixes-june-2018"></a>GitHub 問題修正，2018 年 6 月

- 功能要求 ([發出 1204年](https://github.com/Microsoft/azuredatastudio/issues/1204)):請對結果格線自動調整資料行寬度資料，並請記得手動變更，如果重新執行相同的查詢。
- 修正[發出 1398年](https://github.com/Microsoft/azuredatastudio/issues/1398):應該顯示新增訊息，並新增帳戶 [帳戶] 按鈕，當連結的帳戶為空白時。
- 修正[發出 1399年](https://github.com/Microsoft/azuredatastudio/issues/1399):摺疊檢視時，會中斷連結的帳戶 索引標籤。
- 修正[發出 1374年](https://github.com/Microsoft/azuredatastudio/issues/1374):從磁碟開啟的.sql 檔時，SQL 工具服務會當機。
- 修正[發出 1372年](https://github.com/Microsoft/azuredatastudio/issues/1372):遺漏 SQL 關鍵字"BETWEEN"。
- 修正[發出 1395年](https://github.com/Microsoft/azuredatastudio/issues/1395):比對' 關鍵字會損毀 SQL 工具服務。
- 修正[發出 1496年](https://github.com/Microsoft/azuredatastudio/issues/1496):「 新的 Profiler 」 快顯功能表選項，在 [物件總管] 中的不執行任何動作。
- 修正[發出 1495年](https://github.com/Microsoft/azuredatastudio/issues/1495):查詢編輯器 」 Explain"查詢計劃已中斷。

## <a name="may-2018"></a>2018 年

2018 年 7 日&nbsp;  /  &nbsp;版本：0.29.3 &nbsp;  /  &nbsp;公開預覽

*5月公開預覽版*著重於穩定性及 bug 修正。

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| 宣布可用延伸模組管理員 中的 Redgate SQL Search 延伸模組。 | &nbsp; |
| 適用於 10 種語言的社群當地語系化。 | 德文、 西班牙文、 法文、 義大利文、 日文、 韓文、 葡萄牙文、 俄文、 簡體中文和繁體中文。 |
| 遙測集合的變更。 | &bull; &nbsp; 降低的遙測收集。<br/>&bull; &nbsp; 改善退出體驗。<br/>&bull; &nbsp; 產品中的隱私權聲明連結。 |
| 擴充管理員已改善的 Marketplace 體驗。 | 更容易地探索社群的延伸。 |
| SQL 代理程式擴充功能。 | &bull; &nbsp; 作業。<br/>&bull; &nbsp; 工作歷程記錄檢視的改進。 |
| 更新擴充功能 whoisactive 和伺服器報表。 | &nbsp; |
| 改善的管理儀表板內容捲動。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fix-github-issues"></a>修正 GitHub 問題

- 修正[發出 703](https://github.com/Microsoft/azuredatastudio/issues/703):編輯資料中輸入類似 HTML 的文字會導致無法正確顯示，直到重新整理之前的值
- 修正[問題 821](https://github.com/Microsoft/azuredatastudio/issues/821): azuredatastudio.deb 封裝相依性
- 修正[發出 1260年](https://github.com/Microsoft/azuredatastudio/issues/1260):關鍵字 'distinct' 不反白顯示
- 修正[發出 1332年](https://github.com/Microsoft/azuredatastudio/issues/1332):編輯資料還原的資料列無法運作
- 修正[發出 1215年](https://github.com/Microsoft/azuredatastudio/issues/1215):SQL 代理程式擴充功能和狀態列
- 修正[發出 1316年](https://github.com/Microsoft/azuredatastudio/issues/1316):SQL 代理程式不要之後變更視窗大小的調整大小

## <a name="april-2018"></a>2018 年 4 月

2018 年 4 月 25 日&nbsp;  /  &nbsp;版本：0.28.6 &nbsp;  /  &nbsp;公開預覽

*4 月公開預覽版*包含 bug 修正和增強功能。

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| SQL 代理程式預覽擴充功能的增強功能： | &nbsp; |
| &nbsp; &nbsp; &nbsp; 改善的對檔案的詳細資訊。 | &bull; &nbsp; 大型檔案。<br/>&bull; &nbsp; 受保護的檔案，來儲存受保護的系統管理員。<br/>&bull; &nbsp; 儲存\>256m SQL Operations Studio 內的檔案。 |
| &nbsp; &nbsp; &nbsp; 分割的整合式終端機。 | 同時使用多個開啟的終端機。 |
| &nbsp; &nbsp; &nbsp; 更快速的安裝和啟動時間。 | 減少的安裝磁碟上的檔案計數英呎列印。 |
| &nbsp; | &nbsp; |

### <a name="fix-github-issues-april-2018"></a>修正 GitHub 問題，2018 年 4 月

- 修正[發出 37](https://github.com/Microsoft/azuredatastudio/issues/37):當圖表檢視器擲回錯誤時，就會發生未預期的行為。
- 修正[發出 462](https://github.com/Microsoft/azuredatastudio/issues/462):功能請求：根據預設展開伺服器群組的選項。
- 修正[問題 606](https://github.com/Microsoft/azuredatastudio/issues/606): intellisense-'update' 命令的錯誤提供建議。
- 修正[發出 967](https://github.com/Microsoft/azuredatastudio/issues/967):預期的查詢計劃時結果方格中選取 XML 執行程序。
- 修正[發出 1023年](https://github.com/Microsoft/azuredatastudio/issues/1023):加入 flyfishingdba ms_foreachdb 呼叫的方括號。
- 修正[發出 1048年](https://github.com/Microsoft/azuredatastudio/issues/1048):登入前 SSL/TLS 交握時發生錯誤。
- 修正[發出 1050年](https://github.com/Microsoft/azuredatastudio/issues/1050):顯示錯誤之前的清除 insights 檢視。
- 修正[發出 1057年](https://github.com/Microsoft/azuredatastudio/issues/1057):還原和檔案總管 widget 中新的查詢動作都會中斷。
- 修正[發出 1068年](https://github.com/Microsoft/azuredatastudio/issues/1068):儀表板輸出 windows 彈出並為 Azure SQL Database 的錯誤訊息。
- 修正[發出 1069年](https://github.com/Microsoft/azuredatastudio/issues/1069):連接對話方塊會顯示一開始顯示時的所需的伺服器錯誤。
- 修正[發出 1070年](https://github.com/Microsoft/azuredatastudio/issues/1070):伺服器群組現在需要按兩下以展開。
- 修正[發出 1072年](https://github.com/Microsoft/azuredatastudio/issues/1072):選取的控制項背景是半透明效果。
- 修正[發出 1115年](https://github.com/Microsoft/azuredatastudio/issues/1115):修正 SQL Operations Studio 中的所有高對比的協助工具問題。
- 修正[發出 1101年](https://github.com/Microsoft/azuredatastudio/issues/1101):延伸模組無法升級 「 下載手動 」 連結連至錯誤的位置。
- 修正[發出 1103年](https://github.com/Microsoft/azuredatastudio/issues/1103):在 [首頁] 索引標籤上未使用的 V 捲軸。
- 修正[發出 1104年](https://github.com/Microsoft/azuredatastudio/issues/1104):SQL 延伸模組索引標籤會停止運作。

### <a name="visual-studio-code-121-platform"></a>Visual Studio 程式碼 1.21 平台

4 月公開預覽中的反白顯示為 Visual Studio 程式碼 1.21 平台的原始碼的重新整理。 這會有數個更新的核心編輯器和 workbench 從先前的 1.19 的同步處理點。 以下為部分範例：

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| [新的通知 UI](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui)。 | 輕鬆管理並檢閱 SQL Operations Studio 的通知。 |
| [整合式終端機分割](https://code.visualstudio.com/updates/v1_21#_split-terminals)。 | 同時使用多個開啟的終端機。 |
| [將大型和受保護的檔案儲存](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges)。 | 儲存受保護的系統管理員和\>256m SQL Operations Studio 內的檔案。 |
| [已改善大型檔案支援](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements)。 | 文字緩衝區最佳化大型檔案。 |
| [改良的設定搜尋](https://code.visualstudio.com/updates/v1_20#_settings-search)。 | 輕鬆地找到正確的設定值，以自然語言搜尋。 |
| [全域程式碼片段](https://code.visualstudio.com/updates/v1_20#_global-snippets)。 | 建立您可以使用所有的檔案類型的程式碼片段。 |
| [總管複選](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer)。 | 一次在多個檔案上執行動作。 |
| [錯誤與警告，在 [總管]](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer)。 | 快速瀏覽至您的程式碼基底中的錯誤。 |
| [拖曳和卸除、 複製及貼上整個 windows](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support)。 | 開啟 SQL Operations Studio 視窗之間移動檔案。 |
| [Git 子模組支援](https://code.visualstudio.com/updates/v1_20#_git-submodules)。 | 執行巢狀的 Git 儲存機制的 Git 作業。 |
| [終端機螢幕助讀程式支援](https://code.visualstudio.com/updates/v1_20#_screen-reader-support)。 | 現在有整合式終端機**螢幕讀取器最佳化**模式。 |
| [置中的編輯器配置](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout)。 | 最大化您的程式碼檢視螢幕面積。 |
| [水平的搜尋結果 （預覽）](https://code.visualstudio.com/updates/v1_21#_horizontal-search)。 | 您可以現在水平的面板中檢視搜尋結果。 |
| &nbsp; | &nbsp; |

如需詳細資訊，簽出[Visual Studio Code 2 月版本資訊](https://code.visualstudio.com/updates/v1_21)，而[Visual Studio Code 1 月版本資訊](https://code.visualstudio.com/updates/v1_20)。

如需詳細資訊，請參閱 <<c0> [ 變更記錄檔](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md)。

## <a name="march-2018"></a>2018 年 3 月

2018 年 3 月 28 日&nbsp;  /  &nbsp;版本：0.27.3 &nbsp;  /  &nbsp;公開預覽

*年 3 月公開預覽*愈來愈最常發生的 GitHub 問題，並致力於改善我們的擴充性案例。 特別啟用擴充功能管理員，改善儀表板管理，並提供 SQL Agent和 insights 擴充功能。 此版本包含下列增強功能：

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| 提升儀表板的擴充性模型，來支援索引標籤式的深入解析和設定窗格。 | 延伸模組管理員可讓簡單的併購的延伸模組。<br/><br/>儀表板的預存程序的延伸模組\_從 whoisactive [whoisactive.com](http://www.whoisactive.com)。<br/><br/>如需詳細資訊，請參閱[擴充功能的 SQL Operations Studio](extensions.md)。 |
| 新增額外[連線和物件總管 中的擴充性 Api](https://github.com/Microsoft/azuredatastudio/wiki/Extensibility-API)管理。 | &nbsp; |
| 若要修正問題影響到重要的客戶繼續[的 GitHub 問題](https://github.com/Microsoft/azuredatastudio/issues)。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="february-2018"></a>2018 年 2 月

2018 年 2 月 15 日&nbsp;  /  &nbsp;版本：0.26.7 &nbsp;  /  &nbsp;公開預覽

*2 月公用預覽*含有一些功能建議和高優先順序的 bug 修正。 此版本包含下列增強功能：

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| 新的版本可供下載時引進安裝自動更新，提供通知。 | &nbsp; |
| [連接] 對話方塊**資料庫**欄位現在是以動態方式填入的下拉式清單將包含從指定的伺服器填入資料庫清單。 | &nbsp; |
| 介紹連線擴充性 API。 | &nbsp; |
| VS Code 編輯器 1.19 整合。 | &nbsp; |
| 更新上車數個查詢計劃檢視器改善 JustinPealing/html-查詢計劃的元件。 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixed-issues-february-2018"></a>已修正的問題，2018 年 2 月

- 修正[第 6 期](https://github.com/Microsoft/azuredatastudio/issues/6):開啟新查詢索引標籤時，請保持連線和選取的資料庫。
- 修正[第 22 期](https://github.com/Microsoft/azuredatastudio/issues/22):'Server Name'.database 和資料庫名稱-可以這些是下拉式清單，而不是文字方塊？
- 修正[發出 549](https://github.com/Microsoft/azuredatastudio/issues/549):無訊息模式中極/無訊息安裝會導致在安裝後開啟的應用程式。
- 修正[發出 481](https://github.com/Microsoft/azuredatastudio/issues/481):新增 「 檢查更新 」 的選項。
- SQL 編輯器顏色標示和自動完成的修正程式：
  - 修正[發出 584](https://github.com/Microsoft/azuredatastudio/issues/584):「 完整 」 不反白顯示 intellisense 的關鍵字。
  - 修正[發出 345](https://github.com/Microsoft/azuredatastudio/issues/345):以色彩標示在編輯器中的 SQL 函式。
  - 修正[問題 300](https://github.com/Microsoft/azuredatastudio/issues/300): [#tempData] 最新"]"將會顯示綠色。
  - 修正[發出 225](https://github.com/Microsoft/azuredatastudio/issues/225):關鍵字色彩不相符。
  - 修正[發出 60](https://github.com/Microsoft/azuredatastudio/issues/60):無效的 sql 語法色彩反白顯示使用 from 子句中的暫存資料表時。

## <a name="january-2018"></a>2018 年 1 月

2018 年 1 月 17 日&nbsp;  /  &nbsp;版本：0.25.4 &nbsp;  /  &nbsp;公開預覽

*1 月公用預覽*含有一些功能建議和高優先順序的 bug 修正。 此版本包含下列增強功能：

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| 在 [連接] 對話方塊中提供儲存的伺服器連接。 | &nbsp; |
| 啟用 最忙碌的結束。 根據預設，若要啟用，請參閱熱結束已關閉[熱結束設定](settings.md#hot-exit)。 | &nbsp; |
| 依據伺服器群組 索引標籤-著色。 根據預設，若要啟用，請參閱已關閉的索引標籤著色[索引標籤的色彩設定](settings.md#tab-color)。 | &nbsp; |
| 變更*伺服器名稱*要*Server*連接對話方塊中。 | &nbsp; |
| 修正中斷*執行目前查詢*命令。 | &nbsp; |
| 修正指令碼錯誤的拖放重大。 | &nbsp; |
| 修正不正確的已釘選 [開始] 功能表圖示。 | &nbsp; |
| 修正遺漏商標圖示的 Azure 帳戶。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="december-2017"></a>2017 年 12 月

2017 年 12 月 19 日&nbsp;  /  &nbsp;版本：0.24.1 &nbsp;  /  &nbsp;公開預覽

*年 12 月公開預覽*所有功能領域，以及下列增強功能包括數個 bug 修正：

&nbsp;

| 變更 | 詳細資料 |
| :----- | :------ |
| 建立防火牆規則對話方塊現在是可協助連接至 Azure SQL Database 和 Azure SQL 資料倉儲。 | &nbsp; |
| 已新增的 Windows 安裝程式，以及 Linux DEB 和 RPM 安裝套件。 | &nbsp; |
| 管理儀表板視覺化版面配置編輯器。 | &nbsp; |
| *指令碼為 Alter*並*指令碼執行*命令。 | &nbsp; |
| *使用實際的計劃執行目前查詢*命令。 | &nbsp; |
| 整合 VS Code 1.18.1 編輯器平台。 | &nbsp; |
| 啟用側載的 VSIX 擴充功能檔案。 | &nbsp; |
| 支援"GO N"批次反覆項目語法。 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="november-2017"></a>2017 年 11 月

2017 年 11 月 15 日&nbsp;  /  &nbsp;版本：0.23.6

- 初始版本的[!INCLUDE[name-sos](../includes/name-sos-short.md)]。

## <a name="next-steps"></a>後續步驟

請參閱下列快速入門，以開始使用其中一項：

- [連線與查詢 SQL Server](quickstart-sql-server.md)
- [連線與查詢 Azure SQL Database](quickstart-sql-database.md)
- [連線與查詢 Azure 資料倉儲](quickstart-sql-dw.md)

參與[!INCLUDE[name-sos](../includes/name-sos-short.md)]:

- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio)
