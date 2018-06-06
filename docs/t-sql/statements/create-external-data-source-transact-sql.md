---
title: CREATE EXTERNAL DATA SOURCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL DATA SOURCE
- CREATE_EXTERNAL_DATA_SOURCE
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, data source
- PolyBase, create data source
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9da6613c69319197da22b9b4cee74e8ef0b289d6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
---
# <a name="create-external-data-source-transact-sql"></a>CREATE EXTERNAL DATA SOURCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  建立 PolyBase 的外部資料來源或彈性資料庫查詢。 語法會視案例而擁有顯著的差異。 針對 PolyBase 建立的外部資料來源無法用於彈性資料庫查詢。  同樣地，針對彈性資料庫查詢建立的外部資料來源也無法用於 PolyBase 等。 
  
> [!NOTE]  
>  只有在 SQL Server 2016 (或更新版本)、Azure SQL 資料倉儲，以及平行處理資料倉儲上才支援 PolyBase。 只有在 Azure SQL Database v12 或更新版本上才支援彈性資料庫查詢。  
  
 針對 PolyBase，外部資料來源為 Hadoop 檔案系統 (HDFS)、Azure 儲存體 Blob 容器或 Azure Data Lake Store。 如需詳細資訊，請參閱 [開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)。  
  
 針對彈性資料庫查詢，外部來源為分區對應管理員 (在 Azure SQL Database 上) 或遠端資料庫 (在 Azure SQL Database 上)。  建立外部資料來源後，請使用 [sp_execute_remote &#40;Azure SQL Database&#41;](../../relational-databases/system-stored-procedures/sp-execute-remote-azure-sql-database.md)。 如需詳細資訊，請參閱[彈性資料庫查詢](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)。  

  Azure Blob 儲存體外部資料來源支援 `BULK INSERT` 和 `OPENROWSET` 語法，而且與 PolyBase 的 Azure Blob 儲存體不同。
    
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- PolyBase only:  Hadoop cluster as data source   
-- (on SQL Server 2016)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = HADOOP,
        LOCATION = 'hdfs://NameNode_URI[:port]'  
        [, RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI[:port]' ]  
        [, CREDENTIAL = credential_name ]
    )
[;]  
  
-- PolyBase only: Azure Storage Blob as data source   
-- (on SQL Server 2016 and Azure SQL Data Warehouse)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = HADOOP,  
        LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'
        [, CREDENTIAL = credential_name ]
    )  
[;]

-- PolyBase only: Azure Data Lake Store
-- (on Azure SQL Data Warehouse)
CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalake.net',
    CREDENTIAL = AzureStorageCredential
);

-- PolyBase only: Hadoop cluster as data source
-- (on Parallel Data Warehouse)
CREATE EXTERNAL DATA SOURCE data_source_name
    WITH ( 
        TYPE = HADOOP, 
        LOCATION = 'hdfs://NameNode_URI[:port]'
        [, JOB_TRACKER_LOCATION = 'JobTracker_URI[:port]' ]
    )
[;]

-- PolyBase only: Azure Storage Blob as data source 
-- (on Parallel Data Warehouse)
CREATE EXTERNAL DATA SOURCE data_source_name
    WITH ( 
        TYPE = HADOOP,
        LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'
    )
[;]
  
-- Elastic Database query only: a shard map manager as data source   
-- (only on Azure SQL Database)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = SHARD_MAP_MANAGER,  
        LOCATION = '<server_name>.database.windows.net',  
        DATABASE_NAME = '\<ElasticDatabase_ShardMapManagerDb'>,  
        CREDENTIAL = <ElasticDBQueryCred>,  
        SHARD_MAP_NAME = '<ShardMapName>'  
    )  
[;]  
  
-- Elastic Database query only: a remote database on Azure SQL Database as data source   
-- (only on Azure SQL Database)  
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = RDBMS,  
        LOCATION = '<server_name>.database.windows.net',  
        DATABASE_NAME = '<Remote_Database_Name>',  
        CREDENTIAL = <SQL_Credential>  
    )  
[;]  

-- Bulk operations only: Azure Storage Blob as data source   
-- (on SQL Server 2017 or later, and Azure SQL Database).
CREATE EXTERNAL DATA SOURCE data_source_name  
    WITH (   
        TYPE = BLOB_STORAGE,  
        LOCATION = 'https://storage_account_name.blob.core.windows.net/container_name'
        [, CREDENTIAL = credential_name ]
    )  
```  
  
## <a name="arguments"></a>引數  
 *data_source_name* 指定資料來源的使用者定義名稱。 此名稱在 SQL Server、Azure SQL Database 和 Azure SQL 資料倉儲的資料庫內必須是唯一的。 此名稱在平行處理資料倉儲的伺服器內必須是唯一的。
  
 TYPE = [ HADOOP | SHARD_MAP_MANAGER | RDBMS | BLOB_STORAGE]  
 指定資料來源類型。 當外部資料來源為 Hadoop 或適用於 Hadoop 的 Azure 儲存體 Blob 時，請使用 HADOOP。 建立彈性資料庫查詢的外部資料來源以便在 Azure SQL Database 上建立分區時，請使用 SHARD_MAP_MANAGER。 使用 RDBMS 搭配外部資料來源，以便在 Azure SQL Database 上使用彈性資料庫查詢進行跨資料庫查詢。  使用 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 或 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) 搭配 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 執行大量作業時，請使用 BLOB_STORAGE。
  
LOCATION = \<location_path> **HADOOP**    
針對 HADOOP，指定適用於 Hadoop 叢集的統一資源識別項 (URI)。  
`LOCATION = 'hdfs:\/\/*NameNode\_URI*\[:*port*\]'`  
NameNode_URI：Hadoop 叢集 Namenode 的電腦名稱或 IP 位址。  
連接埠：Namenode IPC 連接埠。 這是以 Hadoop 中的 fs.default.name 組態參數表示。 如果未指定值，預設將會使用 8020。  
範例：`LOCATION = 'hdfs://10.10.10.10:8020'`

針對具有 Hadoop 的 Azure Blob 儲存體，指定用於連線到 Azure Blob 儲存體的 URI。  
`LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'`  
wasb[s]：指定 Azure Blob 儲存體的通訊協定。 [s] 是選用的，而且會指定安全的 SSL 連線；從 SQL Server 傳送的資料會透過 SSL 通訊協定，安全地進行加密。 強烈建議您使用 'wasbs'，而不是 'wasb'。 請注意，此位置可以使用 asv[s]，而不是 wasb[s]。 asv[s] 語法已被取代，並將在未來的版本中移除。  
容器：指定 Azure Blob 儲存體容器的名稱。 若要指定網域儲存體帳戶的根容器，請使用網域名稱而不是容器名稱。 根容器是唯讀的，因此無法將資料寫回至容器。  
account_name：Azure 儲存體帳戶的完整網域名稱 (FQDN)。  
範例：`LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'`

針對 Azure Data Lake Store，location 會指定用於連線至 Azure Data Lake Store 的 URI。



**SHARD_MAP_MANAGER**   
 針對 SHARD_MAP_MANAGER，指定在 Azure SQL Database 中裝載分區對應管理員，或在 Azure 虛擬機器上裝載 SQL Server 資料庫的邏輯伺服器名稱。
 
 ```
 CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
  (TYPE = SHARD_MAP_MANAGER,
  LOCATION = '<server_name>.database.windows.net',
  DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
  CREDENTIAL = ElasticDBQueryCred,
  SHARD_MAP_NAME = 'CustomerIDShardMap'
) ;
```

如需逐步教學課程，請參閱[分區彈性查詢入門 (水平資料分割)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)。
  
**RDBMS**   
針對 RDBMS，在 Azure SQL Database 中指定遠端資料庫的邏輯伺服器名稱。  

```  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';  
  
CREATE DATABASE SCOPED CREDENTIAL SQL_Credential    
WITH IDENTITY = '<username>',  
SECRET = '<password>';  
  
CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH   
    (TYPE = RDBMS,   
    LOCATION = '<server_name>.database.windows.net',   
    DATABASE_NAME = 'Customers',   
    CREDENTIAL = SQL_Credential   
) ;   
```  
  
如需有關 RDBMS 的逐步教學課程，請參閱[跨資料庫查詢入門 (垂直資料分割)](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/)。  

**BLOB_STORAGE**   
僅針對大量作業，`LOCATION` 必須是 Azure Blob 儲存體和容器的有效 URL。 請不要將 **/**、檔案名稱或共用存取簽章參數放置於 `LOCATION` URL 的結尾處。   
使用的認證必須利用 `SHARED ACCESS SIGNATURE` 來建立，以作為身分識別。 如需共用存取簽章的詳細資訊，請參閱[使用共用存取簽章 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。 如需存取 Blob 儲存體的範例，請參閱 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 的範例 F。 

  
 RESOURCE_MANAGER_LOCATION = '*ResourceManager_URI*[:*port*]'  
 指定 Hadoop 資源管理員位置。 當已指定時，查詢最佳化工具可以搭配 MapReduce 使用 Hadoop 的計算功能，制定以成本為基礎的決策，以預先處理 PolyBase 查詢的資料。 這稱為述詞下推，可大幅降低在 Hadoop 與 SQL 之間傳輸的資料量，因而改善查詢效能。  
  
 若未指定，系統會針對 PolyBase 查詢，停用將計算推送到 Hadoop。  
 
若未指定連接埠，系統會使用 ‘hadoop connectivity’ 設定的目前設定決定預設值。

|Hadoop 連線能力|預設資源管理員連接埠|
|-------------------|-----------------------------|
|@shouldalert|50300|
|2|50300|
|3|8021|
|4|8032|
|5|8050|
|6|8032|
|7|8050|

如需每個連線能力值所支援之 Hadoop 散發和版本的完整清單，請參閱 [PolyBase 連線能力設定 (TRANSACT-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。
  
> [!IMPORTANT]  
>  RESOURCE_MANAGER_LOCATION 值是一個字串，而且在您建立外部資料來源時不會經過驗證。 輸入不正確的值可能會導致之後在存取位置時產生延遲。  
  
 Hadoop 範例：  
  
-   Windows 上的 Hortonworks HDP 2.0、2.1、2.2、 2.3：   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
-   Windows 上的 Hortonworks HDP 1.3：   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Linux 上的 Hortonworks HDP 2.0、2.1、2.2、2.3：   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8050'  
    ```  
  
-   Linux 上的 Hortonworks HDP 1.3：   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Linux 上的 Cloudera 4.3：   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8021'  
    ```  
  
-   Linux 上的 Cloudera 5.1 - 5.11：   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
 CREDENTIAL = *credential_name*  
 指定資料庫範圍的認證，以便向外部資料來源進行驗證。 如需範例，請參閱 [C. 建立 Azure Blob 儲存體外部資料來源](../../t-sql/statements/create-external-data-source-transact-sql.md#credential)。 若要建立認證，請參閱 [CREATE CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-credential-transact-sql.md)。 請注意，允許匿名存取的公用資料集不需要 CREDENTIAL。 
  
 DATABASE_NAME = *'QueryDatabaseName'*  
 當作分區對應管理員 (適用於 SHARD_MAP_MANAGER) 或遠端資料庫 (適用於 RDBMS) 運作之資料庫的名稱。  
  
 SHARD_MAP_NAME = *'ShardMapName'*  
 僅適用於 SHARD_MAP_MANAGER。 分區對應的名稱。 如需有關建立分區對應的詳細資訊，請參閱[彈性資料庫查詢入門](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)  
  
## <a name="polybase-specific-notes"></a>PolyBase 專屬附註  
如需支援之外部資料來源的完整清單，請參閱 [PolyBase 連線能力設定 (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。

 若要使用 PolyBase，您必須建立以下三個物件：  
  
-   外部資料來源。  
  
-   外部檔案格式，以及  
  
-   參考外部資料來源和外部檔案格式的外部資料表。  
  
## <a name="permissions"></a>Permissions  
 在 SQL DW、SQL Server、APS 2016 和 SQL DB 中，需要有對資料庫的 CONTROL 權限。

> [!IMPORTANT]  
>  在舊版的 PDW 中，建立外部資料來源需要有 ALTER ANY EXTERNAL DATA SOURCE 權限。
  
  
## <a name="error-handling"></a>錯誤處理  
 如果外部 Hadoop 資料來源對於已定義的 RESOURCE_MANAGER_LOCATION 不一致，將會發生執行階段錯誤。 也就是說，您無法指定兩個參考相同 Hadoop 叢集，然後只為其中一個提供資源管理員位置的外部資料來源。  
  
 SQL 引擎在建立外部資料來源物件時，不會驗證外部資料來源是否存在。 如果資料來源在執行查詢期間不存在，將會發生錯誤。  
  
## <a name="general-remarks"></a>一般備註  
針對 Polybase，外部資料來源在 SQL Server 和 SQL 資料倉儲的資料庫範圍內。 在平行處理資料倉儲中則在伺服器範圍內。
  
針對 Polybase，當 RESOURCE_MANAGER_LOCATION 或 JOB_TRACKER_LOCATION 已定義時，查詢最佳化工具將會考慮在外部 Hadoop 來源上起始對應化簡作業，然後下推計算，以最佳化每個查詢。 這完全是以成本為基礎的決策。  

為確保在 Hadoop NameNode 容錯移轉時能成功進行 PolyBase 查詢，請考慮使用虛擬 IP 位址作為 Hadoop 叢集的 NameNode。 如果您不使用虛擬 IP 位址作為 Hadoop NameNode，Hadoop NameNode 發生容錯移轉時，您必須使用 ALTER EXTERNAL DATA SOURCE 物件指向新位置。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 在相同 Hadoop 叢集位置上定義的所有資料來源都必須為 RESOURCE_MANAGER_LOCATION 或 JOB_TRACKER_LOCATION 使用相同的設定。 如果有不一致的情形，將會發生執行階段錯誤。  
  
 如果 Hadoop 叢集是使用名稱設定的，而且外部資料來源使用 IP 位址作為叢集位置，則在使用資料來源時，PolyBase 必須仍然可以解析叢集名稱。 若要解析名稱，您必須啟用 DNS 轉寄站。  
  
## <a name="locking"></a>鎖定  
 在 EXTERNAL DATA SOURCE 物件上取得共用鎖定。  
  
##  <a name="examples"></a> 範例：SQL Server 2016  
  
### <a name="a-create-external-data-source-to-reference-hadoop"></a>A. 建立參考 Hadoop 的外部資料來源  
若要建立參考 Hortonworks 或 Cloudera Hadoop 叢集的外部資料來源，請指定 Hadoop Namenode 的電腦名稱或 IP 位址與連接埠。  
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8050'
);

```  
  
### <a name="b-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>B. 在已啟用下推的情況下，建立參考 Hadoop 的外部資料來源  
指定 RESOURCE_MANAGER_LOCATION 選項，以便對適用於 PolyBase 查詢的 Hadoop 啟用下推計算。 啟用之後，PolyBase 會使用以成本為基礎的決策來判斷應該將查詢計算推送到 Hadoop，還是應該移動所有資料來處理 SQL Server 中的查詢。
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
);

```
  
###  <a name="credential"></a> C. 建立參考由 Kerberos 保護之 Hadoop 的外部資料來源  
若要確認 Hadoop 叢集是否由 Kerberos 保護，請檢查 Hadoop core-site.xml 中 hadoop.security.authentication 屬性的值。 若要參考由 Kerberos 保護的 Hadoop 叢集，您必須指定資料庫範圍的認證，其中包含您的 Kerberos 使用者名稱與密碼。 資料庫主要金鑰用來加密資料庫範圍的認證密碼。 
  
```sql  
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Kerberos user name and password.
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1 
WITH IDENTITY = '<hadoop_user_name>', 
SECRET = '<hadoop_password>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (
    TYPE = HADOOP, 
    LOCATION = 'hdfs://10.10.10.10:8050', 
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050', 
    CREDENTIAL = HadoopUser1
);
```

### <a name="d-create-external-data-source-to-reference-azure-blob-storage"></a>D. 建立參考 Azure Blob 儲存體的外部資料來源
若要建立參考 Azure Blob 儲存體容器的外部資料來源，請指定 Azure Blob 儲存體 URI 和資料庫範圍的認證，其中包含您的 Azure 儲存體帳戶金鑰。

在此範例中，外部資料來源是稱為 myaccount 之 Azure 儲存體帳戶底下，稱為 dailylogs 的 Azure Blob 儲存體容器。 Azure 儲存體外部資料來源僅供資料傳輸使用，而且不支援述詞下推。

此範例示範如何建立資料庫範圍的認證，以便向 Azure 儲存體進行驗證。 在資料庫認證密碼中指定 Azure 儲存體帳戶金鑰。 在資料庫範圍的認證身分識別中指定任何字串，系統不會使用該字串向 Azure 儲存體進行驗證。 接著，在建立外部資料來源的陳述式中會使用該認證。

```
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential 
WITH IDENTITY = 'myaccount', 
SECRET = '<azure_storage_account_key>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
    TYPE = BLOB_STORAGE, 
    LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/',
    CREDENTIAL = AzureStorageCredential
);
```

## <a name="examples-azure-sql-database"></a>範例：Azure SQL Database

### <a name="e-create-a-shard-map-manager-external-data-source"></a>E. 建立分區對應管理員外部資料來源
若要建立參考 SHARD_MAP_MANAGER 的外部資料來源，請指定在 Azure SQL Database 中裝載分區對應管理員，或在 Azure 虛擬機器上裝載 SQL Server 資料庫的邏輯伺服器名稱。

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc 
WITH (
    TYPE = SHARD_MAP_MANAGER,
    LOCATION = '<server_name>.database.windows.net',
    DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
    CREDENTIAL = ElasticDBQueryCred,
    SHARD_MAP_NAME = 'CustomerIDShardMap'
);
```

### <a name="f-create-an-rdbms-external-data-source"></a>F. 建立 RDBMS 外部資料來源
若要建立參考 RDBMS 的外部資料來源，請在 Azure SQL Database 中指定遠端資料庫的邏輯伺服器名稱。

```sql
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

CREATE DATABASE SCOPED CREDENTIAL SQL_Credential  
WITH IDENTITY = '<username>',
SECRET = '<password>';

CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc 
WITH (
    TYPE = RDBMS, 
    LOCATION = '<server_name>.database.windows.net', 
    DATABASE_NAME = 'Customers', 
    CREDENTIAL = SQL_Credential 
);
```

## <a name="examples-azure-sql-data-warehouse"></a>範例：Azure SQL 資料倉儲

### <a name="g-create-external-data-source-to-reference-azure-data-lake-store"></a>G. 建立參考 Azure Data Lake Store 的外部資料來源
Azure Data Lake Store 連線能力是以您的 ADLS URI 與您的 Azure Acitve Directory 應用程式的服務主體為基礎。 說明如何建立此應用程式的文件可以在[使用 Azure Active Directory 的 Data Lake Store 驗證](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)中找到。

```sql
-- If you do not have a Master Key on your DW you will need to create one.
CREATE MASTER KEY

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLUser 
WITH IDENTITY = '<clientID>@<OAuth2.0TokenEndPoint>',
SECRET = '<KEY>' ;


CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (TYPE = HADOOP,
      LOCATION = '<ADLS URI>'
)
```



## <a name="examples-parallel-data-warehouse"></a>範例：平行處理資料倉儲

### <a name="h-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>H. 在已啟用下推的情況下，建立參考 Hadoop 的外部資料來源
指定 JOB_TRACKER_LOCATION 選項，以便對適用於 PolyBase 查詢的 Hadoop 啟用下推計算。 啟用之後，PolyBase 會使用以成本為基礎的決策來判斷應該將查詢計算推送到 Hadoop，還是應該移動所有資料來處理 SQL Server 中的查詢。 

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    JOB_TRACKER_LOCATION = '10.10.10.10:8050'
);
```

### <a name="i-create-external-data-source-to-reference-azure-blob-storage"></a>I. 建立參考 Azure Blob 儲存體的外部資料來源
若要建立參考 Azure Blob 儲存體容器的外部資料來源，請指定 Azure Blob 儲存體 URI 作為外部資料來源 LOCATION。 將 Azure 儲存體帳戶金鑰加入至 PDW core-site.xml 檔案以進行驗證。

在此範例中，外部資料來源是稱為 myaccount 之 Azure 儲存體帳戶底下，稱為 dailylogs 的 Azure Blob 儲存體容器。 Azure 儲存體外部資料來源僅供資料傳輸使用，而且不支援述詞下推。

```sql
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
        TYPE = HADOOP, 
        LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'
);
```

## <a name="examples-bulk-operations"></a>範例：大量作業   
### <a name="j-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>J. 針對從 Azure Blob 儲存體擷取資料的大量作業，建立外部資料來源。   
**適用於：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。   
針對使用 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) 或 [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) 的大量作業，請使用下列資料來源。 使用的認證必須利用 `SHARED ACCESS SIGNATURE` 來建立，以作為身分識別。 如需共用存取簽章的詳細資訊，請參閱[使用共用存取簽章 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。   
```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = AccessAzureInvoices
    );   
```   
若要查看使用中的這個範例，請參閱 [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)。
  
## <a name="see-also"></a>另請參閱
[ALTER EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/alter-external-data-source-transact-sql.md)  
[CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
[CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
[CREATE EXTERNAL TABLE AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
[CREATE TABLE AS SELECT &#40;Azure SQL 資料倉儲&#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
[sys.external_data_sources (Transact-SQL)](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)  
  
  

