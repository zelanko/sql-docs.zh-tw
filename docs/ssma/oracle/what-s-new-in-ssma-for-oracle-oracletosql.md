---
title: SSMA for Oracle 的新功能 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 07/31/2019
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
author: HJToland3
ms.author: Shamikg
ms.openlocfilehash: 27e1e0ee06f343c63240c1155601b2eab5e8c6cc
ms.sourcegitcommit: a154b3050b6e1993f8c3165ff5011ff5fbd30a7e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/30/2019
ms.locfileid: "68632002"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>SSMA for Oracle 的新功能 (OracleToSQL)
這篇文章列出每個版本中 Oracle 變更的 SQL Server 移轉小幫手 (SSMA)。

## <a name="ssma-v83"></a>SSMA v 8。3

SSMA for Oracle 的 v 8.3 版本已透過專為改善品質和轉換計量而設計的目標修正來增強。 此外, 這一版的 SSMA for Oracle 提供了下列修正:

* 解決協助工具問題
* 在 SQL Server 中新增 ' hierarchyid ' 類型的基本支援
* 解決透過同義字呼叫的函式傳回類型未知的問題
* 將 ODP.NET 更新為 v 19。3

> [!IMPORTANT]
> 在 SSMA 7.4 和更新版本中, .Net 4.5.2 是必要的安裝。

## <a name="ssma-v82"></a>SSMA v8.2

SSMA for Oracle 的8.2 版已增強為:

* 新增對 DBMS_OUTPUT 的支援。啟用/停用。
* 針對預設資料移轉查詢中的 BINARY_FLOAT 和 BINARY_DOUBLE 資料行, 移除 CAST 做為 FLOAT。
* 如果目前的值已變更, 請修正序列重新整理。
* 如果有相同名稱的資料行存在, 請修正與虛擬資料行 (ROWNUM 等) 的錯誤相關的 bug。
* 修正針對具有不明確解析的識別碼之迴圈轉換所發生的損毀。

此外, 此版本還包含一組目標的修正程式, 其設計目的是要改善品質和轉換計量, 以及的修正:

* 在資料移轉後停用非叢集索引的問題。
* 在無訊息安裝期間偵測 .NET Framework。
* 下載新版本時, 會發生間歇性損毀。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA 8.1 到 v4.0 的更新失敗。 如果您遇到此錯誤, 請下載新版本並手動安裝。

> [!IMPORTANT]
> 在 SSMA 7.4 和更新版本中, .Net 4.5.2 是必要的安裝。

## <a name="ssma-v81"></a>SSMA v8.1

SSMA for Oracle 的8.1 版已透過專為改善品質和轉換計量而設計的目標修正來增強。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v4.0 到8.1 版的更新失敗。 如果您遇到此錯誤, 請下載新版本並手動安裝。

## <a name="ssma-v80"></a>SSMA v8.0

SSMA for Oracle 的8.0 版已透過專為改善品質和轉換計量而設計的目標修正來增強。 此版本也提供下列新功能:

* 支援做為目標**Azure SQL Database 受控執行個體**。 您現在可以建立以 Azure SQL Database 受控執行個體為目標的新專案:

  ![SQL DB MI 專案](../media/ssma-newproject-sqldbmi.png)

  > [!NOTE]
  > Oracle 延伸模組套件的 SSMA 也已更新為允許 Azure SQL Database 受控執行個體上的遠端安裝:
  >
  > ![SSMA for Oracle 延伸模組套件](../media/ssma-oracle-ext-pack.png)

  以 Azure SQL Database 受控執行個體為目標時, 不支援某些功能, 包括測試人員和伺服器端資料移轉。 [在這裡](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/)閱讀更多相關資訊。

* 轉換後的**修正建議程式**。 [在這裡](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)深入瞭解。

* 初步的資料庫/架構選擇。

  當連接到來源時, 使用者現在可以選取想要的資料庫/架構。 只選取您打算遷移的架構, 會在初始連接期間節省時間, 並改善整體 SSMA 效能。

  ![SSMA 篩選物件](../media/ssma-filter-objects.png)

* 能夠使用官方的受控網路驅動程式來連接到 Oracle。 OCI 驅動程式不再是使用 SQL Server 移轉小幫手 for Oracle 的必要條件。

* 預設將 ROWID 和 UROWID 對應到 VARCHAR 的能力。 已從 ' uniqueidentifier ' 變更, 以配合明確的 ROWID 資料行進行資料移轉。

## <a name="ssma-v710"></a>SSMA v7.10

SSMA for Oracle 的 v 7.10 版本包含下列變更:

* 專為提供額外的安全性和隱私權保護而設計的目標修正, 以符合全球需求的變更。
* 與階層式查詢相關的轉換改進。

## <a name="ssma-v79"></a>SSMA v7.9

SSMA for Oracle 的 v 7.9 版本包含下列變更:

* 改善品質和轉換計量的目標修正程式。
* 支援將「繼續」語句從 Oracle 遷移至 SQL Server。
* 支援 SSMA 命令列來改變資料類型對應和專案喜好設定。
* 支援使用 SQL Server Integration Services (SSIS) 來遷移資料。 轉換架構之後, 您可以使用滑鼠右鍵內容功能表選項來建立 SSIS 封裝。
* SSMA 中的 [Azure SQL Database 連接] 對話方塊也已更改為指定完整的伺服器名稱。 在舊版的 SSMA 中, 必須在專案設定中明確提及 Azure SQL Database 前置詞。

## <a name="ssma-v78"></a>SSMA v7.8

適用于 Oracle 的 SSMA 7.8 版包含下列變更:

* 支援:
  * IN 子句的資料列運算式。
  * 隱含類型轉換。
  * Azure SQL Database 的 UID 轉換。
* 變更 [專案設定] 中反白顯示的類型對應。
* 使用者停用遙測的能力。

## <a name="ssma-v77"></a>SSMA v7.7

SSMA for Oracle 的7.7 版包含下列變更:

* SSMA for Oracle 已透過改善品質和轉換計量的目標修正來加強。
* 根據受歡迎的需求, 32 位版本的 Oracle SSMA 已恢復。 相較于先前的執行 (在7.4 之前), 有兩個安裝程式套件, 但無法並存安裝。 因此, 您必須根據您擁有的連線元件來選擇最適當的版本。 最好是盡可能使用64位版本。
* SQL Server 2017 支援現已正式提供 Linux 上支援的 Oracle 延伸模組套件 (新的遠端安裝選項)。 請注意, 在 Linux 上安裝時, 延伸模組套件功能會受到限制, 因為測試人員和伺服器端資料移轉功能不受支援。
* 適用于 Oracle 的 SSMA 可讓您將具體化的視圖當做一般資料表來進行遷移 (可透過**專案設定** -> **同步** -> 處理中的設定,**探索具體化視圖的支援資料表**)。

## <a name="ssma-v76"></a>SSMA v7.6

SSMA for Oracle 的 v 7.6 版本已藉由改善品質和轉換計量, 並支援 SQL Server 2017 (公開預覽) 的目標修正來增強。 Windows 和 Linux 上的 SQL Server 2017 支援處於公開預覽狀態, 不應用於生產環境遷移。

## <a name="ssma-v75"></a>SSMA v7.5

SSMA for Oracle 的7.5 版包含下列變更:

* 增強了數項改良功能, 以確保更方便殘障人士使用。
* 已更新以改善目標修正的品質和轉換計量, 例如在資料移轉期間, 根據客戶的意見反應, 改善日期和 float 資料類型的處理。

## <a name="ssma-v74"></a>SSMA v7.4

SSMA for Oracle 的7.4 版包含下列變更:

* SSMA for Oracle 現在支援 Azure SQL 資料倉儲做為遷移的目標平臺。

  ![[新增專案] 視窗](../media/new-project.png)
  * 支援資料倉儲儲存體選項, 如下圖所示:

  ![資料倉儲的儲存選項](../media/storage-options_red.png)
  * 支援資料散發選項, 如下圖所示:

  ![資料倉儲的資料散發](../media/data-distribution_red.png)

* 在來源和目標的架構物件探索期間, 現在可以使用 [**查詢超時**] 選項。

  ![查詢超時選項](../media/query-timeout_red.png)

* 品質和轉換度量已根據客戶的意見反應, 以目標修正進行改善。

> [!IMPORTANT]
> .Net 4.5.2 是安裝 SSMA 7.4 的必要條件。 此外, 從7.4 開始, 32 位版本的 SSMA 即將中止。

## <a name="ssma-v73"></a>SSMA v7.3

SSMA for Oracle 的7.3 版包含下列變更:

* 改善品質和轉換計量, 並根據客戶的意見反應進行目標修正。
* 透過下列專案公開的 SSMA 擴充性架構:
  * 將功能匯出至 SQL Server Data Tools (SSDT) 專案。
    * 您現在可以將架構腳本從 SSMA 匯出至 SSDT 專案。 您可以使用架構腳本來進行其他架構變更, 並部署您的資料庫。

      ![另存為 SSDT 專案命令](../media/export-schema-scripts_red.png)
  * 可供 SSMA 用來執行自訂轉換的程式庫。
    * 您現在可以建立可處理自訂語法轉換的程式碼, 以及 SSMA 先前未處理的轉換。
      * 如需如何建立自訂轉換器的指示, 請前往此 blog 文章,[延伸 SQL Server 移轉小幫手的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      * 下載範例專案, 以便從這[篇 blog 文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)進行轉換。

## <a name="ssma-v72"></a>SSMA v7.2

SSMA for Oracle 的7.2 版包含下列變更:

* 改善品質和轉換計量, 並根據客戶的意見反應進行目標修正。
* 遙測增強功能, 可提供更好的資料點來疑難排解客戶問題, 並改善 SSMA 的轉換率。

## <a name="ssma-v71"></a>SSMA v7.1

SSMA for Oracle 的7.1 版包含下列變更:

* Windows 和 Linux CTP1 上的 SQL Server 2017 現在是支援的目標平臺, 可進行遷移。 這項功能在 technical preview 中, 可讓您以 SQL server 為目標來進行架構和資料移動。
* SSMA 現在支援自動更新, 以在最新版本的 SSMA 推出時立即下載。
* SSMA 可安裝的二進位檔現在會透過 Windows installer 封裝檔案 (.msi) 傳遞。

## <a name="may-2016"></a>5月2016

SSMA for Oracle 的2016年5月版本包含下列變更:  

* 已新增 SQL Server 2016 的支援。
* 將 Oracle 閃回封存資料表的轉換新增至 SQL Server 時態表。

  > [!NOTE]
  > SSMA 不會從 Oracle 閃回資料保存資料表複製記錄資料。 因此, 在遷移過程中, 必須手動複製歷程記錄資料。 此外, 雖然 SSMA 不會在 SQL Server 的中繼資料 explorer 中顯示歷程記錄資料表, 因為它被視為系統資料表, 您可以在 SQL Server Management Studio 中查看記錄資料表。
  >
  > SQL Server 2016 不支援數個 Oracle 閃回功能, 包括:
  >
  > * Oracle 閃回交易查詢
  > * DBMS_FLASHBACK 套件
  > * 閃回交易
  > * 閃資料封存
  > * 閃回資料表
  > * 閃重播置
  > * 閃回資料庫
* 已將 Oracle VPD 原則轉換為 SQL Server 原則物件 (資料列層級安全性適用于 Oracle)。
* 已縮短 Oracle 初始載入的時間。
* 改良的剖析器和解析程式。
* 已移除 .Net 2.0 的安裝程式檢查。
* 已將延伸模組套件相依性從 .Net 3.5 更新為 .Net 4.0。
* 已修正 SSMA 主控台的 [儲存專案] 和 [開啟專案] 命令。
* 已修正 SSMA 主控台的 "securepassword" 命令。
* 已修正初始載入物件的計數。
* 已修正 Oracle 的字元資料類型轉換。
* 已修正全域設定中的 bug。
  
## <a name="march-2016"></a>2016年3月

SSMA for Oracle 的2016年3月預覽版本已新增的支援:  
  
* 遷移至 SQL Server 2016。  
* 遷移 Oracle 資料列層級安全性 (有一些限制)。  
* 將 Oracle in memory 資料表遷移至 SQL Server 資料行存放區。  
  
## <a name="january-2016"></a>2016年1月

SSMA for Oracle 的2014年1月維護版本包含下列變更:  
  
* 已新增對叢集索引的支援。  
* 已修正緩慢的 Oracle 架構查詢 (RFC 5076207)。  
* 已修正從主控台連線至 Azure。  
* 已將 [查看記錄] 功能表項目新增至 SSMA (RFC 5706203)。 
* 已新增遙測。
  
## <a name="july-2014"></a>2014年7月

2014年7月版的 SSMA for Oracle 包含下列變更:  
  
* 已新增 Azure SQL DB 的支援。
* 延伸模組套件功能已移至架構, 以支援 Azure SQL DB。
* 已新增對 Oracle 具體化 views 的支援。  
* 已新增 SQL Server 2014 記憶體優化資料表的支援。  
* 已針對具有超過10k 物件的資料庫測試過的效能改進。  
* 新增了處理大量物件的 UI 改良功能。  
* 已新增反白顯示「已知的」 LOB 架構。  
* 包含轉換速度改進。  
* 已新增在 UI 中顯示物件計數的支援。  
* 減少超過 25% 的報表大小。
* 已改善未分析之結構的錯誤訊息。  
  
## <a name="april-2014"></a>2014年4月

2014年4月版本的 SSMA for Oracle 包含下列變更:  
  
* 已新增 MS SQL Server 2014 的支援。  
* 已新增 Oracle 12 和查詢優化的支援。  
* 已修正關於轉換至 Azure 的 bug。  
* 已修正 IE 10 中不可見報表頁面的相關 bug。  
  
## <a name="january-2012"></a>2012年1月

2012年1月發行的 SSMA for Oracle 新增了 RowType 和 RecordType 輸入參數的支援, 預設為 Null。  
  
## <a name="july-2011"></a>2011年7月

2011年7月版的 SSMA for Oracle 包含下列變更:  
  
* 已新增將 Oracle 序列轉換為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" 序列產生器的支援。
* 改善資料移轉期間的錯誤報表。  
* 已改善使用保留字的語句轉換。  
* 改善函式中 date 值的隱含轉換。  
  
## <a name="april-2011"></a>2011年4月

2011年4月版本的 SSMA for Oracle 包含下列變更:  
  
* 合併「Oracle 的 SSMA」產品, 支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 「Denali」。
* 已新增連接和遷移至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] "Denali" 的支援。  
* 加強的用戶端資料移轉引擎, 支援資料的平行遷移。  
* 使用簡單和大量記錄復原模式來改善資料移轉效能。  
* 已新增舊版 SSMA (v4.0 和4.2 版) 所建立之專案的回溯相容性支援。  
* 已新增在舊版 SSMA (v4.0 和4.2 版) 上安裝 SSMA for Oracle v4.0 產品並存 (SxS) 的功能。
* 已新增報表使用者定義類型 (包括子類型、VARRAY、嵌套資料表、物件資料表和物件檢視) 的支援, 以及其在 PL/SQL 區塊中的使用方式, 並具有特殊錯誤訊息。  

## <a name="july-2010"></a>2010年7月

2010年7月發行的 SSMA for Oracle 已新增:

* 支援遷移至 SQL Server 2008 R2。  
* 用於命令列執行的新 SSMA 主控台應用程式。  
* 支援使用伺服器端和用戶端資料移轉引擎來進行資料移轉。  
* 支援資料移轉中的「自訂 SELECT」語句。  
* 支援從 Oracle 11g R2 進行遷移。  
  
## <a name="june-2008"></a>2008年6月

2008年6月版的 SSMA for Oracle 包含下列變更:  
  
* 增加評量報告的改良功能, 包括同義字的其他資訊、可剖析物件的原始來源、面板、SQL Server 標誌移除, 以及版面配置持續性。  
* 已在物件轉換中新增改良功能:  
  * 已新增封裝 DBMS_LOB、DBMS_SQL 轉換。  
  * 已修訂聯結轉換。  
  * 修改集合和記錄轉換, 現在是在簡單案例中, 透過每個欄位的個別變數發行的記錄轉換。  
  * 改進記錄和集合的實施。  
  * 已加入視窗化彙總函式。  
  * 已新增 ROLLUP/CUBE 子句。  
  * 改善 NEXTVAL/CURVAL。  
  * 已加入 SET 子句、群組集合和群組識別碼中的資料行群組。  
  * 已加入 MERGE 語句。  
  * 支援新的日期時間類型, 以及已加入之 CLR 資料類型的記錄和集合的轉換。  
* 已加入測試人員的新功能。 現在可以使用測試控管將資料表測試成物件, 測試案例中數個可測試物件的呼叫順序可以改變, 使用者可以使用記錄和集合來測試程式和函式做為參數和傳回值, 並加入相依性分析器來進行檢查僅限使用的資料表。  
  
## <a name="august-2007"></a>2007年8月

2007年8月發行的 SSMA for Oracle 已新增:

* 新的測試人員元件可讓您建立、管理和執行測試案例, 以確認已轉換的 SQL 程式碼。  
* SQL 轉換器已加入 Oracle 子類型、集合和本機模組的轉換支援。  
* 新的同步處理功能可讓您將特定物件與 SQL Server 資料庫同步。  
* 新的轉換選項。  
  
## <a name="april-2007"></a>2007年4月

2007年4月版的 SSMA for Oracle 是最初發行版本。
