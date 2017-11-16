---
title: "PolyBase 巢狀 | Microsoft Docs"
ms.custom: 
ms.date: 03/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: polybase
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- PolyBase
helpviewer_keywords:
- PolyBase, import and export
- Hadoop, import with PolyBase
- Hadoop, export with PolyBase
- Azure blob storage, import with PolyBase
- Azure blob storage, export with PolyBase
ms.assetid: 2c5aa2bd-af7d-4f57-9a28-9673c2a4c07e
caps.latest.revision: 18
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d6cc1b4523bdb0b48cfc22b34b205e15613fb290
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="polybase-queries"></a>PolyBase Queries
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  以下是使用 SQL Server 2016 [PolyBase 指南](../../relational-databases/polybase/polybase-guide.md) 功能的範例查詢。 使用這些範例之前，您也必須了解設定 PolyBase 所需的 T-SQL 陳述式 (請參閱 [PolyBase T-SQL 物件](../../relational-databases/polybase/polybase-t-sql-objects.md))。  
  
## <a name="queries"></a>查詢  
 對外部資料表執行 Transact-SQL 陳述式，或使用 BI 工具來查詢外部資料表。  
  
## <a name="select-from-external-table"></a>從外部資料表進行 SELECT  
 從已定義外部資料表傳回資料的簡單查詢。  
  
```tsql  
SELECT TOP 10 * FROM [dbo].[SensorData];   
```  
  
 包含述詞的簡單查詢。  
  
```  
SELECT * FROM [dbo].[SensorData]   
WHERE Speed > 65;   
```  
  
## <a name="join-external-tables-with-local-tables"></a>JOIN 具有本機資料表的外部資料表  
  
```  
SELECT InsuranceCustomers.FirstName,   
                           InsuranceCustomers.LastName,   
                           SensorData.Speed  
FROM InsuranceCustomers INNER JOIN SensorData    
ON InsuranceCustomers.CustomerKey = SensorData.CustomerKey   
WHERE SensorData.Speed > 65   
ORDER BY SensorData.Speed DESC  
  
```  
  
## <a name="pushdown-computation-to-hadoop"></a>將計算下推到 Hadoop  
 下推變量如下所示。  
  
### <a name="pushdown-for-selecting-a-subset-of-rows"></a>用於選取資料列子集的下推  
 使用述詞下推，來改善從外部資料表選取資料列子集之查詢的效能。  
  
 在這裡，SQL Server 2016 會起始 map-reduce 工作，來擷取 Hadoop 上符合 customer.account_balance < 200000 述詞的資料列。 因為查詢可以順利完成，而不需要掃描資料表中的所有資料列，所以只會將符合述詞準則的資料列複製到 SQL Server。 這可以節省大量時間，而且相較於帳戶餘額 >= 200000 的客戶數目，客戶餘額數目 < 200000 需要較少的暫存儲存空間。  
  複製 imageCopy 程式碼   
SELECT * FROM customer WHERE customer.account_balance < 200000。  
  
```  
SELECT * FROM SensorData WHERE Speed > 65;  
```  
  
### <a name="pushdown-for-selecting-a-subset-of-columns"></a>用於選取資料行子集的下推  
 使用述詞下推，來改善從外部資料表選取資料行子集之查詢的效能。  
  
 在此查詢中，SQL Server 會起始 map-reduce 工作來前置處理 Hadoop 分隔符號文字檔，只將兩個資料行 (customer.name 和 customer.zip_code) 的資料複製至 SQL Server PDW。  
  
```  
SELECT customer.name, customer.zip_code FROM customer WHERE customer.account_balance < 200000  
  
```  
  
### <a name="pushdown-for-basic-expressions-and-operators"></a>基本運算式和運算子的下推  
 SQL Server 允許述詞下推的下列基本運算式和運算子。  
  
-   數值、日期和時間值的二進位比較運算子 (\<、>、=、!=、<>、>=、<=)。  
  
-   算術運算子 (+、-、*、/、% )。  
  
-   邏輯運算子 (AND、OR)。  
  
-   一元運算子 (NOT、IS NULL、IS NOT NULL)。  
  
 可能會下推 BETWEEN、NOT、IN 和 LIKE 運算子。 這取決於查詢最佳化工具如何將它們重新寫入為一系列使用基本關係運算子的陳述式。  
  
 此查詢有多個可下推到 Hadoop 的述詞。 SQL Server 可以將 map-reduce 工作推送到 Hadoop，以執行 customer.account_balance <= 200000 述詞。 BETWEEN 92656 and 92677 運算式包含可推送到 Hadoop 的二進位和邏輯運算。 customer.account_balance 與 customer.zipcode 的邏輯 AND 是最終運算式。  
  
 這樣 map-reduce 工作就可以執行所有 WHERE 子句。 只會將符合 SELECT 準則的資料複製回 SQL Server PDW。  
  
```  
SELECT * FROM customer WHERE customer.account_balance <= 200000 AND customer.zipcode BETWEEN 92656 AND 92677  
  
```  
  
### <a name="force-pushdown"></a>強制下推  
  
```  
SELECT * FROM [dbo].[SensorData]   
WHERE Speed > 65  
OPTION (FORCE EXTERNALPUSHDOWN);   
```  
  
### <a name="disable-pushdown"></a>停用下推  
  
```  
SELECT * FROM [dbo].[SensorData]   
WHERE Speed > 65  
OPTION (DISABLE EXTERNALPUSHDOWN);  
```  
  
## <a name="import-data"></a>匯入資料  
 將資料從 Hadoop 或 Azure 儲存體匯入至 SQL Server 以便持續儲存。 使用 SELECT INTO 將外部資料表所參考的資料匯入至 SQL Server 中的永續性儲存體。 在第二個步驟中，快速建立關聯式資料表，然後在資料表上建立資料行存放區索引。  
  
```sql  
-- PolyBase Scenario 2: Import external data into SQL Server.  
-- Import data for fast drivers into SQL Server to do more in-depth analysis and  
-- leverage Columnstore technology.  
  
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
將資料從 SQL Server 匯出至 Hadoop 或 Azure 儲存體。 首先，將 'allow polybase export' 的 sp_configure 值設成 1，以啟用匯出功能。 接下來，建立指向目的地目錄的外部資料表。 然後，使用 INSERT INTO 將資料從本機 SQL Server 資料表匯出至外部資料來源。 如果目的地目錄不存在，INSERT INTO 陳述式會加以建立，並將 SELECT 陳述式的結果以指定檔案格式匯出至指定位置。 外部檔案命名為 *QueryID_date_time_ID.format*，其中 *ID* 是累加識別碼，而 *format* 是匯出的資料格式。 例如，QID776_20160130_182739_0.orc。  
  
```sql  
-- PolyBase Scenario 3: Export data from SQL Server to Hadoop.  
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
  
## <a name="next-steps"></a>後續的步驟  
 若要深入了解疑難排解，請參閱 [PolyBase 疑難排解](../../relational-databases/polybase/polybase-troubleshooting.md)。  
  
  

