---
title: "建立外部資料來源 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL DATA SOURCE
- CREATE_EXTERNAL_DATA_SOURCE
dev_langs: TSQL
helpviewer_keywords:
- External
- External, data source
- PolyBase, create data source
ms.assetid: 75d8a220-0f4d-4d91-8ba4-9d852b945509
caps.latest.revision: "58"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 283971bbd1bfe04b26860f56601c315ac5244717
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="create-external-data-source-transact-sql"></a>建立外部資料來源 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  建立 PolyBase、 彈性資料庫查詢或 Azure Blob 儲存體的外部資料來源。 根據這種情況，語法大幅不同。 Polybase 建立資料來源無法使用彈性資料庫查詢。  同樣地，建立彈性資料庫查詢的資料來源無法用於 PolyBase，依此類推。 
  
> [!NOTE]  
>  PolyBase，SQL Server 2016、 Azure SQL 資料倉儲、 且平行處理資料倉儲上才支援。 只有 Azure SQL Database v12 或更新版本支援彈性資料庫查詢。  
  
 PolyBase 的情況下，外部資料來源是 Hadoop 檔案系統 (HDFS)、 Azure 儲存體 blob 容器或 Azure 資料湖存放區。 如需詳細資訊，請參閱 [開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)。  
  
 彈性資料庫查詢的情況下，外部來源，請為分區對應管理員 （在 Azure SQL Database) 或 （在 Azure SQL Database) 的遠端資料庫。  使用[sp_execute_remote &#40;Azure SQL Database &#41;](../../relational-databases/system-stored-procedures/sp-execute-remote-azure-sql-database.md)後建立外部資料來源。 如需詳細資訊，請參閱[彈性資料庫查詢](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)。  

  Azure Blob 儲存體的外部資料來源支援`BULK INSERT`和`OPENROWSET`語法，以及不同於 PolyBase 的 Azure Blob 儲存體。
    
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
 *data_source_name*指定使用者定義資料來源名稱。 必須在 SQL Server、 Azure SQL Database 和 Azure SQL 資料倉儲資料庫內的唯一名稱。 名稱必須是唯一平行處理資料倉儲伺服器。
  
 類型 = [HADOOP |對包含 SHARD_MAP_MANAGER |RDBMS |BLOB_STORAGE]  
 指定資料來源類型。 外部資料來源時，Hadoop，使用 HADOOP 或 Azure 儲存體 blob 的 Hadoop。 Azure SQL Database 上建立分區化的彈性資料庫查詢外部資料來源時，請使用對包含 SHARD_MAP_MANAGER。 使用外部資料來源的 RDBMS 對 Azure SQL database 的彈性資料庫查詢的跨資料庫查詢。  執行大量作業使用時，使用 BLOB_STORAGE [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)或[OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)與[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。
  
位置 = \<location_path > **HADOOP**    
HADOOP，針對指定的 Hadoop 叢集的 Uniform Resource Indicator (URI)。  
`LOCATION = 'hdfs:\/\/*NameNode\_URI*\[:*port*\]'`  
NameNode_URI: 電腦名稱或 IP 位址，Hadoop 叢集 Namenode。  
連接埠： Namenode IPC 連接埠。 這會指示 Hadoop 中的 「 fs.default.name 」 組態參數。 如果未指定值，預設將會使用 8020。  
範例：`LOCATION = 'hdfs://10.10.10.10:8020'`

Azure blob 儲存體的 Hadoop，指定用於連接到 Azure blob 儲存體 URI。  
`LOCATION = 'wasb[s]://container@account_name.blob.core.windows.net'`  
wasb [s]: 指定的 Azure blob 儲存體通訊協定。 [S] 是選擇性，指定安全的 SSL 連接，安全地透過 SSL 通訊協定加密傳送從 SQL Server 的資料。 我們強烈建議您使用 'wasbs'，而不是 'wasb'。 請注意位置可以使用 asv [s]，而不是 wasb [s]。 Asv [s] 語法已經過時，未來版本將移除。  
容器： 指定的 Azure blob 儲存體容器名稱。 若要指定網域的儲存體帳戶的根容器，請使用網域名稱而不是容器名稱。 根容器是唯讀的所以無法將資料寫入回至容器。  
account_name: Azure 儲存體帳戶的完整的網域名稱 (FQDN)。  
範例：`LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'`

Azure 資料湖存放區位置會指定用於連接到您的 Azure Data Lake Store URI。



**對包含 SHARD_MAP_MANAGER**   
 對包含 SHARD_MAP_MANAGER，指定裝載分區對應管理員，Azure SQL Database 或 Azure 的虛擬機器上的 SQL Server 資料庫中的邏輯伺服器名稱。
 
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

如需逐步教學課程，請參閱[入門 （水平資料分割） 的分區化的彈性查詢](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)。
  
**RDBMS**   
RDBMS，Azure SQL Database 中指定遠端資料庫的邏輯伺服器名稱。  

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
  
如需 RDBMS 的逐步教學課程，請參閱[入門 （垂直資料分割） 的跨資料庫查詢](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started-vertical/)。  

**BLOB_STORAGE**   
針對大量作業，`LOCATION`必須是有效的 Azure Blob 儲存體和容器的 URL。 請不要將 **/** 、 檔案名稱，或共用存取簽章參數的結尾`LOCATION`URL。   
使用的認證必須使用可建立`SHARED ACCESS SIGNATURE`作為身分識別。 如需共用存取簽章的詳細資訊，請參閱[使用共用存取簽章 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。 如需存取 blob 儲存體的範例，請參閱範例 F [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)。 

  
 RESOURCE_MANAGER_LOCATION = '*ResourceManager_URI*[:*連接埠*]'  
 指定 Hadoop 資源管理員位置。 指定時，查詢最佳化工具可以做出成本型決策來前置處理資料的 PolyBase 查詢 Hadoop 的運算功能使用 MapReduce。 呼叫述詞下推，這可以大幅降低 Hadoop 與 SQL 之間傳送的資料磁碟區，因而改善查詢效能。  
  
 當未指定時，將計算推送到 Hadoop 已停用 PolyBase 查詢。  
 
如果未指定連接埠，預設值會判斷 'hadoop connectivity' 的組態中使用的目前設定。

|Hadoop 連接|預設資源管理員的連接埠|
|-------------------|-----------------------------|
|@shouldalert|50300|
|2|50300|
|3|8021|
|4|8032|
|5|8050|
|6|8032|
|7|8050|

如需 Hadoop 散發和版本支援的每個連線值的完整清單，請參閱[PolyBase 連線組態 (TRANSACT-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。
  
> [!IMPORTANT]  
>  RESOURCE_MANAGER_LOCATION 值是字串，而且不會驗證當您建立外部資料來源。 輸入不正確的值可能會導致未來產生延遲存取的位置時。  
  
 Hadoop 範例：  
  
-   Hortonworks HDP 2.0、 2.1、 2.2。 2.3 在 Windows 上：   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
-   1.3 在 Windows 上的 Hortonworks HDP:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   Hortonworks HDP 2.0、 2.1、 2.2、 Linux 2.3 上：   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8050'  
    ```  
  
-   在 Linux 上的 Hortonworks HDP 1.3:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:50300'  
    ```  
  
-   在 Linux 上的 Cloudera 4.3:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8021'  
    ```  
  
-   在 Linux 上的 Cloudera 5.1 5.11:   
    ```  
    RESOURCE_MANAGER_LOCATION = 'ResourceManager_URI:8032'  
    ```  
  
 認證 = *credential_name*  
 指定資料庫範圍認證來驗證外部資料來源。 如需範例，請參閱[C.建立 Azure blob 儲存體外部資料來源](../../t-sql/statements/create-external-data-source-transact-sql.md#credential)。 若要建立的認證，請參閱[CREATE CREDENTIAL (TRANSACT-SQL)](../../t-sql/statements/create-credential-transact-sql.md)。 請注意，認證並不需要針對公用允許匿名存取的資料集。 
  
 DATABASE_NAME = *'QueryDatabaseName'*  
 （適用於 RDBMS) 資料庫當做 （適用於對包含 SHARD_MAP_MANAGER) 分區對應管理員或遠端資料庫的名稱。  
  
 SHARD_MAP_NAME = *'ShardMapName'*  
 如對包含 SHARD_MAP_MANAGER 只。 分區對應名稱。 如需建立分區對應的詳細資訊，請參閱[入門彈性資料庫查詢](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-getting-started/)  
  
## <a name="polybase-specific-notes"></a>PolyBase 特定注意事項  
如需支援的外部資料來源的完整清單，請參閱[PolyBase 連線組態 (TRANSACT-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。

 若要使用 PolyBase，您必須建立這三個物件：  
  
-   外部資料來源。  
  
-   外部檔案格式，並  
  
-   外部資料表所參考的外部資料來源和外部檔案格式。  
  
## <a name="permissions"></a>Permissions  
 需要 CONTROL 權限在 SQL DW、 SQL Server、 AP 2016 和 SQL 資料庫的資料庫。

> [!IMPORTANT]  
>  在舊版本的 PDW 中，建立外部資料來源需要 ALTER ANY EXTERNAL DATA SOURCE 權限。
  
  
## <a name="error-handling"></a>錯誤處理  
 如果外部的 Hadoop 資料來源不一致，讓 RESOURCE_MANAGER_LOCATION 定義，就會發生執行階段錯誤。 也就是說，您不能指定兩個參考相同的 Hadoop 叢集，然後提供資源管理員位置的其中一個，不能用於其他的外部資料來源。  
  
 SQL 引擎不會驗證外部資料來源存在，它會建立外部資料來源物件時。 如果資料來源不存在執行查詢時，會發生錯誤。  
  
## <a name="general-remarks"></a>一般備註  
Polybase，外部資料來源為資料庫範圍的 SQL Server 和 SQL 資料倉儲中。 平行處理資料倉儲是伺服器範圍。
  
Polybase，RESOURCE_MANAGER_LOCATION 或 JOB_TRACKER_LOCATION 定義時，查詢最佳化工具會考慮最佳化每個查詢藉由初始化對應減少上作業 Hadoop 的外部來源，以及將計算下推。 這完全是成本型決策。  

若要確保成功的 PolyBase 查詢 Hadoop NameNode 容錯移轉時，請考慮虛擬 IP 位址用於 NameNode Hadoop 叢集。 如果您不使用 Hadoop NameNode 虛擬 IP 位址，Hadoop NameNode 容錯移轉發生您必須修改外部資料來源物件，以指向新位置。  
  
## <a name="limitations-and-restrictions"></a>限制事項  
 在相同的 Hadoop 叢集位置上所定義的所有資料來源必須都使用相同的設定 RESOURCE_MANAGER_LOCATION 或 JOB_TRACKER_LOCATION。 如果有不一致的情形，就會發生執行階段錯誤。  
  
 如果 Hadoop 叢集設定的名稱，而且針對叢集中位置，外部資料來源使用的 IP 位址，PolyBase 必須仍然可以使用資料來源時，解析叢集名稱。 若要解析名稱，您必須啟用 DNS 轉寄站。  
  
## <a name="locking"></a>鎖定  
 外部資料來源物件上採用共用的鎖定。  
  
##  <a name="examples"></a>範例： SQL Server 2016  
  
### <a name="a-create-external-data-source-to-reference-hadoop"></a>A. 建立參考 Hadoop 的外部資料來源  
若要建立外部資料來源參考 Hortonworks 或 Cloudera Hadoop 叢集，請指定電腦名稱或 IP 位址的 Hadoop Namenode 和連接埠。  
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8050'
);

```  
  
### <a name="b-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>B. 建立參考 Hadoop 的外部資料來源使用啟用的下推  
指定要啟用針對 PolyBase 查詢的下推計算至 Hadoop RESOURCE_MANAGER_LOCATION 選項。 啟用之後，PolyBase 會用來判斷是否應該查詢計算推送到 Hadoop 或所有資料應都移到處理 SQL Server 中的查詢成本型決策。
  
```sql  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    RESOURCE_MANAGER_LOCATION = '10.10.10.10:8050'
);

```
  
###  <a name="credential"></a> C. 建立參考 Kerberos 保護的 Hadoop 的外部資料來源  
若要確認是否 Hadoop 叢集 Kerberos 保護，請檢查在 Hadoop core-site.xml hadoop.security.authentication 屬性的值。 若要參考由 Kerberos 保護的 Hadoop 叢集，您必須指定包含您的 Kerberos 使用者名稱和密碼的資料庫範圍認證。 資料庫主要金鑰用來加密的資料庫範圍的認證的密碼。 
  
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

### <a name="d-create-external-data-source-to-reference-azure-blob-storage"></a>D. 建立參考 Azure blob 儲存體的外部資料來源
若要建立外部資料來源來參考您的 Azure blob 儲存體容器，指定 Azure blob 儲存體 URI 和包含您的 Azure 儲存體帳戶金鑰的資料庫範圍認證。

在此範例中，外部資料來源會呼叫 Azure 儲存體帳戶命名為 myaccount dailylogs Azure blob 儲存體容器。 外部資料來源是資料傳輸; 僅限 Azure 儲存體並不支援述詞下推。

這個範例示範如何建立資料庫範圍認證進行驗證至 Azure 儲存體。 指定 Azure 儲存體帳戶金鑰在資料庫認證密碼。 指定任何字串，在資料庫範圍認證識別時，它將不會用來驗證 Azure 儲存體。 然後，建立外部資料來源的陳述式中使用的認證。

```
-- Create a database master key if one does not already exist, using your own password. This key is used to encrypt the credential secret in next step.
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';

-- Create a database scoped credential with Azure storage account key as the secret.
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential 
WITH IDENTITY = 'myaccount', 
SECRET = '<azure_storage_account_key>';

-- Create an external data source with CREDENTIAL option.
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
    TYPE = HADOOP, 
    LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/',
    CREDENTIAL = AzureStorageCredential
);
```

## <a name="examples-azure-sql-database"></a>範例： Azure SQL Database

### <a name="e-create-a-shard-map-manager-external-data-source"></a>E. 建立分區對應管理員外部資料來源
若要建立外部資料來源參考對包含 SHARD_MAP_MANAGER，指定裝載分區對應管理員，Azure SQL Database 或 Azure 的虛擬機器上的 SQL Server 資料庫中的邏輯伺服器名稱。

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
若要建立外部資料來源參考 RDBMS，指定 Azure SQL Database 中的遠端資料庫的邏輯伺服器名稱。

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

## <a name="examples-azure-sql-data-warehouse"></a>範例： Azure SQL 資料倉儲

### <a name="g-create-external-data-source-to-reference-azure-data-lake-store"></a>G. 建立參考 Azure Data Lake Store 的外部資料來源
Azure Data lake Store 連線根據 ADLS URI 和 Azure 啟用目錄應用程式的服務主體。 建立此應用程式的文件，請參閱[使用 Active Directory 資料湖存放區驗證](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)。

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



## <a name="examples-parallel-data-warehouse"></a>範例： Parallel Data Warehouse

### <a name="h-create-external-data-source-to-reference-hadoop-with-pushdown-enabled"></a>H. 建立參考 Hadoop 的外部資料來源使用啟用的下推
指定要啟用針對 PolyBase 查詢的下推計算至 Hadoop JOB_TRACKER_LOCATION 選項。 啟用之後，PolyBase 會用來判斷是否應該查詢計算推送到 Hadoop 或所有資料應都移到處理 SQL Server 中的查詢成本型決策。 

```sql
CREATE EXTERNAL DATA SOURCE MyHadoopCluster
WITH (
    TYPE = HADOOP,
    LOCATION = 'hdfs://10.10.10.10:8020',
    JOB_TRACKER_LOCATION = '10.10.10.10:8050'
);
```

### <a name="i-create-external-data-source-to-reference-azure-blob-storage"></a>I. 建立參考 Azure blob 儲存體的外部資料來源
若要建立外部資料來源，以參考您的 Azure blob 儲存體容器，指定 Azure blob 儲存體 URI 與外部資料來源位置。 驗證的 PDW core-site.xml 檔案中加入您的 Azure 儲存體帳戶金鑰。

在此範例中，外部資料來源會呼叫 Azure 儲存體帳戶命名為 myaccount dailylogs Azure blob 儲存體容器。 Azure 儲存體的外部資料來源是只有資料傳輸，並不支援述詞下推。

```sql
CREATE EXTERNAL DATA SOURCE MyAzureStorage WITH (
        TYPE = HADOOP, 
        LOCATION = 'wasbs://dailylogs@myaccount.blob.core.windows.net/'
);
```

## <a name="examples-bulk-operations"></a>範例： 大量作業   
### <a name="j-create-an-external-data-source-for-bulk-operations-retrieving-data-from-azure-blob-storage"></a>J. 建立從 Azure Blob 儲存體擷取資料的大量作業的外部資料來源。   
**適用於：** [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]。   
使用下列資料來源的大量作業使用[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)或[OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md)。 使用的認證必須使用可建立`SHARED ACCESS SIGNATURE`作為身分識別。 如需共用存取簽章的詳細資訊，請參閱[使用共用存取簽章 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)。   
```sql
CREATE EXTERNAL DATA SOURCE MyAzureInvoices
    WITH  (
        TYPE = BLOB_STORAGE,
        LOCATION = 'https://newinvoices.blob.core.windows.net/week3',
        CREDENTIAL = AccessAzureInvoices
    );   
```   
若要查看在使用這個範例，請參閱[BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md)。
  
## <a name="see-also"></a>請參閱
[改變外部資料來源 (TRANSACT-SQL)](../../t-sql/statements/alter-external-data-source-transact-sql.md)  
[CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
[CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)   
[建立外部 TABLE AS SELECT &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
[建立 TABLE AS SELECT &#40;Azure SQL 資料倉儲 &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
[sys.external_data_sources (TRANSACT-SQL)](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)  
  
  

