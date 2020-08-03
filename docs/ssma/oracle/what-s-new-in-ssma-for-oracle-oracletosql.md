---
title: SSMA for Oracle 的新功能（OracleToSQL） |Microsoft Docs
description: 瞭解每個版本的 SQL Server 移轉小幫手（SSMA） for Oracle （OracleToSQL）的變更。
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 7/31/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
ms.author: alexiva
ms.openlocfilehash: 1601ae2430ced8a30a04d8ab52d97dbb9bbb095a
ms.sourcegitcommit: 376a6039f917c9f64c45758b257666f5d51387b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/31/2020
ms.locfileid: "87477450"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>SSMA for Oracle 的新功能（OracleToSQL）

這篇文章列出每個版本中 Oracle 變更的 SQL Server 移轉小幫手（SSMA）。

## <a name="ssma-v812"></a>SSMA v 8.12

SSMA for Oracle 的 v 8.12 版本包含下列變更：

* `INSERT` / `UPDATE` / `MERGE` / `DELETE` 語句內的子查詢分解子句支援
* `ON DELETE SET NULL`在多重路徑或迴圈參考的情況下，子句的轉換訊息
* 改善從動態 SQL 字串建立之資料指標的轉換
* 將 ODP.NET 更新為 v 19。8

## <a name="ssma-v811"></a>SSMA v 8.11

SSMA for Oracle 的 v 8.11 版本包含下列變更：

* 語句中的子查詢支援 `INSERT ... VALUES`
* 已改善語句的轉換 `COMMIT`
* 修正子句轉換中的 bug `CONNECT BY LEVEL`
* 已將剖析器錯誤修復邏輯更新為較不的貪婪
* 使用 MSAL.NET 程式庫進行互動式 Azure Active Directory 驗證

## <a name="ssma-v810"></a>SSMA v 8.10

SSMA for Oracle 的 v4.0 版本包含次要效能改進，以及下列變更：

* 修正索引組織型資料表的測試人員問題
* 修正延伸模組套件中擴充預存程式的名稱

## <a name="ssma-v89"></a>SSMA v 8。9

SSMA for Oracle 的 v 8.9 版本包含下列變更：

* 動態 SQL 字串常值的轉換
* `LAG` `FIRST_VALUE` 和 `LAST_VALUE` 分析函數的轉換
* 新增對基本 DDL 的支援 `ALTER TRIGGER` / `ALTER INDEX` （啟用/停用等）
* 改善符合內建函數名稱之資料行的轉換
* 產生可供資料行篩選的唯一索引 `NULL`
* 已改善 Azure SQL 資料倉儲的變數宣告轉換
* 修正專案名稱中特殊字元的問題

## <a name="ssma-v88"></a>SSMA v 8。8

SSMA for Oracle 的 v 8.8 版本包括：

* SQL Server 物件同步處理穩定性改善
* 在評定和轉換期間的 GUI 效能改進
* 改善的分析 `OVER PARTITION` 子句轉換
* 分析函數的新轉換 `LEAD`
* 子查詢分解子句的新轉換
* `REPLICATE`Azure SQL 資料倉儲的新散發選項
* 全新的 Oracle 語法剖析器，以進一步改善轉換效能

## <a name="ssma-v87"></a>SSMA v 8。7

SSMA for Oracle 的 v4.0 版本具有圖形化使用者介面中的次要修正和效能改進。

此外，SSMA for Oracle 現在允許根據 [Advanced objects Selection] 對話方塊中的有效性狀態來篩選物件。

> [!IMPORTANT]
> 在 SSMA 的8.5 和更新版本中，.NET 4.7.2 是必要的安裝。 如果您需要安裝此版本，您可以從[這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v86"></a>SSMA v 8。6

除了針對改善可用性和效能而設計的一組目標修正程式之外，新增可讓使用者在轉換後的程式碼中省略 SSMA 擴充屬性的設定，以增強 SSMA for Oracle 的 v 8.6 版本。

若要利用這項設定，請在 SSMA for Oracle 中流覽至 [**工具]**  >  [**專案設定**]  >  **[一般**  >  **轉換**]，然後在 [**其他**] 下將 [**省略擴充屬性**] 設定的值更新為 **[是]**。

![省略擴充屬性設定](../oracle/media/ssma-omit-extended-properties.png)

此外，SSMA for Oracle 現在提供了更好的 `XMLTABLE` 子句剖析。

> [!IMPORTANT]
> 在 SSMA 的8.5 和更新版本中，.NET 4.7.2 是必要的安裝。 如果您需要安裝此版本，您可以從[這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v85"></a>SSMA v 8。5

SSMA for Oracle 的第8.5 版已增強，並支援 SQL server 中的 Azure Active Directory 驗證和 JSON 功能的基本支援，以及一組專為改善可用性和效能而設計的目標修正程式。

此外，SSMA for Oracle 已透過下列支援而獲得增強：

* 將探索到的選取物件數目限制為990（Oracle 的 `WHERE .. IN (..)` 子句限制為1000個專案）。
* 從到的資料移轉 `RAW` `UNIQUEIDENTIFIER` 。
* 剖析 `PARALLEL_ENABLE` 子句。

最後，SSMA for Oracle 的第8.5 版現已提供：

* 已改善已轉換之封裝常數的效能。
* 適用于 .NET 的 Oracle Data Provider 至版本19.5.0 的更新。

> [!IMPORTANT]
> 使用 SSMA v 8.5 時，.NET 4.7.2 是必要的安裝。 如果您需要安裝此版本，您可以從[這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v84"></a>SSMA v 8。4

SSMA for Oracle 的 v2.0 版本已利用專為解決協助工具問題而設計的目標修正，並修正 SQL Server 2016 和更新版本的最大索引資料行（允許32，而不是16）相關的錯誤。

此外，這一版的 SSMA for Oracle 會將的轉換新增為預存程式 `SYS_REFCURSOR` `OUT` 參數。

> [!IMPORTANT]
> 在 SSMA 版本7.4 到8.4 的情況下，.NET 4.5.2 是必要的安裝。

## <a name="ssma-v83"></a>SSMA v 8。3

SSMA for Oracle 的 v 8.3 版本已透過專為改善品質和轉換計量而設計的目標修正來增強。 此外，這一版的 SSMA for Oracle 提供了下列修正：

* 解決協助工具問題。
* `hierarchyid`在 SQL Server 中新增類型的基本支援。
* 解決透過同義字呼叫的函式傳回類型未知的問題。
* 將 ODP.NET 更新為 v 19.3。

## <a name="ssma-v82"></a>SSMA 8。2

SSMA for Oracle 的8.2 版已增強為：

* 新增的支援 `DBMS_OUTPUT.ENABLE` / `DISABLE` 。
* `CAST AS FLOAT`針對 `BINARY_FLOAT` `BINARY_DOUBLE` 預設資料移轉查詢中的和資料行移除。
* 如果目前的值已變更，請修正序列重新整理。
* `ROWNUM`如果有相同名稱的資料行存在，請修正與虛擬資料行（等）之錯誤的相關 bug。
* 修正 `FOR` 使用不明確的未解析識別碼轉換迴圈所發生的損毀。

此外，此版本還包含一組目標的修正程式，其設計目的是要改善品質和轉換計量，以及的修正：

* 在資料移轉後停用非叢集索引的問題。
* 在無訊息安裝期間偵測 .NET Framework。
* 下載新版本時，會發生間歇性損毀。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA 8.1 到 v4.0 的更新失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v81"></a>SSMA 8。1

SSMA for Oracle 的8.1 版已透過專為改善品質和轉換計量而設計的目標修正來增強。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v4.0 到8.1 版的更新失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v80"></a>SSMA v 8。0

SSMA for Oracle 的8.0 版已透過專為改善品質和轉換計量而設計的目標修正來增強。 此版本也提供下列新功能：

* 支援做為目標**Azure SQL Database 受控執行個體**。 您現在可以建立以 Azure SQL Database 受控執行個體為目標的新專案：

  ![SQL DB MI 專案](../media/ssma-newproject-sqldbmi.png)

  > [!NOTE]
  > Oracle 延伸模組套件的 SSMA 也已更新為允許 Azure SQL Database 受控執行個體上的遠端安裝：
  >
  > ![SSMA for Oracle 延伸模組套件](../media/ssma-oracle-ext-pack.png)

  以 Azure SQL Database 受控執行個體為目標時，不支援某些功能，包括測試人員和伺服器端資料移轉。 請在[此處](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/)閱讀相關資訊。

* 轉換後的**修正建議程式**。 [在這裡](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)深入瞭解。

* 初步的資料庫/架構選擇。

  當連接到來源時，使用者現在可以選取想要的資料庫/架構。 只選取您打算遷移的架構，會在初始連接期間節省時間，並改善整體 SSMA 效能。

  ![SSMA 篩選物件](../media/ssma-filter-objects.png)

* 能夠使用官方的受控 .NET 驅動程式來連接到 Oracle。 OCI 驅動程式不再是使用 SQL Server 移轉小幫手 for Oracle 的必要條件。

* 預設會對應和的功能 `ROWID` `UROWID` `VARCHAR` 。 已從變更 `uniqueidentifier` 為可容納明確資料行的資料移轉 `ROWID` 。

## <a name="ssma-v710"></a>SSMA v 7.10

SSMA for Oracle 的 v 7.10 版本包含下列變更：

* 專為提供額外的安全性和隱私權保護而設計的目標修正，以符合全球需求的變更。
* 與階層式查詢相關的轉換改進。

## <a name="ssma-v79"></a>SSMA v 7。9

SSMA for Oracle 的 v 7.9 版本包含下列變更：

* 改善品質和轉換計量的目標修正程式。
* 支援將「繼續」語句從 Oracle 遷移至 SQL Server。
* 支援 SSMA 命令列來改變資料類型對應和專案喜好設定。
* 支援使用 SQL Server Integration Services （SSIS）來遷移資料。 轉換架構之後，您可以使用滑鼠右鍵內容功能表選項來建立 SSIS 封裝。
* SSMA 中的 [Azure SQL Database 連接] 對話方塊也已更改為指定完整的伺服器名稱。 在舊版的 SSMA 中，必須在專案設定中明確提及 Azure SQL Database 前置詞。

## <a name="ssma-v78"></a>SSMA 7.8 版

適用于 Oracle 的 SSMA 7.8 版包含下列變更：

* 支援：
  * 子句的資料列運算式 `IN` 。
  * 隱含類型轉換。
  * `UID`Azure SQL Database 的轉換。
* 變更 [**專案設定**] 中反白顯示的類型對應。
* 使用者停用遙測的能力。

## <a name="ssma-v77"></a>SSMA 7。7

SSMA for Oracle 的7.7 版包含下列變更：

* SSMA for Oracle 已透過改善品質和轉換計量的目標修正來加強。
* 根據受歡迎的需求，32位版本的 Oracle SSMA 已恢復。 相較于先前的執行（在7.4 之前），有兩個安裝程式套件，但無法並存安裝。 因此，您必須根據您擁有的連線元件來選擇最適當的版本。 最好是盡可能使用64位版本。
* SQL Server 2017 支援現已正式提供 Linux 上支援的 Oracle 延伸模組套件（新的遠端安裝選項）。 請注意，在 Linux 上安裝時，延伸模組套件功能會受到限制，因為測試人員和伺服器端資料移轉功能不受支援。
* 適用于 Oracle 的 SSMA 可讓您將具體化的視圖當做一般資料表來進行遷移（可透過**專案設定**同步處理中的設定，  ->  **Synchronization**  ->  **探索具體化視圖的支援資料表**）。

## <a name="ssma-v76"></a>SSMA v 7。6

SSMA for Oracle 的 v 7.6 版本已藉由改善品質和轉換計量，並支援 SQL Server 2017 （公開預覽）的目標修正來增強。 Windows 和 Linux 上的 SQL Server 2017 支援處於公開預覽狀態，不應用於生產環境遷移。

## <a name="ssma-v75"></a>SSMA v 7。5

SSMA for Oracle 的7.5 版包含下列變更：

* 增強了數項改良功能，以確保更方便殘障人士使用。
* 已更新以改善目標修正的品質和轉換計量，例如在資料移轉期間，根據客戶的意見反應，改善日期和 float 資料類型的處理。

## <a name="ssma-v74"></a>SSMA 7。4

SSMA for Oracle 的7.4 版包含下列變更：

* SSMA for Oracle 現在支援 Azure SQL 資料倉儲做為遷移的目標平臺。

  ![[新增專案] 視窗](../media/new-project.png)
  * 支援資料倉儲儲存體選項，如下圖所示：

  ![資料倉儲的儲存選項](../media/storage-options_red.png)
  * 支援資料散發選項，如下圖所示：

  ![資料倉儲的資料散發](../media/data-distribution_red.png)

* 在來源和目標的架構物件探索期間，現在可以使用 [**查詢超時**] 選項。

  ![查詢超時選項](../media/query-timeout_red.png)

* 品質和轉換度量已根據客戶的意見反應，以目標修正進行改善。

> [!IMPORTANT]
> .NET 4.5.2 是安裝 SSMA 7.4 的必要條件。 此外，從7.4 開始，32位版本的 SSMA 即將中止。

## <a name="ssma-v73"></a>SSMA 7.3 版

SSMA for Oracle 的7.3 版包含下列變更：

* 改善品質和轉換計量，並根據客戶的意見反應進行目標修正。
* 透過下列專案公開的 SSMA 擴充性架構：
  * 將功能匯出至 SQL Server Data Tools （SSDT）專案。
    * 您現在可以將架構腳本從 SSMA 匯出至 SSDT 專案。 您可以使用架構腳本來進行其他架構變更，並部署您的資料庫。

      ![另存為 SSDT 專案命令](../media/export-schema-scripts_red.png)
  * 可供 SSMA 用來執行自訂轉換的程式庫。
    * 您現在可以建立可處理自訂語法轉換的程式碼，以及 SSMA 先前未處理的轉換。
      * 如需如何建立自訂轉換器的指示，請前往此 blog 文章，[延伸 SQL Server 移轉小幫手的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      * 下載範例專案，以便從這[篇 blog 文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)進行轉換。

## <a name="ssma-v72"></a>SSMA 7.2 版

SSMA for Oracle 的7.2 版包含下列變更：

* 改善品質和轉換計量，並根據客戶的意見反應進行目標修正。
* 遙測增強功能，可提供更好的資料點來疑難排解客戶問題，並改善 SSMA 的轉換率。

## <a name="ssma-v71"></a>SSMA 7。1

SSMA for Oracle 的7.1 版包含下列變更：

* Windows 和 Linux CTP1 上的 SQL Server 2017 現在是支援的目標平臺，可進行遷移。 這項功能在 technical preview 中，可讓您以 SQL server 為目標來進行架構和資料移動。
* SSMA 現在支援自動更新，以在最新版本的 SSMA 推出時立即下載。
* SSMA 可安裝的二進位檔現在會透過 Windows Installer 套件檔案（.msi）傳遞。

## <a name="may-2016"></a>2016 年 5 月

SSMA for Oracle 的2016年5月版本包含下列變更：

* 已新增 SQL Server 2016 的支援。
* 將 Oracle 閃回封存資料表的轉換新增至 SQL Server 時態表。

  > [!NOTE]
  > SSMA 不會從 Oracle 閃回資料保存資料表複製記錄資料。 因此，在遷移過程中，必須手動複製歷程記錄資料。 此外，雖然 SSMA 不會在 SQL Server 的中繼資料 explorer 中顯示歷程記錄資料表，因為它被視為系統資料表，您可以在 SQL Server Management Studio 中查看記錄資料表。
  >
  > SQL Server 2016 不支援數個 Oracle 閃回功能，包括：
  >
  >   * Oracle 閃回交易查詢
  >   * `DBMS_FLASHBACK` 封裝
  >   * 閃回交易
  >   * 閃資料封存
  >   * 閃回資料表
  >   * 閃重播置
  >   * 閃回資料庫

* 已將 Oracle VPD 原則轉換為 SQL Server 原則物件（資料列層級安全性適用于 Oracle）。
* 已縮短 Oracle 初始載入的時間。
* 改良的剖析器和解析程式。
* 已移除 .NET 2.0 的安裝程式檢查。
* 已將延伸模組套件相依性從 .NET 3.5 更新為 .NET 4.0。
* 已 `save-project` 修正 `open-project` SSMA 主控台的命令。
* 已修正 `securepassword` SSMA 主控台的命令。
* 已修正初始載入物件的計數。
* 已修正 Oracle 的字元資料類型轉換。
* 已修正全域設定中的 bug。

## <a name="march-2016"></a>2016 年 3 月

SSMA for Oracle 的2016年3月預覽版本已新增的支援：

* 遷移至 SQL Server 2016。
* 遷移 Oracle 資料列層級安全性（有一些限制）。
* 將 Oracle in memory 資料表遷移至 SQL Server 資料行存放區。

## <a name="january-2016"></a>2016 年 1 月

SSMA for Oracle 的2014年1月維護版本包含下列變更：

* 已新增對叢集索引的支援。
* 已修正緩慢的 Oracle 架構查詢（RFC 5076207）。
* 已修正從主控台連線至 Azure。
* 已將 [查看記錄] 功能表項目新增至 SSMA （RFC 5706203）。
* 已新增遙測。

## <a name="july-2014"></a>2014 年 7 月

2014年7月版的 SSMA for Oracle 包含下列變更：

* 已新增 Azure SQL DB 的支援。
* 延伸模組套件功能已移至架構，以支援 Azure SQL DB。
* 已新增對 Oracle 具體化 views 的支援。
* 已新增 SQL Server 2014 記憶體優化資料表的支援。
* 已針對具有超過10k 物件的資料庫測試過的效能改進。
* 新增了處理大量物件的 UI 改良功能。
* 已新增已知 LOB 架構的反白顯示。
* 包含轉換速度改進。
* 已新增在 UI 中顯示物件計數的支援。
* 減少超過25% 的報表大小。
* 已改善未分析之結構的錯誤訊息。

## <a name="april-2014"></a>2014 年 4 月

2014年4月版本的 SSMA for Oracle 包含下列變更：

* 已新增 MS SQL Server 2014 的支援。
* 已新增 Oracle 12 和查詢優化的支援。
* 已修正關於轉換至 Azure 的 bug。
* 已修正 IE 10 中不可見報表頁面的相關 bug。

## <a name="january-2012"></a>2012 年 1 月

2012年1月版的 SSMA for Oracle 會將的支援 `RowType` 和 `RecordType` 輸入參數預設為 `NULL` 。

## <a name="july-2011"></a>2011 年 7 月

2011年7月版的 SSMA for Oracle 包含下列變更：

* 已新增將 Oracle 序列轉換為順序產生器的支援 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] 。
* 改善資料移轉期間的錯誤報表。
* 已改善使用保留字的語句轉換。
* 改善函式中 date 值的隱含轉換。

## <a name="april-2011"></a>2011年4月

2011年4月版本的 SSMA for Oracle 包含下列變更：

* 合併 "SSMA for Oracle" 產品，其支援 [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)] 、 [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] 和 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] 。
* 已新增連接和遷移至的支援 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] 。
* 加強的用戶端資料移轉引擎，支援資料的平行遷移。
* 使用 `Simple` 和記錄復原模式來改善資料移轉效能 `Bulk` 。
* 已新增舊版 SSMA （v4.0 和4.2 版）所建立之專案的回溯相容性支援。
* 已新增在舊版 SSMA （v4.0 和4.2 版）上安裝 SSMA for Oracle v4.0 產品並存（SxS）的功能。
* 新增了報告使用者定義型別（包括子型別、 `VARRAY` 、 `NESTED TABLE` 、物件資料表和物件檢視）的支援，以及其在 PL/SQL 區塊中具有特殊錯誤訊息的使用方式。

## <a name="july-2010"></a>2010 年 7 月

2010年7月發行的 SSMA for Oracle 已新增：

* 支援遷移至 SQL Server 2008 R2。
* 用於命令列執行的新 SSMA 主控台應用程式。
* 支援使用伺服器端和用戶端資料移轉引擎來進行資料移轉。
* 支援資料移轉中的「自訂 SELECT」語句。
* 支援從 Oracle 11g R2 進行遷移。

## <a name="june-2008"></a>2008年6月

2008年6月版的 SSMA for Oracle 包含下列變更：

* 增加評量報告的改良功能，包括同義字的其他資訊、可剖析物件的原始來源、面板、SQL Server 標誌移除，以及版面配置持續性。
* 已在物件轉換中新增改良功能：
  * 封裝 `DBMS_LOB` ， `DBMS_SQL` 已加入轉換。
  * 已修訂聯結轉換。
  * 修改集合和記錄轉換，現在是在簡單案例中，透過每個欄位的個別變數發行的記錄轉換。
  * 改進記錄和集合的實施。
  * 已加入視窗化彙總函式。
  * `ROLLUP`/`CUBE`新增的子句。
  * 的改善 `NEXTVAL` / `CURVAL` 。
  * 已新增資料行群組 in `SET` 子句、群組集合和群組識別碼。
  * `MERGE`已新增語句。
  * 支援新的日期時間類型，以及已加入之 CLR 資料類型的記錄和集合的轉換。
* 已加入測試人員的新功能。 現在可以使用測試控管將資料表測試成物件，測試案例中數個可測試物件的呼叫順序可以改變，使用者可以使用記錄和集合來測試程式和函式做為參數和傳回值，而且已加入相依性分析器來檢查僅使用的資料表。
  
## <a name="august-2007"></a>2007年8月

2007年8月發行的 SSMA for Oracle 已新增：

* 新的測試人員元件可讓您建立、管理和執行測試案例，以確認已轉換的 SQL 程式碼。
* SQL 轉換器已加入 Oracle 子類型、集合和本機模組的轉換支援。
* 新的同步處理功能可讓您將特定物件與 SQL Server 資料庫同步。
* 新的轉換選項。
  
## <a name="april-2007"></a>2007年4月

2007年4月版的 SSMA for Oracle 是最初發行版本。
