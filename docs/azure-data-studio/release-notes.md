---
title: Azure Data Studio 版本資訊 |Microsoft Docs
description: Azure Data Studio 版本資訊
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dfa3636ddba734d9c6ee6c9d9da4560a3cd61304
ms.sourcegitcommit: ef115025e57ec342c14ed3151ce006f484d1fadc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/18/2018
ms.locfileid: "49411195"
---
# <a name="azure-data-studio-release-notes"></a>Azure Data Studio 版本資訊

**[下載 10 月份版本 ！](download.md)**

## <a name="october-2018-october-release"></a>2018 年 10 月起 （年 10 月發行）

發行日期： 2018 年 10 月 18 日  
版本： 1.1.3

- 簡介 Azure 資源總管，瀏覽 Azure SQL Database
- 改善 物件總管 和 查詢編輯器連線強固性
- SQL 代理程式擴充功能改進
- 若要更新[SQL Server 2019 Preview 延伸模組](https://docs.microsoft.com/sql/azure-data-studio/sql-server-2019-extension?view=sql-server-ver15)

### <a name="bug-fixes"></a>錯誤修正

如需詳細資訊，請參閱 <<c0> [ 變更記錄檔](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md)，並[版本](https://github.com/Microsoft/azuredatastudio/releases)。

## <a name="september-2018-september-ga-release"></a>2018 年 9 月起 （9 月 GA 版本）

發行日期： 2018 年 9 月 24 日  
版本： 1.0

一般可用性版本的 Azure Data Studio (先前稱為 SQL Operations Studio)。

- 宣布 SQL Server 2019 預覽版延伸模組。
  - 支援 SQL Server 2019 預覽版功能，包括[巨量資料叢集](../big-data-cluster/big-data-cluster-overview.md)支援。
    - 在連SQL Server 2019 預覽版上連線到HDFS/Spark 閘道。
    - 瀏覽 HDFS、 將檔案上傳、 儲存檔案，並啟動例如在 Notebook 中進行分析有用的 CSV 檔案的動作。
    - 提交 Spark 作業，從儀表板，或以滑鼠右鍵按一下物件總管 中的 HDFS/Spark 連接。
  - Azure Data Studio Notebook
    - 建立或開啟使用整合式的筆記本檢視器的 Notebook。 在此版本中的筆記本檢視器會支援連接到本機的核心和 SQL Server 2019 巨量資料叢集只。
    - 若要了解快速資料準備的檔案格式和資料類型使用在 Notebook 中的文字的程式碼加速器程式庫。
  - Azure 資源總管
    - Azure 資源總管檢視可讓您瀏覽資料相關的端點，您的 Azure 帳戶，並在 [物件總管] 中建立其連線。 在此版本中都支援 Azure SQL Database 和伺服器。
  - SQL Server Polybase 建立外部資料表精靈
    - 使用簡單易用的精靈，建立外部資料表和其支援的中繼資料結構。 在此版本中，支援 SQL Server 和 Oracle 的遠端伺服器。
- 查詢結果方格效能和大量的結果集的 UX 改良功能。
- Visual Studio 程式碼的原始碼重新整理 從 1.23 1.26.1 格線版面配置與改善設定編輯器 （預覽）。
- 螢幕助讀程式、 鍵盤導覽和高對比的協助工具改善。
- 新增`Connection name`選項可以讓您在 [伺服器] 檢視讓替代的顯示名稱。

### <a name="bug-fixes"></a>錯誤修正

- 修正[問題 2647](https://github.com/Microsoft/azuredatastudio/issues/143)： 圖表回溯花了一大步。
- 修正[問題 2648](https://github.com/Microsoft/azuredatastudio/issues/143)： 傳回 JSON 的超連結的整個資料行的選取。
- ...

如需詳細資訊，請參閱 <<c0> [ 變更記錄檔](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md)，並[版本](https://github.com/Microsoft/azuredatastudio/releases)。


## <a name="august-2018-august-public-preview"></a>2018 年 8 月起 （年 8 月公開預覽）

發行日期： 2018 年 8 月 30 日  
版本： 0.32.8

*0.32.8 包含幾個 0.32.7 中找到的迴歸修正 ([# 1971年](https://github.com/Microsoft/azuredatastudio/issues/1971)， [# 2372年](https://github.com/Microsoft/azuredatastudio/issues/2372)*)

*年 8 月公開預覽*著重於 bug 修正、 產品穩定和填滿現有案例中的間距。  

- 宣布 SQL Server 匯入擴充功能
- SQL Server Profiler 工作階段管理
- SQL Server Profiler 工作階段範本支援
- SQL Server Agent 的改進
- 新的社群延伸模組： 第一個回應者套件
- 生活品質改良： 連接字串

### <a name="bug-fixes"></a>錯誤修正

- 剖析 SQL 查詢編輯器 視窗中的，使用`Parse Syntax`命令。
- 修正[問題 143](https://github.com/Microsoft/azuredatastudio/issues/143)： 按兩下不選取變數名稱中的 。
- 修正[問題 387](https://github.com/Microsoft/azuredatastudio/issues/387): SQL DB 索引標籤圖示為紅色。
- 修正[問題 825](https://github.com/Microsoft/azuredatastudio/issues/825)： 要求： 自動連接到目前的伺服器，做為指令碼之後... 
- 修正[問題 1278](https://github.com/Microsoft/azuredatastudio/issues/1278): sqlops.desktop [桌面項目]-名稱和註解的備援值。
- 修正[問題 1285](https://github.com/Microsoft/azuredatastudio/issues/1285)： 更新會導致應用程式是在 Windows 中的 [移除/取代] 圖示。
- 修正[問題 1317](https://github.com/Microsoft/azuredatastudio/issues/1317)： 修正在小數點分隔符號。
- 修正[問題 1474](https://github.com/Microsoft/azuredatastudio/issues/1474)： 取消變更連線會中斷目前的連接。
- 修正[問題 1497](https://github.com/Microsoft/azuredatastudio/issues/1497)： 以圖表方式檢視選項會被截掉底部。
- 修正[問題 1524](https://github.com/Microsoft/azuredatastudio/issues/1524)： 殼層/儀表板： Main viewlet 圖示可拖曳，而且可能會損毀應用程式。
- 修正[問題 1578](https://github.com/Microsoft/azuredatastudio/issues/1578)： 無法展開/摺疊遠端檔案瀏覽器資料夾名稱，即可。
- 修正[問題 1620](https://github.com/Microsoft/azuredatastudio/issues/1620)： 功能建議： 取得現有連接的連接字串。
- 修正[問題 1624](https://github.com/Microsoft/azuredatastudio/issues/1624): SelectBox 不會變更色彩時停用。
- 修正[問題 1728](https://github.com/Microsoft/azuredatastudio/issues/1728)： 將儲存為 JSON/EXCEL/CSV 無法工作。
- 修正[問題 1744](https://github.com/Microsoft/azuredatastudio/issues/1744)： 索引標籤之間切換時，結果窗格會失去其捲動的位置。
- 修正[問題 1748](https://github.com/Microsoft/azuredatastudio/issues/1748)： 儲存 Excel 檔案，第二個 （及後續） 時間時，出現錯誤訊息。
- 修正[問題 1782](https://github.com/Microsoft/azuredatastudio/issues/1782)： 編輯資料： 資料格不會還原為原始值按下 Esc 鍵。
- 修正[問題 1836](https://github.com/Microsoft/azuredatastudio/issues/1836)： 與 SQL Operations Studio 無關的.sql 檔案。
- 修正[問題 1850](https://github.com/Microsoft/azuredatastudio/issues/1850)： 輸入 N '會以 N' '。
- 修正[問題 1985](https://github.com/Microsoft/azuredatastudio/issues/1985)： 從查詢結果方格複製為關閉 1 個資料行。
- 修正[問題 1998](htpts://github.com/Microsoft/azuredatastudio/pull/1998)： 關於對話来加入 VS Code 版本。
- 修正[問題 2042](https://github.com/Microsoft/azuredatastudio/pull/2042)： 代理程式： 已啟用 按鈕，從 sql 檔案匯入查詢。
- 修正[問題 2091](https://github.com/Microsoft/azuredatastudio/issues/2091)： 無法使用快速鍵 Ctrl + C 複製結果 窗格。
- 修正[問題 2099](https://github.com/Microsoft/azuredatastudio/pull/2099)： 新增更多的 saveAsCsv 選項。
- 修正[問題 2107](https://github.com/Microsoft/azuredatastudio/issues/2107)： 儀表板和 Profiler 的文件的更新文件圖示。
- 修正[問題 2129](https://github.com/Microsoft/azuredatastudio/pull/2129)： 儲存編輯資料會切換索引標籤時，捲軸位置。
- 修正[問題 2152](https://github.com/Microsoft/azuredatastudio/issues/2152)： 結果方格資料列指標以零起始。

## <a name="known-issues"></a>已知問題

- [問題 2371](https://github.com/Microsoft/azuredatastudio/issues/2371)儲存為 Excel 僅將第一個資料列的資料
- [問題 2150](https://github.com/Microsoft/azuredatastudio/issues/2150)： 無法連接到容器中的 SQL 的 Ubuntu 16.04


## <a name="july-2018-july-public-preview"></a>2018 年 7 月起 （7 月公開預覽）

發行日期： 2018 年 7 月 19 日  
版本： 0.31.4

*年 7 月公開預覽*著重的初始版本的 SQL Server Agent 設定案例，SQL Server Profiler 工作階段並檢視範本的增強功能和持續的 bug 修正的客戶回報的 GitHub 問題。 此版本包含下列重點：  

- [SQL Operations Studio 擴充功能的 SQL Server Agent](sql-server-agent-extension.md)增強功能
 - 新增的警示、 運算子和 Proxy 和圖示上檢視左窗格
 - 已新增的對話方塊，用於新的工作、 新增作業步驟、 新增警示，和新的運算子
 - 已新增刪除作業、 刪除警示，以及刪除運算子 （右鍵）
 - 新增先前執行視覺效果
 - 已新增的篩選器，針對每個資料行名稱
- [SQL Operations Studio 擴充功能的 SQL Server Profiler](sql-server-profiler-extension.md)增強功能
 - 新增的快速鍵來快速啟動並開始/停止 Profiler
 - 加入預設的 5 個範本，若要檢視擴充事件
 - 已新增的伺服器/資料庫連接名稱
 - 已新增的支援 Azure SQL Database 執行個體
 - 已新增的建議，結束時 Profiler 仍在執行時，系統會關閉索引標籤的 Profiler
- 版本的合併指令碼擴充功能
- 新增延伸模組作者的精靈和對話方塊擴充性點
- 修正 GitHub 問題：
 - 修正[問題 728](https://github.com/Microsoft/azuredatastudio/issues/728)： 在 macOS 上的加入連接沒有回應
 - 修正[問題 1612](https://github.com/Microsoft/azuredatastudio/issues/1612)： 結果方格中文字顯示亂七八糟國際字元
 - 修正[問題 1693](https://github.com/Microsoft/azuredatastudio/issues/1693)： 備份對話方塊： 檔案瀏覽器 UI 已中斷
 - 修正[問題 1713](https://github.com/Microsoft/azuredatastudio/issues/1713)： 受影響的資料列數目
 - 修正[問題 1718](https://github.com/Microsoft/azuredatastudio/issues/1718)： 無法連接到任何資料來源
 - 修正[問題 1719](https://github.com/Microsoft/azuredatastudio/issues/1719): TypeError 連接到伺服器時
 - 修正[問題 1724](https://github.com/Microsoft/azuredatastudio/issues/1724)： 延伸模組對話方塊已停止運作
 - 修正[問題 1749](https://github.com/Microsoft/azuredatastudio/issues/1749)： 錯誤： 資料行中的 HTML 資料取得解譯
 - 修正[問題 1789](https://github.com/Microsoft/azuredatastudio/issues/1789)： 擴充性： 如果您新增的連線提供者解除安裝將會永遠不會從清單移除
 - 修正[問題 1791](https://github.com/Microsoft/azuredatastudio/issues/1791): Sqlops 延伸模組： queryeditor.connect() 連接到目標資料庫，但 UI 不會顯示連接編輯器
 - 修正[問題 1799](https://github.com/Microsoft/azuredatastudio/issues/1799): Top 10 DB 大小圖表在區分大小寫的執行個體上無法運作
 - 修正[問題 1814](https://github.com/Microsoft/azuredatastudio/issues/1814): sqlops.d.ts 打字錯誤導致隱含 'any' 類型的定義
 - 修正[問題 1817](https://github.com/Microsoft/azuredatastudio/issues/1817)： 錯誤 de Ortografia
 - 修正[問題 1830](https://github.com/Microsoft/azuredatastudio/issues/1830)： 設定 ButtonComponent iconPath component() 呼叫之後，不會變更圖示
 - 修正[問題 1843](https://github.com/Microsoft/azuredatastudio/issues/1843)： 較佳的資料表組織


## <a name="june-2018-june-public-preview"></a>2018 年 6 月起 （年 6 月公開預覽）

發行日期： 2018 年 6 月 20 日  
版本： 0.30.6

*年 6 月公開預覽*包含下列重點：  

- **SQL Operations Studio 的 SQL Server Profiler *Preview*** 延伸最初發行版本。
- 新**SQL 資料倉儲**擴充功能包含豐富的可自訂儀表板 widget 呈現到您的資料倉儲的深入解析。 這會解除鎖定金鑰管理和調整您的資料倉儲，以確保它適合一致的效能案例。
- **編輯資料 」 篩選和排序"** 支援。
- **SQL Operations Studio 的 SQL Server Agent *Preview*** 擴充功能增強作業和作業歷程記錄檢視。
- 改善**精靈和對話方塊 UI 產生器架構**擴充性 Api。
- 更新 VS 程式碼平台來源的程式碼整合[年 3 月 2018 (1.22)](https://code.visualstudio.com/updates/v1_22)並[年 4 月 2018 (1.23)](https://code.visualstudio.com/updates/v1_23)釋放。
- 修正 GitHub 問題：
  - 功能要求 ([問題 1204](https://github.com/Microsoft/azuredatastudio/issues/1204)): 請資料，讓結果格線自動調整資料行寬度及 （或) 重新執行相同的查詢時，請記得手動變更。
  - 修正[問題 1398](https://github.com/Microsoft/azuredatastudio/issues/1398)： 應該顯示新增訊息，並新增帳戶 [帳戶] 按鈕，當連結的帳戶為空白時。
  - 修正[問題 1399](https://github.com/Microsoft/azuredatastudio/issues/1399)： 摺疊檢視時，會中斷連結的帳戶 索引標籤。
  - 修正[問題 1374](https://github.com/Microsoft/azuredatastudio/issues/1374): SQL 工具服務損毀時從磁碟開啟的.sql 檔。
  - 修正[問題 1372](https://github.com/Microsoft/azuredatastudio/issues/1372)： 遺漏的 SQL 關鍵字"BETWEEN"。
  - 修正[問題 1395](https://github.com/Microsoft/azuredatastudio/issues/1395): 比對' 關鍵字損毀的 SQL 工具服務。
  - 修正[問題 1496](https://github.com/Microsoft/azuredatastudio/issues/1496): 「 新的 Profiler 」 快顯功能表選項，在 [物件總管] 中不執行任何動作。
  - 修正[問題 1495](https://github.com/Microsoft/azuredatastudio/issues/1495)： 查詢編輯器 」 Explain"查詢計劃已中斷。


## <a name="may-2018-may-public-preview"></a>2018 年 5 月版（ 5 月公開預覽）

發行日期： 2018 年 5 月 7 日  
版本： 0.29.3

*5月公開預覽版*著重於穩定性及 bug 修正。 此版本包含下列重點：  

- 宣布可用延伸模組管理員 中的 Redgate SQL Search 延伸模組。
- 適用於 10 種語言的社群當地語系化： 德文、 西班牙文、 法文、 義大利文、 日文、 韓文、 葡萄牙文、 俄文、 簡體中文和繁體中文。
- 減少的遙測收集、 改善的退出體驗和產品中連結至隱私權聲明。
- 擴充管理員已改善的 Marketplace 體驗來輕鬆地探索社群的延伸。
- SQL 代理程式延伸模組作業和作業歷程記錄檢視改進。
- 更新擴充功能 whoisactive 和伺服器報表。
- 改善管理儀表板內容捲動。
- 修正 GitHub 問題：
   - 修正[問題 703](https://github.com/Microsoft/azuredatastudio/issues/703)： 在編輯資料中輸入類似 HTML 的文字之後，除非重新整理，否則會導致無法正確顯示值
   - 修正[問題 821](https://github.com/Microsoft/azuredatastudio/issues/821): azuredatastudio.deb 封裝相依性
   - 修正[問題 1260](https://github.com/Microsoft/azuredatastudio/issues/1260)： 關鍵字 'distinct' 非反白顯示
   - 修正[問題 1332](https://github.com/Microsoft/azuredatastudio/issues/1332)： 編輯資料還原不適用於資料列
   - 修正[問題 1215](https://github.com/Microsoft/azuredatastudio/issues/1215): SQL Agent擴充功能和狀態列
   - 修正[問題 1316](https://github.com/Microsoft/azuredatastudio/issues/1316): 在視窗大小改變後，SQL Agent 不會隨之調整大小




## <a name="april-2018-april-public-preview"></a>2018 年 4 月版 （ 4 月公開預覽）

發行日期： 2018 年 4 月 25 日  
版本： 0.28.6

*4 月公開預覽版*包含 bug 修正和增強功能。 

- SQL 代理程式預覽延伸模組的功能改進。
- 針對在 SQL Operations Studio 內儲存受系統管理保護與大於 256M 的檔案，改善大型和受保護檔案的支援。
- 分割一次使用多個開啟的終端機的整合式終端機。
- 降低的安裝磁碟上的檔案計數英呎列印更快速的安裝和啟動時間。
- 若要修正之 GitHub 問題繼續：
   - 修正[問題 37](https://github.com/Microsoft/azuredatastudio/issues/37)： 當圖表檢視器擲回錯誤時，就會發生未預期的行為。
   - 修正[問題 462](https://github.com/Microsoft/azuredatastudio/issues/462)： 功能要求： 根據預設展開伺服器群組的選項。
   - 修正[問題 606](https://github.com/Microsoft/azuredatastudio/issues/606): intellisense-'update' 命令的錯誤提供建議。
   - 修正[問題 967](https://github.com/Microsoft/azuredatastudio/issues/967)： 預期的查詢計劃當結果方格中選取 XML 顯示計畫。
   - 修正[問題 1023](https://github.com/Microsoft/azuredatastudio/issues/1023)： 從 flyfishingdba 新增 ms_foreachdb 呼叫的方括號。
   - 修正[問題 1048](https://github.com/Microsoft/azuredatastudio/issues/1048)： 登入前 SSL/TLS 信號交換時發生錯誤。
   - 修正[問題 1050](https://github.com/Microsoft/azuredatastudio/issues/1050)： 清除 insights 檢視之前顯示錯誤。
   - 修正[問題 1057](https://github.com/Microsoft/azuredatastudio/issues/1057)： 還原和檔案總管 widget 中的新查詢動作已中斷。
   - 修正[問題 1068](https://github.com/Microsoft/azuredatastudio/issues/1068)： 儀表板輸出 windows 快顯上使用 Azure SQL Database 的錯誤訊息。
   - 修正[問題 1069](https://github.com/Microsoft/azuredatastudio/issues/1069)： 連接對話方塊顯示時最初顯示的所需的伺服器錯誤。
   - 修正[問題 1070](https://github.com/Microsoft/azuredatastudio/issues/1070)： 伺服器群組現在需要按兩下以展開。
   - 修正[問題 1072](https://github.com/Microsoft/azuredatastudio/issues/1072)： 選取控制項的背景是半透明效果。
   - 修正[問題 1115](https://github.com/Microsoft/azuredatastudio/issues/1115)： 修正所有的高對比 SQL Operations Studio 中的協助工具問題。
   - 修正[問題 1101](https://github.com/Microsoft/azuredatastudio/issues/1101)： 擴充功能無法升級[下載手動]連結會移至錯誤的位置。
   - 修正[問題 1103](https://github.com/Microsoft/azuredatastudio/issues/1103)： 無法在 [首頁] 索引標籤上運作的 V 捲軸。
   - 修正[問題 1104](https://github.com/Microsoft/azuredatastudio/issues/1104): SQL 延伸模組索引標籤停止運作。


4 月公開預覽的重點為 Visual Studio Code 1.21 平台來源程式碼重新整理。 這會從先前的 1.19 同步處理點帶入多項更新至核心編輯器和工作臺。 以下為部分範例：

- [新的通知 UI](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui) -輕鬆地管理與檢閱 SQL Operations Studio 通知。
- [整合式終端機分割](https://code.visualstudio.com/updates/v1_21#_split-terminals)-一次使用多個開啟的終端機。
- [將大型和受保護的檔案儲存](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges)-儲存受保護的系統管理員和 > 256m SQL Operations Studio 內的檔案。
- [已改善大型檔案支援](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements)-大型檔案的文字緩衝區最佳化。
- [改良的設定搜尋](https://code.visualstudio.com/updates/v1_20#_settings-search)-輕鬆地找出使用自然語言搜尋的正確設定。
- [全域程式碼片段](https://code.visualstudio.com/updates/v1_20#_global-snippets)-建立您可以使用所有的檔案類型的程式碼片段。
- [總管複選](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer)-多個檔案一次執行的動作。
- [錯誤與警告，在 [總管]](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer) -可以快速地瀏覽至您的程式碼基底中的錯誤。
- [拖曳和卸除、 複製和貼上整個 windows](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support) -在開啟的 SQL Operations Studio 視窗之間移動檔案。
- [Git 子模組支援](https://code.visualstudio.com/updates/v1_20#_git-submodules)-巢狀的 Git 儲存機制執行 Git 作業。
- [終端機螢幕助讀程式支援](https://code.visualstudio.com/updates/v1_20#_screen-reader-support)-整合式終端機現在具有 「 螢幕讀取器最佳化 」 模式。
- [置中的編輯器配置](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout)-最大化您的程式碼檢視螢幕面積。
- [水平的搜尋結果 （預覽）](https://code.visualstudio.com/updates/v1_21#_horizontal-search) -您可以水平台中的目前檢視搜尋結果。

如需詳細資訊，簽出[Visual Studio Code 2 月版本資訊](https://code.visualstudio.com/updates/v1_21)，而[Visual Studio Code 1 月版本資訊](https://code.visualstudio.com/updates/v1_20)。

如需詳細資訊，請參閱 <<c0> [ 變更記錄檔](https://github.com/Microsoft/azuredatastudio/blob/master/CHANGELOG.md)。

## <a name="march-2018-march-public-preview"></a>2018 年 3 月版 （3 月公開預覽）

發行日期： 2018 年 3 月 28 日  
版本： 0.27.3

*3 月公用預覽版*繼續處理最上層的 GitHub 問題而重點在於提升擴充性故事。 特別啟用擴充功能管理員，改善儀表板管理，並提供 SQL Agent和 insights 擴充功能。 此版本包含下列增強功能：

- 提升儀表板的擴充性模型，來支援索引標籤式的深入解析和設定窗格。
   - 延伸模組管理員可讓簡單的併購的延伸模組。
   - 來自 [whoisactive.com](http://www.whoisactive.com) 的 sp_whoisactive 擴充儀表板。
   - 如需詳細資訊，請參閱[擴充功能的 SQL Operations Studio](extensions.md)。
- 新增額外[連線和物件總管 中的擴充性 Api](https://github.com/Microsoft/azuredatastudio/wiki/Extensibility-API)管理。
- 若要修正問題影響到重要的客戶繼續[的 GitHub 問題](https://github.com/Microsoft/azuredatastudio/issues)。


## <a name="february-2018-february-public-preview"></a>2018 年 2 月版 （ 2 月公開預覽）

發行日期： 2018 年 2 月 15 日，  
版本： 0.26.7

*2 月公用預覽*含有一些功能建議和高優先順序的 bug 修正。 此版本包含下列增強功能：

- 引進安裝自動更新，可通知時新的版本可供下載 
- 連接對話方塊 'Database' 欄位現以動態方式填入的下拉式清單將包含從指定的伺服器填入資料庫清單。
- 修正[問題 6](https://github.com/Microsoft/azuredatastudio/issues/6)： 使連接與選取的資料庫開啟新查詢索引標籤。
- 修正[問題 22](https://github.com/Microsoft/azuredatastudio/issues/22): ' Server Name' 和資料庫名稱-可以這些是下拉式清單而不是文字方塊？
- 修正[問題 549](https://github.com/Microsoft/azuredatastudio/issues/549)： 無訊息/非常無訊息安裝會導致在安裝之後開啟應用程式。
- 修正[問題 481](https://github.com/Microsoft/azuredatastudio/issues/481)： 加入 「 檢查更新 」 選項。
- SQL 編輯器顏色標示和自動完成的修正程式：
   - 修正[問題 584](https://github.com/Microsoft/azuredatastudio/issues/584): 「 完整 」 不反白顯示的 intellisense 的關鍵字。
   - 修正[問題 345](https://github.com/Microsoft/azuredatastudio/issues/345)： 以色彩標示 SQL 函式，在編輯器中的。
   - 修正[問題 300](https://github.com/Microsoft/azuredatastudio/issues/300): [#tempData] 最新"]"將會顯示綠色。
   - 修正[問題 225](https://github.com/Microsoft/azuredatastudio/issues/225)： 關鍵字色彩不相符。
   - 修正[問題 60](https://github.com/Microsoft/azuredatastudio/issues/60)： 無效的 sql 語法色彩反白顯示時使用 from 子句中的暫存資料表。
- 介紹連線擴充性 API。
- VS Code 編輯器 1.19 整合。
- 更新上車數個查詢計劃檢視器改善 JustinPealing/html-查詢計劃的元件。


## <a name="january-2018-january-public-preview"></a>2018 年 1 月 （ 1 月公開預覽）

發行日期： 2018 年 1 月 17 日  
版本： 0.25.4

*1 月公用預覽*含有一些功能建議和高優先順序的 bug 修正。 此版本包含下列增強功能：

- 在 [連接] 對話方塊中提供儲存的伺服器連接。
- 啟用 最忙碌的結束。 根據預設，若要啟用，請參閱熱結束已關閉[熱結束設定](settings.md#hot-exit)。
- 依據伺服器群組 索引標籤-著色。 根據預設，若要啟用，請參閱已關閉的索引標籤著色[索引標籤的色彩設定](settings.md#tab-color)。
- 變更*伺服器名稱*要*Server*連接對話方塊中。
- 修正中斷*執行目前查詢*命令。
- 修正指令碼錯誤的拖放重大。
- 修正不正確的已釘選 [開始] 功能表圖示。
- 修正遺漏商標圖示的 Azure 帳戶。


## <a name="december-2017-december-public-preview"></a>2017 年 12 月（12 月公開預覽）

發行日期： 2017 年 12 月 19 日  
版本： 0.24.1

*年 12 月公開預覽*所有功能領域，以及下列增強功能包括數個 bug 修正：

- 建立防火牆規則對話方塊現在是可協助連接至 Azure SQL Database 和 Azure SQL 資料倉儲。
- 已新增的 Windows 安裝程式，以及 Linux DEB 和 RPM 安裝套件。
- 管理儀表板視覺化版面配置編輯器。
- *指令碼為 Alter*並*指令碼執行*命令。
- *使用實際的計劃執行目前查詢*命令。
- 整合 VS Code 1.18.1 編輯器平台。
- 啟用側載的 VSIX 擴充功能檔案。
- 支援"GO N"批次反覆項目語法。


## <a name="november-2017"></a>2017 年 11 月

發行日期： 2017 年 11 月 15 日  
版本： 0.23.6

- 初始版本的[!INCLUDE[name-sos](../includes/name-sos-short.md)]。


## <a name="next-steps"></a>後續步驟

請參閱下列快速入門，以開始使用其中一項：
- [連線與查詢 SQL Server](quickstart-sql-server.md)
- [連線與查詢 Azure SQL Database](quickstart-sql-database.md)
- [連線與查詢 Azure 資料倉儲](quickstart-sql-dw.md)

參與[!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio)
