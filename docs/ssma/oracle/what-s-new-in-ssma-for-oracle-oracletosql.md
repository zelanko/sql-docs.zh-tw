---
title: SSMA for Oracle 的新功能 (OracleToSQL) |Microsoft Docs
description: 瞭解每個版本的 Oracle (OracleToSQL) SQL Server 移轉小幫手 (SSMA) 的變更。
author: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 10/28/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
ms.author: alexiva
ms.openlocfilehash: d7bcff5c96935dee5b696b0fa828cf3ba33eb56e
ms.sourcegitcommit: 9c6130d498f1cfe11cde9f2e65c306af2fa8378d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/30/2020
ms.locfileid: "93036014"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>SSMA for Oracle 的新功能 (OracleToSQL) 

本文列出每個版本中 Oracle 變更的 SQL Server 移轉小幫手 (SSMA) 。

## <a name="ssma-v815"></a>SSMA v 8.15

除了許多協助工具改進之外，適用于 Oracle 的 SSMA v 8.15 版還包含下列變更：

* 新增設定以使用 `%type` 和屬性的完整類型 `%rowtype` 規格
* 改造評量報告以在新式瀏覽器中工作
* 使用資料庫提供的授權單位進行 Azure AD authentication
* 改善從檔案載入之語句的命名

## <a name="ssma-v814"></a>SSMA v 8.14

除了許多改進以確保殘障人士能獲得更高的協助工具，SSMA for Oracle 的 v 8.14 版包含下列變更：

* 將完整的來源/目標伺服器版本儲存在專案中繼資料 (需要專案升級) 
* 盡可能使用 DBA 資料字典進行物件探索
* 修正多個剖析器問題 (`PIVOT` / `UNPIVOT` 、 `MERGE` 替代引號) 
* 修正觸發程式 `INSERTING` / `DELETING` / `UPDATING` 中特殊函式的轉換

## <a name="ssma-v813"></a>SSMA v 8.13

適用于 Oracle 的 SSMA v 8.13 版包含下列變更：

* 修正 `SQLCODE` `SQLERRM` 本機程式中的和特殊函數的轉換
* 轉換程式和函式呼叫時，請考慮隱含類型轉換
* 改善來源連接字串的記錄，以協助疑難排解連接問題

## <a name="ssma-v812"></a>SSMA v 8.12

適用于 Oracle 的 SSMA v 8.12 版包含下列變更：

* 支援 `INSERT` / `UPDATE` / `MERGE` / `DELETE` 語句中的子查詢分解子句
* `ON DELETE SET NULL`在多重路徑或迴圈參考的情況下，子句的轉換訊息
* 改進從動態 SQL 字串建立之資料指標的轉換
* 將 ODP.NET 更新為 v 19。8

## <a name="ssma-v811"></a>SSMA v 8.11

適用于 Oracle 的 SSMA v 8.11 版包含下列變更：

* 語句中的子查詢支援 `INSERT ... VALUES`
* 改進的 `COMMIT` 語句轉換
* 修正子句轉換中的 bug `CONNECT BY LEVEL`
* 將剖析器錯誤恢復邏輯更新為較不貪婪
* 使用 MSAL.NET 程式庫進行互動式 Azure Active Directory 驗證

## <a name="ssma-v810"></a>SSMA v 8.10

SSMA for Oracle 的 v1.1 發行版本包含了輕微的效能改進，以及下列變更：

* 修正具有索引組織之資料表的測試人員問題
* 修正延伸模組套件中擴充預存程式的名稱

## <a name="ssma-v89"></a>SSMA v 8。9

SSMA for Oracle 的8.9 版包含下列變更：

* 動態 SQL 字串常值的轉換
* `LAG` `FIRST_VALUE` 和 `LAST_VALUE` 分析函數的轉換
* 新增對基本 `ALTER TRIGGER` / `ALTER INDEX` DDL (啟用/停用等等的支援 ) 
* 改進符合內建函數名稱的資料行轉換
* 產生可供資料行篩選的唯一索引 `NULL`
* 改善 Azure Synapse Analytics 的變數宣告轉換
* 修正專案名稱中特殊字元的問題

## <a name="ssma-v88"></a>SSMA v 8。8

適用于 Oracle 的 SSMA 8.8 版包含：

* SQL Server 物件同步處理穩定性改進
* 評估和轉換期間的 GUI 效能改進
* 改進分析子句的轉換 `OVER PARTITION`
* 分析函數的新轉換 `LEAD`
* 子查詢分解子句的新轉換
* `REPLICATE`Azure Synapse Analytics 的新散發選項
* 全新的 Oracle 語法剖析器，進一步改善轉換效能

## <a name="ssma-v87"></a>SSMA v 8。7

SSMA for Oracle 的 v 8.7 版本在圖形化使用者介面中有輕微的修正和效能改進。

此外，SSMA for Oracle 現在可讓您根據 [先進物件選取] 對話方塊中的有效狀態來篩選物件。

> [!IMPORTANT]
> 在 SSMA 的8.5 和更新版本中，.NET 4.7.2 是必要的安裝。 如果您需要安裝這個版本，您可以從 [這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v86"></a>SSMA v 8。6

除了針對改善可用性和效能而設計的一組目標修正之外，還新增了一個可讓使用者在轉換的程式碼中省略 SSMA 擴充屬性的設定，藉此增強 SSMA for Oracle 的 v 8.6 版本。

若要利用這項設定，請在 SSMA for Oracle 中流覽至 [ **工具**  >  **專案設定**  >  **一般**  >  **轉換** ]，然後在 [ **其他** ] 下，將 [ **省略擴充屬性** ] 設定的值更新為 **[是]** 。

![省略擴充屬性設定](../oracle/media/ssma-omit-extended-properties.png)

此外，SSMA for Oracle 現在提供了更好的 `XMLTABLE` 子句剖析。

> [!IMPORTANT]
> 在 SSMA 的8.5 和更新版本中，.NET 4.7.2 是必要的安裝。 如果您需要安裝這個版本，您可以從 [這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v85"></a>SSMA v 8。5

SSMA for Oracle 的8.5 版已透過支援 SQL server 中的 Azure Active Directory authentication 和 JSON 功能的基本支援來增強，並提供一組針對改善可用性和效能而設計的目標修正。

此外，SSMA for Oracle 已透過下列支援來增強：

* 將所選物件的探索數目限制為 990 (Oracle 的 `WHERE .. IN (..)` 子句限制為1000個專案) 。
* 從遷移至的資料 `RAW` `UNIQUEIDENTIFIER` 。
* 正在剖析 `PARALLEL_ENABLE` 子句。

最後，SSMA for Oracle 的8.5 版現在提供：

* 改善已轉換之已封裝常數的效能。
* 適用于 .NET 至版本19.5.0 的 Oracle Data Provider 更新。

> [!IMPORTANT]
> 使用 SSMA v 8.5 時，.NET 4.7.2 是必要的安裝程式。 如果您需要安裝這個版本，您可以從 [這裡](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載執行時間檔案。

## <a name="ssma-v84"></a>SSMA v 8。4

SSMA for Oracle 的8.4 版已利用專為解決協助工具問題而設計的目標修正程式，修正了與 max index 資料行相關的錯誤， (為 SQL Server 2016 和更新版本提供32而非 16) 。

此外，此版本的 Oracle SSMA 會將轉換新增為 `SYS_REFCURSOR` 預存程式 `OUT` 參數。

> [!IMPORTANT]
> 在 SSMA 7.4 至8.4 版中，.NET 4.5.2 是必要的安裝。

## <a name="ssma-v83"></a>SSMA v 8。3

SSMA for Oracle 的 v 8.3 發行版本已利用專為改善品質和轉換度量而設計的目標修正來增強。 此外，此版本的 Oracle SSMA 提供下列修正：

* 解決協助工具問題。
* `hierarchyid`在 SQL Server 中加入類型的基本支援。
* 解決透過同義字呼叫之函式的未知傳回型別問題。
* 將 ODP.NET 更新為 v 19.3。

## <a name="ssma-v82"></a>SSMA v 8。2

SSMA for Oracle 的8.2 版已增強至：

* 新增的支援 `DBMS_OUTPUT.ENABLE` / `DISABLE` 。
* `CAST AS FLOAT` `BINARY_FLOAT` `BINARY_DOUBLE` 在預設資料移轉查詢中移除和資料行。
* 如果目前的值已變更，請修正序列重新整理。
* 修正與虛擬資料行的資料解釋相關的錯誤 (等 `ROWNUM` ) 如果有相同名稱的資料行存在的話。
* 修正在 `FOR` 使用不明確的未解析識別碼進行轉換迴圈時所發生的損毀。

此外，此版本還包含一組目標修正程式，其設計目的是要改善品質和轉換度量，以及下列各項的修正：

* 資料移轉後停用非叢集索引的問題。
* 無訊息安裝期間的 .NET Framework 偵測。
* 下載新版本時所發生的間歇性損毀。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v4.0 至8.2 版的更新失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v81"></a>SSMA v 8。1

SSMA for Oracle 的8.1 版已利用專為改善品質和轉換度量而設計的目標修正來增強。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA 8.0 版更新為 v4.0 的失敗。 如果您遇到此錯誤，請下載新版本並手動安裝。

## <a name="ssma-v80"></a>SSMA 8.0 版

SSMA for Oracle 8.0 版的增強功能，已透過設計來改善品質和轉換度量的目標修正來增強。 此版本也提供下列新功能：

* 支援以 **AZURE SQL 受控執行個體** 作為目標。 您現在可以建立以 Azure SQL 受控執行個體為目標的新專案：

  ![SQL MI 專案](../media/ssma-newproject-sqldbmi.png)

  > [!NOTE]
  > SSMA for Oracle 擴充功能套件也會更新，以允許在 Azure SQL 受控執行個體上進行遠端安裝：
  >
  > ![SSMA for Oracle 擴充功能套件](../media/ssma-oracle-ext-pack.png)

  以 Azure SQL 受控執行個體為目標時，不支援某些功能，包括測試人員和伺服器端資料移轉。 請在[此處](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/)閱讀相關資訊。

* 轉換後的 **修正程式** 。 若要深入瞭解[，請參閱。](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)

* 初步的資料庫/架構選取。

  連接到來源時，使用者現在可以選取想要的資料庫/架構。 只選取您打算遷移的架構，可在初始連接期間節省時間，並改善整體 SSMA 效能。

  ![SSMA 篩選物件](../media/ssma-filter-objects.png)

* 使用官方的 managed .NET 驅動程式來連接到 Oracle 的能力。 OCI 驅動程式不再是使用 SQL Server 移轉小幫手 for Oracle 的先決條件。

* 依預設能夠對應 `ROWID` 和 `UROWID` `VARCHAR` 。 變更 `uniqueidentifier` 為以容納明確資料行的資料移轉 `ROWID` 。

## <a name="ssma-v710"></a>SSMA v 7.10

SSMA for Oracle 的 v 7.10 版本包含下列變更：

* 目標修正程式旨在提供額外的安全性和隱私權保護，以符合全球需求的變更。
* 與階層式查詢相關的轉換改進。

## <a name="ssma-v79"></a>SSMA v 7。9

SSMA for Oracle 的 v 7.9 版本包含下列變更：

* 改善品質和轉換度量的目標修正。
* 支援將 "Continue" 語句從 Oracle 遷移至 SQL Server。
* 支援 SSMA 命令列來改變資料類型對應和專案喜好設定。
* 支援使用 SQL Server Integration Services (SSIS) 來遷移資料。 轉換架構之後，您可以使用滑鼠右鍵內容功能表選項來建立 SSIS 封裝。
* SSMA 中的 [Azure SQL Database 連接] 對話方塊也已經改變，以指定完整的伺服器名稱。 在舊版 SSMA 中，必須在專案設定內明確提及 Azure SQL Database 前置詞。

## <a name="ssma-v78"></a>SSMA v 7。8

SSMA for Oracle 的7.8 版版包含下列變更：

* 支援：
  * 子句的資料列運算式 `IN` 。
  * 隱含類型轉換。
  * `UID` Azure SQL Database 的轉換。
* 在 [ **專案設定** ] 中反白顯示變更類型對應。
* 使用者停用遙測的能力。

## <a name="ssma-v77"></a>SSMA 7。7

SSMA for Oracle 的7.7 版中包含下列變更：

* SSMA for Oracle 已透過改善品質和轉換度量的目標修正來增強。
* 根據受歡迎的需求，SSMA for Oracle 的32位版本會回來。 相較于前一次的執行 (在 7.4) 之前，有兩個安裝程式套件，但無法並存安裝。 因此，您必須根據您擁有的連線元件，選擇最適當的版本。 如果可能的話，最好使用64位版本。
* SQL Server 2017 支援現在已正式推出 Linux 上支援的 Oracle 擴充功能套件，也 (新的遠端安裝選項) 。 請注意，當您在 Linux 上安裝時，擴充功能套件功能會受到限制，因為不支援測試人員和伺服器端資料移轉功能。
* 適用于 Oracle 的 SSMA 可讓您將具體化視圖遷移為一般資料表 (可透過 **專案設定**  ->  **同步** 處理  ->  **探索) 的支援資料表** 的設定。

## <a name="ssma-v76"></a>SSMA v 7。6

SSMA for Oracle 的 v 7.6 版本已透過改善品質和轉換度量的目標修正來增強，並支援 SQL Server 2017 (公開預覽) 。 Windows 和 Linux 上的 SQL Server 2017 支援處於公開預覽狀態，不應該用於生產環境的遷移。

## <a name="ssma-v75"></a>SSMA v 7。5

SSMA for Oracle 的7.5 版包含下列變更：

* 增強了許多改進功能，以確保更能方便殘障人士使用。
* 已更新為利用目標修正來改善品質和轉換度量，例如根據客戶的意見反應，改善日期和浮點數資料類型在資料移轉期間的處理。

## <a name="ssma-v74"></a>SSMA 7。4

SSMA for Oracle 的7.4 版包含下列變更：

* SSMA for Oracle 現在支援作為遷移目標平臺的 Azure Synapse Analytics。

  ![[新增專案] 視窗](../media/new-project.png)
  * 支援如下圖所示的資料倉儲儲存選項：

  ![資料倉儲的儲存選項](../media/storage-options_red.png)
  * 支援如下圖所示的資料散發選項：

  ![資料倉儲的資料散發](../media/data-distribution_red.png)

* **查詢超時** 選項現在可在來源和目標的架構物件探索期間使用。

  ![query timeout 選項](../media/query-timeout_red.png)

* 根據客戶的意見反應，已改善目標修正的品質和轉換度量。

> [!IMPORTANT]
> .NET 4.5.2 是安裝 SSMA 7.4 的先決條件。 此外，從 v4.0 開始，32位版本的 SSMA 將會中止。

## <a name="ssma-v73"></a>SSMA v 7。3

SSMA for Oracle 的7.3 版包含下列變更：

* 根據客戶的意見反應，以目標修正改善品質和轉換度量。
* 透過下列專案公開的延伸架構 SSMA：
  * 將功能匯出至 SQL Server Data Tools (SSDT) 專案。
    * 您現在可以將架構腳本從 SSMA 匯出至 SSDT 專案。 您可以使用架構腳本進行額外的架構變更，並部署您的資料庫。

      ![另存為 SSDT 專案命令](../media/export-schema-scripts_red.png)
  * SSMA 可使用的程式庫，以執行自訂轉換。
    * 您現在可以建立程式碼，該程式碼可以處理 SSMA 先前未處理的自訂語法轉換和轉換。
      * 您可以在這篇 blog 文章中找到如何建立自訂轉換器的指示， [擴充 SQL Server 移轉小幫手的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      * 從這 [篇 blog 文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)下載範例專案以進行轉換。

## <a name="ssma-v72"></a>SSMA 7.2 版

SSMA for Oracle 的7.2 版包含下列變更：

* 根據客戶的意見反應，以目標修正改善品質和轉換度量。
* 遙測增強功能，可提供更好的資料點來對客戶問題進行疑難排解，並改善 SSMA 的轉換率。

## <a name="ssma-v71"></a>SSMA 7。1

適用于 Oracle 的 SSMA 7.1 版包含下列變更：

* Windows 和 Linux CTP1 上的 SQL Server 2017 現在是支援遷移的目標平臺。 這項功能在 technical preview 中，可讓您以 SQL server 為目標來進行架構和資料移動。
* SSMA 現在支援自動更新，以在最新版本的 SSMA 可用時立即下載。
* SSMA 可安裝的二進位檔現在會透過 Windows Installer 套件檔案傳遞 ( .msi) 。

## <a name="may-2016"></a>2016 年 5 月

SSMA for Oracle 的2016版版包含下列變更：

* 已新增 SQL Server 2016 的支援。
* 已將 Oracle 閃回封存表的轉換新增至 SQL Server 時態表。

  > [!NOTE]
  > SSMA 不會從 Oracle 閃回資料封存資料表複製歷程記錄資料。 因此，必須在遷移過程中手動複製歷程記錄資料。 此外，雖然 SSMA 不會在 SQL Server 中繼資料瀏覽器中顯示歷程記錄資料表，因為它會被視為系統資料表，所以您可以在 SQL Server Management Studio 中查看歷程記錄資料表。
  >
  > SQL Server 2016 不支援數個 Oracle 閃回功能，包括：
  >
  >   * Oracle 閃回交易查詢
  >   * `DBMS_FLASHBACK` 封裝
  >   * 閃回交易
  >   * 閃資料保存
  >   * 閃回資料表
  >   * 閃重播置
  >   * 閃資料庫

* 已將 Oracle VPD 原則的轉換新增至 Oracle)  (資料列層級安全性的 SQL Server 原則物件。
* 縮短最初載入 Oracle 的時間。
* 改良的剖析器和解析程式。
* 已移除 .NET 2.0 的安裝程式檢查。
* 已將延伸模組套件相依性從 .NET 3.5 更新為 .NET 4.0。
* Fixed `save-project` 和 `open-project` SSMA 主控台的命令。
* 已修正 `securepassword` SSMA 主控台的命令。
* 修正初始載入的物件計數。
* 修正 Oracle 的字元資料類型轉換。
* 修正全域設定中的 bug。

## <a name="march-2016"></a>2016 年 3 月

SSMA for Oracle 的2016年3月預覽版本新增了下列支援：

* 遷移至 SQL Server 2016。
* 遷移 Oracle 資料列層級安全性 () 有一些限制。
* 將 Oracle in memory 資料表遷移至 SQL Server 資料行存放區。

## <a name="january-2016"></a>2016 年 1 月

SSMA for Oracle 的2014年1月維護版本包含下列變更：

* 已新增叢集索引的支援。
* 修正 (RFC 5076207) 的緩慢 Oracle 架構查詢。
* 已修正從主控台連線到 Azure。
* 將 View Log 功能表項目新增至 SSMA (RFC 5706203) 。
* 已新增遙測。

## <a name="july-2014"></a>2014 年 7 月

SSMA for Oracle 的2014年7月發行版本包含下列變更：

* 已新增 Azure SQL Database 的支援。
* 擴充功能套件功能已移至架構，以支援 Azure SQL Database。
* 已新增 Oracle 具體化視圖的支援。
* 已新增 SQL Server 2014 記憶體優化資料表的支援。
* 已針對具有超過10k 個物件的資料庫測試效能改進。
* 新增了處理大量物件的 UI 改進。
* 新增了已知 LOB 架構的反白顯示。
* 包含的轉換速度改進。
* 已新增在 UI 中顯示物件計數的支援。
* 減少超過25% 的報表大小。
* 已改善未剖析之結構的錯誤訊息。

## <a name="april-2014"></a>2014 年 4 月

2014年4月發行的 Oracle SSMA 包含下列變更：

* 已新增 MS SQL Server 2014 的支援。
* 新增 Oracle 12 和查詢優化的支援。
* 已修正有關轉換至 Azure 的 bug。
* 修正 IE 10 中有關不可見報表頁面的錯誤。

## <a name="january-2012"></a>2012 年 1 月

SSMA for Oracle 的2012年1月發行版本新增了的支援 `RowType` 和 `RecordType` 預設為的輸入參數 `NULL` 。

## <a name="july-2011"></a>2011 年 7 月

SSMA for Oracle 的2011年7月發行版本包含下列變更：

* 已將 Oracle 順序轉換的支援新增至順序產生器 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] 。
* 改進資料移轉期間的錯誤報表。
* 使用保留字改進語句的轉換。
* 改進函數中日期值的隱含轉換。

## <a name="april-2011"></a>2011年4月

2011年4月發行的 Oracle SSMA 包含下列變更：

* 合併 "SSMA for Oracle" 產品，其支援 [!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)] 、 [!INCLUDE [ssSQL10](../../includes/sssql10-md.md)] 和 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] 。
* 已新增連接和遷移至的支援 [!INCLUDE [ssSQL11](../../includes/sssql11-md.md)] 。
* 增強的用戶端資料移轉引擎，支援平行的資料移轉。
* 改善的資料移轉效能 `Simple` 以及 `Bulk` 記錄復原模式。
* 已新增舊版 SSMA 所建立專案的回溯相容性支援 (v4.0 和4.2 版) 。
* 已新增將 SSMA for Oracle v4.0 產品並存安裝 (SxS) 舊版 SSMA (v4.0 和4.2 版) 的功能。
* 新增報表 User-Defined 類型的支援 (包括子類型、 `VARRAY` 、 `NESTED TABLE` 、物件資料表和物件檢視) 及其在 PL/SQL 區塊中的使用方式，以及特殊的錯誤訊息。

## <a name="july-2010"></a>2010 年 7 月

SSMA for Oracle 的2010年7月版本已新增：

* 支援遷移至 SQL Server 2008 R2。
* 用於命令列執行的新 SSMA 主控台應用程式。
* 支援使用 Server-Side 和 Client-Side 資料移轉引擎進行資料移轉。
* 在資料移轉中支援「自訂 SELECT」語句。
* 支援從 Oracle 11g R2 進行遷移。

## <a name="june-2008"></a>2008年6月

2008年6月發行的 Oracle SSMA 包含下列變更：

* 已新增評定報告的增強功能，包括同義字的其他資訊、可剖析物件的原始來源、面板和 SQL Server 標誌移除，以及版面配置持續性。
* 新增物件轉換的增強功能：
  * `DBMS_LOB` `DBMS_SQL` 已新增封裝、轉換。
  * 已修訂聯結轉換。
  * 修改集合和記錄轉換，現在會在簡單案例中，透過每個欄位的個別變數來轉換記錄。
  * 改善記錄和集合的執行。
  * 已加入視窗化彙總函式。
  * `ROLLUP`/`CUBE` 加入的子句。
  * 的改進 `NEXTVAL` / `CURVAL` 。
  * 已新增資料行群組 in `SET` 子句、群組集合和群組識別碼。
  * `MERGE` 已加入語句。
  * 支援新的日期時間類型，以及將記錄和集合轉換為加入的 CLR 資料類型。
* 加入了測試人員的新功能。 現在可以使用測試人員將資料表測試為物件，測試案例中數個可測試物件的呼叫順序可以改變，使用者可以使用記錄和集合來測試程式和函式作為參數和傳回值，而將相依性分析器新增至僅檢查使用的資料表。
  
## <a name="august-2007"></a>2007年8月

SSMA for Oracle 的2007年8月版本已新增：

* 新的測試人員元件可讓您建立、管理和執行測試案例，以確認轉換的 SQL 程式碼。
* 已將 Oracle 子類型、集合和本機模組的轉換支援新增至 SQL 轉換器。
* 新的同步處理功能可讓您將特定物件與 SQL Server 資料庫進行同步處理。
* 新的轉換選項。
  
## <a name="april-2007"></a>2007年4月

2007年4月發行的 SSMA for Oracle 是初始發行版本。
