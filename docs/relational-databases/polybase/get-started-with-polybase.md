---
title: "開始使用 PolyBase | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 5/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- PolyBase
- PolyBase, getting started
- Hadoop import
- Hadoop export
- Azure blob storage import
- Azure blob storage export
- Hadoop import, PolyBase getting started
- Hadoop export, Polybase getting started
ms.assetid: c71ddc50-b4c7-416c-9789-264671bd9ecb
caps.latest.revision: 78
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 3fc2a681f001906cf9e819084679db097bca62c7
ms.openlocfilehash: 59bf4021617603f0720c23ca192f4ddb65aa6834
ms.contentlocale: zh-tw
ms.lasthandoff: 05/31/2017

---
# <a name="get-started-with-polybase"></a>開始使用 PolyBase
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  本主題包含有關 SQL Server 執行個體上執行 PolyBase 的基本概念。
  
 執行下列步驟之後，您將符合下列條件︰  
  
-   PolyBase 已安裝且可於伺服器上執行  
  
-   建立 PolyBase 物件的陳述式範例  
  
-   了解如何在 SQL Server Management Studio (SSMS) 中管理 PolyBase 物件  
  
-   使用 PolyBase 物件的查詢範例  
  
## <a name="prerequisites"></a>必要條件  
 執行個體[SQL Server （64 位元）](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)為下列：  
  
-   Microsoft .NET Framework 4.5。  
  
-   Oracle Java SE RunTime Environment (JRE) 版本 7.51 或更新版本 (64 位元)。 ( [JRE](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) 或 [Server JRE](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) 都可)。 前往 [Java SE Downloads](http://www.oracle.com/technetwork/java/javase/downloads/index.html)(Java SE 下載)。 如果 JRE 不存在，安裝程式將會失敗。   
  
-   最小記憶體︰4 GB  
  
-   最小硬碟空間︰2 GB    
-   必須啟用 TCP/IP 連線。 (請參閱 [啟用或停用伺服器網路通訊協定](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)。)  
  
 
 外部資料來源，下列項目之一：  
  
-   Hadoop 叢集。 如需支援的版本，請參閱 [設定 PolyBase](#supported)。  

-   Azure Blob 儲存體

> [!NOTE]
>   如果您要針對 Hadoop 使用計算下推功能，則需要確定目標 Hadoop 叢集具有 HDFS 的核心元件：啟用 Jobhistory 伺服器的 Yarn/MapReduce。 PolyBase 透過 MapReduce 來提交下推查詢，並從 JobHistory Server 提取狀態。 沒有其中一個元件，則查詢會失敗。 

## <a name="install-polybase"></a>安裝 PolyBase  
 如果您尚未安裝 PolyBase，請參閱[PolyBase 安裝](../../relational-databases/polybase/polybase-installation.md)。  
  
### <a name="how-to-confirm-installation"></a>如何確認安裝  
 安裝之後，執行下列命令來確認已成功安裝 PolyBase。 如果已安裝 PolyBase 會傳回 1，否則會傳回 0。  
  
```tsql  
SELECT SERVERPROPERTY ('IsPolybaseInstalled') AS IsPolybaseInstalled;  
```  
  
##  <a name="supported"></a> Configure PolyBase  
 在安裝之後，您必須設定 SQL Server 使用可能是您 Hadoop 版本或 Azure Blob 儲存體。 PolyBase 支援兩個 Hadoop 提供者，Hortonworks Data Platform (HDP) 和 Cloudera 分散式 Hadoop (CDH)。  支援的外部資料來源包括︰  
  
-   Linux/Windows Server 上的 Hortonworks HDP 1.3  
  
-   在 Linux 上的 Hortonworks HDP 2.1 – 2.6

-   Windows Server 上的 Hortonworks HDP 2.1 - 2.3  
  
-   Linux 上的 Cloudera CDH 4.3  
  
-   Cloudera CDH 5.1 – 5.5、 5.9-5.11 on Linux  
  
-   Azure Blob 儲存體  
  
>  [!NOTE]
> Azure SQL Data Warehouse 中唯一支援 Azure Data Lake Store 連線。
  
### <a name="external-data-source-configuration"></a>外部資料來源設定  
  
1.  執行 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) ‘hadoop connectivity’ 並設定適當的值。 根據預設，Hadoop 連接設為 7。 若要尋找值，請參閱 [PolyBase Connectivity Configuration &#40;Transact-SQL&#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md) (PolyBase 連線組態 &#40;Transact-SQL&#41;)。  
      ```tsql  
    -- Values map to various external data sources.  
    -- Example: value 7 stands for Azure blob storage and Hortonworks HDP 2.3 on Linux.  
    sp_configure @configname = 'hadoop connectivity', @configvalue = 7;   
    GO   
  
    RECONFIGURE   
    GO   
    ```  
  
2.  您必須使用 **services.msc** 重新啟動 SQL Server。 重新啟動 SQL Server 時，會重新啟動下列服務︰  
  
    -   SQL Server PolyBase Data Movement Service  
  
    -   SQL Server PolyBase Engine  
  
 ![在 services.msc 中停止和啟動 PolyBase 服務](../../relational-databases/polybase/media/polybase-stop-start.png "在 services.msc 中停止和啟動 PolyBase 服務")  
  
### <a name="pushdown-configuration"></a>下推設定  
 為改善查詢效能，請將計算下推到 Hadoop 叢集︰  
  
1.  在 SQL Server 的安裝路徑中，尋找 **yarn-site.xml** 檔案。 通常其路徑如下：  
  
    ```  
  
    C:Program FilesMicrosoft SQL ServerMSSQL13.MSSQLSERVERMSSQLBinnPolybaseHadoopconf  
  
    ```  
  
2.  在 Hadoop 電腦上，尋找 Hadoop 組態目錄中的類比檔案。 在檔案中，尋找並複製組態機碼 yarn.application.classpath 的值。  
  
3.  在 SQL Server 電腦上，尋找 **yarn.site.xml** 檔案中的 **yarn.application.classpath** 屬性。 將 Hadoop 電腦的值貼到 value 元素中。  
  
4. 針對所有 CDH 5.X 版本，您需要將 mapreduce.application.classpath 組態參數新增至 yarn.site.xml 檔案結尾或 mapred-site.xml 檔案。 HortonWorks 會將這些組態包含在 yarn.application.classpath 組態內。 如需範例，請參閱 [PolyBase 組態](../../relational-databases/polybase/polybase-configuration.md)。

 
## <a name="scale-out-polybase"></a>相應放大 PolyBase  
 PolyBase 群組功能可讓您建立 SQL Server 執行個體的叢集，利用向外延展方式處理來自外部資料來源的大型資料集，以提高查詢效能。  
  
1.  在多部電腦上安裝含有 PolyBase 的 SQL Server。  
  
2.  選取一個 SQL Server 作為前端節點。  
  
3.  執行 [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)將其他執行個體加入作為計算節點。  
  
    ```  
    -- Enter head node details:   
    -- head node machine name, head node dms control channel port, head node sql server name  
    EXEC sp_polybase_join_group 'PQTH4A-CMP01', 16450, 'MSSQLSERVER';  
  
    ```  
  
4.  重新啟動計算節點上的 PolyBase 資料移動服務。  
  
 如需詳細資訊，請參閱 [PolyBase scale-out groups](../../relational-databases/polybase/polybase-scale-out-groups.md)(PolyBase 向外延展群組)。  
  
## <a name="create-t-sql-objects"></a>建立 T-SQL 物件  
 建立根據外部資料來源，Hadoop 或 Azure 儲存體的物件。  
  
### <a name="hadoop"></a>Hadoop  
  
```sql  
-- 1: Create a database scoped credential.  
-- Create a master key on the database. This is required to encrypt the credential secret.  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
  
-- 2: Create a database scoped credential  for Kerberos-secured Hadoop clusters.  
-- IDENTITY: the Kerberos user name.  
-- SECRET: the Kerberos password  
  
CREATE DATABASE SCOPED CREDENTIAL HadoopUser1   
WITH IDENTITY = '<hadoop_user_name>', Secret = '<hadoop_password>';  
  
-- 3:  Create an external data source.  
-- LOCATION (Required) : Hadoop Name Node IP address and port.  
-- RESOURCE MANAGER LOCATION (Optional): Hadoop Resource Manager location to enable pushdown computation.  
-- CREDENTIAL (Optional):  the database scoped credential, created above.  
  
CREATE EXTERNAL DATA SOURCE MyHadoopCluster WITH (  
        TYPE = HADOOP,   
        LOCATION ='hdfs://10.xxx.xx.xxx:xxxx',   
        RESOURCE_MANAGER_LOCATION = '10.xxx.xx.xxx:xxxx',   
        CREDENTIAL = HadoopUser1        
);  
  
-- 4: Create an external file format.  
-- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).    
CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
        FORMAT_TYPE = DELIMITEDTEXT,   
        FORMAT_OPTIONS (FIELD_TERMINATOR ='|',   
                USE_TYPE_DEFAULT = TRUE)  
  
-- 5:  Create an external table pointing to data stored in Hadoop.  
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
  
-- 6:  Create statistics on an external table.   
CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
  
```  
  
### <a name="azure-blob-storage"></a>Azure Blob 儲存體  
  
```sql  
--1: Create a master key on the database.  
-- Required to encrypt the credential secret.  
  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
  
-- Create a database scoped credential  for Azure blob storage.  
-- IDENTITY: any string (this is not used for authentication to Azure storage).  
-- SECRET: your Azure storage account key.  
  
CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential   
WITH IDENTITY = 'user', Secret = '<azure_storage_account_key>';  
  
--2:  Create an external data source.  
-- LOCATION:  Azure account storage account name and blob container name.  
-- CREDENTIAL: The database scoped credential created above.  
  
CREATE EXTERNAL DATA SOURCE AzureStorage with (  
        TYPE = HADOOP,   
        LOCATION ='wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',  
        CREDENTIAL = AzureStorageCredential  
);  
  
--3:  Create an external file format.  
-- FORMAT TYPE: Type of format in Hadoop (DELIMITEDTEXT,  RCFILE, ORC, PARQUET).  
  
CREATE EXTERNAL FILE FORMAT TextFileFormat WITH (  
        FORMAT_TYPE = DELIMITEDTEXT,   
        FORMAT_OPTIONS (FIELD_TERMINATOR ='|',   
                USE_TYPE_DEFAULT = TRUE)  
  
--4: Create an external table.  
-- The external table points to data stored in Azure storage.  
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
  
--5: Create statistics on an external table.   
CREATE STATISTICS StatsForSensors on CarSensor_Data(CustomerKey, Speed)  
  
```  
  
## <a name="polybase-queries"></a>PolyBase 查詢  
 有三個 PolyBase 適用的函數︰  
  
-   針對外部資料表進行的臨機操作查詢。  
  
-   匯入資料。  
  
-   匯出資料。  
  
### <a name="query-examples"></a>查詢範例  
  
-   臨機操作查詢  
  
    ```tsql  
    -- PolyBase Scenario 1: Ad-Hoc Query joining relational with Hadoop data   
    -- Select customers who drive faster than 35 mph: joining structured customer data stored   
    -- in SQL Server with car sensor data stored in Hadoop.  
    SELECT DISTINCT Insured_Customers.FirstName,Insured_Customers.LastName,   
            Insured_Customers. YearlyIncome, CarSensor_Data.Speed  
    FROM Insured_Customers, CarSensor_Data  
    WHERE Insured_Customers.CustomerKey = CarSensor_Data.CustomerKey and CarSensor_Data.Speed > 35   
    ORDER BY CarSensor_Data.Speed DESC  
    OPTION (FORCE EXTERNALPUSHDOWN);    -- or OPTION (DISABLE EXTERNALPUSHDOWN)  
    ```  
  
-   匯入資料  
  
    ```tsql  
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
  
-   匯出資料  
  
    ```  
    -- PolyBase Scenario 3: Export data from SQL Server to Hadoop.  
  
    -- Enable INSERT into external table  
    sp_configure ‘allow polybase export’, 1;  
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
  
## <a name="managing-polybase-objects-in-ssms"></a>在 SSMS 中管理 PolyBase 物件  
 在 SSMS 中，外部資料表會顯示在個別的資料夾 [外部資料表] 中。 外部資料來源和外部檔案格式會在 [外部資源] 下方的子資料夾中。  
  
 ![SSMS 中的 PolyBase 物件](../../relational-databases/polybase/media/polybase-management.png "SSMS 中的 PolyBase 物件")  
  
## <a name="troubleshooting"></a>疑難排解  
 使用 DMV 疑難排解效能和查詢。 如需詳細資訊，請參閱 [PolyBase troubleshooting](../../relational-databases/polybase/polybase-troubleshooting.md)(疑難排解 PolyBase)。  
  
 從 SQL Server 2016 RC1 升級至 RC2 或 RC3 之後，查詢可能會失敗。 如需詳細資訊及解決方式，請參閱 [SQL Server 2016 版本資訊](../../sql-server/sql-server-2016-release-notes.md) ，並搜尋 "PolyBase"。  
  
## <a name="next-steps"></a>後續的步驟  
 若要了解向外延展功能，請參閱 [PolyBase scale-out groups](../../relational-databases/polybase/polybase-scale-out-groups.md)(PolyBase 向外延展群組)。  若要監視 PolyBase，請參閱 [PolyBase troubleshooting](../../relational-databases/polybase/polybase-troubleshooting.md)(疑難排解 PolyBase)。 若要疑難排解 PolyBase 效能，請參閱 [PolyBase troubleshooting with dynamic management views](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)。  
  
## <a name="see-also"></a>另請參閱  
 [PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)   
 [PolyBase 向外延展群組](../../relational-databases/polybase/polybase-scale-out-groups.md)   
 [PolyBase 預存程序](http://msdn.microsoft.com/library/a522b303-bd1b-410b-92d1-29c950a15ede)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  

