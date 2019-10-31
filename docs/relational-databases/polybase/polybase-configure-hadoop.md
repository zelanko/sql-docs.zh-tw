---
title: 設定 PolyBase 存取 Hadoop 中的外部資料 | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: ecb0f89cb7093587feb9c7e57be56e2cafaee5a0
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907574"
---
# <a name="configure-polybase-to-access-external-data-in-hadoop"></a>設定 PolyBase 存取 Hadoop 中的外部資料

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文說明如何在 SQL Server 執行個體上使用 PolyBase 來查詢位於 Hadoop 中的外部資料。

## <a name="prerequisites"></a>Prerequisites

- 如果您尚未安裝 PolyBase，請參閱 [PolyBase 安裝](polybase-installation.md)。 安裝文章說明必要條件。

<!--SQL Server 2019-->
::: moniker range=">= sql-server-ver15 || =sqlallproducts-allversions"

- 從 SQL Server 2019 開始，您也必須[啟用 PolyBase 功能](polybase-installation.md#enable)。

::: moniker-end

- PolyBase 支援兩個 Hadoop 提供者，Hortonworks Data Platform (HDP) 和 Cloudera 分散式 Hadoop (CDH)。 Hadoop 的新版本遵循 "Major.Minor.Version" 模式，並且支援所支援主要和次要版本內的所有版本。 支援下列 Hadoop 提供者：

  - Linux 上的 Hortonworks HDP 1.3、2.1-2.6、3.0
  - Windows Server 上的 Hortonworks HDP 1.3、2.1-2.3
  - Linux 上的 Cloudera CDH 4.3、5.1-5.5、5.9-5.13

> [!NOTE]
> 從 SQL Server 2016 SP1 CU7 和 SQL Server 2017 CU3 開始，PolyBase 支援 Hadoop 加密區域。 如果您使用 [PolyBase 向外延展群組](polybase-scale-out-groups.md)，則所有計算節點也必須位在支援 Haddop 加密區域的組建上。

### <a name="configure-hadoop-connectivity"></a>設定 Hadoop 連線

首先，設定 SQL Server PolyBase 使用您的特定 Hadoop 提供者。

1. 同時執行 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 與 'hadoop connectivity'，並設定您提供者的適當值。 若要尋找您提供者的值，請參閱 [PolyBase 連線設定](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。 根據預設，Hadoop 連線設定為 7。

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
  
## <a id="pushdown"></a> 啟用下推計算  

為改善查詢效能，請將計算下推到 Hadoop 叢集︰  
  
1. 在 SQL Server 的安裝路徑中，尋找 **yarn-site.xml** 檔案。 通常其路徑如下：  

   ```xml  
   C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Polybase\Hadoop\conf\  
   ```  

1. 在 Hadoop 電腦上，尋找 Hadoop 組態目錄中的類比檔案。 在檔案中，尋找並複製組態機碼 yarn.application.classpath 的值。  
  
1. 在 SQL Server 電腦上，尋找 **yarn-site.xml** 檔案中的 **yarn.application.classpath** 屬性。 將 Hadoop 電腦的值貼到 value 元素中。  
  
1. 針對所有 CDH 5.X 版本，您需要將 mapreduce.application.classpath 設定參數新增至 yarn-site.xml 檔案結尾或 mapred-site.xml 檔案。 HortonWorks 會將這些組態包含在 yarn.application.classpath 組態內。 如需範例，請參閱 [PolyBase 組態](../../relational-databases/polybase/polybase-configuration.md)。

## <a name="configure-an-external-table"></a>設定外部資料表

若要查詢 Hadoop 資料來源中的資料，您必須定義要在 Transact-SQL 查詢中使用的外部資料表。 下列步驟描述如何設定外部資料表。

1. 在資料庫上建立主要金鑰 (如果還沒有任何主要金鑰存在)。 這是加密認證祕密的必要項目。

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';  
     ```
    ## <a name="arguments"></a>引數
    PASSWORD ='password'

    這是用以加密資料庫中主要金鑰的密碼。 password 必須符合裝載 SQL Server 執行個體之電腦的 Windows 密碼原則需求。
1. 針對 Kerberos 保護的 Hadoop 叢集建立資料庫範圍認證。

   ```sql
   -- IDENTITY: the Kerberos user name.  
   -- SECRET: the Kerberos password  
   CREATE DATABASE SCOPED CREDENTIAL HadoopUser1
   WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
   ```

2. 使用 [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) 建立外部資料來源。

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

3. 使用 [CREATE EXTERNAL FILE FORMAT](../../t-sql/statements/create-external-file-format-transact-sql.md) 建立外部檔案格式。

   ```sql
   -- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).
   CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
         FORMAT_TYPE = DELIMITEDTEXT,
         FORMAT_OPTIONS (FIELD_TERMINATOR ='|',
               USE_TYPE_DEFAULT = TRUE))
   ```

4. 使用 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 建立外部資料表以指向 Hadoop 中儲存的資料。 在此範例中，外部資料會包含車輛感應器資料。

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

5. 在外部資料表上建立統計資料。

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

下列查詢會將資料從 SQL Server 匯出至 Hadoop。 若要這樣做，您需要先啟用 PolyBase 匯出。 先建立目的地的外部資料表，再將資料匯出至其中。

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

在 SSMS 中，外部資料表會顯示在個別的資料夾 [外部資料表] 中。 外部資料來源和外部檔案格式會在 [外部資源] 下方的子資料夾中。  
  
![SSMS 中的 PolyBase 物件](media/polybase-management.png)  

## <a name="next-steps"></a>後續步驟

在下列文章中，探索更多使用和監視 PolyBase 的方式：

[PolyBase 向外延展群組](../../relational-databases/polybase/polybase-scale-out-groups.md)。  
[PolyBase 疑難排解](polybase-troubleshooting.md).  
