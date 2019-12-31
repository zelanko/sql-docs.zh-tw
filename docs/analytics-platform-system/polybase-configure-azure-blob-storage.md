---
title: 使用 PolyBase 存取 Azure Blob 儲存體中的外部資料
description: 說明如何在平行處理資料倉儲中設定 PolyBase，以連線至外部 Hadoop。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4ea61ea7e6983f9601783957eee6776f36eccfb4
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400719"
---
# <a name="configure-polybase-to-access-external-data-in-azure-blob-storage"></a>設定 PolyBase 存取 Azure Blob 儲存體中的外部資料

本文說明如何在 SQL Server 實例上使用 PolyBase 來查詢 Azure Blob 儲存體中的外部資料。

> [!NOTE]
> AP 目前僅支援標準一般用途 v1 本機多餘的（LRS） Azure Blob 儲存體。

## <a name="prerequisites"></a>必要條件

 - 訂用帳戶中的 Azure Blob 儲存體。
 - 在 Azure Blob 儲存體中建立的容器。

### <a name="configure-azure-blob-storage-connectivity"></a>設定 Azure Blob 儲存體連線能力

首先，設定要使用 Azure Blob 儲存體的 AP。

1. 使用設定為 Azure Blob 儲存體提供者的「hadoop 連線能力」來執行[sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 。 若要尋找提供者的值，請參閱 [PolyBase 連線設定](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure Blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. 使用[設備 Configuration Manager](launch-the-configuration-manager.md)上的 [服務狀態] 頁面重新開機 ap 區域。
  
## <a name="configure-an-external-table"></a>設定外部資料表

若要查詢 Azure Blob 儲存體中的資料，您必須定義要在 Transact-SQL 查詢中使用的外部資料表。 下列步驟描述如何設定外部資料表。

1. 在資料庫上建立主要金鑰。 需要加密認證秘密。

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

1. 建立外部資料源，並[建立外部資料源](../t-sql/statements/create-external-data-source-transact-sql.md)。。

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
  
- 針對外部資料表的特定查詢。  
- 匯入資料。  
- 匯出資料。  

下列查詢會提供具有虛構車輛感應器資料的範例。

### <a name="ad-hoc-queries"></a>特定查詢  

下列臨機操作查詢會聯結與 Azure Blob 儲存體中資料的關聯式。 它會選取速度低於 35 mph 的客戶，將儲存在 SQL Server 中的結構化客戶資料，聯結到儲存在 Azure Blob 儲存體中的汽車感應器資料。  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
```  

### <a name="importing-data"></a>匯入資料  

下列查詢會將外部資料匯入至 AP。 這個範例會將快速驅動程式的資料匯入至 AP，以進行更深入的分析。 為了改善效能，它會運用 AP 中的資料行存放區技術。  

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

下列查詢會將資料從 AP 匯出至 Azure Blob 儲存體。 它可以用來將關聯式資料封存到 Azure Blob 儲存體，同時仍然可以查詢它。

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

## <a name="view-polybase-objects-in-ssdt"></a>在 SSDT 中查看 PolyBase 物件  

在 SQL Server Data Tools 中，外部資料表會顯示在個別的資料夾**外部資料表**中。 外部資料來源和外部檔案格式會在 [外部資源] **** 下方的子資料夾中。  
  
![SSDT 中的 PolyBase 物件](media/polybase/external-tables-datasource.png)  

## <a name="next-steps"></a>接下來的步驟

如需有關 PolyBase 的詳細資訊，請參閱[什麼是 PolyBase？](../relational-databases/polybase/polybase-guide.md)。 

