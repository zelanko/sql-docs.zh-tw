---
title: SQL Server 2019 延伸模組 (預覽)
titleSuffix: Azure Data Studio
description: 適用於 Azure Data Studio 的 SQL Server 2019 Preview 延伸模組
ms.custom: seodec18
ms.date: 09/11/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: 9ee5564479e1c4334466db7f5b1ce45a6913d68f
ms.sourcegitcommit: 4c7151f9f3f341f8eae70cb2945f3732ddba54af
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/27/2019
ms.locfileid: "71326024"
---
# <a name="sql-server-2019-extension-for-azure-data-studio-preview"></a>適用於 Azure Data Studio 的 SQL Server 2019 延伸模組 (預覽)

Azure Data Studio 的 SQL Server 2019 延伸模組 (預覽) 會針對支援 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的新功能和工具，提供預覽支援。 這包括對於下列各項的預覽支援：[SQL Server 2019 巨量資料叢集](../big-data-cluster/big-data-cluster-overview.md)、整合式[筆記本體驗](../big-data-cluster/notebooks-guidance.md)，以及 PolyBase 的 [建立外部資料表精靈](../relational-databases/polybase/data-virtualization.md?toc=/sql/toc/toc.json)。

## <a name="install-the-sql-server-2019-extension-preview"></a>安裝 SQL Server 2019 延伸模組 (預覽)

若要安裝 SQL Server 2019 延伸模組 (預覽)，請下載並安裝相關聯的 .vsix 檔案。

1. 將 SQL Server 2019 延伸模組 (預覽) .vsix 檔案下載到本機目錄：

   |平台|下載|發行日期|版本
   |:---|:---|:---|:---|
   |Windows|[.vsix](https://go.microsoft.com/fwlink/?linkid=2103613)|2019 年 9 月 11 日 |0.16.0
   |macOS|[.vsix](https://go.microsoft.com/fwlink/?linkid=2103612)|2019 年 9 月 11 日 |0.16.0
   |Linux|[.vsix](https://go.microsoft.com/fwlink/?linkid=2103709)|2019 年 9 月 11 日 |0.16.0

1. 在 Azure Data Studio 的 [檔案]  功能表中，選擇 [從 VSIX 套件安裝延伸模組]  ，然後選取已下載的 .vsix 檔案。

1. 當系統提示您確認安裝時選擇 [是]  ，然後等候安裝成功的通知。

1. 選取 [重新載入]  以啟用此延伸模組 (只有當您第一次安裝延伸模組時才需要)。

1. 重新載入之後，此延伸模組將會安裝相依性。 您可以在 [輸出] 視窗中查看進度，這可能需要幾分鐘的時間。

1. 當相依性完成安裝之後，關閉並重新開啟 Azure Data Studio。 在您重新啟動 Azure Data Studio 之前，將無法使用 **SQL Server 巨量資料叢集**連線類型。

## <a name="changes-in-release-016"></a>0\.16 版中的變更
* 建立外部資料表精靈：
  * 已改善在物件對應頁面上載入資料表和檢視時的錯誤處理。

## <a name="changes-in-release-015"></a>0\.15 版中的變更
* 建立外部資料表精靈：
  * 已縮短在物件對應頁面上載入資料表和資料行資訊所花費的時間。
  * 已修正在連線詳細資料頁面上載入現有資料庫範圍認證的錯誤 (Bug)。
* 從 CSV 檔案精靈建立外部資料表：
  * 已增加用於 PROSE 剖析的預設樣本大小。

## <a name="changes-in-release-0141"></a>版本 0.14.1 中的變更
* 支援 CTP 3.1 資料來源支援

## <a name="changes-in-release-0121"></a>版本 0.12.1 中的變更

* 已從此版本中移除 **SQL Server 巨量資料叢集**連線類型。 先前可從 SQL Server 巨量資料叢集連線中取得的所有功能，現在都可在 SQL Server 連線中取得。
* 您可以在 [資料服務]  資料夾底下找到 HDFS 瀏覽。
* 針對筆記本，PySpark 和其他巨量資料核心均會在連線到您 SQL Server 巨量資料叢集中的 SQL Server 主要執行個體時運作。
* 建立外部資料表精靈：
  * 支援使用現有的外部資料來源建立外部資料表。
  * 整個精靈的效能改進。
  * 已使用特殊字元改進物件名稱的處理。 在某些情況下，這些會導致精靈失敗。
  * 對於 [物件對應] 頁面的可靠性改進。
  * 已從 [資料庫] 下拉式清單中移除系統資料庫：'DWConfiguration'、'DWDiagnostics'、'DWQueue'。
  * 支援在 [從 CSV 檔案建立外部資料表]  精靈中設定外部檔案格式物件的名稱。
  * 已將重新整理按鈕新增至 [從 CSV 檔案建立外部資料表]  精靈的第一頁。

## <a name="release-notes-v0110"></a>版本資訊 (v0.11.0)

* 已將 Jupyter Notebook 支援 (特別是對於 Python3 和 Spark 核心的支援) 移至 Azure Data Studio。 您不再需要此延伸模組，也能使用 Notebook。
* 外部資料精靈中的多個 Bug 修正：
  * 已更新 Oracle 類型對應，以符合 SQL Server 2019 CTP 2.3 中隨附的變更。
  * 已修正下列問題：已遺失輸入至資料表對應控制項的新結構描述。
  * 已修正下列問題：檢查資料表對應中的資料庫節點，並未導致檢查所有資料表和檢視。


## <a name="release-notes-v0102"></a>版本資訊 (v0.10.2)
### <a name="sql-server-2019-support"></a>SQL Server 2019 支援
已更新對 SQL Server 2019 的支援。 連線到 SQL Server 巨量資料叢集執行個體時，新的「資料服務」  資料夾將會出現在瀏覽器樹狀結構中。 此資料夾含有諸如下列各項的動作啟動點：針對連線開啟新的 Notebook、提交 Spark 作業，以及使用 HDFS。 請注意，對於某些動作 (例如透過 HDFS 檔案/資料夾「建立外部資料」  )，必須安裝 _SQL Server 2019 Preview_ 延伸模組。

### <a name="notebook-support"></a>Notebook 支援
我們已在此版本中對 Notebook 使用者介面進行重大更新。 我們的重點在於能夠輕鬆閱讀與您共用的 Notebook。 這表示會移除資料格周圍的所有外框方塊，但保留已選取或滑鼠游標暫留的資料格外框；新增在不需選取資料格的情況下，對簡單資料格層級動作的滑鼠游標暫留支援；以及藉由新增執行計數、動畫的「停止執行」  按鈕和其他項目來釐清執行狀態。 我們也針對「新增筆記本」  (`Ctrl+Shift+N`)、「執行資料格」  (`F5`)、「新增程式碼資料格」  (`Ctrl+Shift+C`)、「新增文字資料格」  (`Ctrl+Shift+T`) 新增了鍵盤快速鍵。 繼續進行，我們的目標將是讓所有重要動作都可透過快速鍵啟動，好讓我們能夠知道您遺漏了什麼！

其他改進和修正包括：
* 「SQL Server 2019 Preview」  延伸模組現在會提示使用者挑選適用於 Python 相依性的安裝目錄。 它也不再於 `.vsix file` 中包含 Python，因而可縮減整個延伸模組的大小。 需要有 Python 相依性才能支援 Spark 和 Python3 核心，因此，必須安裝此延伸模組才能使用這些項目。
* 已新增從命令列啟動新筆記本的支援。 使用 `--command=notebook.command.new --server=myservername` 引數來啟動，應該會開啟新的筆記本並連線到此伺服器。
* 對於資料格內具有大型程式碼長度之筆記本的效能修正。 如果程式碼資料格超過 250 行，則將新增捲軸。
* 已改進 .ipynb 檔案支援。 現在支援版本 3 或更高版本。 請注意，儲存檔案將更新為版本 4 或更高版本。
* 由於內建的 Notebook 檢視器目前處於穩定狀態，因而已移除 `notebook.enabled` 使用者設定。
* 在此情況下，目前會透過對物件版面配置進行的數個修正來支援高對比佈景主題。
* 已修正 #3680：輸出有時會錯誤地顯示一些 `,,,` 字元。
* 已修正 #3602：在巡覽離開 Azure Data Studio 之後，適用於資料格的編輯器會消失。
* 已新增支援，以針對 `application/vnd.dataresource+json` 輸出 MIME 類型使用方格檢視。 這表示許多使用此功能的 Notebook (例如，透過在 Python 筆記本中設定 `pd.options.display.html.table_schema`) 將會有更好的表格式輸出。已修正 #3959：Azure Data Studio 會在關閉筆記本之後嘗試關閉筆記本伺服器兩次。

#### <a name="known-issues"></a>已知問題
* 開啟 Notebook 時，[安裝 Python] 對話方塊隨即出現。 取消此安裝，將導致 [核心] 和 [附加至] 下拉式清單不會顯示預期的值。 因應措施是完成 Python 安裝。
* 使用不支援的核心開啟筆記本時，[核心] 和 [附加至]  下拉式清單將導致 Azure Data Studio 停止回應。 您將需要關閉 Azure Data Studio，並確定您使用的是支援的核心 (Python3、Spark | R、Spark | Scala、PySpark、PySpark3)。
* 針對 SQL Server 端點使用 PySpark3 或其他 Spark 核心時，Spark UI 連結會失敗。 因應措施是，請從儀表板按一下 Spark UI，或使用 SQL Server 巨量資料叢集連線類型進行連線，因為這樣將會有正確的 Spark UI 超連結。

### <a name="extensibility-improvements"></a>擴充性改進
已在此版本中新增了一些有助於擴充項控制項的改進
* 新的 `ObjectExplorerNodeProvider` API 讓延伸模組可在 SQL Server 或其他連線節點底下提供資料夾。 這就是在 SQL Server `Data Services` 2019 執行個體底下新增節點的方式，但可用來輕鬆地將 [監視] 或其他資料夾新增至 UI。
* 有兩個新的內容索引鍵值可用來協助顯示/隱藏對儀表板的貢獻。
  * `mssql:iscluster` 指出這是否為 SQL Server 2019 巨量資料叢集。
  * `mssql:servermajorversion` 具有伺服器版本 (針對 SQL Server 2019 為 15、針對 SQL Server 2017 為 14，依此類推)。 例如，如果只應顯示適用於 SQL Server 2017 或更新版本的功能，則這可能很有幫助。


## <a name="release-notes-v080"></a>版本資訊 (v0.8.0)
*Notebook*：
* 現在可透過按一下 [更多動作] 資料格按鈕，來支援在現有資料格之前或之後新增資料格
* 已將 [加入新連線]  選項新增至 [附加至] 下拉式清單中的連線
* 已新增 [重新安裝筆記本相依性]  命令來協助 Python 套件更新，並透過關閉應用程式來解決安裝已暫停中途的情況。 這可以從命令選擇區中執行 (使用 `Ctrl/Cmd+Shift+P` 並輸入 `Reinstall Notebook Dependencies`)
* 已將 PROSE Python 套件更新為 1.1.0，並包含許多 Bug 修正。 使用 [重新安裝筆記本相依性]  命令來更新此套件
* 目前可按一下 [更多動作]  資料格按鈕來支援 [清除輸出]  命令
* 已修正下列客戶回報的問題：
  * Notebook 工作階段因為路徑問題而無法在 Windows 上啟動
  * 無法從磁碟機的根資料夾 (例如 C:\ 或 D:\) 啟動 Notebook
  * [#2820](https://github.com/Microsoft/azuredatastudio/issues/2820) \(英文\) 無法編輯從 VS Code 的 ADS 中建立的筆記本
  * Spark UI 連結現在可在執行 Spark 核心時運作
  * 已將「受控套件」重新命名為「安裝套件」

建立外部資料  ：

* 錯誤訊息是可複製的，並已將其分成摘要和詳細檢視，讓您能夠更輕鬆地閱讀
* 已改進 UI 版面配置，並已大幅改進可靠性和錯誤處理
* 已修正下列客戶回報的問題：
  * 具有無效資料行對應的資料表會顯示為已停用，並出現一則說明錯誤的警告

## <a name="release-notes-v072"></a>版本資訊 (v0.7.2)
* Azure 資源總管現已內建於 Azure Data Studio，並已從此延伸模組中移除。 謝謝您為此所提供的寶貴意見！
* 已改進具有許多 Markdown 資料格之筆記本的效能。
* 在 Notebook 中自動調整程式碼資料格的大小。 這仍然具有以資料格工具列為基礎的最小大小。
* 安裝 Notebook 相依性時通知使用者。 特別是在 Windows 上，這可能需要很長的時間，因此通知現在會顯示於 [工作] 檢視中。
* 支援重新安裝 Notebook 相依性。 如果使用者先前已在安裝中途關閉了 Azure Data Studio，這就很有用。
* 支援在 Notebook 中取消資料格執行。
* 已改進使用 [建立外部資料] 精靈時的可靠性，特別是在發生連線錯誤時。
* 如果目標伺服器中未啟用或執行 PolyBase，則會封鎖使用 [建立外部資料] 精靈。
* 與 SQL Server 2019 和 [建立外部資料] 相關的拼寫與命名修正。
* 已從 Azure Data Studio 的偵錯主控台中移除大量錯誤。
