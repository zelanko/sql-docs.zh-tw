---
title: 設定存取 Azure Blob 儲存體中的外部資料的 PolyBase |Microsoft Docs
description: 說明如何設定連接至外部 Hadoop 的平行處理資料倉儲的 PolyBase。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7bbf2dface759da63bd6b9845f4e62321b1cbe76
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63027519"
---
# <a name="configure-polybase-to-access-external-data-in-azure-blob-storage"></a>設定 PolyBase 以存取 Azure Blob 儲存體中的外部資料

本文說明如何使用 PolyBase 來查詢 Azure Blob 儲存體中的外部資料的 SQL Server 執行個體上。

> [!NOTE]
> AP 時，目前僅支援標準的一般用途 v1 本地備援 (LRS) Azure Blob 儲存體。

## <a name="prerequisites"></a>先決條件

 - 您的訂用帳戶中的 azure Blob 儲存體。
 - 在 Azure Blob 儲存體中建立容器。

### <a name="configure-azure-blob-storage-connectivity"></a>設定 Azure Blob 儲存體連線能力

首先，設定 AP，以使用 Azure Blob 儲存體。

1. 執行[sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 'hadoop connectivity' 設定為 Azure Blob 儲存體提供者使用。 若要尋找提供者的值，請參閱 [PolyBase 連線設定](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure Blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. 重新啟動使用服務狀態] 頁面上的 APS 地區[設備 Configuration Manager](launch-the-configuration-manager.md)。
  
## <a name="configure-an-external-table"></a>設定外部資料表

若要查詢您的 Azure Blob 儲存體中的資料，您必須定義在 TRANSACT-SQL 查詢中使用外部資料表。 下列步驟描述如何設定外部資料表。

1. 在資料庫上建立主要金鑰。 必須加密的認證密碼。

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

1. 使用 [CREATE EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md) 建立外部資料來源。

   ```sql
   -- LOCATION:  Azure account storage account name and blob container name.  
   -- CREDENTIAL: The database scoped credential created above.  
   CREATE EXTERNAL DATA SOURCE AzureStorage with (  
         TYPE = HADOOP,
         LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
         CREDENTIAL = AzureStorageCredential  
   );  
   ```

1. 使用 [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md) 建立外部檔案格式。

   ```sql
   -- FORMAT TYPE: Type of format in Azure Blob storage (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   -- In this example, the files are pipe (|) delimited
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

1. 使用 [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md) 建立外部資料表以指向 Azure 儲存體中所儲存的資料。 在此範例中，外部資料會包含車輛感應器資料。

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
  
- 臨機操作查詢外部資料表的詳細資訊。  
- 匯入資料。  
- 匯出資料。  

下列查詢會提供具有虛構車輛感應器資料的範例。

### <a name="ad-hoc-queries"></a>特定查詢  

下列臨機操作查詢會聯結關聯式資料在 Azure Blob 儲存體。 它會選取磁碟機速度 35 英哩/小時，聯結的結構化的客戶資料儲存在 SQL Server 與 Azure Blob 儲存體中的車輛感應器資料的客戶。  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
```  

### <a name="importing-data"></a>匯入資料  

下列查詢會將外部資料匯 AP。 此範例會將資料快速的驅動程式匯 AP，以執行更多的深入分析。 若要改善效能，它會利用 APS 中的資料行存放區技術。  

```sql
CREATE TABLE Fast_Customers
WITH
(CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = HASH (CustomerKey))
AS
SELECT DISTINCT
      Insured_Customers.CustomerKey, Insured_Customers.FirstName, Insured_Customers.LastName,   
      Insured_Customers.YearlyIncome, Insured_Customers.MaritalStatus  
from Insured_Customers INNER JOIN   
(  
      SELECT * FROM CarSensor_Data where Speed > 35   
) AS SensorD  
ON Insured_Customers.CustomerKey = SensorD.CustomerKey  
```  

### <a name="exporting-data"></a>匯出資料  

下列查詢會將資料從 AP 匯出至 Azure Blob 儲存體。 它可以用來保存關聯式資料到 Azure Blob 儲存體，同時仍能夠查詢它。

```sql
-- Export data: Move old data to Azure Blob storage while keeping it query-able via an external table.  
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] 
WITH (  
      LOCATION='/archive/customer/2009',  
      DATA_SOURCE = AzureStorage,  
      FILE_FORMAT = TextFileFormat
)  
AS
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```  

## <a name="view-polybase-objects-in-ssdt"></a>在 SSDT 中的檢視 PolyBase 物件  

在 SQL Server Data Tools，外部資料表會顯示在個別的資料夾**外部資料表**。 外部資料來源和外部檔案格式會在 [外部資源] 下方的子資料夾中。  
  
![在 SSDT 中的 PolyBase 物件](media/polybase/external-tables-datasource.png)  

## <a name="next-steps"></a>後續步驟

如需有關 PolyBase 的詳細資訊，請參閱 [ 什麼是 PolyBase？](../relational-databases/polybase/polybase-guide.md)。 

