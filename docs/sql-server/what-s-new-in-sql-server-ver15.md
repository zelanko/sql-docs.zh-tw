---
title: SQL Server 2019 的新功能 | Microsoft Docs
ms.custom: ''
ms.date: 09/26/2018
ms.prod: sql-server-2018
ms.reviewer: ''
ms.technology:
- server-general
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 68a872164528bec49b0342f603107fb86e31fe50
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47678266"
---
# <a name="whats-new-in-sql-server-2019"></a>SQL Server 2019 的新功能

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sql-server-2019](..\includes\sssqlv15-md.md)] 是以舊版本為基礎，可讓 SQL Server 成長為平台，以供您選擇開發語言、資料類型、內部部署或雲端以及作業系統。 本文摘要說明 SQL Server 2019 的新功能。 如需詳細資訊和已知問題，請參閱 [SQL Server 2019 版本資訊](sql-server-ver15-release-notes.md)。

**試用 SQL Server 2019！**
- [![從評估中心下載](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=862101) [下載 SQL Server 2019 以安裝於 Windows](http://go.microsoft.com/fwlink/?LinkID=862101)
- 安裝於 Linux for [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md)、[SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) 和 [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)。
- [在 Docker 的 SQL Server 2019 上執行](../linux/quickstart-install-connect-docker.md)。

## <a name="ctp-20"></a>CTP 2.0 

Community Technology Preview (CTP) 2.0 是第一個 [!INCLUDE[sql-server-2019](..\includes\sssqlv15-md.md)] 公用版本。 下列是針對 [!INCLUDE[sql-server-2019](..\includes\sssqlv15-md.md)] CTP 2.0 所新增或強化的功能。

- [巨量資料叢集](#bigdatacluster)
  - 在 Kubernetes 上部署具有 SQL 和 Spark Linux 容器的巨量資料叢集
  - 從 HDFS 中存取巨量資料
  - 使用 Spark 執行進階分析和機器學習
  - 使用 Spark 串流將資料串流至 SQL 資料集區
  - 使用 Azure Data Studio 來執行可提供筆記型體驗的查詢活頁簿

- [資料庫引擎](#databaseengine)
  - UTF-8 支援
  - 可繼續的線上索引建立允許索引建立在中斷後繼續
  - 叢集資料行存放區線上索引建置和重建
  - 具有安全記憶體保護區的 Always Encrypted
  - 智慧查詢處理
  - Java 語言可程式性延伸模組
  - SQL Graph 功能
  - 線上和可繼續 DDL 作業的資料庫範圍組態設定
  - Always On 可用性群組 - 次要複本連線重新導向
  - 資料探索和分類 - 原生內建 SQL Server
  - 持續性記憶體裝置的擴充支援
  - `DBCC CLONEDATABASE` 中資料行存放區統計資料的支援
  - 新增至 `sp_estimate_data_compression_savings` 的新選項
  - SQL Server 機器學習服務容錯移轉叢集
  - 預設已啟用的輕量型查詢分析基礎結構
  - 新的 Polybase 連接器
  - 新的 `sys.dm_db_page_info` 系統函數會傳回頁面資訊

- [Linux 上的 SQL Server](#sqllinux)
  - 複寫支援
  - Microsoft Distributed Transaction Coordinator (MSDTC) 支援
  - 具有 Kubernetes 之 Docker 容器上的 Always On 可用性群組
  - 第三方 AD 提供者的 OpenLDAP 支援
  - Linux 上的機器學習
  - 新的容器登錄
  - 新的 RHEL 型容器映像
  - 記憶體不足的壓力通知

- [Master Data Services](#mds)
  - 已取代 Silverlight 控制項

- [Security](#security)
  - SQL Server 組態管理員中的憑證管理

- [工具](#tools)
  - SQL Server Management Studio (SSMS) 18.0 (預覽)
  - Azure Data Studio

如需這些功能的詳細資料，請繼續閱讀。

## <a id="bigdatacluster"></a>巨量資料叢集

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] [巨量資料叢集](../big-data-cluster/big-data-cluster-overview.md)會啟用新的情節，包括下列：

- 在 Kubernetes 上部署具有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和 Spark Linux 容器的巨量資料叢集
- 從 HDFS 中存取巨量資料
- 使用 Spark 執行進階分析和機器學習
- 使用 Spark 串流將資料串流至 SQL 資料集區
- 在 [**Azure Data Studio**](../sql-operations-studio/what-is.md) 中執行可提供筆記型體驗的查詢活頁簿。
  
[!INCLUDE [Big Data Clusters preview](../includes/big-data-cluster-preview-note.md)]

## <a id="databaseengine"></a> 資料庫引擎

CTP 2.0 引進或增強下列 [!INCLUDE[ssdeNoVersion](../includes/ssdenoversion_md.md)] 新功能。

### <a name="database-compatibility-level"></a>資料庫相容性層級

新增資料庫 **COMPATIBILITY_LEVEL 150**。 若要針對特定使用者資料庫啟用，請執行：

   ```sql
   ALTER DATABASE database_name SET COMPATIBILITY_LEVEL =  150;
   ```

### <a name="utf-8-support"></a>UTF-8 支援

完整支援廣泛使用 UTF-8 字元編碼作為匯入或匯出編碼，或作為文字資料的資料庫層級或資料行層級定序。 UTF-8 允許用於 `CHAR` 和 `VARCHAR` 資料類型，並且在建立物件定序或將其變更為具有 `UTF8` 尾碼的定序時啟用。 

例如，`LATIN1_GENERAL_100_CI_AS_SC` 至 `LATIN1_GENERAL_100_CI_AS_SC_UTF8`。 UTF-8 僅適用於支援增補字元 (在 SQL Server 2012 中引進) 的 Windows 定序。 `NCHAR` 和 `NVARCHAR` 只允許 UTF-16 編碼，並維持不變。

此功能可能會節省大量儲存空間 (視使用的字元集而定)。 例如，使用啟用 UTF-8 的定序，將具有 ASCII 字串的現有資料行資料類型從 `NCHAR(10)` 變更為 `CHAR(10)` 會翻譯為接近減少儲存體需求的 50%。 這項減少的原因是 `NCHAR(10)` 需要 22 個位元組作為儲存空間，而 `CHAR(10)` 針對相同的 Unicode 字串需要 12 個位元組。

### <a name="resumable-online-index-create"></a>可繼續的線上索引建立

- **可繼續的線上索引建立**允許索引建立作業暫停並稍後可從作業暫停或失敗處繼續，而不是從頭重新啟動。

  可繼續的線上索引建立支援下列情節：
  - 在索引建立失敗之後繼續索引建立作業；例如，在資料庫容錯移轉之後或磁碟空間不足之後。
  - 暫停進行中索引建立作業，並稍後繼續視需要允許暫時釋放系統資源，然後稍後繼續此作業。
  - 建立大型索引，而不需要使用最多記錄空間，以及封鎖其他維護活動並允許截斷記錄的長時間執行交易。

  如果索引建立失敗，則沒有此功能，必須重新執行線上索引建立作業，而且必須從頭重新啟動作業。

使用此版本，我們會擴充可繼續的功能，以將此功能新增至可用的[可繼續線上索引重建](http://azure.microsoft.com/blog/modernize-index-maintenance-with-resumable-online-index-rebuild/)。

此外，可以使用[線上和可繼續 DDL 作業的資料庫範圍預設設定](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)將此功能設定為特定資料庫的預設值。

如需詳細資訊，請參閱[可繼續的線上索引建立](../t-sql/statements/create-index-transact-sql.md#resumable-indexes)。

### <a name="build-and-rebuild-clustered-columnstore-indexes-online"></a>線上建置和重建叢集資料行存放區索引

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

### <a name="always-encrypted-with-secure-enclaves"></a>具有安全記憶體保護區的 Always Encrypted

在具有就地加密和豐富計算的 Always Encrypted 時展開。 在伺服器端的安全記憶體保護區內，擴充來自啟用純文字資料的計算。

密碼編譯作業包含資料行加密和資料行加密金鑰輪替。 現在可以使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 發出這些作業，而且它們不需要將該資料移出資料庫。 安全記憶體保護區將 Always Encrypted 提供給一組同時具有下列需求的更廣泛情節：  

- 讓高權限但未經授權的使用者 (包含資料庫管理員、系統管理員、雲端操作員或惡意程式碼) 無法存取敏感性資料的需求。
- 資料庫系統內支援對受保護資料進行豐富計算的需求。

如需詳細資料，請參閱[具有安全記憶體保護區的 Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md)。

> [!NOTE]
> 只有在 Windows OS 上才能使用具有安全記憶體保護區的 Always Encrypted。

### <a name="intelligent-query-processing"></a>智慧查詢處理

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

### <a id="programmability"></a> Java 語言可程式性延伸模組

- **Java 語言延伸模組 (預覽)**：使用 Java 語言延伸模組，在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中執行 Java 程式碼。 在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 中，當您將「機器學習服務 (資料庫內)」功能新增至 SQL Server 執行個體時，會安裝此延伸模組。

### <a id="sqlgraph"></a> SQL Graph 功能

- **`MERGE` DML 中的比對支援**可讓您在單一陳述式中指定圖形關聯性，而不是個別 `INSERT`、`UPDATE` 或 `DELETE` 陳述式。 在 `MERGE` 陳述式中使用 `MATCH` 述詞，以合併節點或邊緣資料表中的目前圖形資料與新資料。 此功能會在邊緣資料表上啟用 `UPSERT` 情節。 使用者現在可以使用單一合併陳述式來插入新的邊緣或更新兩個節點之間的現有邊緣。

- **邊緣條件約束**是針對 SQL Graph 中的邊緣資料表所引進。 邊緣資料表可以將任何節點連線至資料庫中的任何其他節點。 引進邊緣條件約束時，您現在可以對此行為套用一些限制。 新的 `CONNECTION` 條件約束可以用來指定將允許指定邊緣資料表連線至結構描述的節點類型。

### <a name="database-scoped-default-setting-for-online-and-resumable-ddl-operations"></a>線上和可繼續 DDL 作業的資料庫範圍預設設定 

- **線上和可繼續 DDL 作業的資料庫範圍預設設定**允許資料庫層級 `ONLINE` 和 `RESUMABLE` 索引作業的預設行為設定，而不是針對每個個別索引 DDL 陳述式定義這些選項 (例如索引建立或重建)。

- 使用 `ELEVATE_ONLINE` 和 `ELEVATE_RESUMABLE` 資料庫範圍設定選項，設定這些預設值。 這兩個選項都會讓引擎自動將支援的作業提升為索引線上或可繼續執行。 您可以使用這些選項來啟用下列行為：

  - `FAIL_UNSUPPORTED` 選項允許線上或可繼續所有索引作業，並讓不支援線上或可繼續的索引作業失敗。
  - `WHEN_SUPPPORTED` 選項允許線上或可繼續支援的作業，並離線或不可繼續執行索引的不受支援作業。
  - 除非 DDL 陳述式中明確指定，否則 `OFF` 選項允許離線和不可繼續執行所有索引作業的目前行為。

若要覆寫預設設定，請在索引建立和重建命令中包含 ONLINE 或 RESUMABLE 選項。  

如果沒有此功能，您必須直接在索引 DDL 陳述式中指定線上和可繼續選項 (例如索引建立和重建)。

詳細資訊：如需索引可繼續作業的詳細資訊，請參閱[可繼續的線上索引建立](http://azure.microsoft.com/blog/resumable-online-index-create-is-in-public-preview-for-azure-sql-db/)。

### <a id="ha"></a>Always On 可用性群組 - 更多同步複本 

- **最多五個同步複本**：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 會將同步複本數目上限增加為 5，從 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 中最多為 3。 您可以設定這個 5 個複本的群組在群組內具有自動容錯移轉。 有 1 個主要複本，再加上 4 個同步次要複本。

- **次要到主要複本連線重新導向**：允許將用戶端應用程式連線導向至主要複本，而不論連接字串中指定的目標伺服器為何。 此功能允許在沒有接聽程式的情況下進行連線重新導向。 在下列情況下，使用次要到主要複本連線重新導向：

  - 叢集技術不提供接聽程式功能。
  - 重新導向變得複雜的多子網路設定。
  - 閱讀叢集類型為 `NONE` 的向外延展或災害復原情節。

如需詳細資料，請參閱[次要到主要複本讀取/寫入連線重新導向 (Always On 可用性群組)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md)。

### <a name="data-discovery-and-classification"></a>資料探索與分類

資料探索與分類提供 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 原生內建的進階功能。 分類和標記您最敏感的資料具有下列優點：
- 協助符合資料隱私權標準和法規合規性需求。
- 支援安全性情節，例如監視 (稽核)，以及警示敏感性資料的異常存取。
- 更輕鬆地識別敏感性資料在企業中的位置，讓系統管理員可以採取正確的步驟來保護資料庫。

如需詳細資訊，請參閱 [SQL 資料探索與分類](../relational-databases/security/sql-data-discovery-and-classification.md)。

也已經增強[稽核](../relational-databases/security/auditing/sql-server-audit-database-engine.md)，在稱為 `data_sensitivity_information` 的稽核記錄中包含新欄位，其中記錄查詢所傳回的實際資料敏感度分類 (標籤)。 如需詳細資料和範例，請參閱[新增敏感度分類](../t-sql/statements/add-sensitivity-classification-transact-sql.md)。

>[!NOTE]
>啟用稽核方式沒有任何變更。 有一個新欄位新增至稽核記錄 `data_sensitivity_information`，以記錄查詢所傳回的實際資料敏感度分類 (標籤)。 請參閱[稽核存取敏感性資料](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-data-discovery-and-classification#subheading-3)。

### <a name="expanded-support-for-persistent-memory-devices"></a>持續性記憶體裝置的擴充支援

任何放在持續性記憶體裝置上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 檔案現在可在「已啟用」模式中操作。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會直接存取裝置，並使用有效率的 memcpy 作業來略過作業系統的儲存體堆疊。 此模式會改善效能，因為它允許這類裝置的低延遲輸入/輸出。
    - [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 檔案範例包含：
        - 資料庫檔案
        - 交易記錄檔
        - 記憶體內部 OLTP 檢查點檔案
    - 持續性記憶體也稱為儲存類別記憶體。
    - 在一些非 Microsoft 網站上，持續性記憶體偶而會非正式地稱為 *pmem*。

> [!NOTE]
> 在此預覽版本中，只有在 Linux 上才能在持續性記憶體裝置上啟用檔案。 從 SQL Server 2016 開始，Windows 上的 SQL Server 支援持續性記憶體裝置。

### <a name="support-for-columnstore-statistics-in-dbcc-clonedatabase"></a>DBCC CLONEDATABASE 中資料行存放區統計資料的支援

`DBCC CLONEDATABASE` 會建立資料庫的僅限結構描述複本，其中包含為查詢效能問題進行疑難排解所需的所有項目，而不需要複製資料。  在舊版 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中，此命令不會複製準確疑難排解資料行存放區索引查詢所需的統計資料，而且需要手動步驟才能擷取這項資訊。 現在，在 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 中，DBCC CLONEDATABASE 會自動擷取資料行存放區索引的統計資料 Blob，因此不需要任何手動步驟。

### <a name="new-options-added-to-spestimatedatacompressionsavings"></a>新增至 sp_estimate_data_compression_savings 的新選項

`sp_estimate_data_compression_savings` 傳回所要求物件的目前大小，並針對所要求的壓縮狀態預估物件大小。  此程序目前支援三個選項：`NONE`、`ROW` 和 `PAGE`。 SQL Server 2019 引進兩個新選項：`COLUMNSTORE` 和 `COLUMNSTORE_ARCHIVE`。 如果在使用標準或封存資料行存放區壓縮的資料表上建立資料行存放區索引，則這些新選項可讓您估計節省的空間。

### <a id="ml"></a> SQL Server 機器學習服務容錯移轉叢集和磁碟分割型模型

- **資料分割型模型**：使用新增至 `sp_execute_external_script` 的新參數，處理您資料每個資料分割的外部指令碼。 此功能支援訓練許多小型模型 (每個資料的資料分割一個模型)，而不是一個大型模型。

- **Windows Server 容錯移轉叢集**：設定 Windows Server 容錯移轉叢集上機器學習服務的高可用性。

如需詳細資訊，請參閱 [SQL Server 機器學習服務的新功能](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md)。

### <a name="lightweight-query-profiling-infrastructure-enabled-by-default"></a>預設已啟用的輕量型查詢分析基礎結構

輕量型查詢分析基礎結構 (LWP) 所提供的查詢效能資料比標準分析技術更具效率。 根據預設，現在會啟用輕量型分析。 它已在 [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1 中引進。 相較於標準查詢分析機制有最多 75% CPU 的額外負荷，輕量型查詢分析提供預期額外負荷為 2% CPU 的查詢執行統計資料收集機制。 在舊版中，根據預設，它為 OFF。 資料庫管理員可以使用[追蹤旗標 7412](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) 來啟用它。 

如需輕量型分析的詳細資訊，請參閱 [Developers Choice: Query progress – anytime, anywhere](http://blogs.msdn.microsoft.com/sql_server_team/query-progress-anytime-anywhere/) (開發人員選擇：隨時隨地查詢進度)。

### <a id="polybase"></a>新的 Polybase 連接器

- **[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、Oracle、Teradata 和 MongoDB 的新連接器**：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 引進 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、Oracle、Teradata 和 MongoDB 的外部資料新連接器。

### <a name="new-sysdmdbpageinfo-system-function-returns-page-information"></a>新的 sys.dm_db_page_info 系統函數會傳回頁面資訊

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

- **複寫支援**：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 支援 Linux 上的 SQL Server 複寫。 具有 SQL Agent 的 Linux 虛擬機器可以是發行者、散發者或訂閱者。 

  建立下列類型的發行：
  - 異動
  - 快照式
  - 合併式

  設定複寫 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或使用[複寫預存程序](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)。

- **Microsoft Distributed Transaction Coordinator (MSDTC) 支援**：Linux 上的 SQL Server 2019 支援 Microsoft Distributed Transaction Coordinator (MSDTC)。 如需詳細資料，請參閱[如何在 Linux 上設定 MSDTC](../linux/sql-server-linux-configure-msdtc.md)。

- **具有 Kubernetes 之 Docker 容器上的 Always On 可用性群組**：Kubernetes 可以協調執行 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體的容器，以提供一組具有 SQL Server Always On 可用性群組的高可用性資料庫。 Kubernetes 運算子會部署 StatefulSet，包括具有 **mssql-server 容器**和健康狀態監視的容器。

- **第三方 AD 提供者的 OpenLDAP 支援**：Linux 上的 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 支援 OpenLDAP，以允許第三方提供者加入 Active Directory。

- **Linux 上的機器學習**：Linux 上現在支援 SQL Server 2019 機器學習服務 (資料庫內)。 支援包含 `sp_execute_external_script` 預存程序。 如需如何在 Linux 上安裝機器學習服務的指示，請參閱[在 Linux 上安裝 SQL Server 2019 機器學習服務 R 和 Python 支援](../linux/sql-server-linux-setup-machine-learning.md)。

- **新的容器登錄**：[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 和 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] 的所有容器映像現在都位於 Microsoft 容器登錄。 Microsoft 容器登錄是散發 Microsoft 產品容器的官方容器登錄。 此外，現在已發佈認證的 RHEL 型映像。

  - Microsoft 容器登錄：`mcr.microsoft.com/mssql/server:vNext-CTP2.0`
  - 認證的 RHEL 型容器映像：`mcr.microsoft.com/mssql/rhel/server:vNext-CTP2.0`

## <a id="mds"></a> Master Data Services (MDS)

- **已取代為 HTML 的 Silverlight 控制項**：Master Data Services (MDS) 入口網站不再相依於 Silverlight。 所有先前的 Silverlight 元件已取代為 HTML 控制項。

## <a id="security"></a>安全性

- **SQL Server 組態管理員中的憑證管理**：SSL/TLS 憑證廣泛用來保護 SQL Server 執行個體的存取。 憑證管理現在整合至 SQL Server 組態管理員，並簡化一般工作，例如：

  - 檢視和驗證 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行個體中所安裝的憑證。 
  - 檢視即將到期的憑證。
  - 將憑證部署到參與 Always On 可用性群組的電腦 (從保留主要複本的節點)。
  - 將憑證部署到參與容錯移轉叢集執行個體的電腦 (從使用中節點)。

  > [!NOTE]
  > 使用者必須具有所有叢集節點的管理員權限。

## <a id="tools"></a>工具

- [**Azure Data Studio**](../azure-data-studio/what-is.md)：先前以 SQL Operations Studio 預覽名稱發行，Azure Data Studio 是輕量級、現代化、開放原始碼且跨平台的桌面工具，適用於資料開發和管理中的最常見工作。 使用 Azure Data Studio，您可以在 Windows、macOS 和 Linux 的內部部署上和雲端中連線至 SQL Server。 Azure Data Studio 可讓您：

  - 在具有快速 Intellisense、程式碼片段和原始檔控制整合的新式開發環境中編輯和執行查詢。  
  - 使用內建結果集圖表，將資料快速視覺化。  
  - 使用可自訂的小工具建立伺服器和資料庫的自訂儀表板。  
  - 輕鬆地管理更廣泛使用具有內建終端機的環境。  
  - 分析建置在 Jupyter 上整合式筆記型體驗中的資料。  
  - 使用自訂佈景主題和延伸模組來增強您的體驗。  
  - 以及使用內建訂用帳戶和資源瀏覽器來探索 Azure 資源。
  - 支援使用 SQL Server 巨量資料叢集的情節。


- [**SQL Server Management Studio (SSMS) 18.0 (預覽)**](../ssms/sql-server-management-studio-ssms.md)

  - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] 支援。
  - 具有安全記憶體保護區的 Always Encrypted 支援。
  - 較小的下載大小。
  - 現在根據 Visual Studio 2017 Isolated Shell。
  - 如需完整清單，請參閱 [SSMS 變更記錄](../ssms/sql-server-management-studio-changelog-ssms.md)。

## <a name="other-services"></a>其他服務

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0 未引進下列服務的新功能：

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Analysis Services (SSAS)
- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS)
- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (SSRS)

## <a name="next-steps"></a>後續步驟

- [SQL Server 2019 版本資訊](sql-server-ver15-release-notes.md)

- [Microsoft SQL Server 2019：技術白皮書](https://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />在 2018 年 9 月發佈。 適用於 Microsoft SQL Server 2019 CTP 2.0 for Windows、Linux 和 Docker 容器。


[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
