---
title: 存取外部資料：Azure Blob 儲存體 - PolyBase
ms.date: 12/13/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.custom: seo-dt-2019, seo-lt-2019
ms.openlocfilehash: 680a8e28e807505f4824524a686f244621cb3dd0
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "75258687"
---
# <a name="configure-polybase-to-access-external-data-in-azure-blob-storage"></a>設定 PolyBase 存取 Azure Blob 儲存體中的外部資料

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何在 SQL Server 執行個體上使用 PolyBase 來查詢位於 Azure Blob 儲存體中的外部資料。

## <a name="prerequisites"></a>Prerequisites

如果您尚未安裝 PolyBase，請參閱 [PolyBase 安裝](polybase-installation.md)。 安裝文章說明必要條件。

### <a name="configure-azure-blob-storage-connectivity"></a>設定 Azure Blob 儲存體連線

首先，設定 SQL Server PolyBase 使用 Azure Blob 儲存體。

1. 執行 'hadoop connectivity' 設定為 Azure Blob 儲存體提供者的 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。 若要尋找提供者的值，請參閱 [PolyBase 連線設定](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。 根據預設，Hadoop 連線設定為 7。

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. 您必須使用 **services.msc** 重新啟動 SQL Server。 重新啟動 SQL Server 時，會重新啟動下列服務︰  

   - SQL Server PolyBase Data Movement Service  
   - SQL Server PolyBase Engine  
  
   ![在 services.msc 中停止和啟動 PolyBase 服務](../../relational-databases/polybase/media/polybase-stop-start.png "在 services.msc 中停止和啟動 PolyBase 服務")  
  
## <a name="configure-an-external-table"></a>設定外部資料表

若要查詢 Hadoop 資料來源中的資料，您必須定義要在 Transact-SQL 查詢中使用的外部資料表。 下列步驟描述如何設定外部資料表。

1. 在資料庫上建立主要金鑰。 這是加密認證祕密的必要項目。

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

1. 建立 Azure Blob 儲存體的資料庫範圍認證。

   ```sql
   -- IDENTITY: any string (this is not used for authentication to Azure storage).  
   -- SECRET: your Azure storage account key.  
   CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
   WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';
   ```

1. 使用 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) 建立外部資料來源。

   ```sql
   -- LOCATION:  Azure account storage account name and blob container name.  
   -- CREDENTIAL: The database scoped credential created above.  
   CREATE EXTERNAL DATA SOURCE AzureStorage with (  
         TYPE = HADOOP,
         LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
         CREDENTIAL = AzureStorageCredential  
   );  
   ```

1. 使用 [CREATE EXTERNAL FILE FORMAT](../../t-sql/statements/create-external-file-format-transact-sql.md) 建立外部檔案格式。

   ```sql
   -- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE))  
   ```

1. 使用 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 建立外部資料表以指向 Azure 儲存體中所儲存的資料。 在此範例中，外部資料會包含車輛感應器資料。

   ```sql
   -- LOCATION: path to file or directory that contains the data (relative to HDFS root).  
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

1. 在外部資料表上建立統計資料。

   ```sql
   CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
   ```

## <a name="polybase-queries"></a>PolyBase 查詢

有三個 PolyBase 適用的函數︰  
  
- 針對外部資料表進行的臨機操作查詢。  
- 匯入資料。  
- 匯出資料。  

下列查詢會提供具有虛構車輛感應器資料的範例。

### <a name="ad-hoc-queries"></a>臨機操作查詢  

下列臨機操作查詢會聯結與 Hadoop 資料的關聯式。 它會選取開車速度超過 35 mph 的客戶，並聯結 SQL Server 中所儲存的結構化客戶資料與 Hadoop 中儲存的車輛感應器資料。  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
OPTION (FORCE EXTERNALPUSHDOWN);   -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
```  

### <a name="importing-data"></a>匯入資料  

下列查詢會將外部資料匯入至 SQL Server。 此範例會將快速驅動程式的資料匯入至 SQL Server，以執行更深入的分析。 為了改善效能，它利用資料行存放區技術。  

```sql
SELECT DISTINCT
      Insured_Customers.FirstName, Insured_Customers.LastName,   
      Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
INTO Fast_Customers from Insured_Customers INNER JOIN   
(  
      SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
ORDER BY YearlyIncome  
  
CREATE CLUSTERED COLUMNSTORE INDEX CCI_FastCustomers ON Fast_Customers;  
```  

### <a name="exporting-data"></a>匯出資料  

下列查詢會將資料從 SQL Server 匯出至 Azure Blob 儲存體。 若要這樣做，您需要先啟用 PolyBase 匯出。 先建立目的地的外部資料表，再將資料匯出至其中。

```sql
-- Enable INSERT into external table  
sp_configure 'allow polybase export', 1;  
reconfigure  
  
-- Create an external table.
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] (  
      [FirstName] char(25) NOT NULL,
      [LastName] char(25) NOT NULL,
      [YearlyIncome] float NULL,
      [MaritalStatus] char(1) NOT NULL  
)  
WITH (  
      LOCATION='/old_data/2009/customerdata',  
      DATA_SOURCE = HadoopHDP2,  
      FILE_FORMAT = TextFileFormat,  
      REJECT_TYPE = VALUE,  
      REJECT_VALUE = 0  
);  

-- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
INSERT INTO dbo.FastCustomer2009  
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  

## <a name="view-polybase-objects-in-ssms"></a>在 SSMS 中檢視 PolyBase 物件  

在 SSMS 中，外部資料表會顯示在個別的資料夾 [外部資料表]  中。 外部資料來源和外部檔案格式會在 [外部資源]  下方的子資料夾中。  
  
![SSMS 中的 PolyBase 物件](media/polybase-management.png)  

## <a name="next-steps"></a>後續步驟

在下列文章中，探索更多使用和監視 PolyBase 的方式：

[PolyBase 向外延展群組](../../relational-databases/polybase/polybase-scale-out-groups.md)。  
[PolyBase 疑難排解](polybase-troubleshooting.md).  
