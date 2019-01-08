---
title: 設定 PolyBase 存取 Hadoop 中的外部資料 | Microsoft Docs
description: 說明如何設定連接至外部 Hadoop 的平行處理資料倉儲的 PolyBase。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 94c8d399f7b6ba36b48b4c5aa7f35bbd67ce6909
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527806"
---
# <a name="configure-polybase-to-access-external-data-in-hadoop"></a>設定 PolyBase 存取 Hadoop 中的外部資料

本文說明如何使用 PolyBase 來查詢 Hadoop 中的外部資料的 APS 應用裝置上。

## <a name="prerequisites"></a>先決條件

PolyBase 支援兩個 Hadoop 提供者，Hortonworks Data Platform (HDP) 和 Cloudera 分散式 Hadoop (CDH)。 Hadoop 的新版本遵循 "Major.Minor.Version" 模式，並且支援所支援主要和次要版本內的所有版本。 支援下列 Hadoop 提供者：
 - Linux/Windows Server 上的 Hortonworks HDP 1.3  
 - 在 Linux 上的 Hortonworks HDP 2.1 2.6
 - Windows Server 上的 Hortonworks HDP 2.1 - 2.3  
 - Linux 上的 Cloudera CDH 4.3  
 - Cloudera CDH 5.1-5.5、 5.9-5.13 Linux 上

### <a name="configure-hadoop-connectivity"></a>設定 Hadoop 連線

首先，設定 AP，以使用特定的 Hadoop 提供者。

1. 同時執行 [sp_configure](../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 與 'hadoop connectivity'，並設定您提供者的適當值。 若要尋找您提供者的值，請參閱 [PolyBase 連線設定](../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。 

   ```sql  
   -- Values map to various external data sources.  
   -- Example: value 7 stands for Hortonworks HDP 2.1 to 2.6 on Linux,
   -- 2.1 to 2.3 on Windows Server, and Azure blob storage  
   sp_configure @configname = 'hadoop connectivity', @configvalue = 7;
   GO

   RECONFIGURE
   GO
   ```  

2. 重新啟動使用服務狀態 頁面上的 APS 地區[設備 Configuration Manager](launch-the-configuration-manager.md)。
  
## <a id="pushdown"></a> 啟用下推計算  

為改善查詢效能，請將計算下推到 Hadoop 叢集︰  
  
1. 開啟 PDW 控制節點的遠端桌面連線。

2. 尋找檔案**yarn-site.xml**控制節點上。 通常其路徑如下：  

   ```xml  
   C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\Hadoop\conf\  
   ```  

3. 在 Hadoop 電腦上，尋找 Hadoop 組態目錄中的類比檔案。 在檔案中，尋找並複製組態機碼 yarn.application.classpath 的值。  
  
4. 在 [控制] 節點中，在**yarn.site.xml 檔案**尋找**yarn.application.classpath**屬性。 將 Hadoop 電腦的值貼到 value 元素中。  
  
5. 針對所有 CDH 5.X 版本，您需要將 mapreduce.application.classpath 組態參數新增至 yarn.site.xml 檔案結尾或 mapred-site.xml 檔案。 HortonWorks 會將這些組態包含在 yarn.application.classpath 組態內。 如需範例，請參閱 [PolyBase 組態](../relational-databases/polybase/polybase-configuration.md)。

## <a name="configure-an-external-table"></a>設定外部資料表

若要查詢 Hadoop 資料來源中的資料，您必須定義要在 Transact-SQL 查詢中使用的外部資料表。 下列步驟描述如何設定外部資料表。

1. 在資料庫上建立主要金鑰。 必須加密的認證密碼。

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
   ```

2. 針對 Kerberos 保護的 Hadoop 叢集建立資料庫範圍認證。

   ```sql
   -- IDENTITY: the Kerberos user name.  
   -- SECRET: the Kerberos password  
   CREATE DATABASE SCOPED CREDENTIAL HadoopUser1
   WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
   ```

3. 使用 [CREATE EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md) 建立外部資料來源。

   ```sql
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

4. 使用 [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md) 建立外部檔案格式。

   ```sql
   -- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE)  
   ```

5. 使用 [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md) 建立外部資料表以指向 Hadoop 中儲存的資料。 在此範例中，外部資料包含車輛感應器資料。

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
         DATA_SOURCE = MyHadoopCluster,  
         FILE_FORMAT = TextFileFormat  
   );  
   ```

6. 在外部資料表上建立統計資料。

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

下列臨機操作查詢會聯結關聯式 Hadoop 資料。 它會選取磁碟機速度 35 英哩/小時，聯結的結構化的客戶資料儲存在 AP 並儲存在 Hadoop 中的車輛感應器資料的客戶。  

```sql  
SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,
       Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
FROM Insured_Customers, CarSensor_Data  
WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35
ORDER BY CarSensor_Data.Speed DESC  
OPTION (FORCE EXTERNALPUSHDOWN);   -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
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

下列查詢會將資料從 AP 匯出到 Hadoop。 它可以用來封存至 Hadoop 的關聯式資料時仍然可以進行查詢。

```sql
-- Export data: Move old data to Hadoop while keeping it query-able via an external table.  
CREATE EXTERNAL TABLE [dbo].[FastCustomers2009] 
WITH (  
      LOCATION='/archive/customer/2009',  
      DATA_SOURCE = HadoopHDP2,  
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

針對 Hadoop 安全性設定，請參閱[設定 Hadoop 安全性](polybase-configure-hadoop-security.md)。<br>
如需有關 PolyBase 的詳細資訊，請參閱 [ 什麼是 PolyBase？](../relational-databases/polybase/polybase-guide.md)。 
 
