---
title: PolyBase T-SQL 物件 | Microsoft Docs
ms.custom: ''
ms.date: 08/15/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: polybase
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- PolyBase, fundamentals
- PolyBase, SQL statements
- PolyBase, SQL objects
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d2c8dd55adf32bb835113073c79fcfcc00003371
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/12/2018
ms.locfileid: "38983540"
---
# <a name="polybase-t-sql-objects"></a>PolyBase T-SQL 物件
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  若要使用 PolyBase，您必須建立外部資料表來參考您的外部資料。  
  
 [CREATE DATABASE SCOPED CREDENTIAL &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)  
  
 [CREATE EXTERNAL DATA SOURCE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
 [CREATE EXTERNAL FILE FORMAT &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
 [CREATE EXTERNAL TABLE &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
 [CREATE STATISTICS &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)  
 
> [!NOTE]
>  SQL Server 2016 的 PolyBase 僅支援 Windows 使用者。 如果您嘗試使用 SQL 使用者查詢 PolyBase 外部資料表，則查詢會失敗。

## <a name="prerequisites"></a>Prerequisites  
 設定 PolyBase。 請參閱 [PolyBase configuration](../../relational-databases/polybase/polybase-configuration.md)。  
  
## <a name="create-external-tables-for-hadoop"></a>建立 Hadoop 的外部資料表
適用對象：SQL Server (自 2016 版開始)、平行處理資料倉儲
  
 **1.建立資料庫範圍認證**  
  
 由 Kerberos 保護的 Hadoop 叢集才需要此步驟。  
  
```sql  
-- Create a master key on the database.  
-- Required to encrypt the credential secret.  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
  
-- Create a database scoped credential  for Kerberos-secured Hadoop clusters.  
-- IDENTITY: the Kerberos user name.  
-- SECRET: the Kerberos password  
  
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1   
WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
  
```  
  
 **2.建立外部資料來源**  
  
```sql  
-- Create an external data source.  
-- LOCATION (Required) : Hadoop Name Node IP address and port.  
-- RESOURCE MANAGER LOCATION (Optional): Hadoop Resource Manager location to enable pushdown computation.  
-- CREDENTIAL (Optional):  the database scoped credential, created above.  
  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (  
        TYPE = HADOOP,   
        LOCATION ='hdfs://10.xxx.xx.xxx:xxxx',   
        RESOURCE_MANAGER_LOCATION = '10.xxx.xx.xxx:xxxx',   
        CREDENTIAL = HadoopUser1      
);  
  
```  
  
 **3.建立外部檔案格式**  
  
```sql  
-- Create an external file format.  
-- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).  
  
CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
        FORMAT_TYPE = DELIMITEDTEXT,   
        FORMAT_OPTIONS (FIELD_TERMINATOR ='|',   
                USE_TYPE_DEFAULT = TRUE)  
  
```  
  
 **4.建立外部資料表**  
  
```sql  
-- Create an external table pointing to data stored in Hadoop.  
-- LOCATION: path to file or directory that contains the data (relative to HDFS root).  
  
CREATE EXTERNAL TABLE [dbo].[CarSensor_Data] (  
        [SensorKey] int NOT NULL,   
        [CustomerKey] int NOT NULL,   
        [GeographyKey] int NULL,   
        [Speed] float NOT NULL,   
        [YearMeasured] int NOT NULL  
)  
WITH (LOCATION='/Demo/',   
        DATA_SOURCE = MyHadoopCluster,  
        FILE_FORMAT = TextFileFormat  
);  
  
```  
  
 **5.建立統計資料**  
  
```sql  
-- Create statistics on an external table.   
CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
  
```  
  
## <a name="create-external-tables-for-azure-blob-storage"></a>建立 Azure Blob 儲存體的外部資料表  
適用對象：SQL Server (自 2016 版開始)、Azure SQL 資料倉儲、平行處理資料倉儲

 **1.建立資料庫範圍認證**  
  
```sql  
-- Create a master key on the database.  
-- Required to encrypt the credential secret.  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
  
-- Create a database scoped credential  for Azure blob storage.  
-- IDENTITY: any string (this is not used for authentication to Azure storage).  
-- SECRET: your Azure storage account key.  
  
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential   
WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';  
  
```  
  
 **2.建立外部資料來源**  
  
```sql  
-- Create an external data source.  
-- LOCATION:  Azure account storage account name and blob container name.  
-- CREDENTIAL: The database scoped credential created above.  
  
CREATE EXTERNAL DATA SOURCE AzureStorage with (  
        TYPE = HADOOP,   
        LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
        CREDENTIAL = AzureStorageCredential  
);  
  
```  
  
 **3.建立外部檔案格式**  
  
```sql  
-- Create an external file format.  
-- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).  
  
CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
        FORMAT_TYPE = DELIMITEDTEXT,   
        FORMAT_OPTIONS (FIELD_TERMINATOR ='|',   
                USE_TYPE_DEFAULT = TRUE)  
  
```  
  
 **4.建立外部資料表**  
  
```sql  
-- Create an external table pointing to data stored in Azure storage.  
-- LOCATION: path to a file or directory that contains the data (relative to the blob container).  
-- To point to all files under the blob container, use LOCATION='/'   
  
CREATE EXTERNAL TABLE [dbo].[CarSensor_Data] (  
        [SensorKey] int NOT NULL,   
        [CustomerKey] int NOT NULL,   
        [GeographyKey] int NULL,   
        [Speed] float NOT NULL,   
        [YearMeasured] int NOT NULL  
)  
WITH (LOCATION='/Demo/',   
        DATA_SOURCE = AzureStorage,  
        FILE_FORMAT = TextFileFormat  
);  
  
```  
  
 **5.建立統計資料**  
  
```sql  
-- Create statistics on an external table.   
CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
  
```  
 
## <a name="create-external-tables-for-azure-data-lake-store"></a>建立 Azure Data Lake Store 的外部資料表
適用對象：Azure SQL 資料倉儲

如需詳細資訊，請參閱[使用 Azure Data Lake Store 載入](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store)
 
 **1.建立資料庫範圍認證**   

```sql
-- Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.

CREATE MASTER KEY;

-- Create a database scoped credential
-- IDENTITY: Pass the client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADL_User
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>'
    ,SECRET = '<key>'
;
```  
  
 **2.建立外部資料來源**  
  
```sql  
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure Data Lake Store.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide the credential created in the previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalake.net,
    CREDENTIAL = AzureStorageCredential
);
```  
  
 **3.建立外部檔案格式**  
  
```sql  
-- FIELD_TERMINATOR: Marks the end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies the field terminator for data of type string in the text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

CREATE EXTERNAL FILE FORMAT TextFileFormat
WITH
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE
                    )
);
```  
  
 **4.建立外部資料表**  
  
```sql  
-- LOCATION: Folder under the ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object to use.
-- FILE_FORMAT: Specifies which File Format Object to use
-- REJECT_TYPE: Specifies how you want to deal with rejected rows. Either Value or percentage of the total
-- REJECT_VALUE: Sets the Reject value based on the reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;
```  
  
 **5.建立統計資料**  
  
```sql     
CREATE STATISTICS StatsForProduct on DimProduct_external(ProductKey)  
```  

## <a name="next-steps"></a>後續步驟  
 如需查詢的範例，請參閱 [PolyBase Queries](../../relational-databases/polybase/polybase-queries.md)(PolyBase 查詢)。  
  
## <a name="see-also"></a>另請參閱  
 [開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)   
 [PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)  
  
  
