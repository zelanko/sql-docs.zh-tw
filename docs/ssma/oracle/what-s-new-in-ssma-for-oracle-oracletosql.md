---
title: 甲骨文(OracleToSQL)SSMA的新增功能 |微軟文件
authors: HJToland3;nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 4/2/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f305ebb6-7393-4a43-abb3-6332b739d690
ms.author: jtoland;alexiva
ms.openlocfilehash: 88b87aad931f28637accc95aa4d993037fcf0b0a
ms.sourcegitcommit: d818a307725983c921987749915fe1a381233d98
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/03/2020
ms.locfileid: "80625602"
---
# <a name="whats-new-in-ssma-for-oracle-oracletosql"></a>Oracle SSMA 中的新增功能 (OracleToSQL)

本文列出了每個版本中 Oracle 更改的 SQL 伺服器遷移助手 (SSMA)。

## <a name="ssma-v88"></a>SSMA v8.8

Oracle SSMA 的 v8.8 版本包括:

* SQL Server 物件同步穩定性改進
* 評估並轉換期間的 GUI 效能改進
* 改進分析`OVER PARTITION`條款的轉換
* 分析函數`LEAD`的新轉換
* 子查詢保理子句的新轉換
* Azure `REPLICATE` SQL 資料主目錄的新分轉選項
* 全新 Oracle 語法解析器,進一步提高轉換性能

## <a name="ssma-v87"></a>SSMA v8.7

Oracle 的 SSMA v8.7 版本在圖形使用者介面中具有輕微的修復和性能改進。

此外,Oracle 的 SSMA 現在允許在「進階物件選擇」對話框中根據有效性狀態篩選物件。

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本,.NET 4.7.2 是安裝的先決條件。 如果需要安裝此版本,可以[在此處](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載運行時檔。

## <a name="ssma-v86"></a>SSMA v8.6

除了一組旨在提高可用性和性能的有針對性的修補程式外,Oracle 的 V8.6 版本還透過添加允許使用者在轉換後的代碼中省略 SSMA 擴充屬性的設置進行了增強。

要利用此設定,在 Oracle 的 SSMA 中,導航到**工具** > **專案設定** > **常規** > **轉換**,然後在**Misc**下,將 **「Omit 擴展屬性**」設置的值更新為 **"是**"。

![省略延伸屬性設定](../oracle/media/ssma-omit-extended-properties.png)

此外,Oracle 的 SSMA`XMLTABLE`現在提供了對子句的改進解析。

> [!IMPORTANT]
> 使用 SSMA v8.5 及更高版本,.NET 4.7.2 是安裝的先決條件。 如果需要安裝此版本,可以[在此處](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載運行時檔。

## <a name="ssma-v85"></a>SSMA v8.5

支援 Azure Active Directory 身份驗證和對 SQL 伺服器中的 JSON 功能的基本支援,以及一組旨在提高可用性和性能的有針對性的修補程式,增強了 Oracle SSMA 的 v8.5 版本。

此外,Oracle 的 SSMA 得到了增強,支援:

* 將用於發現選擇的物件數限制為 990(Oracle`WHERE .. IN (..)`子 句限制為 1000 項)。
* 從`RAW`到`UNIQUEIDENTIFIER`的數據遷移。
* 解析`PARALLEL_ENABLE`子句。

最後,Oracle 的 SSMA v8.5 版本現在提供了:

* 改進轉換的打包常量的性能。
* .NET 的 Oracle 資料提供程式更新到版本 19.5.0。

> [!IMPORTANT]
> 使用 SSMA v8.5 時,.NET 4.7.2 是安裝的先決條件。 如果需要安裝此版本,可以[在此處](https://dotnet.microsoft.com/download/dotnet-framework/net472)下載運行時檔。

## <a name="ssma-v84"></a>SSMA v8.4

Oracle 的 SSMA v8.4 版本通過有針對性的修補程式進行增強,這些修補程式旨在解決輔助功能問題並修復 SQL Server 2016 和更高版本的最大索引列(允許 32 而不是 16)相關的 Bug。

此外,此版本的 Oracle SSMA`SYS_REFCURSOR`增加了`OUT`作為儲存過程 參數的轉換。

> [!IMPORTANT]
> 對於 SSMA 版本 7.4 到 8.4,.NET 4.5.2 是安裝的先決條件。

## <a name="ssma-v83"></a>SSMA v8.3

Oracle 的 SSMA v8.3 版本透過旨在提高品質和轉換指標的有針對性的修補程式進行增強。 此外,此版本的 Oracle SSMA 提供了以下修補程式:

* 解決輔助功能問題。
* 添加對`hierarchyid`SQL Server 類型的基本支援。
* 解決通過同義詞調用的函數的未知返回類型的問題。
* 將ODP.NET更新為v19.3。

## <a name="ssma-v82"></a>SSMA v8.2

Oracle 的 SSMA v8.2 版本已增強為:

* 添加對`DBMS_OUTPUT.ENABLE`/`DISABLE`的支援。
* 刪除`CAST AS FLOAT``BINARY_FLOAT``BINARY_DOUBLE`預設資料移轉查詢中的和欄位。
* 如果當前值已更改,修復序列將刷新。
* 如果存在同名列,則修復與誤解偽列`ROWNUM`(等) 相關的 Bug。
* 修復發生轉換具有不明確未解析`FOR`標識符的循環的崩潰。

此外,此版本還包括一組旨在提高品質和轉化指標的有針對性的修補程式,以及用於以下的修補程式:

* 數據遷移后禁用的非群集索引的問題。
* 在靜默安裝期間檢測 .NET 框架。
* 下載新版本時發生的間歇性崩潰。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v8.1 到 v8.2 的更新失敗。 如果您遇到此錯誤,請下載新版本並手動安裝。

## <a name="ssma-v81"></a>SSMA v8.1

Oracle 的 SSMA v8.1 版本透過旨在提高品質和轉換指標的有針對性的修補程式進行增強。

> [!NOTE]
> 自動更新的已知問題可能會導致從 SSMA v8.0 到 v8.1 的更新失敗。 如果您遇到此錯誤,請下載新版本並手動安裝。

## <a name="ssma-v80"></a>SSMA v8.0

Oracle SSMA 的 v8.0 版本透過旨在提高品質和轉換指標的有針對性的修補程式得到增強。 此版本還提供以下新功能:

* 支援**Azure SQL 資料庫託管實例**作為目標。 現在,您可以建立針對 Azure SQL 資料庫託管實例的新專案:

  ![SQL DB MI 專案](../media/ssma-newproject-sqldbmi.png)

  > [!NOTE]
  > Oracle 延伸套件的 SSMA 也進行了更新,以允許在 Azure SQL 資料庫託管實例上進行遠端安裝:
  >
  > ![Oracle 延伸套件的 SSMA](../media/ssma-oracle-ext-pack.png)

  定位 Azure SQL 資料庫託管實例時,不支援某些功能,包括測試人員和伺服器端數據遷移。 請在[此處](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/migrate-your-oracle-database-to-azure-sql-database-managed-instance-using-ssma-8-0/)閱讀相關資訊。

* 轉換後**修復顧問**。 此處瞭解有關它的更多[。](https://blogs.msdn.microsoft.com/datamigration/2019/02/17/%20accelerate-your-oracle-migrations-with-new-machine-learning-capabilities-in-ssma/)

* 初步資料庫/架構選擇。

  連接到源時,用戶現在可以選擇感興趣的資料庫/架構。 僅選擇計畫遷移的架構將節省時間連接期間的時間,並提高 SSMA 的整體性能。

  ![SSMA 篩選物件](../media/ssma-filter-objects.png)

* 能夠使用官方管理的 .NET 驅動程式連接到 Oracle。 OCI 驅動程式不再是使用 Oracle SQL 伺服器遷移助手的先決條件。

* 預設情況下,可以映射`ROWID`與`UROWID`對應到`VARCHAR`。 更改了`uniqueidentifier`,以適應顯`ROWID`式 列的數據遷移。

## <a name="ssma-v710"></a>SSMA v7.10

Oracle 的 SSMA v7.10 版本包含以下變更:

* 旨在提供額外安全和隱私保護以滿足全球需求變化的有針對性的修補程式。
* 與分層查詢相關的轉換改進。

## <a name="ssma-v79"></a>SSMA v7.9

Oracle 的 SSMA v7.9 版本包含以下變更:

* 提高品質和轉化指標的針對性修復。
* 支援將「繼續」語句從 Oracle 移轉到 SQL 伺服器。
* 支援 SSMA 命令列以更改資料類型映射和專案首選項。
* 支援使用 SQL 伺服器整合服務 (SSIS) 遷移資料。 轉換架構後,可以使用右鍵單擊上下文菜單選項創建 SSIS 包。
* SSMA 中的 Azure SQL 資料庫連接對話方塊也已更改,以指定完全限定的伺服器名稱。 在 SSMA 的早期版本中,必須在專案設置中顯式提及 Azure SQL 資料庫前綴。

## <a name="ssma-v78"></a>SSMA v7.8

Oracle 的 SSMA v7.8 版本包含以下變更:

* 支援:
  * 子句的`IN`行表達式。
  * 隱式類型強制轉換。
  * `UID`Azure SQL 資料庫的轉換。
* 更改類型對應在**項目設定**中突出顯示。
* 使用者禁用遙測功能。

## <a name="ssma-v77"></a>SSMA v7.7

Oracle 的 SSMA v7.7 版本包含以下變更:

* Oracle 的 SSMA 已通過提高品質和轉化指標的針對性修補程式進行了增強。
* 根據大眾需求,甲骨文的32位版SSMA又回來了。 與以前的實現(在 v7.4 之前)相比,有兩個安裝程式包,但不能並排安裝。 因此,您必須根據擁有的連接元件選擇最合適的版本。 如果可能,最好使用 64 位元版本。
* SQL Server 2017 支援現在正式,在 Linux 上支援 Oracle 擴展套件(新的遠端安裝選項)。 請注意,在 Linux 上安裝擴展包功能受到限制,因為不支援測試人員和伺服器端數據遷移功能。
* Oracle 的 SSMA 允許您將具體化檢視移至常規表(可透過**專案設定** -> **同步** -> 中的設定配置 **,發現具體檢視的備份表**)。

## <a name="ssma-v76"></a>SSMA v7.6

Oracle SSMA 的 v7.6 版本透過提高品質和轉換指標的針對性修補程式以及支援 SQL Server 2017(公共預覽)來增強。 Windows 和 Linux 上對 SQL Server 2017 的支援處於公共預覽版,不應用於生產遷移。

## <a name="ssma-v75"></a>SSMA v7.5

Oracle 的 SSMA v7.5 版本包含以下變更:

* 通過多項改進進行改進,確保殘疾人獲得更多無障礙環境。
* 通過有針對性的修復改進品質和轉換指標,例如根據客戶反饋改進數據遷移期間的日期和浮動數據類型的處理。

## <a name="ssma-v74"></a>SSMA v7.4

Oracle 的 SSMA v7.4 版本包含以下變更:

* Oracle 的 SSMA 現在支援 Azure SQL 資料倉庫作為遷移的目標平臺。

  ![[新增專案] 視窗](../media/new-project.png)
  * 支援資料倉儲記憶體選項,如下圖所示:

  ![資料倉儲的儲存選項](../media/storage-options_red.png)
  * 支援影像的標題的資料分發選項:

  ![資料倉儲資料分發](../media/data-distribution_red.png)

* **查詢超時**選項現在在源和目標架構對象發現期間可用。

  ![查詢逾時選項](../media/query-timeout_red.png)

* 品質和轉化指標已根據客戶反饋通過有針對性的修復得到了改進。

> [!IMPORTANT]
> .NET 4.5.2 是安裝 SSMA v7.4 的先決條件。 此外,從 v7.4 開始,SSMA 的 32 位元版本正在停產。

## <a name="ssma-v73"></a>SSMA v7.3

Oracle 的 SSMA v7.3 版本包含以下變更:

* 根據客戶反饋有針對性地修復,提高品質和轉化指標。
* 透過以下項目公開的 SSMA 可擴充性框架:
  * 將功能匯出到 SQL 伺服器資料工具 (SSDT) 專案。
    * 現在,您可以將架構腳本從 SSMA 匯出到 SSDT 專案。 您可以使用架構腳本進行其他架構更改並部署資料庫。

      ![另存為 SSDT 專案指令](../media/export-schema-scripts_red.png)
  * SSMA 可使用用於執行自定義轉換的庫。
    * 現在,您可以建構可以處理 SSMA 以前未處理的自訂語法轉換和轉換的代碼。
      * 有關如何建構自訂轉換器的說明,可在此部落格文章,[擴充 SQL 伺服器移轉助手的轉換功能](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/)。
      * 從這個[博客文章](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/)下載一個轉換的範例專案。

## <a name="ssma-v72"></a>SSMA v7.2

Oracle 的 SSMA v7.2 版本包含以下變更:

* 根據客戶反饋有針對性地修復,提高品質和轉化指標。
* 遙測增強功能,以提供更好的數據點,以解決客戶問題並提高 SSMA 的轉化率。

## <a name="ssma-v71"></a>SSMA v7.1

Oracle 的 SSMA v7.1 版本包含以下變更:

* Windows 和 Linux CTP1 上的 SQL Server 2017 現在是支援遷移的目標平臺。 此功能處於技術預覽中,允許架構和數據移動以目標 SQL 伺服器為目標。
* SSMA 現在支援自動更新,以便一旦 SSMA 可用,立即下載。
* SSMA 可安裝二進位檔案現在透過 Windows 安裝套件檔 (.msi) 傳遞。

## <a name="may-2016"></a>2016 年 5 月

2016 年 5 月版本的 Oracle SSMA 包含以下變更:

* 添加了對 SQL Server 2016 的支援。
* 將 Oracle 快閃回存檔表轉換為 SQL Server 臨時表。

  > [!NOTE]
  > SSMA 不會從 Oracle 快閃記憶體資料存檔表複製歷史資料。 因此,必須在遷移過程中手動複製歷史記錄數據。 此外,雖然 SSMA 不會在 SQL Server 中繼資料資源管理器中顯示歷史記錄表,因為它被視為系統表,但您可以在 SQL Server 管理工作室中查看歷史記錄表。
  >
  > SQL Server 2016 不支援多個 Oracle 閃回功能,包括:
  >
  >   * 甲骨文閃回事務查詢
  >   * `DBMS_FLASHBACK`包
  >   * 閃回交易
  >   * 快閃回資料存檔
  >   * 閃回表
  >   * 閃回丟棄
  >   * 閃回資料庫

* 將 Oracle VPD 策略轉換為 SQL 伺服器策略物件(Oracle 的行級安全性)。
* 減少了 Oracle 的初始載入時間。
* 改進的解析器和解析器。
* 已刪除的安裝程式檢查 .NET 2.0。
* 將擴展包依賴項從 .NET 3.5 更新為 .NET 4.0。
* SSMA 主控台`save-project`的`open-project`固定和命令。
* SSMA 主控台`securepassword`的固定 命令。
* 修復了初始載入的物件計數。
* 修復了 Oracle 字元數據類型的轉換。
* 修復了全域設置中的 Bug。

## <a name="march-2016"></a>2016 年 3 月

2016 年 3 月為 Oracle 發表的 SSMA 預覽版增加了對以下支援:

* 遷移到 SQL Server 2016。
* 遷移 Oracle 行級級安全性(具有限制)。
* 將記憶體表中的 Oracle 移至 SQL 伺服器列儲存。

## <a name="january-2016"></a>2016 年 1 月

2014 年 1 月適用於 Oracle 的 SSMA 維護版本包含以下變更:

* 添加了對群集索引的支援。
* 修復了慢速 Oracle 架構查詢 (RFC 5076207)。
* 修復了從控制台連接到 Azure 的連接。
* 將檢視日誌功能表項添加到 SSMA (RFC 5706203)。
* 添加了遙測。

## <a name="july-2014"></a>2014 年 7 月

2014 年 7 月版本的 Oracle SSMA 包含以下變更:

* 添加了對 Azure SQL DB 的支援。
* 擴展包功能移動到架構以支援 Azure SQL DB。
* 添加了對 Oracle 具體化檢視的支援。
* 添加了對 SQL Server 2014 記憶體優化表的支援。
* 包括為具有 10k 個以上對象的資料庫測試的性能改進。
* 添加了用於處理大量物件的UI改進。
* 添加了已知 LOB 架構的突出顯示。
* 包括轉換速度改進。
* 添加了對在 UI 中顯示物件計數的支援。
* 報表大小減少 25% 以上。
* 改進了未解析構造的錯誤消息。

## <a name="april-2014"></a>2014 年 4 月

2014 年 4 月版本的 Oracle SSMA 包含以下變更:

* 添加了對 MS SQL Server 2014 的支援。
* 添加了對 Oracle 12 和查詢優化的支援。
* 修復了有關轉換為 Azure 的錯誤。
* 修復了 IE 10 中不可見報表頁的 Bug。

## <a name="january-2012"></a>2012 年 1 月

2012 年 1 月版本的 Oracle SSMA 添加了對 預設`RowType`的`RecordType``NULL`和預設的輸入參數的支援和 輸入參數。

## <a name="july-2011"></a>2011 年 7 月

2011 年 7 月版本的 Oracle SSMA 包含以下變更:

* 添加了對將 Oracle 序列[!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]轉換為 序列生成器的支援。
* 改進了數據遷移期間的錯誤報告。
* 使用保留詞改進語句的轉換。
* 改進了函數中日期值的隱式轉換。

## <a name="april-2011"></a>2011年4月

2011 年 4 月版本的 Oracle SSMA 包含以下變更:

* 整合的「甲骨文 SSMA」產品,[!INCLUDE [ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE [ssSQL10](../../includes/sssql10-md.md)]支援[!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]與 。
* 添加了對連接和遷移到[!INCLUDE [ssSQL11](../../includes/sssql11-md.md)]的支援。
* 增強的用戶端數據遷移引擎,支援數據的並行遷移。
* 使用`Simple`和`Bulk`記錄恢復模型提高了數據遷移性能。
* 添加了對早期版本的 SSMA(v4.0 和 v4.2)創建的專案的向後相容性的支援。
* 添加了使用舊版本的 SSMA(v4.0 和 v4.2)並排安裝 Oracle v5.0 產品 SSMA (SxS) 的能力。
* 添加了對報告使用者定義類型(包括子類型、`VARRAY``NESTED TABLE`物件 表和物件檢視)及其在 PL/SQL 塊中的用法的支援,並帶有特殊錯誤消息。

## <a name="july-2010"></a>2010 年 7 月

2010 年 7 月發布的 Oracle SSMA 新增了:

* 支援遷移到 SQL Server 2008 R2。
* 用於命令列執行的新 SSMA 主控台應用程式。
* 使用伺服器端和客戶端數據遷移引擎支援數據遷移。
* 在資料遷移中支援"自定義 SELECT"語句。
* 支援從 Oracle 11g R2 移轉。

## <a name="june-2008"></a>2008 年 6 月

2008 年 6 月版本的 Oracle SSMA 包含以下變更:

* 增加了評估報告的改進,包括同義詞的其他資訊、可解析物件的原始源、面板和 SQL Server 徽標刪除以及佈局持久性。
* 在物件轉換方面增加了改進:
  * 套件`DBMS_LOB``DBMS_SQL`, 轉換新增.
  * 加入已修訂的轉化。
  * 修改集合和記錄轉換,現在轉換記錄,在通過每個欄位的單獨變數發佈的簡單情況下。
  * 改進記錄和集合實現。
  * 添加了視窗聚合函數。
  * `ROLLUP`/`CUBE`添加了子句。
  * 改進。 `NEXTVAL` / `CURVAL`
  * 添加了子句`SET`、分組集和分組 ID 中的列分組。
  * `MERGE`聲明添加。
  * 支援新的日期時間類型,並在添加 CLR 數據類型時轉換記錄和集合。
* 添加了測試器的新功能。 現在可以使用 Tester 將表作為物件進行測試,可以更改測試用例中多個可測試物件的調用順序,使用者可以使用記錄和集合作為參數和返回值來測試過程和函數,並添加了依賴關係分析器以僅檢查使用的表。
  
## <a name="august-2007"></a>2007 年 8 月

2007 年 8 月發布的 Oracle SSMA 增加了:

* 新的 Tester 元件允許您建立、管理和運行測試用例,以驗證轉換後的 SQL 代碼。
* 支援轉換 Oracle 子類型、集合和本地模組已添加到 SQL 轉換器中。
* 新的同步功能允許您將特定物件與 SQL Server 資料庫同步。
* 新的轉換選項。
  
## <a name="april-2007"></a>2007年4月

2007 年 4 月發布的 Oracle SSMA 是首次發表。
