---
title: PolyBase 查詢情節 | Microsoft Docs
description: 請參閱使用 SQL Server PolyBase 功能的查詢範例，包括 SELECT、結合 (JOIN) 外部資料表與本機資料表、匯入/匯出資料和新的目錄檢視。
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
keywords:
- PolyBase
helpviewer_keywords:
- PolyBase, import and export
- Hadoop, import with PolyBase
- Hadoop, export with PolyBase
- Azure blob storage, import with PolyBase
- Azure blob storage, export with PolyBase
ms.assetid: 2c5aa2bd-af7d-4f57-9a28-9673c2a4c07e
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016'
ms.openlocfilehash: 2eec9c64a65ae0fb548944dc88a056c15e5c1e80
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97416739"
---
# <a name="polybase-query-scenarios"></a>PolyBase 查詢情節

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

下文提供使用 SQL Server (從 2016 版開始) [PolyBase](../../relational-databases/polybase/polybase-guide.md) 功能的查詢範例。 使用這些範例之前，您必須先安裝和設定 PolyBase。 如需詳細資訊，請參閱 [PolyBase 概觀](polybase-guide.md)。
  
對外部資料表執行 Transact-SQL 陳述式，或使用 BI 工具來查詢外部資料表。
  
## <a name="select-from-external-table"></a>從外部資料表進行 SELECT  

從已定義外部資料表傳回資料的簡單查詢。  

```sql  
SELECT TOP 10 * FROM [dbo].[SensorData];   
```

包含述詞的簡單查詢。

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65;
```

## <a name="join-external-tables-with-local-tables"></a>JOIN 具有本機資料表的外部資料表

```sql
SELECT InsuranceCustomers.FirstName,   
   InsuranceCustomers.LastName,   
   SensorData.Speed  
FROM InsuranceCustomers INNER JOIN SensorData    
ON InsuranceCustomers.CustomerKey = SensorData.CustomerKey   
WHERE SensorData.Speed > 65   
ORDER BY SensorData.Speed DESC  
  
```  

## <a name="import-data"></a>匯入資料

將資料從 Hadoop 或 Azure 儲存體匯入至 SQL Server 以便持續儲存。 針對 SQL Server 中的永續性儲存體，使用 SELECT INTO 來匯入外部資料表所參考的資料。 即時建立關聯式資料表，然後在第二個步驟中於資料表上建立資料行存放區索引。

```sql
-- PolyBase scenario - import external data into SQL Server
-- Import data for fast drivers into SQL Server to do more in-depth analysis
-- Leverage columnstore technology
  
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

## <a name="export-data"></a>匯出資料

將資料從 SQL Server 匯出至 Hadoop 或 Azure 儲存體。 

首先，將 'allow polybase export' 的 `sp_configure` 值設定成 1，以啟用匯出功能。 接下來，建立指向目的地目錄的外部資料表。 CREATE EXTERNAL TABLE 陳述式會建立目的地目錄，如果它尚未存在。 然後，使用 INSERT INTO 將資料從本機 SQL Server 資料表匯出至外部資料來源。 

SELECT 陳述式的結果會以指定的檔案格式匯出到指定的位置。 外部檔案命名為 *QueryID_date_time_ID.format*，其中 *ID* 是累加識別碼，而 *format* 是匯出的資料格式。 例如，某個檔案的名稱可能是 QID776_20160130_182739_0.orc。

> [!NOTE]
> 當透過 PolyBase 將檔案匯出到 Hadoop 或 Azure Blob 儲存體時，會如 CREATE EXTERNAL TABLE 命令中所定義，只有資料會被匯出，而不含資料行名稱 (中繼資料)。

```sql  
-- PolyBase scenario  - export data from SQL Server to Hadoop
-- Create an external table
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
INSERT INTO dbo.FastCustomers2009  
SELECT T.* FROM Insured_Customers T1 JOIN CarSensor_Data T2  
ON (T1.CustomerKey = T2.CustomerKey)  
WHERE T2.YearMeasured = 2009 and T2.Speed > 40;  
```

## <a name="new-catalog-views"></a>新目錄檢視

下列新目錄檢視顯示外部資源。

```sql
SELECT * FROM sys.external_data_sources;   
SELECT * FROM sys.external_file_formats;  
SELECT * FROM sys.external_tables;  
```

 使用 `is_external`  

```sql  
SELECT name, type, is_external FROM sys.tables WHERE name='myTableName'   
```  

## <a name="next-steps"></a>後續步驟  

若要深入了解疑難排解，請參閱 [PolyBase 疑難排解](../../relational-databases/polybase/polybase-troubleshooting.md)。
