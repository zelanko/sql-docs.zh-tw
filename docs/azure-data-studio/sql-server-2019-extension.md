---
title: SQL Server 2019 擴充功能 （預覽）
titleSuffix: Azure Data Studio
description: Azure Data Studio 的 SQL Server 2019 Preview 延伸模組
ms.custom: seodec18
ms.date: 04/19/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: fe3c7fa2a383ea7d8b969ed149a2a762531e0a84
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63472186"
---
# <a name="sql-server-2019-extension-preview"></a>SQL Server 2019 擴充功能 （預覽）

SQL Server 2019 擴充功能 （預覽） 提供的預覽支援的新功能和工具支援的出貨[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]。 這包括提供的預覽支援[SQL Server 2019 巨量資料叢集](../big-data-cluster/big-data-cluster-overview.md)，整合[notebook 體驗](../big-data-cluster/notebooks-guidance.md)，和 PolyBase [Create External Table 精靈](../relational-databases/polybase/data-virtualization.md?toc=%2fsql%2fbig-data-cluster%2ftoc.json)。

## <a name="install-the-sql-server-2019-extension-preview"></a>安裝 SQL Server 2019 擴充功能 （預覽）

若要安裝 SQL Server 2019 擴充功能 （預覽版），下載並安裝相關聯的.vsix 檔案。

1. 將 SQL Server 2019 擴充功能 （預覽版）.vsix 檔案下載到本機目錄：

   |平台|下載|發行日期|版本
   |:---|:---|:---|:---|
   |視窗|[.vsix](https://go.microsoft.com/fwlink/?linkid=2087443)|2019 年 4 月 18日日 |0.12.1
   |macOS|[.vsix](https://go.microsoft.com/fwlink/?linkid=2087442)|2019 年 4 月 18日日 |0.12.1
   |Linux|[.vsix](https://go.microsoft.com/fwlink/?linkid=2087441)|2019 年 4 月 18日日 |0.12.1

1. 在 Azure Data Studio 選擇**VSIX 套件安裝延伸模組**從**檔案**功能表，然後選取已下載的.vsix 檔案。

1. 選擇**是**時提示您確認安裝，並等候安裝成功的通知。

1. 選取**重新載入**以啟用該擴充功能 (只有第一次安裝擴充功能時需要)。

1. 重新載入後，擴充功能會安裝相依性。 您可以看到在 [輸出] 視窗中，進度，並可能需要幾分鐘的時間。

1. 在相依性後面完成安裝，關閉再重新開啟 Azure Data Studio。 **巨量資料的 SQL Server 叢集**連接類型不可以使用，直到您重新啟動 Azure Data Studio。

## <a name="changes-in-release-0121"></a>版本 0.12.1 中的變更

* **巨量資料的 SQL Server 叢集**連接類型已在此版本中移除。 從 SQL Server 的巨量資料叢集連接先前提供的所有功能都位於 SQL Server 連接。
* HDFS 瀏覽您可以找到**Data Services**資料夾
* Notebook 的 PySpark 和其他巨量資料的核心會在連接至 SQL Server 巨量資料叢集 SQL Server 主要執行個體時。
* 建立外部資料表精靈：
  * 建立使用現有的外部資料來源的外部資料表的支援。
  * 在精靈的效能改進。
  * 改進處理含有特殊字元的物件名稱。 在某些情況下，這些使精靈失敗
  * 物件對應 頁面的可靠性改進。
  * 已移除的系統資料庫-': DWConfiguration'、 'DWDiagnostics'、 'DWQueue'-從資料庫下拉式清單。
  * 設定外部檔案格式物件的名稱的支援**從 CSV 檔案建立外部資料表**精靈。
  * 重新整理 按鈕加入的第一頁**從 CSV 檔案建立外部資料表**精靈。

## <a name="release-notes-v0110"></a>版本資訊 (v0.11.0)

* Jupyter Notebook 支援，特別是支援的 Python3 和 Spark 核心，已移至 Azure Data Studio。 此延伸模組已不再需要為了使用 Notebook。
* 在外部資料精靈中的多個錯誤修正：
  * Oracle 型別對應已更新以符合隨附於 SQL Server 2019 CTP 2.3 的變更。
  * 已修正的問題，已遺失輸入資料表的對應控制項的新結構描述。
  * 已修正的問題，檢查 [資料庫] 節點中的資料表對應不會造成所有的資料表和檢視表正在檢查。


## <a name="release-notes-v0102"></a>版本資訊 (v0.10.2)
### <a name="sql-server-2019-support"></a>SQL Server 2019 支援
已更新 SQL Server 2019 的支援。 在連接到 SQL Server 巨量資料叢集執行個體上的新_Data Services_資料夾會出現在檔案總管 樹狀目錄中。 這有動作，例如開啟新的 Notebook，針對連接、 提交 Spark 作業，以及使用 HDFS 的啟動點。 請注意，對於某些動作這類_建立外部資料_HDFS 檔案/資料夾，透過_SQL Server 2019 Preview_必須安裝延伸模組。

### <a name="notebook-support"></a>Notebook 支援
Notebook 使用者介面，在此版本中，我們已進行重大更新。 我們的重點是於更容易閱讀與您共用的 Notebook。 這是移除所有概述資料格周圍的方塊，選取或動態顯示，除非加入暫留支援簡單資料格層級的動作而不需要選取一個資料格，並釐清加上動畫的執行計數的執行狀態_停止執行_  按鈕和更多功能。 我們也新增的鍵盤快速鍵_新的 Notebook_ (`Ctrl+Shift+N`)，_執行資料格_(`F5`)，_新的程式碼儲存格_(`Ctrl+Shift+C`)， _新的文字儲存格_(`Ctrl+Shift+T`)。 接下來，我們會設法讓我們知道您遺漏了什麼的快顯的所有索引鍵的動作可啟動 ！

其他改進和修正程式包括：
* _SQL Server 2019 Preview_延伸模組現在提示用以挑選 Python 相依性安裝目錄。 它也不會再包含中的 Python `.vsix file`，縮小整體的延伸模組。 Python 相依性所需支援 Spark 和 Python3 核心，因此安裝此延伸模組，才能使用這些項目。
* 已新增支援啟動新的 notebook，從命令列。 使用引數啟動`--command=notebook.command.new --server=myservername`應該會開啟新的 notebook，並連線到此伺服器。
* 效能修正 notebook 資料格在大型程式碼長度。 如果程式碼儲存格，則會有捲軸加入的行超過 250 個。
* 已改善.ipynb 檔案支援。 現在支援 3 個或更高版本的版本。 請注意，在儲存檔案將會更新為 4 或更新版本的版本。
* `notebook.enabled`使用者設定已移除了現在具有內建筆記本檢視器是穩定
* 高對比佈景主題現在在此情況下支援數目的物件配置的修正程式。
* 已修正 #3680 輸出有時示範一些`,,,`不正確字元
* 已修正的 # 3602 之後離開 azure 資料 studio 編輯器會消失的資料格
* 已新增支援，使用方格檢視`application/vnd.dataresource+json`輸出 MIME 類型。 這表示使用此選項的許多 Notebook (例如藉由設定`pd.options.display.html.table_schema`Python notebook 中) 會有固定的 #3959 Azure Data Studio 關閉 notebook 之後，兩次嘗試關閉 notebook 伺服器的還棒表格式輸出

#### <a name="known-issues"></a>已知問題
* 開啟 Notebook 安裝 python 會出現對話方塊。 取消此安裝會導致核心，並附加至下拉式清單未顯示預期的值。 解決方法是完成的 Python 安裝。
* 使用不支援的核心開啟 notebook 時，核心和_附加至_下拉式清單會導致 Azure 資料 Studio 停止回應。 您必須關閉 Azure Data Studio，並確定您使用支援的核心 (Python3、 Spark |R、 Spark |PySpark、 Scala PySpark3)
* 使用 PySpark3 或其他對 SQL Server 端點的 Spark 核心時，Spark UI 連結就會失敗。 因應措施，請按一下儀表板，從 Spark UI，或使用 SQL Server 的巨量資料叢集連線類型，因為這將會有正確的 Spark UI 超連結進行連線

### <a name="extensibility-improvements"></a>擴充性改進
在此版本中加入幾個的改良功能，協助擴充項
* 新`ObjectExplorerNodeProvider`API 可讓擴充功能，提供 SQL Server 或其他連線節點下的資料夾。 這是如何`Data Services`節點會新增至 SQL Server 2019 執行個體，但可用來輕鬆地新增至 UI 的監視或其他資料夾。
* 兩個新的內容金鑰值是可幫助的儀表板的顯示/隱藏貢獻。
  * `mssql:iscluster` 指出這是否為 SQL Server 2019 巨量資料叢集
  * `mssql:servermajorversion` 具有伺服器的版本 (如 SQL Server 2019，SQL Server 2017 和等等的 14 15)。 如果功能應該只會顯示針對 SQL Server 2017 或更新版本，例如，這可以幫助。


## <a name="release-notes-v080"></a>版本資訊 (0.8.0)
*Notebook*:
* 加入儲存格前 / 後現有的資料格現在支援依序按一下 [更多動作] 資料格按鈕
* **加入新的連接**選項已新增至 [附加至] 下拉式清單中的連線
* A**重新安裝 Notebook 相依性**協助 Python 套件更新，並解決其中安裝已暫止中途關閉應用程式的情況下已新增命令。 這可以從命令選擇區中執行 (使用`Ctrl/Cmd+Shift+P`並輸入`Reinstall Notebook Dependencies`)
* 已更新為 1.1.0 PROSE python 套件，並包含數個 bug 修正。 使用**重新安裝 Notebook 相依性**命令來更新此套件
* A**清除輸出**現在支援按一下命令**其他動作**資料格按鈕
* 已修正下列客戶回報問題：
  * 筆記本工作階段無法啟動 Windows 上因為路徑相關問題
  * 在根資料夾的磁碟機，例如 C:\ 或 D:\，無法啟動 notebook
  * [# 2820年](https://github.com/Microsoft/azuredatastudio/issues/2820)無法編輯從廣告在 VS Code 中建立的 notebook
  * 執行 Spark 核心時，現在適用於 Spark UI 連結
  * 重新命名為 「 受管理的套件 」 來 [安裝套件]

*建立外部資料*:

* 複製的錯誤訊息和已分隔成摘要和詳細的檢視，以更容易
* 經過改良的 UI 配置大幅改善的可靠性和錯誤處理
* 已修正下列客戶回報問題：
  * 具有無效的資料行對應的資料表會顯示為已停用，並警告說明此錯誤

## <a name="release-notes-v072"></a>版本資訊 (v0.7.2)
* Azure 資源總管現在內建 Azure Data Studio，並已經移除了此延伸模組。 您的意見反應，在此感謝您 ！
* 使用 Markdown 格 notebook 的提升的效能。
* 在 Notebook 中的自動調整大小的程式碼儲存格。 這仍會有根據儲存格工具列的最小大小。
* 安裝 Notebook 相依性時，請通知使用者。 特別是在 Windows 上這可能需要很長的時間，因此通知現在會顯示在 [工作] 檢視中。
* 重新安裝 Notebook 相依性的支援。 這非常有用，如果使用者先前會關閉 Azure Data Studio 中途完成安裝。
* 取消在 Notebook 中的資料格執行的支援。
* 使用精靈建立外部資料時更高的可靠性，特別是連線發生錯誤時。
* 如果 PolyBase 不啟用或未在目標伺服器中執行，請封鎖使用建立外部資料精靈。
* 拼字檢查，並命名與 SQL Server 2019 和建立外部資料相關的修正程式。
* 從 Azure Data Studio 偵錯主控台中移除大量錯誤。

##  <a name="sql-server-2019-big-data-cluster-support"></a>SQL Server 2019 巨量資料叢集支援

* 按一下 **加入連接**中*物件總管*，然後選擇 **巨量資料的 SQL Server 叢集**作為連線類型。

   > [!TIP]
   > 如果您看不見**巨量資料的 SQL Server 叢集**連接類型，重新啟動 Azure Data Studio。

* 輸入主機名稱或 IP 位址的叢集端點加上使用者名稱和密碼用來連接。
* （選擇性） 包含中的易記顯示名稱**名稱**欄位。
* 按一下 [ **Connect** ，然後您可以啟動一般工作的儀表板中，瀏覽**HDFS**在物件總管] 中，並從該處執行的內容中工作。
* 若要提交 Spark 作業，針對叢集，以滑鼠右鍵按一下伺服器節點中*物件總管*，然後選擇 **提交 Spark 作業**來顯示 提交 對話方塊。
* 若要開啟 Notebook 時，請參閱下一節。

如需詳細資訊，請參閱 <<c0> [ 巨量資料叢集](../big-data-cluster/big-data-cluster-overview.md)。


## <a name="azure-data-studio-notebooks"></a>Azure Data Studio Notebook

* 其中一種以下列方式開啟 notebook:
  * 開啟新的 notebook，從*命令選擇區*。
  * 開啟 SQL Server 2019 巨量資料叢集以及其中一個的 HDFS 物件總管 樹狀結構：
    * 以滑鼠右鍵按一下伺服器節點，然後選擇**新的 Jupyter Notebook**。
    * CSV 檔案中，以滑鼠右鍵按一下，然後選擇**Notebook 中的分析**。
  * 開啟現有.ipynb 檔案從**檔案** 功能表或檔案總管 *（.ipynb 檔案必須升級為 4 或更新版本，才能正確地載入的版本）*
* 選擇 [核心]。 對於本機 notebook 執行中，選擇 [Python 3]。 針對遠端執行，選擇 PySpark 或 Spark |Scala。
* 選擇 連線到遠端執行的 SQL Server 巨量資料叢集端點 （這是不必要的本機開發與 Python 3）。
* 在 notebook 標頭加入透過按鈕的程式碼或 markdown 資料格。 移除資源回收筒可以圖示，左邊的每個資料格的資料格。
* [播放] 按鈕的程式碼儲存格，以執行資料格和切換 markdown 編輯和預覽的眼睛圖示

## <a name="polybase-create-external-table-wizard"></a>PolyBase 建立外部資料表精靈

* 從 SQL Server 2019 的執行個體*建立外部資料表精靈*可以開啟下列三種方法：
  * 以滑鼠右鍵按一下 在伺服器上，選擇**管理**，按一下索引標籤上的 SQL Server 2019 （預覽），然後選擇**Create External Table**。
  * 與 SQL Server 2019 執行個體中選取*物件總管*，啟動*建立外部精靈*透過*命令選擇區*。
  * 中的 SQL Server 2019 資料庫上按一下滑鼠右鍵*物件總管*，然後選擇**Create External Table**。
* 在這個版本的延伸模組，您可以建立外部資料表來存取遠端 SQL Server 和 Oracle 資料表。

  > [!NOTE]
  > SQL 2019 功能的外部資料表功能時，遠端 SQL Server 可能會執行舊版的 SQL Server。

* 選擇是否要在精靈的第一頁上存取 SQL Server 或 Oracle，並繼續。
* 系統會提示您建立資料庫主要金鑰，如果其中一個不已建立 （沒有足夠的複雜性的密碼將會封鎖）。
* 建立資料來源連接，和名為遠端伺服器的認證。
* 選擇要將對應至新的外部資料表物件。
* 選擇**產生指令碼**或是**建立**以完成精靈。
* 建立外部資料表之後, 就會立即顯示在物件樹狀目錄中資料庫的建立位置。


## <a name="known-issues"></a>已知問題

* 如果建立的連接時，不會儲存密碼，例如將提交 Spark 作業的某些動作可能會失敗。
* 現有.ipynb notebook 必須升級為 4 或更新版本，才能載入內容檢視器中的版本。
* 執行**重新安裝 Notebook 相依性**命令可能會顯示 2 個工作，在 [工作] 檢視，其中會失敗。 這不會造成安裝失敗
* 選擇**加入新連接**Notebook，然後按一下 [取消] 會使**選取連接**顯示，即使您已連線。
