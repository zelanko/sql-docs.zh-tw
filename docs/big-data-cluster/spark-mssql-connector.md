---
title: 將 Spark 連線到 SQL Server
titleSuffix: SQL Server big data clusters
description: 了解如何使用適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器來讀取和寫入 SQL Server。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning-bdc
ms.openlocfilehash: 3cb36c4bdddfaa97b9b6c08015308799d54cb0dc
ms.sourcegitcommit: 56f6892b3795da308d226d4b3c5c859ead2e830a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/17/2020
ms.locfileid: "86438070"
---
# <a name="how-to-read-and-write-to-sql-server-from-spark-using-the-apache-spark-connector-for-sql-server-and-azure-sql"></a>如何使用適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器來從 Spark 讀取和寫入 SQL Server

巨量資料的一個主要使用模式是在 Spark 中進行大量資料處理，再將資料寫入 SQL Server，存取企業營運應用程式。 這些使用模式會受益於連接器，其利用主要 SQL 最佳化功能並提供高效率寫入機制。

本文提供適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器介面概觀，並將其具現化以搭配非 AD 模式與 AD 模式使用。 接著提供範例來示範如何使用適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器，以讀取和寫入巨量資料叢集內的下列位置：
1. SQL Server 主要執行個體
1. SQL Server 資料集區

   ![適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器圖表](./media/spark-mssql-connector/mssql-spark-connector-diagram.png)

## <a name="apache-spark-connector-for-sql-server-and-azure-sql-interface"></a>適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器介面

SQL Server 2019 為巨量資料叢集提供[**適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器**](https://github.com/microsoft/sql-spark-connector)，使用 SQL Server 大量寫入 API 來進行 Spark 對 SQL 的寫入。 適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器是以 Spark 資料來源 API 為基礎，並提供熟悉的 Spark JDBC 連接器介面。 如需介面參數，請參閱 [Apache Spark 文件](http://spark.apache.org/docs/latest/sql-data-sources-jdbc.html)。 適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器是依名稱 **com.microsoft.sqlserver.jdbc.spark** 來參考。 適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器支援兩種安全性模式 (非 Active Directory 模式和 Active Directory (AD) 模式) 來與 SQL Server 連線：
### <a name="non-ad-mode"></a>非 AD 模式：
在非 AD 模式安全性中，每個使用者都有使用者名稱和密碼，在連接器具現化期間必須將這些使用者名稱和密碼提供為參數，以執行讀取和/或寫入。
非 AD 模式的範例連接器具現化如下：
```python
# Note: '?' is a placeholder for a necessary user-specified value
connector_type = "com.microsoft.sqlserver.jdbc.spark" 

url = "jdbc:sqlserver://master-p-svc;databaseName=?;"
writer = df.write \ 
   .format(connector_type)\ 
   .mode("overwrite") 
   .option("url", url) \ 
   .option("user", ?) \ 
   .option("password",?) 
writer.save() 
```
### <a name="ad-mode"></a>AD 模式：
在 AD 模式安全性中，使用者在產生金鑰表檔案之後，必須在連接器具現化期間提供 `principal` 和 `keytab` 作為參數。

在此模式中，驅動程式會將金鑰表檔案載入至個別的執行程式容器。 然後，執行程式會使用主體名稱和金鑰表來產生權杖，以用來建立用於讀取/寫入的 JDBC 連接器。

AD 模式的範例連接器具現化如下：
```python
# Note: '?' is a placeholder for a necessary user-specified value
connector_type = "com.microsoft.sqlserver.jdbc.spark"

url = "jdbc:sqlserver://master-p-svc;databaseName=?;integratedSecurity=true;authenticationScheme=JavaKerberos;" 
writer = df.write \ 
   .format(connector_type)\ 
   .mode("overwrite") 
   .option("url", url) \ 
   .option("principal", ?) \ 
   .option("keytab", ?)   

writer.save() 
```

下表描述已變更或新增的介面參數：

| 屬性名稱 | 選用 | 描述 |
|---|---|---|
| **isolationLevel** | 是 | 這會描述連線的隔離等級。 連接器的預設值為 **READ_COMMITTED** |

連接器使用 SQL Server 大量寫入 API。 使用者可以以選擇性參數傳遞任何大量寫入參數，再由連接器依現狀將其傳遞至基礎 API。 如需大量寫入作業的詳細資訊，請參閱 [SQLServerBulkCopyOptions]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions)。

## <a name="apache-spark-connector-for-sql-server-and-azure-sql-sample"></a>適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器範例
此範例會執行下列工作：

- 從 HDFS 讀取檔案並執行一些基本處理。
- 將資料框架寫入 SQL Server 主要執行個體作為 SQL 資料表，然後將資料表讀入資料框架。
- 將資料框架寫入 SQL Server 資料集區作為 SQL 外部資料表，然後將外部資料表讀入資料框架。
### <a name="prerequisites"></a>Prerequisites

- [SQL Server 巨量資料叢集](deploy-get-started.md)。

- [Azure Data Studio](https://aka.ms/getazuredatastudio)。

### <a name="create-the-target-database"></a>建立目標資料庫

1. 開啟 Azure Data Studio，然後[連線到巨量資料叢集的 SQL Server 主要執行個體](connect-to-big-data-cluster.md)。

1. 建立新的查詢，然後執行下列命令，建立名為 **MyTestDatabase** 的範例資料庫。

   ```sql
   Create DATABASE MyTestDatabase
   GO
   ```

### <a name="load-sample-data-into-hdfs"></a>將範例資料載入 HDFS

1. 將 [AdultCensusIncome.csv](https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv) 下載到您的本機電腦。

1. 啟動 Azure Data Studio，然後[連線到巨量資料叢集](connect-to-big-data-cluster.md)。

1. 以滑鼠右鍵按一下巨量資料叢集中的 HDFS 資料夾，然後選取 [新增目錄]  。 將目錄命名為 **spark_data**。

1. 以滑鼠右鍵按一下 [spark_data]  目錄，然後選取 [上傳檔案]  。 上傳 **AdultCensusIncome.csv** 檔案。

   ![AdultCensusIncome CSV 檔案](./media/spark-mssql-connector/spark_data.png)

### <a name="run-the-sample-notebook"></a>執行範例筆記本

若要示範如何在非 AD 模式下以適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器運用此資料，則可下載範例筆記本，並於 Azure Data Studio 中開啟，然後執行每個程式碼區塊。 如需使用筆記本的詳細資訊，請參閱[如何搭配 SQL Server 使用筆記本](../azure-data-studio/notebooks-guidance.md)。

1. 從 PowerShell 或 bash 命令列執行下列命令，以下載 **mssql_spark_connector_non_ad_pyspark.ipynb** 範例筆記本：

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-virtualization/mssql_spark_connector_non_ad_pyspark.ipynb"
   ```

1. 在 Azure Data Studio 中，開啟範例筆記本檔案。 確認已連線到巨量資料叢集的 HDFS/Spark 閘道。

1. 執行範例中的每個程式碼資料格，以查看適用於 SQL Server 和 Azure SQL 的 Apache Spark 連接器其使用方式。

## <a name="next-steps"></a>後續步驟

如需巨量資料叢集的詳細資訊，請參閱[如何在 Kubernetes 上部署 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](deployment-guidance.md)

有 SQL Server 巨量資料叢集的意見反應或功能建議嗎？ [請在 SQL Server 巨量資料叢集意見反應中留言](https://aka.ms/sql-server-bdc-feedback)。
