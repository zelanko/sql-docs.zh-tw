---
title: SQL Server 2019 的新功能 | Microsoft Docs
ms.date: 01/09/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ef507ebef690dc75e21539311e45b8932a721c3a
ms.sourcegitcommit: 769b71f01052ec9b4fc5eb02d9da9a1a58118029
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56319219"
---
# <a name="whats-new-in-sql-server-2019"></a>SQL Server 2019 的新功能

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

  > [!div class="nextstepaction"]
  > [請提供您對 SQL Docs 目錄的意見反應！](https://aka.ms/sqldocsurvey)

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 是以舊版本為基礎，可讓 SQL Server 成長為平台，以供您選擇開發語言、資料類型、內部部署或雲端以及作業系統。 本文摘要說明 SQL Server 2019 的新功能。 如需詳細資訊和已知問題，請參閱 [SQL Server 2019 版本資訊](sql-server-ver15-release-notes.md)。

**試用 SQL Server 2019！**
- [![從評估中心下載](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=862101) [下載 SQL Server 2019 以安裝於 Windows](https://go.microsoft.com/fwlink/?LinkID=862101)
- 安裝於 Linux for [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md)、[SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) 和 [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)。
- [在 Docker 的 SQL Server 2019 上執行](../linux/quickstart-install-connect-docker.md)。

## <a name="ctp-22"></a>CTP 2.2

Community Technical Preview (CTP) 2.2 是 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 的最新公開版本。 這個版本對先前的 CTP 版本做了改進，以修正 Bug，提升安全性，以及將效能最佳化。 此外，也為 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.2 新增或強化了下列功能。

- [巨量資料叢集](#bigdatacluster)
  - 對巨量資料叢集使用 Azure Data Studio 的 SparkR

- [資料庫引擎](#databaseengine)
  - 在 SQL Server 複寫中使用 UTF-8 字元編碼。

## <a name="previous-ctps"></a>舊版 CTP

更早的 CTP 版本為 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 新增或強化了下列功能。

- [巨量資料叢集](#bigdatacluster) 
  - 在 Kubernetes 上部署具有 SQL 和 Spark Linux 容器的巨量資料叢集 (CTP 2.0)
  - 從 HDFS 中存取巨量資料 (CTP 2.0)
  - 使用 Spark 執行進階分析和機器學習 (CTP 2.0)
  - 使用 Spark 串流將資料串流至 SQL 資料集區 (CTP 2.0)
  - 使用 Azure Data Studio 來執行提供筆記本體驗的查詢簿 (CTP 2.0)
  - 部署 Python 和 R 應用程式 (CTP 2.1)

- [資料庫引擎](#databaseengine)
  - UTF-8 支援 (CTP 2.0)
  - 可繼續的線上索引建立允許索引建立在中斷後繼續 (CTP 2.0)
  - 叢集資料行存放區線上索引建置和重建 (CTP 2.0)
  - 具有安全記憶體保護區的 Always Encrypted (CTP 2.0)
  - 智慧查詢處理 (CTP 2.0)
  - Java 語言可程式性延伸模組 (CTP 2.0)
  - SQL Graph 功能 (CTP 2.0)
  - 線上和可繼續 DDL 作業的資料庫範圍組態設定 (CTP 2.0)
  - Always On 可用性群組 - 次要複本連線重新導向 (CTP 2.0)
  - 資料探索和分類 - 原生建置於 SQL Server 中 (CTP 2.0)
  - 持續性記憶體裝置的擴充支援 (CTP 2.0)
  - `DBCC CLONEDATABASE` 中資料行存放區統計資料的支援 (CTP 2.0)
  - 新增至 `sp_estimate_data_compression_savings` 的選項 (CTP 2.0)
  - SQL Server 機器學習服務容錯移轉叢集 (CTP 2.0)
  - 預設已啟用的輕量型查詢分析基礎結構 (CTP 2.0)
  - 新 PolyBase 連接器 (CTP 2.0)
  - 新 `sys.dm_db_page_info` 系統函數會傳回頁面資訊 (CTP 2.0)
  - 智慧型查詢處理新增純量 UDF 內嵌 (CTP 2.1)
  - 改善截斷錯誤訊息，以包含資料表和資料行名稱，以及被截斷的值 (CTP 2.1)
  - 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 安裝程式中支援 UTF-8 定序 (CTP 2.1)
  - 在圖形比對查詢中使用衍生資料表或檢視別名 (CTP 2.1)
  - 改善統計資料封鎖的診斷資料 (CTP 2.1)
  - 混合式緩衝集區 (CTP 2.1)
  - 靜態資料遮罩 (CTP 2.1)

- [Linux 上的 SQL Server](#sqllinux)
  - 複寫支援 (CTP 2.0)
  - Microsoft Distributed Transaction Coordinator (MSDTC) 支援 (CTP 2.0)
  - 具有 Kubernetes 之 Docker 容器上的 Always On 可用性群組 (CTP 2.0)
  - 協力廠商 AD 提供者的 OpenLDAP 支援 (CTP 2.0)
  - Linux 上的機器學習 (CTP 2.0)
  - 新容器登錄 (CTP 2.0)
  - 新的以 RHEL 為基礎容器映像 (CTP 2.0)
  - 記憶體不足的壓力通知 (CTP 2.0)

- [Master Data Services](#mds)
  - 已取代 Silverlight 控制項 (CTP 2.0)

- [安全性](#security)
  - SQL Server 組態管理員中的憑證管理 (CTP 2.0)

- [工具](#tools)
  - SQL Server Management Studio (SSMS) 18.0 (預覽) (CTP 2.0)
  - Azure Data Studio (CTP 2.0)
  - Azure Data Studio (CTP 2.1)

如需這些功能的詳細資料，請繼續閱讀。

## <a id="bigdatacluster"></a>巨量資料叢集

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] [巨量資料叢集](../big-data-cluster/big-data-cluster-overview.md)會啟用新的案例，包括下列：

- 對巨量資料叢集使用 Azure Data Studio 的 SparkR。 (CTP 2.2)
- [部署 Python 和 R 應用程式](../big-data-cluster/big-data-cluster-create-apps.md)。 (CTP 2.1)
- 在 Kubernetes 上部署具有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 Spark Linux 容器的巨量資料叢集 (CTP 2.0)
- 從 HDFS 中存取巨量資料 (CTP 2.0)
- 使用 Spark 執行進階分析和機器學習 (CTP 2.0)
- 使用 Spark 串流將資料串流至 SQL 資料集區 (CTP 2.0)
- 在 [**Azure Data Studio**](../sql-operations-studio/what-is.md) 中執行可提供筆記型體驗的查詢活頁簿。 (CTP 2.0)
 
[!INCLUDE [Big data clusters preview](../includes/big-data-cluster-preview-note.md)]

## <a id="databaseengine"></a> 資料庫引擎

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 推出或強化了下列 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的新功能

### <a name="scalar-udf-inlining-ctp-21"></a>純量 UDF 內嵌 (CTP 2.1)

純量 UDF 內嵌會將純量使用者定義函數 (UDF) 自動轉換成關聯運算式，並將它們內嵌在呼叫 SQL 查詢中，以改善運用純量 UDF 之工作負載的效能。 純量 UDF 內嵌有助於對 UDF 內的作業進行以成本為基礎的最佳化，以促成集合導向、平行且有效率的計畫，而不是無效率、反覆且連續的執行計畫。 根據預設，資料庫相容性層級 150 會啟用此功能。

如需詳細資訊，請參閱[純量 UDF 內嵌](../relational-databases/user-defined-functions/scalar-udf-inlining.md)。

### <a name="truncation-error-message-improved-to-include-table-and-column-names-and-truncated-value-ctp-21"></a>改善截斷錯誤訊息，以包含資料表和資料行名稱，以及被截斷的值 (CTP 2.1)

許多曾開發或維護資料移動工作負載的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 開發人員，都很熟悉錯誤訊息識別碼 8152 `String or binary data would be truncated`；此錯誤會在於結構描述不同的來源與目的地之間轉送資料，且來源資料太大而無法納入目的地資料類型的情況下發生。 對此錯誤訊息進行疑難排解，可能需要花費很多時間。 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 針對此案例引進了更加特定的新錯誤訊息 (2628)：  

`String or binary data would be truncated in table '%.*ls', column '%.*ls'. Truncated value: '%.*ls'.`

新的錯誤訊息 2628 能針對資料截斷問題提供更多內容，以簡化疑難排解的程序。 對 CTP 2.1 和 CTP 2.2 而言，這是加入錯誤訊息，而且需要啟用[追蹤旗標](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 460。

### <a name="improved-diagnostic-data-for-stats-blocking-ctp-21"></a>改善統計資料封鎖的診斷資料 (CTP 2.1)

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 能針對等候同步統計資料更新作業的長時間執行查詢，提供改善的診斷資料。 動態管理檢視 `sys.dm_exec_requests` 資料行 `command` 會在 `SELECT` 正在等候同步統計資料更新作業完成以繼續查詢執行的情況下，顯示 `SELECT (STATMAN)`。  此外，新的等候類型 `WAIT_ON_SYNC_STATISTICS_REFRESH` 會顯示在 `sys.dm_os_wait_stats` 動態管理檢視中。 它會顯示花費在同步統計資料重新整理作業上的累積執行個體層級時間。

### <a name="static-data-masking-ctp-21"></a>靜態資料遮罩 (CTP 2.1)

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 提供靜態資料遮罩。 您可以使用靜態資料遮罩來處理 SQL Server 資料庫複本中的敏感性資料。 靜態資料遮罩可協助建立已處理的資料庫複本，其中的所有敏感性資訊都已經被更改為使該複本可與非生產使用者共用的形式。 靜態資料遮罩可用於開發、測試、分析與商務報告、合規性、疑難排解，以及任何其他無法將特定資料複製到不同環境的案例。

靜態資料遮罩會在資料行層級運作。 請選取要進行遮罩的資料行，並針對每個選取的資料行指定遮罩功能。 靜態資料遮罩會複製資料庫，然後將指定的遮罩功能套用至資料行。

#### <a name="static-data-masking-vs-dynamic-data-masking"></a>靜態資料遮罩與動態資料遮罩

資料遮罩是將遮罩套用到資料庫上以隱藏敏感性資訊，並以新的或已刪除的資料取代它的程序。 Microsoft 提供兩個遮罩選項：靜態資料遮罩與動態資料遮罩。 動態資料遮罩已於 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 中推出。 下表會比較這兩個解決方案：

|靜態資料遮罩 |動態資料遮罩|
|:----|:----|
|在資料庫的複本上發生 <br/><br/>無法擷取原始資料<br/><br/>遮罩會在儲存體層級上發生<br/><br/>所有使用者都可以存取相同的已遮罩資料<br/><br/>適用於持續的全體小組存取|在原始資料庫上發生<br/><br/>原始資料保持不變<br/><br/>遮罩會在查詢階段即時發生<br/><br/>遮罩會視使用者權限而有所不同 <br/><br/>適用於精確的使用者特定存取|

### <a name="database-compatibility-level-ctp-20"></a>資料庫相容性層級 (CTP 2.0)

新增資料庫 **COMPATIBILITY_LEVEL 150**。 若要針對特定使用者資料庫啟用，請執行：

   ```sql
   ALTER DATABASE database_name SET COMPATIBILITY_LEVEL =  150;
   ```

### <a name="utf-8-support-ctp-22"></a>UTF-8 支援 (CTP 2.2)

完整支援廣泛使用 UTF-8 字元編碼作為匯入或匯出編碼，或作為文字資料的資料庫層級或資料行層級定序。 UTF-8 允許用於 `CHAR` 和 `VARCHAR` 資料類型，並且在建立物件定序或將其變更為具有 `UTF8` 尾碼的定序時啟用。 

例如，`LATIN1_GENERAL_100_CI_AS_SC` 至 `LATIN1_GENERAL_100_CI_AS_SC_UTF8`。 UTF-8 僅適用於支援增補字元的 Windows 定序，已於 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 中推出。 `NCHAR` 和 `NVARCHAR` 只允許 UTF-16 編碼，並維持不變。

此功能可能會節省大量儲存空間 (視使用的字元集而定)。 例如，使用啟用 UTF-8 的定序，將具有拉丁文字串的現有資料行資料類型從 `NCHAR(10)` 變更為 `CHAR(10)` 會使儲存體需求減少 50%。 這項減少的原因是 `NCHAR(10)` 需要 20 個位元組作為儲存空間，而 `CHAR(10)` 針對相同的 Unicode 字串需要 10 個位元組。

如需詳細資訊，請參閱 [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)。

CTP 2.1 新增了在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 安裝期間選取 UTF-8 定序作為預設的支援。

CTP 2.2 新增了在 SQL Server 複寫中使用 UTF-8 字元編碼的支援。

### <a name="resumable-online-index-create-ctp-20"></a>可繼續的線上索引建立 (CTP 2.0)

- **可繼續的線上索引建立**允許索引建立作業暫停並稍後可從作業暫停或失敗處繼續，而不是從頭重新啟動。

  可繼續的線上索引建立支援下列情節：
  - 在索引建立失敗之後繼續索引建立作業；例如，在資料庫容錯移轉之後或磁碟空間不足之後。
  - 暫停進行中索引建立作業，並稍後繼續視需要允許暫時釋放系統資源，然後稍後繼續此作業。
  - 建立大型索引，而不需要使用最多記錄空間，以及封鎖其他維護活動並允許截斷記錄的長時間執行交易。

  如果索引建立失敗，則沒有此功能，必須重新執行線上索引建立作業，而且必須從頭重新啟動作業。

使用此版本，我們會擴充可繼續的功能，以將此功能新增至可用的[可繼續線上索引重建](https://azure.microsoft.com/blog/modernize-index-maintenance-with-resumable-online-index-rebuild/)。

此外，可以使用[線上和可繼續 DDL 作業的資料庫範圍預設設定](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)將此功能設定為特定資料庫的預設值。

如需詳細資訊，請參閱[可繼續的線上索引建立](../t-sql/statements/create-index-transact-sql.md#resumable-indexes)。

### <a name="build-and-rebuild-clustered-columnstore-indexes-online-ctp-20"></a>線上建置和重建叢集資料行存放區索引 (CTP 2.0)

將資料列存放區資料表轉換成資料行存放區格式。 建立叢集資料行存放區索引 (CCI) 是舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中的離線程序；需要所有變更在建立 CCI 時停止。 使用 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 和 [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]，您可以在線上建立或重新建立 CCI。 工作負載不會遭到封鎖，而且對基礎資料所做的所有變更都會以透明的方式新增至目標資料行存放區資料表。 可使用的新 [!INCLUDE[tsql](../includes/tsql-md.md)] 陳述式範例如下：

  ```sql
  CREATE CLUSTERED COLUMNSTORE INDEX cci
    ON <tableName>
    WITH (ONLINE = ON);
  ```

  ```sql
  ALTER INDEX cci
    ON <tableName>
    REBUILD WITH (ONLINE = ON);
  ```

### <a name="always-encrypted-with-secure-enclaves-ctp-20"></a>具有安全記憶體保護區的 Always Encrypted (CTP 2.0)

在具有就地加密和豐富計算的 Always Encrypted 時展開。 在伺服器端的安全記憶體保護區內，擴充來自啟用純文字資料的計算。

密碼編譯作業包含資料行加密和資料行加密金鑰輪替。 現在可以使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 發出這些作業，而且它們不需要將該資料移出資料庫。 安全記憶體保護區將 Always Encrypted 提供給一組同時具有下列需求的更廣泛情節：  

- 讓高權限但未經授權的使用者 (包括資料庫管理員、系統管理員、雲端操作員或惡意程式碼) 無法存取敏感性資料的需求。
- 資料庫系統內支援對受保護資料進行豐富計算的需求。

如需詳細資料，請參閱[具有安全記憶體保護區的 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md)。

> [!NOTE]
> 只有在 Windows OS 上才能使用具有安全記憶體保護區的 Always Encrypted。

### <a name="intelligent-query-processing-ctp-20"></a>智慧查詢處理 (CTP 2.0)

- 藉由調整批次和資料列模式運算子的記憶體授與大小，以在 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 引進的記憶體授與意見反應功能上展開**資料列模式記憶體授與意見反應**。  針對記憶體授與過多的狀況，如果授與的記憶體超過實際使用記憶體大小的兩倍，記憶體授與回饋便會重新計算記憶體授與。 連續執行接著會要求較少的記憶體。 針對記憶體授與大小不足以致磁碟溢出，記憶體授與意見反應會觸發記憶體授與的重新計算。 連續執行接著會要求更多的記憶體。 根據預設，資料庫相容性層級 150 會啟用此功能。

- **近似 COUNT DISTINCT** 會傳回群組中唯一非 Null 值的近似數目。 此函式設計成用於巨量資料情節。 此函式最適合用於下列所有條件都成立的查詢：
   - 存取最少數百萬個資料列的資料集。
   - 彙總一或多個具有大量不同值的資料行。
   - 回應比絕對精確更為重要。
      - `APPROX_COUNT_DISTINCT` 會傳回通常位於 2% 準確答案內的結果。
      - 而且它會在準確答案所需的一小段時間傳回概略答案。

- **資料列存放區上的批次模式**不再需要資料行存放區索引以批次模式處理查詢。 批次模式可讓查詢運算子作用於一組資料列，而不是一次只有一個資料列。 根據預設，資料庫相容性層級 150 會啟用此功能。 下列所有條件都成立時，批次模式可改善存取資料列存放區資料表的查詢速度：
   - 此查詢使用分析運算子 (例如聯結或彙總運算子)。
   - 查詢包含 100,000 個以上的資料列。
   - 查詢是 CPU 繫結，而不是輸入/輸出資料繫結。
   - 建立和使用資料行存放區索引有下列其中一個缺點：
      - 會在查詢中新增太多的額外負荷。
      - 或者，不可行，因為您的應用程式相依於資料行存放區索引尚未支援的功能。

- **資料表變數延遲編譯**可針對參考資料表變數的查詢，提升計劃品質和整體效能。 在最佳化和初始編譯期間，此功能將會根據實際資料表變數的資料列計數，傳播基數估計值。  這個精確的資料列計數資訊將用於最佳化下游計劃作業。 根據預設，資料庫相容性層級 150 會啟用此功能。

若要使用智慧查詢處理功能，請設定資料庫 `COMPATIBILITY_LEVEL = 150`。

### <a id="programmability"></a> Java 語言可程式性延伸模組 (CTP 2.0)

- **Java 語言延伸模組 (預覽)**：使用 Java 語言延伸模組在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中執行 Java 程式碼。 在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 中，當您將 [機器學習服務 (資料庫內)] 功能新增至 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體時，會安裝此延伸模組。

### <a id="sqlgraph"></a> SQL Graph 功能

- **在圖表比對查詢中使用衍生資料表或檢視別名 (CTP 2.1)** SQL Server 2019 預覽上的圖表查詢，支援在 `MATCH` 語法中使用檢視和衍生資料表別名。 若要在 `MATCH` 中使用這些別名，檢視和衍生資料表必須是在節點集合或邊緣資料表集合上使用 `UNION ALL` 運算子建立。 節點或邊緣資料表上有可能會有，也有可能不會有篩選。 在 `MATCH` 查詢中使用衍生資料表和檢視別名的能力，對於您想要查詢圖形中兩個或多個實體之間的異質實體或異質連線的案例來說非常有用。

- **`MERGE` DML 中的比對支援 (CTP 2.0)** 可讓您在單一陳述式中指定圖形關聯性，而不必使用個別的 `INSERT`、`UPDATE` 或 `DELETE` 陳述式。 在 `MERGE` 陳述式中使用 `MATCH` 述詞，以合併節點或邊緣資料表中的目前圖形資料與新資料。 此功能會在邊緣資料表上啟用 `UPSERT` 情節。 使用者現在可以使用單一合併陳述式來插入新的邊緣或更新兩個節點之間的現有邊緣。

- **邊緣條件約束 (CTP 2.0)** 是針對 SQL Graph 中的邊緣資料表所引進。 邊緣資料表可以將任何節點連線至資料庫中的任何其他節點。 引進邊緣條件約束時，您現在可以對此行為套用一些限制。 新的 `CONNECTION` 條件約束可以用來指定將允許指定邊緣資料表連線至結構描述的節點類型。

### <a name="database-scoped-default-setting-for-online-and-resumable-ddl-operations--ctp-20"></a>線上和可繼續 DDL 作業的資料庫範圍預設設定 (CTP 2.0)

- **線上和可繼續 DDL 作業的資料庫範圍預設設定**允許資料庫層級 `ONLINE` 和 `RESUMABLE` 索引作業的預設行為設定，而不是針對每個個別索引 DDL 陳述式定義這些選項 (例如索引建立或重建)。

- 使用 `ELEVATE_ONLINE` 和 `ELEVATE_RESUMABLE` 資料庫範圍設定選項，設定這些預設值。 這兩個選項都會讓引擎自動將支援的作業提升為索引線上或可繼續執行。 您可以使用這些選項來啟用下列行為：

  - `FAIL_UNSUPPORTED` 選項允許線上或可繼續所有索引作業，並讓不支援線上或可繼續的索引作業失敗。
  - `WHEN_SUPPPORTED` 選項允許線上或可繼續支援的作業，並離線或不可繼續執行索引的不受支援作業。
  - 除非 DDL 陳述式中明確指定，否則 `OFF` 選項允許離線和不可繼續執行所有索引作業的目前行為。

若要覆寫預設設定，請在索引建立和重建命令中包含 `ONLINE` 或 `RESUMABLE` 選項。  

如果沒有此功能，您必須直接在索引 DDL 陳述式中指定線上和可繼續選項 (例如索引建立和重建)。

如需索引可繼續作業的詳細資訊，請參閱 [Resumable Online Index Create](https://azure.microsoft.com/blog/resumable-online-index-create-is-in-public-preview-for-azure-sql-db/) (可繼續的線上索引建立)。

### <a id="ha"></a>Always On 可用性群組 - 更多同步複本 (CTP 2.0)

- **最多五個同步複本**：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 會將同步複本數目上限增加為 5，從 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 中最多為 3。 您可以設定這個 5 個複本的群組在群組內具有自動容錯移轉。 有 1 個主要複本，再加上 4 個同步次要複本。

- **次要到主要複本連線重新導向**：可將用戶端應用程式連線導向至主要複本，而不論連接字串中指定的目標伺服器為何。 此功能允許在沒有接聽程式的情況下進行連線重新導向。 在下列情況下，使用次要到主要複本連線重新導向：

  - 叢集技術不提供接聽程式功能。
  - 重新導向變得複雜的多子網路設定。
  - 閱讀叢集類型為 `NONE` 的向外延展或災害復原情節。

如需詳細資料，請參閱[次要到主要複本讀取/寫入連線重新導向 (Always On 可用性群組)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md)。

### <a name="data-discovery-and-classification-ctp-20"></a>資料探索與分類 (CTP 2.0)

資料探索與分類提供 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 原生內建的進階功能。 分類和標記您最敏感的資料具有下列優點：
- 協助符合資料隱私權標準和法規合規性需求。
- 支援安全性情節，例如監視 (稽核)，以及警示敏感性資料的異常存取。
- 更輕鬆地識別敏感性資料在企業中的位置，讓系統管理員可以採取正確的步驟來保護資料庫。

如需詳細資訊，請參閱 [SQL 資料探索與分類](../relational-databases/security/sql-data-discovery-and-classification.md)。

也已經增強[稽核](../relational-databases/security/auditing/sql-server-audit-database-engine.md)，在稱為 `data_sensitivity_information` 的稽核記錄中包含新欄位，其中記錄查詢所傳回的實際資料敏感度分類 (標籤)。 如需詳細資料和範例，請參閱[新增敏感度分類](../t-sql/statements/add-sensitivity-classification-transact-sql.md)。

>[!NOTE]
>啟用稽核方式沒有任何變更。 有一個新欄位新增至稽核記錄 `data_sensitivity_information`，以記錄查詢所傳回的實際資料敏感度分類 (標籤)。 請參閱[稽核存取敏感性資料](https://docs.microsoft.com/azure/sql-database/sql-database-data-discovery-and-classification#subheading-3)。

### <a name="expanded-support-for-persistent-memory-devices-ctp-20"></a>持續性記憶體裝置的擴充支援 (CTP 2.0)

任何放在持續性記憶體裝置上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 檔案現在可在「已啟用」模式中操作。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會直接存取裝置，並使用有效率的 memcpy 作業來略過作業系統的儲存體堆疊。 此模式會改善效能，因為它允許這類裝置的低延遲輸入/輸出。
    - [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 檔案範例包含：
        - 資料庫檔案
        - 交易記錄檔
        - 記憶體內部 OLTP 檢查點檔案
    - 持續性記憶體也稱為儲存類別記憶體。
    - 在一些非 Microsoft 網站上，持續性記憶體偶而會非正式地稱為 *pmem*。

> [!NOTE]
> 在此預覽版本中，只有在 Linux 上才能在持續性記憶體裝置上啟用檔案。 自 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] 開始，Windows 上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 支援持續性記憶體裝置。

### <a name="hybrid-buffer-pool-ctp-21"></a>混合式緩衝集區 (CTP 2.1)

混合式緩衝集區是 SQL Server 資料庫的新功能，其中坐落在置於持續性記憶體 (PMEM) 裝置上之資料庫檔案上的資料庫頁面，會在必要時被直接存取。 由於 PMEM 裝置能為資料存取提供非常低的延遲，引擎便能放棄為緩衝集區之「乾淨頁面」區域中的資料製作複本，而可以直接在 PMEM 上存取該頁面。 存取是使用記憶體對應的 I/O 來執行，與啟用檔案的情況相同。 這可透過避免針對 DRAM 複製頁面，以及透過避免作業系統的 I/O 堆疊以存取持續性儲存體上的頁面來提供效能優勢。 此功能已於 Windows 及 Linux 上的 SQL Server 提供使用。

如需詳細資訊，請參閱[混合式緩衝集區](../database-engine/configure-windows/hybrid-buffer-pool.md)

### <a name="support-for-columnstore-statistics-in-dbcc-clonedatabase-ctp-20"></a>DBCC CLONEDATABASE 中資料行存放區統計資料的支援 (CTP 2.0)

`DBCC CLONEDATABASE` 會建立資料庫的僅限結構描述複本，其中包含為查詢效能問題進行疑難排解所需的所有項目，而不需要複製資料。  在舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，此命令不會複製準確疑難排解資料行存放區索引查詢所需的統計資料，而且需要手動步驟才能擷取這項資訊。 現在，在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 中，`DBCC CLONEDATABASE` 會自動擷取資料行存放區索引的統計資料 blob，因此不需要任何手動步驟。

### <a name="new-options-added-to-spestimatedatacompressionsavings-ctp-20"></a>新增至 sp_estimate_data_compression_savings 的新選項 (CTP 2.0)

`sp_estimate_data_compression_savings` 傳回所要求物件的目前大小，並針對所要求的壓縮狀態預估物件大小。  此程序目前支援三個選項：`NONE`、`ROW` 和 `PAGE`。 `COLUMNSTORE_ARCHIVE` 推出了兩個新選項：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 和 `COLUMNSTORE`。 如果在使用標準或封存資料行存放區壓縮的資料表上建立資料行存放區索引，則這些新選項可讓您估計節省的空間。

### <a id="ml"></a> SQL Server 機器學習服務容錯移轉叢集和磁碟分割型模型 (CTP 2.0)

- **資料分割型模型**：使用新增至 `sp_execute_external_script` 的參數，處理您資料每個資料分割的外部指令碼。 此功能支援訓練許多小型模型 (每個資料的資料分割一個模型)，而不是一個大型模型。

- **Windows Server 容錯移轉叢集**：在 Windows Server 容錯移轉叢集上設定機器學習服務的高可用性。

如需詳細資訊，請參閱 [SQL Server 機器學習服務的新功能](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)。

### <a name="lightweight-query-profiling-infrastructure-enabled-by-default-ctp-20"></a>預設已啟用的輕量型查詢分析基礎結構 (CTP 2.0)

輕量型查詢分析基礎結構 (LWP) 提供比標準分析機制更具效率的查詢效能資料。 根據預設，現在會啟用輕量型分析。 它已在 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1 中引進。 相較於標準查詢分析機制有最多 75% CPU 的額外負荷，輕量型查詢分析提供預期額外負荷為 2% CPU 的查詢執行統計資料收集機制。 在舊版中，根據預設，它為 OFF。 資料庫管理員可以使用[追蹤旗標 7412](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 來啟用它。 

如需輕量型分析的詳細資訊，請參閱[查詢分析基礎結構](../relational-databases/performance/query-profiling-infrastructure.md)。

### <a id="polybase"></a>新的 PolyBase 連接器

- **[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、Oracle、Teradata 和 MongoDB 的新連接器**：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 引進 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、Oracle、Teradata 和 MongoDB 的外部資料新連接器。

### <a name="new-sysdmdbpageinfo-system-function-returns-page-information-ctp-20"></a>新的 sys.dm_db_page_info 系統函數會傳回頁面資訊 (CTP 2.0)

`sys.dm_db_page_info(database_id, file_id, page_id, mode)` 傳回資料庫中頁面的資訊。 此函式會傳回包含頁面中標頭資訊的資料列，包含 `object_id`、`index_id` 和 `partition_id`。 在大部分情況下，有此函式就不需要使用 `DBCC PAGE`。  

為了簡化頁面相關等候的疑難排解，也已將稱為 page_resource 的新資料行新增至 `sys.dm_exec_requests` 和 `sys.sysprocesses`。 這個新的資料行可讓您透過另一個新的系統函數 `sys.fn_PageResCracker` 將 `sys.dm_db_page_info` 加入這些檢視表。 請參閱下列指令碼作為範例：

```sql
SELECT page_info.* 
FROM sys.dm_exec_requests AS d 
  CROSS APPLY sys.fn_PageResCracker(d.page_resource) AS r
  CROSS APPLY sys.dm_db_page_info(r.db_id, r.file_id, r.page_id,'DETAILED')
    AS page_info;
```

## <a id="sqllinux"></a> Linux 上的 SQL Server

- **複寫支援 (CTP 2.0)**：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 支援 Linux 上的 SQL Server 複寫。 具有 SQL Agent 的 Linux 虛擬機器可以是發行者、散發者或訂閱者。 

  建立下列類型的發行：
  - 異動
  - 快照式
  - 合併式

  設定複寫 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或使用[複寫預存程序](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

- **Microsoft Distributed Transaction Coordinator (MSDTC) 的支援 (CTP 2.0)**：Linux 上的 SQL Server 2019 支援 Microsoft Distributed Transaction Coordinator (MSDTC)。 如需詳細資料，請參閱[如何在 Linux 上設定 MSDTC](../linux/sql-server-linux-configure-msdtc.md)。

- **具有 Kubernetes 之 Docker 容器上的 Always On 可用性群組 (CTP 2.2)**：Kubernetes 可協調執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的容器，以提供一組具有 SQL Server Always On 可用性群組的高可用性資料庫。 Kubernetes 運算子會部署 StatefulSet，包括具有 **mssql-server 容器**和健康狀態監視的容器。

- **協力廠商 AD 提供者的 OpenLDAP 支援 (CTP 2.0)**：Linux 上的 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 支援 OpenLDAP，可讓協力廠商提供者加入 Active Directory。

- **Linux 上的機器學習 (CTP 2.0)**：Linux 現在支援 SQL Server 2019 機器學習服務 (資料庫內)。 支援包含 `sp_execute_external_script` 預存程序。 如需如何在 Linux 上安裝機器學習服務的指示，請參閱[在 Linux 上安裝 SQL Server 2019 機器學習服務 R 和 Python 支援](../linux/sql-server-linux-setup-machine-learning.md)。

- **新容器登錄 (CTP 2.1)**：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 和 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的所有容器映像現在都位於 Microsoft 容器登錄中。 Microsoft 容器登錄是散發 Microsoft 產品容器的官方容器登錄。 此外，現在已發佈認證的 RHEL 型映像。

  - Microsoft 容器登錄：`mcr.microsoft.com/mssql/server:vNext-CTP2.0`
  - 認證的 RHEL 型容器映像：`mcr.microsoft.com/mssql/rhel/server:vNext-CTP2.0`

## <a id="mds"></a> Master Data Services (CTP 2.0) 

- **Silverlight 控制項已取代為 HTML**：Master Data Services (MDS) 入口網站已不再相依於 Silverlight。 所有先前的 Silverlight 元件已取代為 HTML 控制項。

## <a id="security"></a>安全性 (CTP 2.0)

- **SQL Server 組態管理員中的憑證管理**：SSL/TLS 憑證普遍用來保護 SQL Server 執行個體的存取。 憑證管理現在整合至 SQL Server 組態管理員，並簡化一般工作，例如：

  - 檢視和驗證 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體中所安裝的憑證。 
  - 檢視即將到期的憑證。
  - 將憑證部署到參與 Always On 可用性群組的電腦 (從保留主要複本的節點)。
  - 將憑證部署到參與容錯移轉叢集執行個體的電腦 (從使用中節點)。

  > [!NOTE]
  > 使用者必須具有所有叢集節點的管理員權限。

## <a id="tools"></a>工具

- [**Azure Data Studio**](../azure-data-studio/what-is.md)：先前以 SQL Operations Studio 預覽名稱發行，Azure Data Studio 是輕量級、現代化、開放原始碼且跨平台的桌面工具，適用於資料開發和管理中的最常見工作。 使用 Azure Data Studio，您可以在 Windows、macOS 和 Linux 的內部部署上和雲端中連線至 SQL Server。 Azure Data Studio 可讓您：

  - 更新至 [SQL Server 2019 (預覽) 延伸模組](../azure-data-studio/sql-server-2019-extension.md)。 (CTP 2.1)
  - 在具有快速 Intellisense、程式碼片段和原始檔控制整合的新式開發環境中編輯和執行查詢。 (CTP 2.0) 
  - 使用內建結果集圖表，將資料快速視覺化。 (CTP 2.0)
  - 使用可自訂的小工具建立伺服器和資料庫的自訂儀表板。 (CTP 2.0)  
  - 輕鬆地管理更廣泛使用具有內建終端機的環境。 (CTP 2.0)
  - 分析建置在 Jupyter 上整合式筆記型體驗中的資料。 (CTP 2.0)
  - 使用自訂佈景主題和延伸模組來增強您的體驗。(CTP 2.0)
  - 以及使用內建訂用帳戶和資源瀏覽器來探索 Azure 資源。 (CTP 2.0)
  - 支援使用 SQL Server 巨量資料叢集的案例。 (CTP 2.0)

- [**SQL Server Management Studio (SSMS) 18.0 (預覽)**](../ssms/sql-server-management-studio-ssms.md)

  - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 支援。 (CTP 2.0)
  - 具有安全記憶體保護區的 Always Encrypted 支援。 (CTP 2.0)
  - 較小的下載大小。 (CTP 2.0)
  - 現在根據 Visual Studio 2017 Isolated Shell。 (CTP 2.0)
  - 如需完整清單，請參閱 [SSMS 變更記錄](../ssms/sql-server-management-studio-changelog-ssms.md)。 (CTP 2.0)

## <a name="other-services"></a>其他服務

自 CTP 2.2 開始，[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 不會針對下列服務推出新功能：

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Analysis Services (SSAS)
- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS)
- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS)

## <a name="next-steps"></a>後續步驟

- [SQL Server 2019 版本資訊](sql-server-ver15-release-notes.md)

- [Microsoft SQL Server 2019:Technical white paper](https://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />在 2018 年 9 月發佈。 適用於 Microsoft SQL Server 2019 CTP 2.0 for Windows、Linux 和 Docker 容器。


[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
