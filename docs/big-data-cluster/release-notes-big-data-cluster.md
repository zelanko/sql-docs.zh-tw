---
title: 版本資訊
titleSuffix: SQL Server big data clusters
description: 本文說明 SQL Server 2019 big data 叢集 (預覽) 的最新更新和已知問題。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c0dd96d4a3227fda76921764429b4566e3e5dd28
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419311"
---
# <a name="release-notes-for-big-data-clusters-on-sql-server"></a>SQL Server 上 big data 叢集的版本資訊

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文列出最新版本 SQL Server big data 叢集的更新和已知問題。

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a id="ctp32"></a>CTP 3.2 (7 月)

下列各節說明 SQL Server 2019 CTP 3.2 中 big data 叢集的新功能和已知問題。

|新功能或更新 | 詳細資料 |
|:---|:---|
|公開預覽 |在 CTP 3.2 之前, 已註冊的早期採用者可以使用 SQL Server big data cluster。 此版本可讓任何人都能體驗 SQL Server Big data 叢集的功能。 <br/><br/> 請參閱[開始使用 SQL Server big data](deploy-get-started.md)叢集。|
|`azdata` |CTP 3.2 引進`azdata`了一種以 Python 撰寫的命令列公用程式, 可讓叢集系統管理員透過 REST api 啟動和管理 big data cluster。 `azdata`取代`mssqlctl`。 請[參閱`azdata`Install ](deploy-install-azdata.md)。 |
|PolyBase |外部資料表資料行名稱現在是用來查詢 SQL Server、Oracle、Teradata、MongoDB 和 ODBC 資料來源。 |
|HDFS 分層重新整理 |簡介 HDFS 階層處理的重新整理功能, 可針對遠端資料的最新快照集重新整理現有的掛接。 查看[HDFS 分層](hdfs-tiering.md) |
|以筆記本為基礎的疑難排解 |CTP 3.2 引進 Jupyter 的筆記本, 協助您針對 SQL Server big data 叢集中的元件進行[部署](deploy-notebooks.md)和[探索、診斷和疑難排解](manage-notebooks.md)。 |
| &nbsp; | &nbsp; |

## <a id="ctp31"></a>CTP 3.1 (六月)

下列各節說明 SQL Server 2019 CTP 3.1 中 big data 叢集的新功能和已知問題。

|新功能或更新 | 詳細資料 |
|:---|:---|
|公開預覽 |在 CTP 3.2 之前, 已註冊的早期採用者可以使用 SQL Server big data cluster。 此版本可讓任何人都能體驗 SQL Server Big data 叢集的功能。 <br/><br/> 請參閱[開始使用 SQL Server big data](deploy-get-started.md)叢集。|
|以筆記本為基礎的疑難排解。|CTP 3.2 引進 Jupyter 的筆記本, 協助您進行[部署](deploy-notebooks.md), 以及[探索、診斷和疑難排解](manage-notebooks.md)SQL Server big data cluster 中的元件。 |
|`azdata` |CTP 3.2 引進`azdata`了一種以 Python 撰寫的命令列公用程式, 可讓叢集系統管理員透過 REST api 啟動和管理 big data cluster。 `azdata`取代`mssqlctl`。 請[參閱`azdata`Install ](deploy-install-azdata.md)。 |
|HDFS 分層重新整理 |簡介 HDFS 階層處理的重新整理功能, 可針對遠端資料的最新快照集重新整理現有的掛接。 查看[HDFS 分層](hdfs-tiering.md) |
| &nbsp; | &nbsp; |

### <a name="whats-new"></a>新功能

| 新功能或更新 | 詳細資料 |
|:---|:---|
| `mssqlctl` 命令變更 | `mssqlctl cluster` 命令已重新命名為 `mssqlctl bdc`。 如需詳細資訊，請參閱 [`mssqlctl` 參考](reference-azdata.md)。 |
| 新`mssqlctl`的狀態命令和移除叢集系統管理入口網站。 | 此版本中已移除叢集系統管理入口網站。 已將新的狀態命令新增`mssqlctl`至, 以補充現有的監視命令。 |
| Spark 計算集區 | 可建立額外的節點，提升 Spark 的計算能力，而無須相應增加儲存體。 此外，您可以啟動不會用於 Spark 的儲存體集區節點。 Spark 與儲存體彼此分離。 如需詳細資訊，請參閱 [Configure SQL Server Agent](deployment-custom-configuration.md#sparkstorage)。 |
| MSSQL Spark 連接器 | 可對資料集區外部資料表提供讀寫支援。 先前的版本只支援對 MASTER 執行個體資料表進行讀寫。 如需詳細資訊，請參閱 [How to read and write to SQL Server from Spark using the MSSQL Spark Connector](spark-mssql-connector.md)。 |
| 使用 MLeap 的機器學習 | [可在 Spark 中訓練 MLeap 機器學習模型，並使用 Java 語言延伸模組在 SQL Server 中評分](spark-create-machine-learning-model.md)。 |

### <a name="known-issues"></a>已知問題

下列各節說明此版本的已知問題和限制。

#### <a name="hdfs"></a>HDFS

- 如果您以滑鼠右鍵按一下 HDFS 中的檔案來預覽它, 您可能會看到下列錯誤:

   `Error previewing file: File exceeds max size of 30MB`

   目前沒有任何方法可以在 Azure Data Studio 中預覽大於 30 MB 的檔案。

- 不支援對 hdfs-site.xml 進行變更之 HDFS 的設定變更。

#### <a name="deployment"></a>部署

- 不支援從舊版本升級 big data 資料叢集。

   > [!IMPORTANT]
   > 您必須先備份資料, 然後刪除現有的 big data 叢集 (使用舊版的**azdata**), 然後再部署最新版本。 如需詳細資訊, 請參閱[升級至新版本](deployment-upgrade.md)。

- 在 AKS 上部署之後, 您可能會看到來自部署的下列兩個警告事件。 這兩個事件都是已知的問題, 但不會讓您無法在 AKS 上成功部署 big data cluster。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果 big data cluster 部署失敗, 則不會移除相關聯的命名空間。 這可能會導致叢集上有孤立的命名空間。 因應措施是在部署具有相同名稱的叢集之前, 手動刪除命名空間。

#### <a name="external-tables"></a>外部資料表

- Big data cluster 部署不再建立**SqlDataPool**和**SqlStoragePool**外部資料源。 您可以手動建立這些資料來源, 以支援資料集區和存放集區的資料虛擬化。

   > [!NOTE]
   > 建立這些外部資料源的 URI 在 Ctp 之間不同。 請參閱下列 Transact-sql 命令, 以瞭解如何建立它們 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- 您可以為具有不支援之資料行類型的資料表建立資料集區外部資料表。 如果您查詢外部資料表, 您會收到類似下列的訊息:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果您查詢存放集區外部資料表, 當基礎檔案同時複製到 HDFS 時, 您可能會收到錯誤。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 如果您要為使用字元資料類型的 Oracle 建立外部資料表, Azure Data Studio virtualization wizard 會在外部資料表定義中, 將這些資料行轉譯為 VARCHAR。 這會導致外部資料表 DDL 失敗。 請修改 Oracle 架構, 以使用 NVARCHAR2 類型, 或手動建立外部資料表語句並指定 NVARCHAR, 而不是使用 wizard。

#### <a name="application-deployment"></a>應用程式部署

- 從 RESTful API 呼叫 R、Python 或 MLeap 應用程式時, 呼叫會在5分鐘內超時。

#### <a name="spark-and-notebooks"></a>Spark 和筆記本

- POD 重新開機時, Kubernetes 環境中的 POD IP 位址可能會變更。 在主要 pod 重新開機的案例中, Spark 會話可能會失敗並出現`NoRoteToHostException`。 這是由不會以新的 IP 位址重新整理的 JVM 快取所造成。

- 如果您已在 Windows 上安裝 Jupyter 和個別的 Python, Spark 筆記本可能會失敗。 若要解決此問題, 請將 Jupyter 升級至最新版本。

- 在筆記本中, 如果您按一下 [**加入文字**] 命令, 文字資料格就會以預覽模式加入, 而不是編輯模式。 您可以按一下 [預覽] 圖示來切換至編輯模式, 並編輯資料格。

#### <a name="security"></a>安全性

- SA_PASSWORD 是環境的一部分, 而且可探索 (例如, 在纜線傾印檔案中)。 部署之後, 您必須在主要實例上重設 SA_PASSWORD。 這不是一個 bug, 而是一個安全性步驟。 如需如何在 Linux 容器中變更 SA_PASSWORD 的詳細資訊, 請參閱[變更 SA 密碼](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 記錄可能包含適用于 big data cluster 部署的 SA 密碼。

#### <a name="kibana-logs-dashboards"></a>Kibana 記錄儀表板

- 在 Aris CTP 3.0 和3.1 之間, Kibana 版本已從6.3.1 升級至7.0.1 版。  這會使 Edge 瀏覽器與 Kibana 不相容。 在 Edge 中載入目前版本的 Kibana 儀表板時, 使用者會看到空白頁面。 如需 Kibana.rs 支援的瀏覽器, 請參閱[這裡]( https://www.elastic.co/support/matrix#matrix_browse) 


## <a id="ctp30"></a>CTP 3.0 (可能)

下列各節說明 SQL Server 2019 CTP 3.0 中 big data 叢集的新功能和已知問題。

### <a name="whats-new"></a>新功能

| 新功能或更新 | 詳細資料 |
|:---|:---|
| **mssqlctl** 更新 | 數個 **mssqlctl** [命令與參數更新](reference-azdata.md)。 這包含 **mssqlctl login** 命令的更新，此命令現在針對控制器使用者名稱和端點。 |
| 儲存體增強功能 | 支援記錄檔和資料的不同儲存體設定。 此外，巨量資料叢集的永續性磁碟區宣告數已減少。 |
| 多重計算集區執行個體 | 支援多重計算集區執行個體。 |
| 新的集區行為和功能 | 根據預設，現在計算集區只會用於 **ROUND_ROBIN** 散發中的存放集區和資料集區作業。 資料集區現在可以使用新的 **REPLICATED** 散發類型，這表示相同的資料會出現在所有資料集區執行個體上。 |
| 外部資料表改善 | HADOOP 資料來源類型的外部資料表，現在支援讀取最高 1 MB 的資料列。 外部資料表 (ODBC、存放集區、資料集區) 現在支援如 SQL Server 資料表寬度的資料列。 |

### <a name="known-issues"></a>已知問題

下列各節說明此版本的已知問題和限制。

#### <a name="hdfs"></a>HDFS

- 當您嘗試在 HDFS 中建立新資料夾時, Azure Data Studio 會傳回錯誤。 若要啟用這項功能, 請安裝 Azure Data Studio 的內部人員組建:
  
   - [Windows 使用者安裝程式-**內部人員組建**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-user/insider)
   - [Windows 系統安裝程式-**內部人員組建**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64/insider)
   - [Windows ZIP-**內部人員組建**](https://azuredatastudio-update.azurewebsites.net/latest/win32-x64-archive/insider)
   - [macOS ZIP-**內部人員組建**](https://azuredatastudio-update.azurewebsites.net/latest/darwin/insider)
   - [Linux TAR。GZ-內部人員**組建**](https://azuredatastudio-update.azurewebsites.net/latest/linux-x64/insider)

- 如果您以滑鼠右鍵按一下 HDFS 中的檔案來預覽它, 您可能會看到下列錯誤:

   `Error previewing file: File exceeds max size of 30MB`

   目前沒有任何方法可以在 Azure Data Studio 中預覽大於 30 MB 的檔案。

- 不支援對 hdfs-site.xml 進行變更之 HDFS 的設定變更。

#### <a name="deployment"></a>部署

- CTP 3.0 不支援先前已啟用 GPU 之 big data 叢集的部署程式。 正在調查替代的部署程式。 目前, 「部署具有 GPU 支援和回合 TensorFlow 的大型資料叢集」一文已暫時取消發佈, 以避免混淆。

- 不支援從舊版本升級 big data 資料叢集。

   > [!IMPORTANT]
   > 您必須先備份資料, 然後刪除現有的 big data 叢集 (使用舊版的**azdata**), 然後再部署最新版本。 如需詳細資訊, 請參閱[升級至新版本](deployment-upgrade.md)。

- 在 AKS 上部署之後, 您可能會看到來自部署的下列兩個警告事件。 這兩個事件都是已知的問題, 但不會讓您無法在 AKS 上成功部署 big data cluster。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果 big data cluster 部署失敗, 則不會移除相關聯的命名空間。 這可能會導致叢集上有孤立的命名空間。 因應措施是在部署具有相同名稱的叢集之前, 手動刪除命名空間。

#### <a name="external-tables"></a>外部資料表

- Big data cluster 部署不再建立**SqlDataPool**和**SqlStoragePool**外部資料源。 您可以手動建立這些資料來源, 以支援資料集區和存放集區的資料虛擬化。

   > [!NOTE]
   > 建立這些外部資料源的 URI 在 Ctp 之間不同。 請參閱下列 Transact-sql 命令, 以瞭解如何建立它們 

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://controller-svc/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://controller-svc/default');
   ```

- 您可以為具有不支援之資料行類型的資料表建立資料集區外部資料表。 如果您查詢外部資料表, 您會收到類似下列的訊息:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果您查詢存放集區外部資料表, 當基礎檔案同時複製到 HDFS 時, 您可能會收到錯誤。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 如果您要為使用字元資料類型的 Oracle 建立外部資料表, Azure Data Studio virtualization wizard 會在外部資料表定義中, 將這些資料行轉譯為 VARCHAR。 這會導致外部資料表 DDL 失敗。 請修改 Oracle 架構, 以使用 NVARCHAR2 類型, 或手動建立外部資料表語句並指定 NVARCHAR, 而不是使用 wizard。

#### <a name="application-deployment"></a>應用程式部署

- 從 RESTful API 呼叫 R、Python 或 MLeap 應用程式時, 呼叫會在5分鐘內超時。

#### <a name="spark-and-notebooks"></a>Spark 和筆記本

- POD 重新開機時, Kubernetes 環境中的 POD IP 位址可能會變更。 在主要 pod 重新開機的案例中, Spark 會話可能會失敗並出現`NoRoteToHostException`。 這是由不會以新的 IP 位址重新整理的 JVM 快取所造成。

- 如果您已在 Windows 上安裝 Jupyter 和個別的 Python, Spark 筆記本可能會失敗。 若要解決此問題, 請將 Jupyter 升級至最新版本。

- 在筆記本中, 如果您按一下 [**加入文字**] 命令, 文字資料格就會以預覽模式加入, 而不是編輯模式。 您可以按一下 [預覽] 圖示來切換至編輯模式, 並編輯資料格。

#### <a name="security"></a>安全性

- SA_PASSWORD 是環境的一部分, 而且可探索 (例如, 在纜線傾印檔案中)。 部署之後, 您必須在主要實例上重設 SA_PASSWORD。 這不是一個 bug, 而是一個安全性步驟。 如需如何在 Linux 容器中變更 SA_PASSWORD 的詳細資訊, 請參閱[變更 SA 密碼](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 記錄可能包含適用于 big data cluster 部署的 SA 密碼。

## <a id="ctp25"></a>CTP 2.5 (四月)

下列各節說明 SQL Server 2019 CTP 2.5 中 big data 叢集的新功能和已知問題。

### <a name="whats-new"></a>新功能

| 新功能或更新 | 詳細資料 |
|:---|:---|
| 部署設定檔 | 將預設和自訂[部署設定 JSON 檔案](deployment-guidance.md#configfile)用於巨量資料叢集部署，而不是環境變數。 |
| 提示的部署 | `azdata cluster create` 現在會提示您輸入預設部署的任何必要設定。 |
| 服務端點和 Pod 名稱變更 | 下列外部端點已變更名稱:<br/>&nbsp;&nbsp;&nbsp;- **endpoint-master-pool** => **master-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-controller** => **controller-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-service-proxy** => **mgmtproxy-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-security** => **gateway-svc-external**<br/>&nbsp;&nbsp;&nbsp;- **endpoint-app-service-proxy** => **appproxy-svc-external**|
| **azdata**改良功能 | 使用**azdata**來[列出外部端點](deployment-guidance.md#endpoints), 並使用`--version`參數來檢查**azdata**版本。 |
| 離線安裝 | 適用于離線海量資料叢集部署的指引。 |
| HDFS 階層處理改善 | ADLS Gen2 的 S3 分層、裝載快取和 OAuth 支援。 |
| 新`mssql`的 Spark SQL Server 連接器 | |

### <a name="known-issues"></a>已知問題

下列各節說明此版本的已知問題和限制。

#### <a name="deployment"></a>部署

- 不支援從舊版本升級 big data 資料叢集。

   > [!IMPORTANT]
   > 您必須先備份資料, 然後刪除現有的 big data 叢集 (使用舊版的**azdata**), 然後再部署最新版本。 如需詳細資訊, 請參閱[升級至新版本](deployment-upgrade.md)。

- 在 AKS 上部署之後, 您可能會看到來自部署的下列兩個警告事件。 這兩個事件都是已知的問題, 但不會讓您無法在 AKS 上成功部署 big data cluster。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果 big data cluster 部署失敗, 則不會移除相關聯的命名空間。 這可能會導致叢集上有孤立的命名空間。 因應措施是在部署具有相同名稱的叢集之前, 手動刪除命名空間。

#### <a name="external-tables"></a>外部資料表

- Big data cluster 部署不再建立**SqlDataPool**和**SqlStoragePool**外部資料源。 您可以手動建立這些資料來源, 以支援資料集區和存放集區的資料虛擬化。

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://nmnode-0-svc:50070');
   ```

- 您可以為具有不支援之資料行類型的資料表建立資料集區外部資料表。 如果您查詢外部資料表, 您會收到類似下列的訊息:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果您查詢存放集區外部資料表, 當基礎檔案同時複製到 HDFS 時, 您可能會收到錯誤。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 如果您要為使用字元資料類型的 Oracle 建立外部資料表, Azure Data Studio virtualization wizard 會在外部資料表定義中, 將這些資料行轉譯為 VARCHAR。 這會導致外部資料表 DDL 失敗。 請修改 Oracle 架構, 以使用 NVARCHAR2 類型, 或手動建立外部資料表語句並指定 NVARCHAR, 而不是使用 wizard。

#### <a name="application-deployment"></a>應用程式部署

- 從 RESTful API 呼叫 R、Python 或 MLeap 應用程式時, 呼叫會在5分鐘內超時。

#### <a name="spark-and-notebooks"></a>Spark 和筆記本

- POD 重新開機時, Kubernetes 環境中的 POD IP 位址可能會變更。 在主要 pod 重新開機的案例中, Spark 會話可能會失敗並出現`NoRoteToHostException`。 這是由不會以新的 IP 位址重新整理的 JVM 快取所造成。

- 如果您已在 Windows 上安裝 Jupyter 和個別的 Python, Spark 筆記本可能會失敗。 若要解決此問題, 請將 Jupyter 升級至最新版本。

- 在筆記本中, 如果您按一下 [**加入文字**] 命令, 文字資料格就會以預覽模式加入, 而不是編輯模式。 您可以按一下 [預覽] 圖示來切換至編輯模式, 並編輯資料格。

#### <a name="hdfs"></a>HDFS

- 如果您以滑鼠右鍵按一下 HDFS 中的檔案來預覽它, 您可能會看到下列錯誤:

   `Error previewing file: File exceeds max size of 30MB`

   目前沒有任何方法可以在 Azure Data Studio 中預覽大於 30 MB 的檔案。

- 不支援對 hdfs-site.xml 進行變更之 HDFS 的設定變更。

#### <a name="security"></a>安全性

- SA_PASSWORD 是環境的一部分, 而且可探索 (例如, 在纜線傾印檔案中)。 部署之後, 您必須在主要實例上重設 SA_PASSWORD。 這不是一個 bug, 而是一個安全性步驟。 如需如何在 Linux 容器中變更 SA_PASSWORD 的詳細資訊, 請參閱[變更 SA 密碼](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 記錄可能包含適用于 big data cluster 部署的 SA 密碼。

## <a id="ctp24"></a>CTP 2.4 (三月)

下列各節說明 SQL Server 2019 CTP 2.4 中 big data 叢集的新功能和已知問題。

### <a name="whats-new"></a>新功能

| 新功能或更新 | 詳細資料 |
|:---|:---|
| 說明在 Spark 中透過 TensorFlow 執行深度學習時的 GPU 支援。 | [部署具有 GPU 支援的巨量資料叢集並執行 TensorFlow](spark-gpu-tensorflow.md)。 |
| 預設不會再建立 **SqlDataPool** 和 **SqlStoragePool** 資料來源。 | 視需要手動建立這些資料來源。 請參閱[已知問題](#externaltablesctp24)。 |
| 資料集區的 `INSERT INTO SELECT` 支援。 | 如需範例，請參閱[教學課程：使用 Transact-SQL 將資料內嵌到 SQL Server 資料集區](tutorial-data-pool-ingest-sql.md)。 |
| `FORCE SCALEOUTEXECUTION` 和 `DISABLE SCALEOUTEXECUTION` 選項。 | 強制或停用計算集區以用於外部資料表上的查詢。 例如： `SELECT TOP(100) * FROM web_clickstreams_hdfs_book_clicks OPTION(FORCE SCALEOUTEXECUTION)` 。 |
| 更新的 AKS 部署建議。 | 評估 AKS 上的巨量資料叢集時，我們現在建議您使用大小為 **Standard_L8s** 的單一節點。 |
| 將 Spark 執行階段升級至 Spark 2.4。 | |

### <a name="known-issues"></a>已知問題

下列各節說明此版本的已知問題和限制。

#### <a name="deployment"></a>部署

- 不支援從舊版本升級 big data 資料叢集。

   > [!IMPORTANT]
   > 您必須先備份資料, 然後刪除現有的 big data 叢集 (使用舊版的**azdata**), 然後再部署最新版本。 如需詳細資訊, 請參閱[升級至新版本](deployment-upgrade.md)。

- 在 AKS 上部署之後, 您可能會看到來自部署的下列兩個警告事件。 這兩個事件都是已知的問題, 但不會讓您無法在 AKS 上成功部署 big data cluster。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果 big data cluster 部署失敗, 則不會移除相關聯的命名空間。 這可能會導致叢集上有孤立的命名空間。 因應措施是在部署具有相同名稱的叢集之前, 手動刪除命名空間。

#### <a name="kubeadm-deployments"></a>kubeadm 部署

如果您使用 kubeadm 在多部電腦上部署 Kubernetes, 叢集系統管理入口網站就不會正確顯示連接到 big data 叢集所需的端點。 如果您遇到此問題, 請使用下列解決方法來探索服務端點 IP 位址:

- 如果您是從叢集內進行連線, 請查詢 Kubernetes 以取得您想要連接之端點的服務 IP。 例如, 下列**kubectl**命令會顯示 SQL Server 主要實例的 IP 位址:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- 如果您是從叢集外部連線, 請使用下列步驟來連接:

   1. 取得執行 SQL Server 主要實例之節點的 IP 位址: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`。

   1. 使用此 IP 位址連接到 SQL Server 的主要實例。

   1. 在 master 資料庫中查詢其他外部端點的**cluster_endpoint_table** 。

      如果這是因為連接逾時而失敗, 則可能是防火牆個別節點。 在此情況下, 您必須聯絡 Kubernetes 叢集系統管理員, 並要求外部公開的節點 IP。 這可能是任何節點。 接著, 您可以使用該 IP 和對應的埠, 連接到叢集中執行的各種服務。 例如, 系統管理員可以藉由執行下列來尋找此 IP:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a name="delete-cluster-fails"></a>刪除叢集失敗

當您嘗試使用**azdata**刪除叢集時, 它會因下列錯誤而失敗:

```
2019-03-26 20:38:11.0614 UTC | INFO | Deleting cluster ...
Error processing command: "TypeError"
delete_namespaced_service() takes 3 positional arguments but 4 were given
Makefile:61: recipe for target 'delete-cluster' failed
make[2]: *** [delete-cluster] Error 1
Makefile:223: recipe for target 'deploy-clean' failed
make[1]: *** [deploy-clean] Error 2
Makefile:203: recipe for target 'deploy-clean' failed
make: *** [deploy-clean] Error 2
```

新的 Python Kubernetes 用戶端 (版本 9.0.0) 已變更刪除命名空間 API, 其目前會中斷**azdata**。 只有在您已安裝較新的 Kubernetes python 用戶端時, 才會發生這種情況。 若要解決這個問題, 您可以使用**kubectl** (`kubectl delete ns <ClusterName>`) 直接刪除叢集, 也可以使用`sudo pip install kubernetes==8.0.1`來安裝較舊的版本。

#### <a id="externaltablesctp24"></a>外部資料表

- Big data cluster 部署不再建立**SqlDataPool**和**SqlStoragePool**外部資料源。 您可以手動建立這些資料來源, 以支援資料集區和存放集區的資料虛擬化。

   ```sql
   -- Create default data sources for SQL Big Data Cluster
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
       CREATE EXTERNAL DATA SOURCE SqlDataPool
       WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
 
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlStoragePool')
       CREATE EXTERNAL DATA SOURCE SqlStoragePool
       WITH (LOCATION = 'sqlhdfs://service-master-pool:50070');
   ```

- 您可以為具有不支援之資料行類型的資料表建立資料集區外部資料表。 如果您查詢外部資料表, 您會收到類似下列的訊息:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果您查詢存放集區外部資料表, 當基礎檔案同時複製到 HDFS 時, 您可能會收到錯誤。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 如果您要為使用字元資料類型的 Oracle 建立外部資料表, Azure Data Studio virtualization wizard 會在外部資料表定義中, 將這些資料行轉譯為 VARCHAR。 這會導致外部資料表 DDL 失敗。 請修改 Oracle 架構, 以使用 NVARCHAR2 類型, 或手動建立外部資料表語句並指定 NVARCHAR, 而不是使用 wizard。

#### <a name="application-deployment"></a>應用程式部署

- 從 RESTful API 呼叫 R、Python 或 MLeap 應用程式時, 呼叫會在5分鐘內超時。

#### <a name="spark-and-notebooks"></a>Spark 和筆記本

- POD 重新開機時, Kubernetes 環境中的 POD IP 位址可能會變更。 在主要 pod 重新開機的案例中, Spark 會話可能會失敗並出現`NoRoteToHostException`。 這是由不會以新的 IP 位址重新整理的 JVM 快取所造成。

- 如果您已在 Windows 上安裝 Jupyter 和個別的 Python, Spark 筆記本可能會失敗。 若要解決此問題, 請將 Jupyter 升級至最新版本。

- 在筆記本中, 如果您按一下 [**加入文字**] 命令, 文字資料格就會以預覽模式加入, 而不是編輯模式。 您可以按一下 [預覽] 圖示來切換至編輯模式, 並編輯資料格。

#### <a name="hdfs"></a>HDFS

- 如果您以滑鼠右鍵按一下 HDFS 中的檔案來預覽它, 您可能會看到下列錯誤:

   `Error previewing file: File exceeds max size of 30MB`

   目前沒有任何方法可以在 Azure Data Studio 中預覽大於 30 MB 的檔案。

- 不支援對 hdfs-site.xml 進行變更之 HDFS 的設定變更。

#### <a name="security"></a>安全性

- SA_PASSWORD 是環境的一部分, 而且可探索 (例如, 在纜線傾印檔案中)。 部署之後, 您必須在主要實例上重設 SA_PASSWORD。 這不是一個 bug, 而是一個安全性步驟。 如需如何在 Linux 容器中變更 SA_PASSWORD 的詳細資訊, 請參閱[變更 SA 密碼](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 記錄可能包含適用于 big data cluster 部署的 SA 密碼。

## <a id="ctp23"></a>CTP 2.3 (二月)

下列各節說明 SQL Server 2019 CTP 2.3 中 big data 叢集的新功能和已知問題。

### <a name="whats-new"></a>新功能

| 新功能或更新 | 詳細資料 |
| :---------- | :------ |
| 在 IntelliJ 中於巨量資料叢集上提交 Spark 作業。 | [在 IntelliJ 中於 SQL Server 巨量資料叢集上提交 Spark 作業](spark-submit-job-intellij-tool-plugin.md) |
| 適用於應用程式部署和叢集管理的一般 CLI。 | [如何在 SQL Server 2019 巨量資料叢集 (預覽) 上部署應用程式](big-data-cluster-create-apps.md) |
| 用來將應用程式部署到巨量資料叢集的 VS Code 延伸模組。 | [如何使用 VS Code 將應用程式部署到 SQL Server 巨量資料叢集](app-deployment-extension.md) |
| **Azdata**工具命令使用方式的變更。 | 如需詳細資訊, 請參閱[azdata 的已知問題](#azdatactp23)。 |
| 在大型資料叢集中使用 Sparklyr | [在 SQL Server 2019 巨量資料叢集中使用 Sparklyr](sparklyr-from-RStudio.md) |
| 將外部 HDFS 相容儲存體裝載至具備 **HDFS 階層處理**的巨量資料叢集。 | 請參閱 [HDFS 階層處理](hdfs-tiering.md)。 |
| SQL Server 主要執行個體與 HDFS/Spark 閘道的新整合連線體驗。 | 請參閱 [SQL Server 主要執行個體與 HDFS/Spark 閘道](connect-to-big-data-cluster.md)。 |
| 刪除具有 azdata 叢集**刪除**功能的叢集現在只會刪除屬於 big data 叢集一部分之命名空間中的物件。 | 不會刪除命名空間。 但是在舊版中，此命令確實會刪除整個命名空間。 |
| _Security_ 端點名稱已變更並合併。 | **service-security-lb** 和 **service-security-nodeport** 已合併為 **endpoint-security** 端點。 |
| _Proxy_ 端點名稱已變更並合併。 | **service-proxy-lb** 和 **service-proxy-nodeport** 已合併為 **endpoint-service-proxy** 端點。 |
| _Controller_ 端點名稱已變更並合併。 | **service-mssql-controller-lb** 和 **service-mssql-controller-nodeport** 已合併為 **endpoint-controller** 端點。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知問題

下列各節說明此版本的已知問題和限制。

#### <a name="deployment"></a>部署

- 不支援從舊版本升級 big data 資料叢集。

   > [!IMPORTANT]
   > 您必須先備份資料, 然後刪除現有的 big data 叢集 (使用舊版的**azdata**), 然後再部署最新版本。 如需詳細資訊, 請參閱[升級至新版本](deployment-upgrade.md)。

- **ACCEPT_EULA**環境變數必須是 [是] 或 [是], 才能接受 EULA。 先前的版本允許「y」和「Y」, 但不再接受, 而且將導致部署失敗。

- **CLUSTER_PLATFORM**環境變數沒有預設值, 如同在先前版本中所做的一樣。

- 在 AKS 上部署之後, 您可能會看到來自部署的下列兩個警告事件。 這兩個事件都是已知的問題, 但不會讓您無法在 AKS 上成功部署 big data cluster。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果 big data cluster 部署失敗, 則不會移除相關聯的命名空間。 這可能會導致叢集上有孤立的命名空間。 因應措施是在部署具有相同名稱的叢集之前, 手動刪除命名空間。

#### <a name="kubeadm-deployments"></a>kubeadm 部署

如果您使用 kubeadm 在多部電腦上部署 Kubernetes, 叢集系統管理入口網站就不會正確顯示連接到 big data 叢集所需的端點。 如果您遇到此問題, 請使用下列解決方法來探索服務端點 IP 位址:

- 如果您是從叢集內進行連線, 請查詢 Kubernetes 以取得您想要連接之端點的服務 IP。 例如, 下列**kubectl**命令會顯示 SQL Server 主要實例的 IP 位址:

   ```bash
   kubectl get service endpoint-master-pool -n <clusterName> -o=custom-columns="IP:.spec.clusterIP,PORT:.spec.ports[*].nodePort"
   ```

- 如果您是從叢集外部連線, 請使用下列步驟來連接:

   1. 取得執行 SQL Server 主要實例之節點的 IP 位址: `kubectl get pod mssql-master-pool-0 -o jsonpath="Name: {.metadata.name} Status: {.status.hostIP}" -n <clusterName>`。

   1. 使用此 IP 位址連接到 SQL Server 的主要實例。

   1. 在 master 資料庫中查詢其他外部端點的**cluster_endpoint_table** 。

      如果這是因為連接逾時而失敗, 則可能是防火牆個別節點。 在此情況下, 您必須聯絡 Kubernetes 叢集系統管理員, 並要求外部公開的節點 IP。 這可能是任何節點。 接著, 您可以使用該 IP 和對應的埠, 連接到叢集中執行的各種服務。 例如, 系統管理員可以藉由執行下列來尋找此 IP:

      ```
      [root@m12hn01 config]# kubectl cluster-info
      Kubernetes master is running at https://172.50.253.99:6443
      KubeDNS is running at https://172.30.243.91:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
      ```

#### <a id="azdatactp23"></a>azdata

- **Azdata**工具會從動詞-名詞命令順序變更為名詞動詞。 例如, `azdata create cluster`現在`azdata cluster create`是。

- `--name` 使用`azdata cluster create`建立叢集時, 現在需要參數。

   ```bash
   azdata cluster create --name <cluster_name>
   ```

- 如需升級至最新版本的 big data 叢集和**azdata**的重要資訊, 請參閱[升級至新](deployment-upgrade.md)版本。

#### <a name="external-tables"></a>外部資料表

- 您可以為具有不支援之資料行類型的資料表建立資料集區外部資料表。 如果您查詢外部資料表, 您會收到類似下列的訊息:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果您查詢存放集區外部資料表, 當基礎檔案同時複製到 HDFS 時, 您可能會收到錯誤。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

- 如果您要為使用字元資料類型的 Oracle 建立外部資料表, Azure Data Studio virtualization wizard 會在外部資料表定義中, 將這些資料行轉譯為 VARCHAR。 這會導致外部資料表 DDL 失敗。 請修改 Oracle 架構, 以使用 NVARCHAR2 類型, 或手動建立外部資料表語句並指定 NVARCHAR, 而不是使用 wizard。

#### <a name="application-deployment"></a>應用程式部署

- 從 RESTful API 呼叫 R、Python 或 MLeap 應用程式時, 呼叫會在5分鐘內超時。

#### <a name="spark-and-notebooks"></a>Spark 和筆記本

- POD 重新開機時, Kubernetes 環境中的 POD IP 位址可能會變更。 在主要 pod 重新開機的案例中, Spark 會話可能會失敗並出現`NoRoteToHostException`。 這是由不會以新的 IP 位址重新整理的 JVM 快取所造成。

- 如果您已在 Windows 上安裝 Jupyter 和個別的 Python, Spark 筆記本可能會失敗。 若要解決此問題, 請將 Jupyter 升級至最新版本。

- 在筆記本中, 如果您按一下 [**加入文字**] 命令, 文字資料格就會以預覽模式加入, 而不是編輯模式。 您可以按一下 [預覽] 圖示來切換至編輯模式, 並編輯資料格。

#### <a name="hdfs"></a>HDFS

- 如果您以滑鼠右鍵按一下 HDFS 中的檔案來預覽它, 您可能會看到下列錯誤:

   `Error previewing file: File exceeds max size of 30MB`

   目前沒有任何方法可以在 Azure Data Studio 中預覽大於 30 MB 的檔案。

- 不支援對 hdfs-site.xml 進行變更之 HDFS 的設定變更。

#### <a name="security"></a>安全性

- SA_PASSWORD 是環境的一部分, 而且可探索 (例如, 在纜線傾印檔案中)。 部署之後, 您必須在主要實例上重設 SA_PASSWORD。 這不是一個 bug, 而是一個安全性步驟。 如需如何在 Linux 容器中變更 SA_PASSWORD 的詳細資訊, 請參閱[變更 SA 密碼](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 記錄可能包含適用于 big data cluster 部署的 SA 密碼。

## <a id="ctp22"></a>CTP 2.2 (2018 年12月)

下列各節說明 SQL Server 2019 CTP 2.2 中 big data 叢集的新功能和已知問題。

### <a name="new-features"></a>新增功能

- 以 ( `/portal` **HTTPs://\<ip位址\>: 30777/入口網站**) 存取的叢集管理員入口網站。
- 主要集區服務名稱已`service-master-pool-lb`從`service-master-pool-nodeport`變更`endpoint-master-pool`為。
- 新版本的**azdata**和更新的映射。
- 其他 bug 修正和改善。

### <a name="known-issues"></a>已知問題

下列各節說明此版本的已知問題和限制。

#### <a name="deployment"></a>部署

- 不支援從舊版本升級 big data 資料叢集。 在部署最新版本之前, 您必須先備份和刪除任何現有的大型資料叢集。 如需詳細資訊, 請參閱[升級至新版本](deployment-upgrade.md)。

- 在 AKS 上部署之後, 您可能會看到來自部署的下列兩個警告事件。 這兩個事件都是已知的問題, 但不會讓您無法在 AKS 上成功部署 big data cluster。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果 big data cluster 部署失敗, 則不會移除相關聯的命名空間。 這可能會導致叢集上有孤立的命名空間。 因應措施是在部署具有相同名稱的叢集之前, 手動刪除命名空間。

#### <a name="cluster-administration-portal"></a>叢集系統管理入口網站

叢集系統管理入口網站不會顯示 SQL Server 主要實例的端點。 若要尋找主要實例的 IP 位址和埠, 請使用下列**kubectl**命令:

```
kubectl get svc endpoint-master-pool -n <your-big-data-cluster-name>
```

#### <a name="external-tables"></a>外部資料表

- 您可以為具有不支援之資料行類型的資料表建立資料集區外部資料表。 如果您查詢外部資料表, 您會收到類似下列的訊息:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果您查詢存放集區外部資料表, 當基礎檔案同時複製到 HDFS 時, 您可能會收到錯誤。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 和筆記本

- POD 重新開機時, Kubernetes 環境中的 POD IP 位址可能會變更。 在主要 pod 重新開機的案例中, Spark 會話可能會失敗並出現`NoRoteToHostException`。 這是由不會以新的 IP 位址重新整理的 JVM 快取所造成。

- 如果您已在 Windows 上安裝 Jupyter 和個別的 Python, Spark 筆記本可能會失敗。 若要解決此問題, 請將 Jupyter 升級至最新版本。

- 在筆記本中, 如果您按一下 [**加入文字**] 命令, 文字資料格就會以預覽模式加入, 而不是編輯模式。 您可以按一下 [預覽] 圖示來切換至編輯模式, 並編輯資料格。

#### <a name="hdfs"></a>HDFS

- 如果您以滑鼠右鍵按一下 HDFS 中的檔案來預覽它, 您可能會看到下列錯誤:

   `Error previewing file: File exceeds max size of 30MB`

   目前沒有任何方法可以在 Azure Data Studio 中預覽大於 30 MB 的檔案。

- 不支援對 hdfs-site.xml 進行變更之 HDFS 的設定變更。

#### <a name="security"></a>安全性

- SA_PASSWORD 是環境的一部分, 而且可探索 (例如, 在纜線傾印檔案中)。 部署之後, 您必須在主要實例上重設 SA_PASSWORD。 這不是一個 bug, 而是一個安全性步驟。 如需如何在 Linux 容器中變更 SA_PASSWORD 的詳細資訊, 請參閱[變更 SA 密碼](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 記錄可能包含適用于 big data cluster 部署的 SA 密碼。

## <a id="ctp21"></a>CTP 2.1 (2018 年11月)

下列各節說明 SQL Server 2019 CTP 2.1 中 big data 叢集的新功能和已知問題。

### <a name="new-features"></a>新增功能

- 在龐大的資料叢集中[部署 Python 和 R 應用程式](big-data-cluster-create-apps.md)。
- 新版本的**azdata**和更新的映射。 
- 其他 bug 修正和改善。

### <a name="known-issues"></a>已知問題

下列各節提供 CTP 2.1 中 SQL Server big data 叢集的已知問題。

#### <a name="deployment"></a>部署

- 不支援從舊版本升級 big data 資料叢集。 在部署最新版本之前, 您必須先備份和刪除任何現有的大型資料叢集。 如需詳細資訊, 請參閱[升級至新版本](deployment-upgrade.md)。

- 在 AKS 上部署之後, 您可能會看到來自部署的下列兩個警告事件。 這兩個事件都是已知的問題, 但不會讓您無法在 AKS 上成功部署 big data cluster。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果 big data cluster 部署失敗, 則不會移除相關聯的命名空間。 這可能會導致叢集上有孤立的命名空間。 因應措施是在部署具有相同名稱的叢集之前, 手動刪除命名空間。

#### <a name="admin-portal"></a>管理員入口網站

- 當您[建立應用程式使用 msqlctl ctp 命令](big-data-cluster-create-apps.md)並將其部署巨量資料叢集，叢集系統管理員入口網站顯示 pod 已部署應用程式為 「 不明 」 的 Admin 部分的 [控制器] 區段中的 SQL Server 上。

#### <a name="external-tables"></a>外部資料表

- 您可以為具有不支援之資料行類型的資料表建立資料集區外部資料表。 如果您查詢外部資料表, 您會收到類似下列的訊息:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果您查詢存放集區外部資料表, 當基礎檔案同時複製到 HDFS 時, 您可能會收到錯誤。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 和筆記本

- POD 重新開機時, Kubernetes 環境中的 POD IP 位址可能會變更。 在主要 pod 重新開機的案例中, Spark 會話可能會失敗並出現`NoRoteToHostException`。 這是由不會以新的 IP 位址重新整理的 JVM 快取所造成。

- 如果您已在 Windows 上安裝 Jupyter 和個別的 Python, Spark 筆記本可能會失敗。 若要解決此問題, 請將 Jupyter 升級至最新版本。

- 在筆記本中, 如果您按一下 [**加入文字**] 命令, 文字資料格就會以預覽模式加入, 而不是編輯模式。 您可以按一下 [預覽] 圖示來切換至編輯模式, 並編輯資料格。

#### <a name="hdfs"></a>HDFS

- 如果您以滑鼠右鍵按一下 HDFS 中的檔案來預覽它, 您可能會看到下列錯誤:

   `Error previewing file: File exceeds max size of 30MB`

   目前沒有任何方法可以在 Azure Data Studio 中預覽大於 30 MB 的檔案。

- 不支援對 hdfs-site.xml 進行變更之 HDFS 的設定變更。

#### <a name="security"></a>安全性

- SA_PASSWORD 是環境的一部分, 而且可探索 (例如, 在纜線傾印檔案中)。 部署之後, 您必須在主要實例上重設 SA_PASSWORD。 這不是一個 bug, 而是一個安全性步驟。 如需如何在 Linux 容器中變更 SA_PASSWORD 的詳細資訊, 請參閱[變更 SA 密碼](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 記錄可能包含適用于 big data cluster 部署的 SA 密碼。

## <a id="ctp20"></a>CTP 2.0 (2018 年10月)

下列各節說明 SQL Server 2019 CTP 2.0 中 big data 叢集的新功能和已知問題。

### <a name="new-features"></a>新增功能

- 使用 azdata 管理工具的簡單部署體驗
- Azure Data Studio 中的原生筆記本體驗
- 透過 SQL Server 的儲存體實例來查詢 HDFS 檔案
- 透過主要 SQL Server、Oracle、MongoDB 和 HDFS 的資料虛擬化
- Azure Data Studio 中 SQL Server 和 Oracle 的資料虛擬化 wizard
- 主要機器上的 ML 服務
- 叢集系統管理入口網站, 可用於監視和疑難排解
- Azure Data Studio 中的 Spark 作業提交 
- 叢集系統管理入口網站中的 Spark UI
- 磁片區掛接到存放裝置類別
- 從 master 對資料集區進行查詢
- 在 SSMS 中顯示分散式查詢的計畫
- Azdata 管理工具的 Pip 套件
- 透過控制器服務的內建部署引擎

### <a name="known-issues"></a>已知問題

下列各節提供 CTP 2.0 中 SQL Server big data 叢集的已知問題。

#### <a name="deployment"></a>部署

- 如果您使用 Azure Kubernetes Service (AKS), 建議的 Kubernetes 版本為 1.10. *, 這不支援調整磁片大小。 您應該確定您是在部署時據以調整儲存體大小。 如需有關如何調整儲存體大小的詳細資訊, 請參閱[資料持續](concept-data-persistence.md)性一文。 針對部署在 Vm 上的 Kubernetes, 建議的版本為1.11。

- 在 AKS 上部署之後, 您可能會看到來自部署的下列兩個警告事件。 這兩個事件都是已知的問題, 但不會讓您無法在 AKS 上成功部署 big data cluster。

   `Warning  FailedMount: Unable to mount volumes for pod "mssql-storage-pool-default-1_sqlarisaksclus(c83eae70-c81b-11e8-930f-f6b6baeb7348)": timeout expired waiting for volumes to attach or mount for pod "sqlarisaksclus"/"mssql-storage-pool-default-1". list of unmounted volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs]. list of unattached volumes=[storage-pool-storage hdfs storage-pool-mlservices-storage hadoop-logs storage-pool-java-storage secrets default-token-q9mlx]`

   `Warning  Unhealthy: Readiness probe failed: cat: /tmp/provisioner.done: No such file or directory`

- 如果 big data cluster 部署失敗, 則不會移除相關聯的命名空間。 這可能會導致叢集上有孤立的命名空間。 因應措施是在部署具有相同名稱的叢集之前, 手動刪除命名空間。

#### <a name="external-tables"></a>外部資料表

- 您可以為具有不支援之資料行類型的資料表建立資料集區外部資料表。 如果您查詢外部資料表, 您會收到類似下列的訊息:

   `Msg 7320, Level 16, State 110, Line 44 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 105079; Columns with large object types are not supported for external generic tables.`

- 如果您查詢存放集區外部資料表, 當基礎檔案同時複製到 HDFS 時, 您可能會收到錯誤。

   `Msg 7320, Level 16, State 110, Line 157 Cannot execute the query "Remote Query" against OLE DB provider "SQLNCLI11" for linked server "(null)". 110806;A distributed query failed: One or more errors occurred.`

#### <a name="spark-and-notebooks"></a>Spark 和筆記本

- POD 重新開機時, Kubernetes 環境中的 POD IP 位址可能會變更。 在主要 pod 重新開機的案例中, Spark 會話可能會失敗並出現`NoRoteToHostException`。 這是由不會以新的 IP 位址重新整理的 JVM 快取所造成。

- 如果您已在 Windows 上安裝 Jupyter 和個別的 Python, Spark 筆記本可能會失敗。 若要解決此問題, 請將 Jupyter 升級至最新版本。

- 在筆記本中, 如果您按一下 [**加入文字**] 命令, 文字資料格就會以預覽模式加入, 而不是編輯模式。 您可以按一下 [預覽] 圖示來切換至編輯模式, 並編輯資料格。

#### <a name="hdfs"></a>HDFS

- 如果您以滑鼠右鍵按一下 HDFS 中的檔案來預覽它, 您可能會看到下列錯誤:

   `Error previewing file: File exceeds max size of 30MB`

   目前沒有任何方法可以在 Azure Data Studio 中預覽大於 30 MB 的檔案。

- 不支援對 hdfs-site.xml 進行變更之 HDFS 的設定變更。

#### <a name="security"></a>安全性

- SA_PASSWORD 是環境的一部分, 而且可探索 (例如, 在纜線傾印檔案中)。 部署之後, 您必須在主要實例上重設 SA_PASSWORD。 這不是一個 bug, 而是一個安全性步驟。 如需如何在 Linux 容器中變更 SA_PASSWORD 的詳細資訊, 請參閱[變更 SA 密碼](../linux/quickstart-install-connect-docker.md#sapassword)。

- AKS 記錄可能包含適用于 big data cluster 部署的 SA 密碼。

## <a name="next-steps"></a>後續步驟

如需有關 SQL Server big data 叢集的詳細資訊, 請參閱[什麼是 SQL Server 2019 big data 叢集？](big-data-cluster-overview.md)。
